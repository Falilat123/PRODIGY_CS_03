# Password Strength Checker

This project is a simple tool that assesses the strength of a password based on several criteria. It provides real-time feedback to users on the strength of the password entered.

## Features

- **Password strength assessment** based on:
  - Length (minimum of 8 characters)
  - Presence of both lowercase and uppercase letters
  - Presence of numbers
  - Presence of special characters (e.g., `!@#$%^&*()`)
  
- **Feedback**: The tool provides real-time feedback, categorizing the password strength as:
  - Weak
  - Medium
  - Strong

## Prerequisites

Before you can run the script, you need to have Python installed. The project uses `Tkinter`, which is included by default with Python.

## How It Works

1. **Password Length**: The password must be at least 8 characters long to contribute to its strength.
2. **Character Variety**: The presence of lowercase letters, uppercase letters, numbers, and special characters increases the strength score.
3. **Strength Levels**:
   - If a password satisfies 2 or fewer criteria, it is considered **Weak**.
   - If a password satisfies 3 to 4 criteria, it is considered **Medium**.
   - If a password satisfies all 5 criteria, it is considered **Strong**.

## How to Use

1. Clone or download the project.
2. Run the script using Python:

    ```bash
    python password_strength_checker.py
    ```

3. A window will appear prompting you to enter your password. The strength of your password will be updated in real-time as you type.

## Code Explanation

```python
import re
import tkinter as tk
from tkinter import StringVar
```
- `re` is used for regular expression checks to validate password criteria.
- `tkinter` is used to create a simple GUI for user interaction.

## Password Strength Function
```python
def assess_password_strength(password):
    strength = 0

    # Criteria checks
    if len(password) >= 8:
        strength += 1  # Length criteria
    if re.search(r'[a-z]', password):
        strength += 1  # Lowercase
    if re.search(r'[A-Z]', password):
        strength += 1  # Uppercase
    if re.search(r'\d', password):
        strength += 1  # Number
    if re.search(r'[!@#$%^&*(),.?":{}|<>]', password):
        strength += 1  # Special character

    # Feedback based on strength score
    if strength <= 2:
        return 'Weak'
    elif 3 <= strength <= 4:
        return 'Medium'
    elif strength == 5:
        return 'Strong'
```
This function checks the length of the password and uses regular expressions to verify the presence of lowercase letters, uppercase letters, numbers, and special characters. Based on the number of criteria met, it returns a strength rating.

## Real-Time Feedback
``` python
def update_strength_label(event=None):
    password = password_var.get()
    feedback = assess_password_strength(password)
    strength_label.config(text=f"Password strength: {feedback}")
```
- The update_strength_label function updates the displayed password strength as the user types, providing real-time feedback.

## GUI Layout
- The GUI consists of a label prompting the user to enter a password, a password entry box, and a label that displays the strength of the password.
```python
root = tk.Tk()
root.title("Password Strength Checker")
root.geometry("400x200")

password_var = StringVar()
tk.Label(root, text="Enter your password:", font=('Helvetica', 12)).pack(pady=10)
password_entry = tk.Entry(root, textvariable=password_var, font=('Helvetica', 12), show="*")
password_entry.pack(pady=5)

strength_label = tk.Label(root, text="Password strength: ", font=('Helvetica', 12), fg="blue")
strength_label.pack(pady=10)

password_entry.bind("<KeyRelease>", update_strength_label)
```

## Customization
- You can adjust the password criteria by modifying the regular expressions or adding new rules to the assess_password_strength function.
- You can also customize the feedback messages or add additional strength levels if needed.