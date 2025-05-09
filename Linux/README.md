# 🐧 RHEL 9 & Linux Essentials - Complete Revision Guide

<div align="center">
  
  ![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
  ![Red Hat](https://img.shields.io/badge/Red%20Hat-EE0000?style=for-the-badge&logo=redhat&logoColor=white)
  ![Terminal](https://img.shields.io/badge/Terminal-4D4D4D?style=for-the-badge&logo=windows-terminal&logoColor=white)
  
</div>

## 📚 Table of Contents
- [TTY in Red Hat Enterprise Linux 9](#-tty-in-red-hat-enterprise-linux-9)
- [Linux Filesystem Hierarchy](#-linux-filesystem-hierarchy)
- [Essential Linux Commands](#-essential-linux-commands)
- [User, Group & Permission Management](#-linux-user-group-and-permission-management)

---

# 🖥️ TTY in Red Hat Enterprise Linux 9

## What is TTY?

**TTY** (Teletypewriter) refers to virtual text-based terminals in RHEL 9 that provide direct shell access independent of the graphical interface.

**Key Points:**
- Originally physical terminals, now implemented as virtual consoles
- Accessible via keyboard shortcuts
- Essential for system troubleshooting and recovery

## Purpose of TTY

- ⚠️ **Fallback interface** when GUI crashes
- 🔧 **Low-level system access** for maintenance
- 👥 **Multi-user sessions** capability
- 📊 **Diagnostics** without graphical overhead

## Accessing TTY

### From GUI to TTY
```
Ctrl + Alt + F3    # TTY3
Ctrl + Alt + F4    # TTY4
Ctrl + Alt + F5    # TTY5
Ctrl + Alt + F6    # TTY6
```

> 💡 **Pro Tip:** In RHEL 9, TTYs typically start from F3 to F6

Alternatively (with root privileges):
```bash
sudo chvt 3    # Switch to TTY3
```

### From TTY Back to GUI
```
Ctrl + Alt + F2    # Back to GNOME session
```

> 💡 **Pro Tip:** RHEL 9 uses TTY2 for the GNOME graphical session by default

## Common TTY Use Cases

```bash
# Restart a failed graphical session
sudo systemctl restart gdm

# Troubleshoot X server issues
cat /var/log/Xorg.0.log | grep EE

# Install drivers from command line when GUI unavailable
sudo dnf install kernel-devel gcc
```

---

# 📁 Linux Filesystem Hierarchy

## Root Structure

| Directory | Purpose | Contents |
|:----------|:--------|:---------|
| `/` | Root of filesystem | Contains all other directories |
| `/home` | User home directories | `/home/username` directories |
| `/root` | Root user's home | Root user configuration files |

## System Binaries & Libraries

| Directory | Purpose | Contains |
|:----------|:--------|:---------|
| `/bin` | Essential commands | `ls`, `cp`, `mv`, `bash` |
| `/sbin` | System admin commands | `fdisk`, `mkfs`, `reboot` |
| `/lib`, `/lib64` | Shared libraries | Libraries for `/bin` & `/sbin` |
| `/usr` | User programs | Applications, docs, most software |
| `/usr/bin` | Non-essential commands | `git`, `firefox`, `vim` |
| `/usr/sbin` | Admin commands | `useradd`, `groupadd` |

## System Configuration & Data

| Directory | Purpose | Contains |
|:----------|:--------|:---------|
| `/etc` | System config files | `/etc/passwd`, `/etc/fstab` |
| `/var` | Variable data | Logs, mail spools, caches |
| `/var/log` | System logs | Messages, audit logs, app logs |
| `/proc` | Virtual kernel filesystem | Process info, system stats |
| `/sys` | Virtual hardware filesystem | Hardware info, driver control |
| `/dev` | Device files | `sda`, `null`, `tty` devices |

## Special Purpose Directories

| Directory | Purpose | Notes |
|:----------|:--------|:------|
| `/tmp` | Temporary files | Cleared on reboot |
| `/boot` | Boot loader files | Kernel, initramfs, GRUB config |
| `/mnt` | Manual filesystems mount | For admin use |
| `/media` | Removable media | USB drives, optical media |
| `/opt` | Optional applications | Third-party software |
| `/run` | Runtime variable data | PID files, socket files |

---

# 🧰 Essential Linux Commands

## User & Session Management

| Command | Description | Example |
|:--------|:------------|:--------|
| `whoami` | Show current username | `whoami` |
| `id` | Display user & group IDs | `id`, `id username` |
| `su` | Switch user | `su john`, `su -` (for root) |
| `sudo` | Execute as another user | `sudo dnf update` |
| `passwd` | Change password | `passwd`, `sudo passwd user` |
| `exit` | Exit current shell | `exit` |
| `logout` | Log out of session | `logout` |

## File & Directory Navigation

| Command | Description | Example |
|:--------|:------------|:--------|
| `pwd` | Print working directory | `pwd` |
| `cd` | Change directory | `cd /etc`, `cd ~`, `cd ..` |
| `ls` | List directory contents | `ls -la`, `ls /var` |
| `ls -l` | Long listing with details | `ls -l /etc/passwd` |
| `ls -a` | Show all files (inc. hidden) | `ls -a ~` |
| `ls -lh` | Human-readable sizes | `ls -lh /var/log` |
| `ls -R` | Recursive listing | `ls -R /etc/ssh` |
| `tree` | Display directory tree | `tree`, `tree -L 2` |
| `find` | Search for files | `find /home -name "*.txt"` |

## File Operations

| Command | Description | Example |
|:--------|:------------|:--------|
| `cat` | Display file content | `cat /etc/hosts` |
| `less` | View file with pagination | `less /var/log/messages` |
| `head` | Show first lines | `head -n 10 file.txt` |
| `tail` | Show last lines | `tail -f /var/log/syslog` |
| `touch` | Create empty file | `touch newfile.txt` |
| `mkdir` | Create directory | `mkdir -p dir1/dir2` |
| `cp` | Copy files/directories | `cp -r source/ dest/` |
| `mv` | Move or rename files | `mv oldname newname` |
| `rm` | Remove files/directories | `rm -rf directory/` ⚠️ |
| `rmdir` | Remove empty directories | `rmdir emptydir` |
| `chmod` | Change file permissions | `chmod 755 script.sh` |
| `chown` | Change file owner | `chown user:group file` |

## System Information & Control

| Command | Description | Example |
|:--------|:------------|:--------|
| `uname -a` | System information | `uname -a` |
| `hostname` | Show/set hostname | `hostname` |
| `df -h` | Disk usage | `df -h` |
| `free -h` | Memory usage | `free -h` |
| `top` | Process viewer | `top` |
| `htop` | Enhanced process viewer | `htop` |
| `ps aux` | List processes | `ps aux | grep firefox` |
| `systemctl` | Manage systemd services | `systemctl status sshd` |
| `journalctl` | Query systemd journal | `journalctl -u sshd` |
| `reboot` | Restart system | `sudo reboot` |
| `shutdown` | Shutdown system | `sudo shutdown -h now` |

## Text Processing

| Command | Description | Example |
|:--------|:------------|:--------|
| `grep` | Search text patterns | `grep "error" /var/log/syslog` |
| `sed` | Stream editor | `sed 's/old/new/g' file.txt` |
| `awk` | Text processing language | `awk '{print $1}' file.txt` |
| `sort` | Sort lines | `sort -n numbers.txt` |
| `uniq` | Filter repeated lines | `sort file.txt \| uniq` |
| `wc` | Count lines/words/chars | `wc -l file.txt` |

## Terminal Shortcuts

| Shortcut | Action |
|:---------|:-------|
| `Ctrl + A` | Move to beginning of line |
| `Ctrl + E` | Move to end of line |
| `Ctrl + U` | Delete from cursor to start |
| `Ctrl + K` | Delete from cursor to end |
| `Ctrl + L` | Clear screen |
| `Ctrl + C` | Kill current process |
| `Ctrl + Z` | Suspend process |
| `Ctrl + D` | Exit shell/terminate input |
| `Ctrl + R` | Search command history |
| `Tab` | Auto-complete |
| `↑` / `↓` | Navigate history |

## Command Chaining & Redirection

| Operator | Description | Example |
|:---------|:------------|:--------|
| `cmd1 ; cmd2` | Run sequentially | `cd /tmp ; ls` |
| `cmd1 && cmd2` | Run cmd2 if cmd1 succeeds | `mkdir dir && cd dir` |
| `cmd1 \|\| cmd2` | Run cmd2 if cmd1 fails | `ping -c1 server \|\| echo "down"` |
| `cmd > file` | Redirect output (overwrite) | `ls > listing.txt` |
| `cmd >> file` | Redirect output (append) | `echo "text" >> log.txt` |
| `cmd < file` | Read input from file | `sort < unsorted.txt` |
| `cmd1 \| cmd2` | Pipe output to next command | `cat file.txt \| grep "error"` |

## Process Management

| Command | Description | Example |
|:--------|:------------|:--------|
| `jobs` | List background jobs | `jobs` |
| `bg` | Resume job in background | `bg %1` |
| `fg` | Bring job to foreground | `fg %1` |
| `kill` | Send signal to process | `kill -9 1234` |
| `killall` | Kill processes by name | `killall firefox` |
| `nohup` | Run immune to hangups | `nohup command &` |
| `nice` | Run with modified priority | `nice -n 19 command` |

## Power User Tips

- `sudo !!` - Repeat previous command with sudo
- `cd -` - Switch to previous directory
- Add `-i` to destructive commands for safety: `rm -i`, `mv -i`
- Use tab completion to save typing and avoid errors
- For detailed help: `man command` or `command --help`

---

# 👥 Linux User, Group, and Permission Management

## User Management

### Core Commands

| Command | Description | Example |
|:--------|:------------|:--------|
| `useradd username` | Create user | `sudo useradd john` |
| `useradd -m username` | Create with home dir | `sudo useradd -m sarah` |
| `useradd -m -s /bin/bash user` | Create with login shell | `sudo useradd -m -s /bin/bash dave` |
| `passwd username` | Set/change password | `sudo passwd mary` |
| `usermod -L username` | Lock account | `sudo usermod -L temporaryuser` |
| `usermod -U username` | Unlock account | `sudo usermod -U temporaryuser` |
| `userdel username` | Delete account | `sudo userdel john` |
| `userdel -r username` | Delete account & home | `sudo userdel -r sarah` |
| `id username` | Show IDs & groups | `id john` |

### User Information Files

| File | Purpose | View Command |
|:-----|:--------|:-------------|
| `/etc/passwd` | User account info | `cat /etc/passwd` |
| `/etc/shadow` | Encrypted passwords | `sudo cat /etc/shadow` |
| `/etc/login.defs` | User creation defaults | `cat /etc/login.defs` |
| `/etc/skel/` | New home dir templates | `ls -la /etc/skel` |

## Group Management

### Core Commands

| Command | Description | Example |
|:--------|:------------|:--------|
| `groupadd groupname` | Create group | `sudo groupadd developers` |
| `groupmod -n newname oldname` | Rename group | `sudo groupmod -n devs developers` |
| `groupdel groupname` | Delete group | `sudo groupdel obsoletegroup` |
| `usermod -g group user` | Change primary group | `sudo usermod -g developers john` |
| `usermod -a -G g1,g2 user` | Add to groups | `sudo usermod -a -G sudo,docker mary` |
| `gpasswd -a user group` | Add to group | `sudo gpasswd -a john developers` |
| `gpasswd -d user group` | Remove from group | `sudo gpasswd -d john developers` |

### Group Information Files

| File | Purpose | View Command |
|:-----|:--------|:-------------|
| `/etc/group` | Group definitions | `cat /etc/group` |
| `/etc/gshadow` | Group passwords | `sudo cat /etc/gshadow` |

## Understanding File Permissions

### Permission Types

| Symbol | Value | Type | File Effect | Directory Effect |
|:-------|:------|:-----|:------------|:----------------|
| `r` | 4 | Read | View contents | List contents |
| `w` | 2 | Write | Modify | Create/delete files |
| `x` | 1 | Execute | Run as program | Enter directory |
| `-` | 0 | None | Access denied | Access denied |

### Permission Classes

| Symbol | Class | Description |
|:-------|:------|:------------|
| `u` | User | Owner |
| `g` | Group | Group members |
| `o` | Others | Everyone else |
| `a` | All | All users |

### Permissions Notation

```
-rwxr-xr--  1 john developers  4096 May 1 12:34 script.sh
↑ ↑↑↑ ↑↑↑ ↑↑↑
| ||| ||| |||
| ||| ||| +++-- Others (r--)
| ||| +++------ Group (r-x)
| +++---------- Owner (rwx)
+-------------- File type (- = file, d = directory)
```

## Permission Management

### Core Commands

| Command | Description | Example |
|:--------|:------------|:--------|
| `ls -l file` | Show permissions | `ls -l /etc/passwd` |
| `ls -ld dir` | Show dir permissions | `ls -ld /home/john` |
| `chmod perm file` | Change permissions | `chmod 755 script.sh` |
| `chown user:group file` | Change owner & group | `sudo chown john:developers file.txt` |
| `chown user file` | Change owner only | `sudo chown john file.txt` |
| `chgrp group file` | Change group only | `sudo chgrp developers file.txt` |

### Common Permission Values

| Numeric | Symbolic | Meaning | Typical Use |
|:--------|:---------|:--------|:------------|
| `755` | `rwxr-xr-x` | Owner all, others read/execute | Scripts, directories |
| `700` | `rwx------` | Owner all, no others | Private scripts |
| `644` | `rw-r--r--` | Owner read/write, others read | Regular files |
| `600` | `rw-------` | Owner read/write only | Sensitive configs |
| `444` | `r--r--r--` | Read-only for all | Reference files |

### Symbolic Permission Mode

| Command | Effect |
|:--------|:-------|
| `chmod u+x file` | Add execute for owner |
| `chmod g-w file` | Remove write from group |
| `chmod o=r file` | Set others to read-only |
| `chmod a+r file` | Add read for all |
| `chmod -R g+w dir` | Recursively add group write |

## Special Permissions

| Command | Description | Effect |
|:--------|:------------|:-------|
| `chmod u+s file` | Set SUID | Execute as owner |
| `chmod 4755 file` | Set SUID (numeric) | Same as above |
| `chmod g+s dir` | Set SGID on directory | New files inherit group |
| `chmod 2775 dir` | Set SGID (numeric) | Same as `g+s` |
| `chmod o+t dir` | Set sticky bit | Only owner can delete files |
| `chmod 1777 dir` | Set sticky bit (numeric) | Same as `o+t` |

### Examples

- SUID: `ls -l /usr/bin/passwd` (notice the `s` in user permissions)
- SGID: `ls -ld /var/mail` (notice the `s` in group permissions)
- Sticky bit: `ls -ld /tmp` (notice the `t` in others permissions)

## Advanced Permission Topics

### Default Permissions with umask

| Command | Description | Result |
|:--------|:------------|:-------|
| `umask` | Show current umask | Typically `022` or `002` |
| `umask 022` | Set umask | Files: 644, Dirs: 755 |
| `umask 027` | Restrictive umask | Files: 640, Dirs: 750 |

### Access Control Lists (ACLs)

| Command | Description | Example |
|:--------|:------------|:--------|
| `getfacl file` | Show ACLs | `getfacl /shared/project.txt` |
| `setfacl -m u:user:rw file` | Add user ACL | `setfacl -m u:john:rw /shared/project.txt` |
| `setfacl -m g:group:rx file` | Add group ACL | `setfacl -m g:devs:rx /shared/script.sh` |
| `setfacl -x u:user file` | Remove user ACL | `setfacl -x u:john /shared/project.txt` |
| `setfacl -b file` | Remove all ACLs | `setfacl -b /shared/project.txt` |

## Common Permission Recipes

### Setting Up a Shared Directory

```bash
# Create group
sudo groupadd project

# Add users
sudo gpasswd -a user1 project
sudo gpasswd -a user2 project

# Create shared directory
sudo mkdir -p /shared/project
sudo chown root:project /shared/project
sudo chmod 2775 /shared/project

# Verify setup
ls -ld /shared/project
```

### Securing Configuration Files

```bash
# Make configs read-only
chmod 644 config.ini

# Or more secure (owner only)
chmod 600 sensitive-config.ini

# Set proper ownership
chown root:root important-config.ini
```

### Making Scripts Executable

```bash
# Basic script permission
chmod +x script.sh

# More secure (owner execute only)
chmod 700 sensitive-script.sh
```

---

