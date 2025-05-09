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

# 👥 Linux User, Group, and Permission Management

A comprehensive guide to managing users, groups, and file permissions in Linux systems.

---

## 🧑‍💼 User Management

| Command                          | Description                                  | Example                                    |
|----------------------------------|----------------------------------------------|-------------------------------------------|
| `useradd username`               | Create a new user account                    | `sudo useradd john`                        |
| `useradd -m username`            | Create user with home directory              | `sudo useradd -m sarah`                    |
| `useradd -m -s /bin/bash user`   | Create user with login shell                 | `sudo useradd -m -s /bin/bash dave`        |
| `useradd -u 1500 username`       | Create user with specific UID                | `sudo useradd -u 1500 robert`              |
| `passwd username`                | Set or change a user's password              | `sudo passwd mary`                         |
| `usermod -L username`            | Lock a user account                          | `sudo usermod -L temporaryuser`            |
| `usermod -U username`            | Unlock a user account                        | `sudo usermod -U temporaryuser`            |
| `userdel username`               | Delete a user account                        | `sudo userdel john`                        |
| `userdel -r username`            | Delete user and their home directory         | `sudo userdel -r sarah`                    |
| `id username`                    | Display user ID and group memberships        | `id john`                                  |

### 📄 User Information Files

| File Path             | Description                                   | Example Command                              |
|-----------------------|-----------------------------------------------|---------------------------------------------|
| `/etc/passwd`         | User account information                      | `cat /etc/passwd` or `getent passwd john`    |
| `/etc/shadow`         | Encrypted user passwords                      | `sudo cat /etc/shadow`                       |
| `/etc/login.defs`     | User creation policy defaults                 | `cat /etc/login.defs`                        |
| `/etc/skel/`          | Template files for new user home directories  | `ls -la /etc/skel`                           |
| `/home/`              | Standard location for user home directories   | `ls -l /home`                                |

---

## 👪 Group Management

| Command                             | Description                                  | Example                               |
|-------------------------------------|----------------------------------------------|---------------------------------------|
| `groupadd groupname`                | Create a new group                           | `sudo groupadd developers`            |
| `groupadd -g 1500 groupname`        | Create group with specific GID               | `sudo groupadd -g 1500 marketing`     |
| `groupmod -n newname oldname`       | Rename a group                               | `sudo groupmod -n devs developers`    |
| `groupdel groupname`                | Delete a group                               | `sudo groupdel obsoletegroup`         |
| `usermod -g groupname username`     | Change a user's primary group                | `sudo usermod -g developers john`     |
| `usermod -a -G group1,group2 user`  | Add user to supplementary groups             | `sudo usermod -a -G sudo,docker mary` |
| `gpasswd -a username groupname`     | Add user to a group (alternative)            | `sudo gpasswd -a john developers`     |
| `gpasswd -d username groupname`     | Remove user from a group                     | `sudo gpasswd -d john developers`     |

### 📄 Group Information Files

| File Path             | Description                                   | Example Command                            |
|-----------------------|-----------------------------------------------|-------------------------------------------|
| `/etc/group`          | Group definitions                             | `cat /etc/group` or `getent group devs`   |
| `/etc/gshadow`        | Encrypted group passwords                     | `sudo cat /etc/gshadow`                   |

---

## 🔐 Understanding File Permissions

### Permission Types

| Symbol | Numeric | Permission    | Effect on Files                   | Effect on Directories              |
|--------|---------|---------------|-----------------------------------|-----------------------------------|
| `r`    | 4       | Read          | View file contents                | List directory contents           |
| `w`    | 2       | Write         | Modify file contents              | Create, rename, delete files      |
| `x`    | 1       | Execute       | Run as program/script             | Enter directory, access files     |
| `-`    | 0       | No permission | Access denied                     | Access denied                     |

### Permission Classes

| Symbol | Class   | Description                            |
|--------|---------|----------------------------------------|
| `u`    | User    | The file/directory owner               |
| `g`    | Group   | Users in the file's group              |
| `o`    | Others  | All other users                        |
| `a`    | All     | All users (same as ugo)                |

### Interpreting Permissions in `ls -l` Output

```
-rwxr-xr--  1 john developers  4096 May 1 12:34 script.sh
↑ ↑↑↑ ↑↑↑ ↑↑↑
| ||| ||| |||
| ||| ||| +++-- Others permissions (r--)
| ||| +++------ Group permissions (r-x)
| +++---------- Owner permissions (rwx)
+-------------- File type (- for regular file, d for directory)
```

---

## 🛠️ Permission Management Commands

| Command                   | Description                              | Example                                 |
|---------------------------|------------------------------------------|----------------------------------------|
| `ls -l filename`          | Show file permissions                    | `ls -l /etc/passwd`                    |
| `ls -ld directoryname`    | Show directory permissions               | `ls -ld /home/john`                    |
| `chmod permissions file`  | Change file permissions                  | `chmod 755 script.sh`                  |
| `chown user:group file`   | Change file owner and group              | `sudo chown john:developers file.txt`  |
| `chown user file`         | Change only the file owner               | `sudo chown john file.txt`             |
| `chgrp group file`        | Change only the file group               | `sudo chgrp developers file.txt`       |

### Common `chmod` Numeric Values

| Numeric | Symbolic | Meaning                            | Typical Use                     |
|---------|----------|------------------------------------|---------------------------------|
| `777`   | `rwxrwxrwx` | Full permissions for everyone     | Avoid this (security risk)      |
| `755`   | `rwxr-xr-x` | RWX for owner, RX for others      | Directories, scripts            |
| `700`   | `rwx------` | RWX for owner only                | Private scripts                 |
| `644`   | `rw-r--r--` | RW for owner, R for others        | Regular files                   |
| `600`   | `rw-------` | RW for owner only                 | Sensitive config files          |
| `444`   | `r--r--r--` | Read-only for all                 | Public reference files          |

