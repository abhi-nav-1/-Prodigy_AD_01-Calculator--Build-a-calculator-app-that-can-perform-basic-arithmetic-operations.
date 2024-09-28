# -Prodigy_AD_01-Calculator--Build-a-calculator-app-that-can-perform-basic-arithmetic-operations.
prodigy_task_01.zip
import tkinter as tk
from tkinter import ttk

class RoundedButton(ttk.Button):
    def __init__(self, master=None, **kwargs):
        super().__init__(master, style="Rounded.TButton", **kwargs)

def on_button_click(value):
    current_text = display_var.get()
    display_var.set(current_text + value)

def calculate():
    try:
        result = str(eval(display_var.get()))
        display_var.set(result)
    except Exception as e:
        display_var.set("Error")

def clear():
    display_var.set("")

root = tk.Tk()
root.title("Calculator")
root.geometry("400x600")
root.configure(bg="#f0f0f0")

display_var = tk.StringVar()
display_entry = tk.Entry(root, textvariable=display_var, font=("Arial", 36), bd=10, insertwidth=4, width=14, justify='right', bg="#ffffff")
display_entry.grid(row=0, column=0, columnspan=4, padx=20, pady=20, ipadx=10, ipady=10, sticky="nsew")

button_grid = [
    'C', '(', ')', '/',
    '7', '8', '9', '*',
    '4', '5', '6', '-',
    '1', '2', '3', '+',
    '', '0', '.', '='
]

row_val = 1
col_val = 0
for button in button_grid:
    if button == '=':
        action = calculate
    elif button == 'C':
        action = clear
    else:
        action = lambda x=button: on_button_click(x)
    RoundedButton(root, text=button, command=action).grid(row=row_val, column=col_val, padx=10, pady=10, ipadx=20, ipady=20, sticky="nsew")
    col_val += 1
    if col_val > 3:
        col_val = 0
        row_val += 1

for i in range(1, 6):
    root.grid_rowconfigure(i, weight=1)
for i in range(4):
    root.grid_columnconfigure(i, weight=1)

style = ttk.Style()
style.configure("Rounded.TButton", font=("Arial", 18), relief="flat", borderwidth=0, padding=10, borderradius=20)

root.mainloop()
