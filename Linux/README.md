# 📘 TTY in Red Hat Enterprise Linux 9 (RHEL 9)

## 🧾 What is TTY?

**TTY** stands for **Teletypewriter**. In Linux systems like **RHEL 9**, it refers to **virtual text-based terminals** that allow direct interaction with the shell, independent of the graphical interface.

Originally, TTYs were physical terminals. In modern systems, they are implemented as **virtual consoles** accessible via keyboard shortcuts.

---

## 🧭 Purpose of TTY

- Provides a **fallback interface** when the GUI crashes or fails to load
- Allows **low-level system access** for maintenance or administration
- Useful for **multi-user sessions**, scripting, and diagnostics

---

## 🖥️ Accessing TTY in RHEL 9

### 🔄 From GUI to TTY

To switch from the GNOME GUI to a TTY console:

1. Press one of the following key combinations:
   - **Ctrl + Alt + F3**
   - **Ctrl + Alt + F4**
   - **Ctrl + Alt + F5**
   - **Ctrl + Alt + F6**

> ✅ In RHEL 9, TTYs typically start from **F3** to **F6**.

2. Alternatively, use the `chvt` command (if you have appropriate permissions):
   ```bash
   sudo chvt 3    # Switch to TTY3
   ```

3. A black screen with a login prompt will appear where you can enter your **username** and **password** to access the shell.

### ↩️ From TTY Back to GUI

To return to the GNOME GUI session:

1. Press **Ctrl + Alt + F2**
2. You will be taken back to the graphical interface

> 📌 RHEL 9 uses **TTY2** for the GNOME graphical session by default.

---

## 🛠️ Example Use Cases for TTY

- Restart a failed graphical session:  
  ```bash
  sudo systemctl restart gdm
  ```

- Troubleshoot when X server fails:
  ```bash
  # Check X server logs
  cat /var/log/Xorg.0.log | grep EE
  
  # Restart the system
  sudo reboot
  ```

- Install graphics drivers from command line:
  ```bash
  sudo dnf install kernel-devel
  sudo dnf install gcc
  # Run driver installation script
  ```

---

# 📁 Linux Filesystem Hierarchy

This is a comprehensive reference to the main Linux filesystem directories and their purposes.

---

## 🌲 Root Structure

| Directory | Purpose                           | Examples                              |
|-----------|-----------------------------------|---------------------------------------|
| `/`       | Root of filesystem hierarchy      | Contains all other directories        |
| `/home`   | User home directories             | `/home/alice`, `/home/bob`            |
| `/root`   | Home directory for `root` user    | Configuration files for root user     |

---

## ⚙️ System Binaries & Libraries

| Directory       | Purpose                           | Examples                          |
|-----------------|-----------------------------------|-----------------------------------|
| `/bin`          | Essential commands for all users  | `ls`, `cp`, `mv`, `bash`          |
| `/sbin`         | System administration commands    | `fdisk`, `mkfs`, `reboot`         |
| `/lib`, `/lib64`| Shared libraries                  | Libraries needed by `/bin`, `/sbin` |
| `/usr`          | User programs and data            | Applications, documentation       |
| `/usr/bin`      | Non-essential user commands       | `git`, `firefox`, `vim`           |
| `/usr/sbin`     | Non-essential admin commands      | `useradd`, `groupadd`             |

---

## 📝 System Configuration & Data

| Directory     | Purpose                           | Examples                              |
|---------------|-----------------------------------|---------------------------------------|
| `/etc`        | System configuration files        | `/etc/passwd`, `/etc/fstab`           |
| `/var`        | Variable data files               | Logs, mail spools, caches             |
| `/var/log`    | System log files                  | `/var/log/messages`, `/var/log/syslog`|
| `/proc`       | Virtual filesystem for kernel     | Process information, system stats     |
| `/sys`        | Virtual filesystem for hardware   | Hardware information, driver control  |
| `/dev`        | Device files                      | `/dev/sda`, `/dev/null`, `/dev/tty`   |

---

## 🧪 Special Purpose Directories

| Directory     | Purpose                           | Examples                              |
|---------------|-----------------------------------|---------------------------------------|
| `/tmp`        | Temporary files                   | Cleared on reboot                     |
| `/boot`       | Boot loader files                 | Kernel, initramfs, GRUB configuration |
| `/mnt`        | Mount point for filesystems       | Manual mount point for admin use      |
| `/media`      | Mount point for removable media   | USB drives, CD-ROMs                   |
| `/opt`        | Optional application software     | Third-party applications              |
| `/run`        | Runtime variable data             | PID files, socket files               |

---

# 🧰 Essential Linux Commands

## 👤 User & Session Management

| Command              | Description                                     | Example                         |
|----------------------|-------------------------------------------------|---------------------------------|
| `whoami`             | Display current username                        | `whoami`                        |
| `id`                 | Show user ID and group memberships              | `id`, `id username`             |
| `su`                 | Switch user                                     | `su john`, `su -` (for root)    |
| `sudo`               | Execute command as another user                 | `sudo dnf update`               |
| `passwd`             | Change password                                 | `passwd`, `sudo passwd user`    |
| `exit`               | Exit current shell/session                      | `exit`                          |
| `logout`             | Log out of current session                      | `logout`                        |

---

## 📂 File & Directory Navigation

| Command              | Description                                     | Example                         |
|----------------------|-------------------------------------------------|---------------------------------|
| `pwd`                | Print working directory                         | `pwd`                           |
| `cd`                 | Change directory                                | `cd /etc`, `cd ~`, `cd ..`      |
| `ls`                 | List directory contents                         | `ls -la`, `ls /var`             |
| `ls -l`              | Long listing with details                       | `ls -l /etc/passwd`             |
| `ls -a`              | Show all files including hidden                 | `ls -a ~`                       |
| `ls -lh`             | Human-readable file sizes                       | `ls -lh /var/log`               |
| `ls -R`              | Recursive listing                               | `ls -R /etc/ssh`                |
| `tree`               | Display directory tree                          | `tree`, `tree -L 2`             |
| `find`               | Search for files                                | `find /home -name "*.txt"`      |

