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

# 📁 Linux Filesystem Overview 

This is a quick reference to the main Linux filesystem directories and their purposes.

---

## 🌲 Root Directory `/`

- Top-level directory; everything starts from here.

---

## 🏠 `/home`  
- User directories (e.g., `/home/alice`).

## 👑 `/root`  
- Home of the `root` (admin) user.

---

## ⚙️ `/bin`  
- Essential commands for all users (`ls`, `cp`, etc.).

## 🔧 `/sbin`  
- System/admin commands (`reboot`, `fsck`).

## 📦 `/usr`  
- User software and libraries.
  - `/usr/bin`, `/usr/sbin`, `/usr/lib`, etc.

## 📚 `/lib` and `/lib64`  
- Shared libraries needed by `/bin` and `/sbin`.

---

## 📝 `/etc`  
- System configuration files (`passwd`, `hosts`, etc.).

## 💾 `/var`  
- Variable data: logs, mail, cache (`/var/log`, `/var/spool`).

## 🧠 `/proc`  
- Virtual system info (CPU, memory, processes).

## 💻 `/dev`  
- Device files (`/dev/sda`, `/dev/null`).

---

## 🧪 `/tmp`  
- Temporary files; cleared on reboot.

## 📁 `/mnt`  
- Temporary mount point (e.g., for admin).

## 💿 `/media`  
- Auto-mounted external drives (USB, DVD).

## 📦 `/opt`  
- Optional third-party software.

## 🚀 `/boot`  
- Kernel and bootloader files.

## 🔄 `/run`  
- Runtime data (PID files, sockets); resets on reboot.

---

## 📑 Summary Table

| Directory | Purpose                       |
|-----------|-------------------------------|
| `/`       | Root of the system            |
| `/home`   | User files                    |
| `/root`   | Admin home                    |
| `/bin`    | Basic commands                |
| `/sbin`   | System commands               |
| `/usr`    | User software                 |
| `/lib`    | Libraries                     |
| `/etc`    | Config files                  |
| `/var`    | Logs, cache, spool            |
| `/proc`   | Kernel & process info         |
| `/dev`    | Devices                       |
| `/tmp`    | Temporary files               |
| `/mnt`    | Manual mounts                 |
| `/media`  | Auto mounts (USB, etc.)       |
| `/opt`    | Optional software             |
| `/boot`   | Bootloader & kernel           |
| `/run`    | Runtime data                  |

---

# 🧰 Basic Linux Commands (Quick Revision)

Essential commands for navigating and managing the Linux system.

---

## 👤 User & Session

| Command            | Description                                 |
|--------------------|---------------------------------------------|
| `id`               | Show current user ID and group info         |
| `id username`      | Show ID info for a specific user            |
| `su -`             | Switch to root user (with login environment)|
| `exit`             | Exit the current shell/user session         |

---

## 💿 CD-ROM Control

| Command       | Description                          |
|---------------|--------------------------------------|
| `eject`       | Eject the CD-ROM tray                |
| `eject -t`    | Close the CD-ROM tray                |

---

## 📂 File & Directory Navigation

| Command            | Description                                     |
|--------------------|-------------------------------------------------|
| `ls`               | List files in current directory                 |
| `ls /`             | List files in the root directory                |
| `pwd`              | Show current working directory                  |
| `cd`               | Change to home directory                        |
| `cd -`             | Switch to previous directory                    |
| `cd ~`             | Go to current user's home directory             |
| `cd ~user`         | Go to another user's home directory             |
| `cd ..`            | Move to parent directory                        |
| `.`                | Refers to current directory                     |
| `..`               | Refers to parent directory                      |

---

## 📄 File Handling

| Command        | Description                                   |
|----------------|-----------------------------------------------|
| `cat`          | Display contents of a file                    |
| `touch`        | Create a new empty file                       |

---

## ✅ Tip
- Use `man <command>` to learn more about any command.
---
# 📁 File System Utilities 

Common commands for creating, copying, moving, and deleting files and directories in Linux.

---

## 🌳 Directory Structure

| Command      | Description                          |
|--------------|--------------------------------------|
| `tree`       | Display directory tree structure     |

---

## 📂 Create Directories

| Command                                | Description                                   |
|----------------------------------------|-----------------------------------------------|
| `mkdir dirname`                        | Create a directory named `dirname`            |
| `mkdir dirname1 dirname2 dirname3`     | Create multiple directories at once           |

---

## 📄 Copy Files & Directories

