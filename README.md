# ceaser-cipher
#The code provided is a Python script that uses the Tkinter library to create a basic graphical user interface (GUI) for encrypting and decrypting messages using the Caesar Cipher.
import tkinter as tk
from tkinter import ttk

def caesar_cipher_encrypt(plaintext, shift):
    encrypted_text = ""
    for char in plaintext:
        if char.isalpha():
            is_upper = char.isupper()
            char_code = ord(char)
            encrypted_char = chr((char_code - ord('A' if is_upper else 'a') + shift) % 26 + ord('A' if is_upper else 'a'))
            encrypted_text += encrypted_char
        else:
            encrypted_text += char
    return encrypted_text

def caesar_cipher_decrypt(ciphertext, shift):
    return caesar_cipher_encrypt(ciphertext, -shift)

def encrypt_decrypt_text():
    input_text = input_entry.get("1.0", "end-1c")
    shift_value = int(shift_entry.get())
    
    encrypted_text = caesar_cipher_encrypt(input_text, shift_value)
    decrypted_text = caesar_cipher_decrypt(input_text, shift_value)
    
    encrypted_output.config(state=tk.NORMAL)
    decrypted_output.config(state=tk.NORMAL)
    
    encrypted_output.delete("1.0", tk.END)
    decrypted_output.delete("1.0", tk.END)
    
    encrypted_output.insert(tk.END, encrypted_text)
    decrypted_output.insert(tk.END, decrypted_text)
    
    encrypted_output.config(state=tk.DISABLED)
    decrypted_output.config(state=tk.DISABLED)

# Create the main window
window = tk.Tk()
window.title("Caesar Cipher Encryption/Decryption")

# Create and place widgets
input_label = ttk.Label(window, text="Enter Text:")
input_label.grid(row=0, column=0, padx=10, pady=10)

input_entry = tk.Text(window, height=5, width=40)
input_entry.grid(row=0, column=1, padx=10, pady=10)

shift_label = ttk.Label(window, text="Enter Shift Value:")
shift_label.grid(row=1, column=0, padx=10, pady=10)

shift_entry = ttk.Entry(window)
shift_entry.grid(row=1, column=1, padx=10, pady=10)

encrypt_button = ttk.Button(window, text="Encrypt/Decrypt", command=encrypt_decrypt_text)
encrypt_button.grid(row=2, column=0, columnspan=2, pady=10)

encrypted_output = tk.Text(window, height=5, width=40, state=tk.DISABLED)
encrypted_output.grid(row=3, column=0, columnspan=2, padx=10, pady=10)

decrypted_output = tk.Text(window, height=5, width=40, state=tk.DISABLED)
decrypted_output.grid(row=4, column=0, columnspan=2, padx=10, pady=10)

# Run the main loop
window.mainloop()