---

## 📄 File Operations

| Command              | Description                                     | Example                          |
|----------------------|-------------------------------------------------|----------------------------------|
| `cat`                | Display file content                            | `cat /etc/hosts`                 |
| `less`               | View file with pagination                       | `less /var/log/messages`         |
| `head`               | Show first lines of file                        | `head -n 10 file.txt`            |
| `tail`               | Show last lines of file                         | `tail -f /var/log/syslog`        |
| `touch`              | Create empty file or update timestamp           | `touch newfile.txt`              |
| `mkdir`              | Create directory                                | `mkdir -p dir1/dir2`             |
| `cp`                 | Copy files or directories                       | `cp -r source/ dest/`            |
| `mv`                 | Move or rename files                            | `mv oldname newname`             |
| `rm`                 | Remove files or directories                     | `rm -rf directory/`              |
| `rmdir`              | Remove empty directories                        | `rmdir emptydir`                 |
| `chmod`              | Change file permissions                         | `chmod 755 script.sh`            |
| `chown`              | Change file owner                               | `chown user:group file`          |

---

## 💿 System Information & Control

| Command              | Description                                     | Example                          |
|----------------------|-------------------------------------------------|----------------------------------|
| `uname -a`           | Show system information                         | `uname -a`                       |
| `hostname`           | Show or set system hostname                     | `hostname`                       |
| `df -h`              | Show disk usage                                 | `df -h`                          |
| `free -h`            | Display memory usage                            | `free -h`                        |
| `top`                | Dynamic process viewer                          | `top`                            |
| `htop`               | Enhanced process viewer                         | `htop`                           |
| `ps aux`             | List all running processes                      | `ps aux | grep firefox`          |
| `systemctl`          | Control systemd services                        | `systemctl status sshd`          |
| `journalctl`         | Query systemd journal                           | `journalctl -u sshd`             |
| `reboot`             | Restart system                                  | `sudo reboot`                    |
| `shutdown`           | Shutdown system                                 | `sudo shutdown -h now`           |
| `eject`              | Eject removable media                           | `eject`, `eject -t`              |

---

## 🧭 Text Processing

| Command              | Description                                     | Example                          |
|----------------------|-------------------------------------------------|----------------------------------|
| `grep`               | Search text patterns                            | `grep "error" /var/log/syslog`   |
| `sed`                | Stream editor for text manipulation             | `sed 's/old/new/g' file.txt`     |
| `awk`                | Text processing language                        | `awk '{print $1}' file.txt`      |
| `sort`               | Sort lines in text files                        | `sort -n numbers.txt`            |
| `uniq`               | Report or filter repeated lines                 | `sort file.txt | uniq`           |
| `wc`                 | Count lines, words, and characters              | `wc -l file.txt`                 |

---

## ⌨️ Terminal Shortcuts

| Shortcut           | Description                                     |
|--------------------|-------------------------------------------------|
| `Ctrl + A`         | Move cursor to beginning of line                |
| `Ctrl + E`         | Move cursor to end of line                      |
| `Ctrl + U`         | Delete from cursor to beginning of line         |
| `Ctrl + K`         | Delete from cursor to end of line               |
| `Ctrl + L`         | Clear terminal screen                           |
| `Ctrl + C`         | Interrupt/kill current process                  |
| `Ctrl + Z`         | Suspend current process                         |
| `Ctrl + D`         | Exit shell or terminate input                   |
| `Ctrl + R`         | Search command history                          |
| `Tab`              | Auto-complete commands and filenames            |
| `↑` / `↓`          | Navigate command history                        |

---

## 🔄 Command Chaining & Redirection

| Operator            | Description                                     | Example                          |
|---------------------|-------------------------------------------------|----------------------------------|
| `command1 ; command2` | Run commands sequentially                     | `cd /tmp ; ls`                   |
| `command1 && command2` | Run command2 only if command1 succeeds       | `mkdir dir && cd dir`            |
| `command1 || command2` | Run command2 only if command1 fails          | `ping -c1 server || echo "down"` |
| `command > file`    | Redirect output to file (overwrite)             | `ls > listing.txt`               |
| `command >> file`   | Redirect output to file (append)                | `echo "text" >> log.txt`         |
| `command < file`    | Read input from file                            | `sort < unsorted.txt`            |
| `command1 | command2` | Pipe output of command1 to command2           | `cat file.txt | grep "error"`    |

---

## 🧪 Process Management

| Command              | Description                                     | Example                          |
|----------------------|-------------------------------------------------|----------------------------------|
| `jobs`               | List background jobs                            | `jobs`                           |
| `bg`                 | Resume suspended job in background              | `bg %1`                          |
| `fg`                 | Bring background job to foreground              | `fg %1`                          |
| `kill`               | Send signal to process                          | `kill -9 1234`                   |
| `killall`            | Kill processes by name                          | `killall firefox`                |
| `nohup`              | Run command immune to hangups                   | `nohup command &`                |
| `nice`               | Run command with modified priority              | `nice -n 19 command`             |

---

## ✅ Tips & Tricks

- Add `-i` to `rm`, `mv`, and `cp` for interactive mode (ask before overwriting)
- Use `sudo !!` to repeat the previous command with sudo
- `cd -` switches to the previous directory
- Use wildcards (`*`, `?`) with caution in `rm` commands
- Always backup important data before major system changes
- For detailed help on any command: `man command` or `command --help`

---