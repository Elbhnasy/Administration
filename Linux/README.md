# 📘 TTY in Red Hat Enterprise Linux 9 (RHEL 9)

## 🧾 What is TTY?

**TTY** stands for **Teletypewriter**. In Linux systems like **RHEL 9**, it refers to **virtual text-based terminals** that allow direct interaction with the shell, independent of the graphical interface.

Originally, TTYs were physical terminals. In modern systems, they are implemented as **virtual consoles** accessible via keyboard shortcuts.

---

## 🧭 Purpose of TTY

- Provides a **fallback interface** when the GUI crashes or fails to load.
- Allows **low-level system access** for maintenance or administration.
- Useful for **multi-user sessions**, scripting, and diagnostics.

---

## 🖥️ Accessing TTY in RHEL 9

### 🔄 From GUI to TTY

To switch from the GNOME GUI to a TTY console:

1. Press one of the following key combinations:

Ctrl + Alt + F3
Ctrl + Alt + F4
Ctrl + Alt + F5

2. chvt <tty_number> (e.g., chvt 3)
---

> ✅ In RHEL 9, TTYs typically start from **F3** to **F6**.

2. A black screen with a login prompt will appear:

3. Enter your **username** and **password** to access the shell.

---

### ↩️ From TTY Back to GUI

To return to the GNOME GUI session (usually on TTY2):

1. Press **Ctrl + Alt + F2**.
2. You will be taken back to the graphical interface.
---

> 📌 RHEL 9 uses **TTY2** for the GNOME graphical session by default.

---

## 🛠️ Example Use Cases

- Restart graphical session:  
  ```bash
  sudo systemctl restart gdm
  sudo reboot
  ```