| Command                              | Description                                             |
|--------------------------------------|---------------------------------------------------------|
| `cp file file2`                      | Copy `file` to `file2`                                  |
| `cp file /tmp`                       | Copy `file` to `/tmp` directory                         |
| `cp -r dir1 /dir2/`                  | Recursively copy `dir1` into `/dir2/`                   |
| `cp -r dir/ /tmp/report`             | Recursively copy `dir/` into `/tmp/report`              |

---

## 📦 Move or Rename

| Command                              | Description                                             |
|--------------------------------------|---------------------------------------------------------|
| `mv work/ /var/`                     | Move `work/` directory to `/var/`                       |
| `mv dir1 /tmp/newdir`                | Move `dir1` to `/tmp/newdir`                            |
| `mv file newname_file`              | Rename `file` to `newname_file`                        |

---

## 🗑️ Delete Files & Directories

| Command               | Description                                      |
|------------------------|--------------------------------------------------|
| `rm file`              | Remove a file named `file`                       |
| `rmdir dir2`           | Remove empty directory `dir2`                    |
| `rm -r dir2`           | Remove `dir2` and its contents recursively       |
| `rm -rf dir`           | Forcefully remove `dir` and everything inside    |

---

## ✅ Tips

- Use `-r` with `cp` and `rm` for recursive operations.
- Add `-f` to `rm` to **force** deletion without prompts.
- Always double-check paths before running `rm -rf`.

---

# 📁 More Linux Commands 

This section extends basic Linux commands with options for listing files, managing the terminal, and handling background processes.

---

## 📄 File Listing with `ls`

| Command        | Description                                      |
|----------------|--------------------------------------------------|
| `ls -l`        | Long format listing (details like permissions)   |
| `ls -a`        | Show all files, including hidden (`.` dotfiles)  |
| `ls -R`        | List directories and subdirectories recursively  |
| `ls -r`        | List files in reverse order                      |

---

## 🧼 Terminal Management

| Command        | Description                          |
|----------------|--------------------------------------|
| `clear`        | Clears the terminal screen           |
| `reset`        | Resets terminal to default state     |

---

## 🧠 Process Control

| Command | Description                                      |
|---------|--------------------------------------------------|
| `bg`    | Resume a suspended process in the background     |

---

## ✅ Tip

- Use `ls -la` to combine long listing with hidden files.
- Use `jobs`, `fg`, and `bg` to manage foreground/background tasks.

---
# ⌨️ Linux Shortcuts & System Commands 

Useful keyboard shortcuts and system power commands to streamline terminal usage and manage the system.

---

## 🧭 Cursor Movement & Text Editing

| Shortcut     | Description                                            |
|--------------|--------------------------------------------------------|
| `Ctrl + A`   | Move cursor to the **beginning** of the line           |
| `Ctrl + E`   | Move cursor to the **end** of the line                 |
| `Ctrl + K`   | Delete from cursor to the **end** of the line          |
| `Ctrl + U`   | Delete from cursor to the **beginning** of the line    |
| `Ctrl + Y`   | **Paste** text cut by `Ctrl + K` or `Ctrl + U`         |

---

## 🖥️ Terminal & Process Control

| Shortcut     | Description                                            |
|--------------|--------------------------------------------------------|
| `Ctrl + D`   | Logout / exit shell, or delete character under cursor  |
| `Ctrl + L`   | Clear the terminal screen                              |
| `Ctrl + C`   | Cancel the current command                             |
| `Ctrl + Z`   | Suspend the current foreground process                 |
| `Ctrl + S`   | Pause terminal output (XOFF)                           |
| `Ctrl + Q`   | Resume terminal output (XON)                           |

---

## 🔄 Reboot & Shutdown Commands

| Command                | Description                          |
|------------------------|--------------------------------------|
| `reboot`               | Restart the system                   |
| `shutdown -r now`      | Shutdown and restart immediately     |
| `systemctl reboot`     | Reboot using systemd                 |
| `init 6`               | Reboot via runlevel change           |
| `shutdown -h now`      | Shutdown immediately                 |
| `systemctl shutdown`   | Shutdown using systemd               |
| `init 0`               | Halt the system                      |

---

## 🧪 Command Chaining

| Command         | Description                                       |
|------------------|--------------------------------------------------|
| `ls; date`       | Run `ls` and then `date` in sequence             |

---

## ✅ Tip

- Combine shortcuts with command history (`↑`, `↓`) for faster navigation.
- Use `man shutdown` or `man systemctl` for more options.

---
