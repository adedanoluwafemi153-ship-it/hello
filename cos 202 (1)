import tkinter as tk
from tkinter import messagebox

class MathematicalCalculator:
    def __init__(self, root):
        self.root = root
        self.root.title("COS202 - Calculator")
        self.root.geometry("350x450")
        self.root.configure(bg="#2c3e50")
        self.root.resizable(False, False)
        
        self.expression = ""
        self.display_var = tk.StringVar()
        
        self.create_widgets()
        
    def create_widgets(self):
        # Entry Screen
        display = tk.Entry(
            self.root, textvariable=self.display_var, font=("Arial", 20, "bold"),
            bd=10, insertwidth=4, width=14, borderwidth=0, justify="right",
            bg="#ecf0f1", fg="#2c3e50"
        )
        display.grid(row=0, column=0, columnspan=4, padx=15, pady=20, ipady=10)
        
        # Button layout mapping
        buttons = [
            ('C', 1, 0), ('^', 1, 1), ('%', 1, 2), ('/', 1, 3),
            ('7', 2, 0), ('8', 2, 1), ('9', 2, 2), ('*', 2, 3),
            ('4', 3, 0), ('5', 3, 1), ('6', 3, 2), ('-', 3, 3),
            ('1', 4, 0), ('2', 4, 1), ('3', 4, 2), ('+', 4, 3),
            ('0', 5, 0), ('.', 5, 1), ('//', 5, 2), ('=', 5, 3),
            ('OFF', 6, 0)
        ]
        
        for (text, row, col) in buttons:
            action = lambda x=text: self.on_button_click(x)
            
            # Special styling rules
            bg_color = "#34495e"
            fg_color = "#ffffff"
            colspan = 1
            
            if text in ['+', '-', '*', '/', '%', '^', '//']:
                bg_color = "#3498db"
            elif text == '=':
                bg_color = "#2ecc71"
            elif text == 'C':
                bg_color = "#e67e22"
            elif text == 'OFF':
                bg_color = "#e74c3c"
                colspan = 4
                
            btn = tk.Button(
                self.root, text=text, padx=20, pady=12, font=("Arial", 12, "bold"),
                bg=bg_color, fg=fg_color, activebackground="#bdc3c7",
                borderwidth=0, command=action
            )
            
            if text == 'OFF':
                btn.grid(row=row, column=col, columnspan=colspan, sticky="nsew", padx=15, pady=10)
            else:
                btn.grid(row=row, column=col, padx=5, pady=5, sticky="nsew")

    def on_button_click(self, char):
        if char == 'OFF':
            self.root.destroy()
        elif char == 'C':
            self.expression = ""
            self.display_var.set("")
        elif char == '=':
            try:
                # Replace visual operators with valid Python syntax
                expr = self.expression.replace('^', '**')
                result = str(eval(expr))
                self.display_var.set(result)
                self.expression = result # allow continued operations
            except ZeroDivisionError:
                messagebox.showerror("Error", "Cannot divide by zero")
                self.clear_display()
            except Exception:
                messagebox.showerror("Error", "Invalid Expression")
                self.clear_display()
        else:
            self.expression += str(char)
            self.display_var.set(self.expression)
            
    def clear_display(self):
        self.expression = ""
        self.display_var.set("")

if __name__ == "__main__":
    root = tk.Tk()
    calculator = MathematicalCalculator(root)
    root.mainloop()