### Using Symbolic Mode with `chmod`

| Command                        | Description                                       |
|--------------------------------|---------------------------------------------------|
| `chmod u+x file`               | Add execute permission for owner                  |
| `chmod g-w file`               | Remove write permission from group                |
| `chmod o=r file`               | Set other permissions to read-only                |
| `chmod a+r file`               | Add read permission for all (same as +r)          |
| `chmod ug+rw,o-rwx file`       | Add RW for user & group, remove all for others    |
| `chmod -R g+w directory`       | Recursively add write permission for group        |

---

## 🔑 Special Permissions

| Command                | Description                                     | Effect                                       |
|------------------------|-------------------------------------------------|----------------------------------------------|
| `chmod u+s file`       | Set SUID bit                                    | Execute as file owner regardless of user     |
| `chmod 4755 file`      | Set SUID (numeric)                              | Same as above                                |
| `chmod g+s file`       | Set SGID bit on file                            | Execute with file's group permissions        |
| `chmod g+s directory`  | Set SGID bit on directory                       | New files inherit directory's group          |
| `chmod 2755 file`      | Set SGID (numeric)                              | Same as `g+s`                                |
| `chmod o+t directory`  | Set sticky bit                                  | Only owner can delete files in directory     |
| `chmod 1777 directory` | Set sticky bit (numeric)                        | Same as `o+t`                                |
| `ls -la /tmp`          | Example of sticky bit directory                 | Notice the `t` in permissions                |

### Special Permission Examples

| Command                        | Description                                       | Example Use Case                           |
|--------------------------------|---------------------------------------------------|-------------------------------------------|
| `ls -l /usr/bin/passwd`        | SUID example (notice the `s`)                     | Allows users to change their own password  |
| `ls -ld /var/mail`             | SGID example on directory                         | Mail files inherit mail group              |
| `ls -ld /tmp`                  | Sticky bit example                                | Public directory where only owners can delete |

---

## 🧩 Advanced Permission Topics

### Default Permissions with `umask`

| Command                | Description                                     | Default Result                              |
|------------------------|-------------------------------------------------|--------------------------------------------|
| `umask`                | Display current umask value                     | Typically `022` or `002`                    |
| `umask 022`            | Set umask value                                 | Files: 644, Directories: 755                |
| `umask 027`            | More restrictive umask                          | Files: 640, Directories: 750                |

### Access Control Lists (ACLs)

| Command                            | Description                                  | Example                                     |
|------------------------------------|----------------------------------------------|---------------------------------------------|
| `getfacl file`                     | Show ACLs for a file                         | `getfacl /shared/project.txt`               |
| `setfacl -m u:user:rw file`        | Give specific user permissions               | `setfacl -m u:john:rw /shared/project.txt` |
| `setfacl -m g:group:rx file`       | Give specific group permissions              | `setfacl -m g:devs:rx /shared/script.sh`   |
| `setfacl -x u:user file`           | Remove specific user ACL                     | `setfacl -x u:john /shared/project.txt`    |
| `setfacl -b file`                  | Remove all ACLs                              | `setfacl -b /shared/project.txt`           |

---

## 🔍 Permission Troubleshooting

### Common Issues & Solutions

| Issue                            | Possible Solutions                                    |
|----------------------------------|------------------------------------------------------|
| Cannot access directory          | Check execute (`x`) permission on directory           |
| Cannot list directory contents   | Check read (`r`) permission on directory              |
| Cannot create files in directory | Check write (`w`) permission on directory             |
| Cannot modify a file             | Check write (`w`) permission on file                  |
| Cannot run a script              | Check execute (`x`) permission, use `chmod +x script` |
| Permission denied despite rights | Check parent directory permissions                    |

### Security Best Practices

1. **Follow the principle of least privilege**
   ```bash
   # Instead of 777, use more restrictive permissions
   chmod 750 script.sh
   ```

2. **Use groups for collaborative work**
   ```bash
   # Create a project group
   sudo groupadd project1
   # Add users to the group
   sudo gpasswd -a john project1
   sudo gpasswd -a mary project1
   # Set directory for collaboration
   sudo mkdir /shared/project1
   sudo chgrp project1 /shared/project1
   sudo chmod 2775 /shared/project1
   ```

3. **Set secure umask in shell startup files**
   ```bash
   # Add to ~/.bashrc for more security
   umask 027
   ```

4. **Use ACLs for complex permissions**
   ```bash
   # Give read-only access to one user, read-write to another
   setfacl -m u:guest:r,u:developer:rw /shared/project/config
   ```

---

## ✅ Quick Reference Examples

### Creating a New User with Specific Settings

```bash
# Create user with custom settings
sudo useradd -m -s /bin/bash -c "John Doe" -g developers john
# Set initial password
sudo passwd john
# Add to supplementary groups
sudo usermod -a -G sudo,docker john
```

### Setting Up a Shared Directory for a Group

```bash
# Create group
sudo groupadd project
# Add users to group
sudo gpasswd -a user1 project
sudo gpasswd -a user2 project
# Create and configure shared directory
sudo mkdir -p /shared/project
sudo chown root:project /shared/project
sudo chmod 2775 /shared/project
# Verify setup
ls -ld /shared/project
```

### Fixing Common Permission Problems

```bash
# Make a script executable
chmod +x script.sh

# Fix "Permission denied" for a directory structure
find /path/to/dir -type d -exec chmod 755 {} \;
find /path/to/dir -type f -exec chmod 644 {} \;

# Allow group members to modify files
chmod g+w filename
# or recursively for directories
chmod -R g+w directory
```

---