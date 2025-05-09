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
- [Linux Redirection & Piping](#-linux-redirection--piping)
- [File Viewing & Command Search](#-file-viewing--command-search)
- [Partitioning & Mounting](#-partitioning--mounting)


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

# 🔁 Linux Redirection & Piping

Control where command input and output go—whether it's to files, other commands, or discarded entirely.

## Understanding I/O Streams

Every command has three standard streams:
- **stdin (0)**: Standard input - where the command reads its input
- **stdout (1)**: Standard output - where successful command results are written
- **stderr (2)**: Standard error - where error messages are written

## 📤 Output Redirection

| Command | Description | Example |
|:--------|:------------|:--------|
| `command > file` | Redirect **stdout** to file (overwrite) | `ls > filelist.txt` |
| `command >> file` | Redirect **stdout** to file (append) | `echo "new line" >> notes.txt` |
| `command 2> file` | Redirect **stderr** to file (overwrite) | `find / -name abc 2> errors.log` |
| `command 2>> file` | Redirect **stderr** to file (append) | `gcc program.c 2>> compile_errors.log` |
| `command > file 2>&1` | Redirect **both stdout and stderr** to same file | `ls -la /root > output.txt 2>&1` |
| `command &> file` | Redirect both streams (shorthand, overwrite) | `find / -name "*.conf" &> results.txt` |
| `command &>> file` | Redirect both streams (shorthand, append) | `make &>> build.log` |

## 📥 Input Redirection

| Command | Description | Example |
|:--------|:------------|:--------|
| `command < file` | Use file as **stdin** for command | `sort < unsorted.txt` |
| `command << MARKER` | Use here-document (multi-line input) | `cat << EOF > script.sh` |
| `command <<< "string"` | Use here-string (single string input) | `grep "user" <<< "username: admin"` |

## 🔗 Pipes

| Command | Description | Example |
|:--------|:------------|:--------|
| `cmd1 \| cmd2` | Send output of cmd1 to input of cmd2 | `ls -la \| grep ".txt"` |
| `cmd1 \| tee file \| cmd2` | Send output to both file and cmd2 | `ls \| tee files.txt \| grep ".log"` |
| `cmd1 \|& cmd2` | Pipe both stdout and stderr | `find / -type f -name "*.conf" \|& grep -v "Permission denied"` |

## 🗑️ Discard Output

| Command | Description | Example |
|:--------|:------------|:--------|
| `command > /dev/null` | Discard standard output | `apt update > /dev/null` |
| `command 2> /dev/null` | Discard standard error | `find / -name core 2> /dev/null` |
| `command &> /dev/null` | Discard both stdout and stderr | `wget https://example.com &> /dev/null` |

## 📄 File Content Redirection

| Command | Description | Example |
|:--------|:------------|:--------|
| `cat file1 > file2` | Copy content from file1 to file2 (overwrite) | `cat source.txt > destination.txt` |
| `cat file1 >> file2` | Append contents of file1 to file2 | `cat header.txt >> document.txt` |
| `cat < file1 > file2` | Redirect file1 contents to file2 | `cat < input.txt > output.txt` |

### Here Document Example

```bash
# Create a script with multi-line content
cat << 'EOT' > myscript.sh
#!/bin/bash
echo "This is a generated script"
echo "Created on $(date)"
ls -la
EOT

# Add content to a configuration file
sudo tee -a /etc/hosts << EOF
192.168.1.10  server1
192.168.1.11  server2
EOF
```

## 💡 Pro Tips

1. Use `tee` to view output while saving to a file:
   ```bash
   command | tee output.txt
   ```

2. Use process substitution for complex commands:
   ```bash
   diff <(ls dir1) <(ls dir2)
   ```

3. Combine redirections for detailed logs:
   ```bash
   command > output.log 2> error.log
   ```

4. Redirect and append to same file without clobbering:
   ```bash
   command >> logfile.txt 2>> logfile.txt
   ```

5. Remember the file descriptor numbers:
   - **0**: stdin
   - **1**: stdout
   - **2**: stderr

---

# 📑 File Viewing & Command Search

Commands for viewing file contents, managing output, and retrieving system/command information.

## 📄 File Viewing & Output

| Command | Description | Example |
|:--------|:------------|:--------|
| `cat file` | Display entire file content | `cat /etc/hostname` |
| `less file` | View file with pagination & search | `less /var/log/syslog` |
| `more file` | View file one screen at a time | `more README.md` |
| `head file` | View first 10 lines of file | `head -n 20 large_file.txt` |
| `tail file` | View last 10 lines of file | `tail -f /var/log/auth.log` |
| `file filename` | Identify file type | `file unknown_file` |
| `tee file` | Read from stdin, write to stdout & file | `ls -la | tee listing.txt` |

### 📊 less Navigation Keys

| Key | Action |
|:----|:-------|
| `Space` or `Page Down` | Forward one page |
| `b` or `Page Up` | Back one page |
| `/pattern` | Search forward for "pattern" |
| `?pattern` | Search backward for "pattern" |
| `n` | Next search match |
| `N` | Previous search match |
| `q` | Quit |
| `g` | Go to first line |
| `G` | Go to last line |

## 🔍 Command & User Information

| Command | Description | Example |
|:--------|:------------|:--------|
| `w` | Show logged-in users and activity | `w` |
| `who` | List currently logged-in users | `who -a` |
| `whoami` | Show current username | `whoami` |
| `id` | Show user identity and groups | `id username` |
| `which command` | Show path of executable | `which python` |
| `whatis command` | Brief description of command | `whatis grep` |
| `whereis command` | Locate binary, source, manual | `whereis bash` |
| `last` | Show login history & reboots | `last -10` |
| `lastlog` | Last login time for all users | `lastlog | grep -v "Never"` |
| `type command` | Show how command would be interpreted | `type ls` |

## 📖 Help & Documentation

| Command | Description | Example |
|:--------|:------------|:--------|
| `man command` | Display manual page | `man find` |
| `info command` | Show GNU info documentation | `info coreutils` |
| `command --help` | Brief command help | `grep --help` |
| `apropos keyword` | Search man pages for keyword | `apropos partition` |

## 💡 Pro Tips

1. Live-monitor logs with tail:
   ```bash
   tail -f /var/log/syslog
   ```

2. Use less with syntax highlighting for code:
   ```bash
   less -R file.py   # When used with syntax highlighters
   ```

3. Combine multiple commands to find information:
   ```bash
   ps aux | grep httpd | less
   ```

4. Search through command history:
   ```bash
   history | grep "apt install"
   ```

5. View only specific parts of a file with sed:
   ```bash
   sed -n '10,20p' file.txt | less
   ```

---

# 💽 Partitioning & Mounting

Commands for managing disk partitions, filesystems, and mounting in Linux systems.

## 📊 Disk Usage & Space

| Command | Description | Example |
|:--------|:------------|:--------|
| `df` | Show filesystem disk space usage | `df -h` (human-readable) |
| `df -i` | Show inode usage | `df -i /home` |
| `du` | Show directory space usage | `du -sh /var` |
| `lsblk` | List block devices | `lsblk -f` (with filesystems) |
| `ls -li` | List files with inode numbers | `ls -li /etc/hosts` |
| `stat file` | Display detailed file status | `stat /etc/passwd` |

## 🔗 File Links

| Command | Description | Example |
|:--------|:------------|:--------|
| `ln file linkname` | Create hard link | `ln /etc/hosts hosts.hard` |
| `ln -s file linkname` | Create symbolic (soft) link | `ln -s /var/log/syslog current_log` |
| `readlink symlink` | Show target of symbolic link | `readlink /usr/bin/python` |
| `find -type l` | Find symbolic links | `find /usr -type l -name "*.so"` |

## 🔍 Disk & Partition Management

| Command | Description | Example |
|:--------|:------------|:--------|
| `fdisk -l` | List partition tables | `sudo fdisk -l /dev/sda` |
| `parted -l` | List partitions (alternative) | `sudo parted -l` |
| `gdisk -l` | GPT partition listing | `sudo gdisk -l /dev/nvme0n1` |
| `blkid` | List block device attributes | `sudo blkid` |
| `partprobe` | Inform OS of partition changes | `sudo partprobe /dev/sda` |

### 🧰 Partition Creation & Editing

| Command | Description | Example |
|:--------|:------------|:--------|
| `fdisk /dev/sdX` | Create/modify MBR partitions | `sudo fdisk /dev/sdb` |
| `gdisk /dev/sdX` | Create/modify GPT partitions | `sudo gdisk /dev/sdc` |
| `parted /dev/sdX` | GNU Parted partition editor | `sudo parted /dev/sdb` |
| `cfdisk /dev/sdX` | Curses-based fdisk | `sudo cfdisk /dev/sdb` |

## 🧱 Filesystem Operations

| Command | Description | Example |
|:--------|:------------|:--------|
| `mkfs.ext4 /dev/sdXn` | Create ext4 filesystem | `sudo mkfs.ext4 /dev/sdb1` |
| `mkfs.xfs /dev/sdXn` | Create XFS filesystem | `sudo mkfs.xfs /dev/sdc1` |
| `mkswap /dev/sdXn` | Create swap area | `sudo mkswap /dev/sdb2` |
| `swapon /dev/sdXn` | Enable swap | `sudo swapon /dev/sdb2` |
| `swapoff /dev/sdXn` | Disable swap | `sudo swapoff /dev/sdb2` |

### 🔧 Filesystem Tools

| Command | Description | Example |
|:--------|:------------|:--------|
| `e2fsck /dev/sdXn` | Check ext2/3/4 filesystem | `sudo e2fsck -f /dev/sdb1` |
| `xfs_repair /dev/sdXn` | Repair XFS filesystem | `sudo xfs_repair /dev/sdc1` |
| `dumpe2fs /dev/sdXn` | Display ext filesystem info | `sudo dumpe2fs /dev/sdb1` |
| `tune2fs /dev/sdXn` | Adjust ext filesystem parameters | `sudo tune2fs -l /dev/sdb1` |
| `resize2fs /dev/sdXn` | Resize ext filesystem | `sudo resize2fs /dev/sdb1` |

## 🔗 Mounting & Unmounting

| Command | Description | Example |
|:--------|:------------|:--------|
| `mount /dev/sdXn /mnt/point` | Mount filesystem | `sudo mount /dev/sdb1 /mnt/data` |
| `mount -o options /dev/sdXn /mnt` | Mount with options | `sudo mount -o ro /dev/sdb1 /mnt` |
| `umount /mnt/point` | Unmount by mountpoint | `sudo umount /mnt/data` |
| `umount /dev/sdXn` | Unmount by device | `sudo umount /dev/sdb1` |
| `mount -a` | Mount all from fstab | `sudo mount -a` |
| `fuser -m /mnt/point` | Show processes using mount | `sudo fuser -mv /mnt/data` |

### 📄 /etc/fstab Configuration

```
# Device       Mount Point     Filesystem  Options          Dump  Pass
/dev/sda1      /              ext4        defaults         0     1
/dev/sda2      /home          ext4        defaults         0     2
UUID=1234-5678 /data          xfs         defaults         0     2
```

## 📡 Remote Filesystems

| Command | Description | Example |
|:--------|:------------|:--------|
| `mount -t nfs server:/share /mnt` | Mount NFS share | `sudo mount -t nfs 192.168.1.10:/exports /mnt/nfs` |
| `mount -t cifs //server/share /mnt` | Mount SMB/CIFS share | `sudo mount -t cifs //server/docs /mnt/docs -o user=name` |
| `sshfs user@host:/path /mnt` | Mount via SSHFS | `sshfs admin@server:/var/log /mnt/logs` |

## 💡 Pro Tips

1. Create filesystem with label:
   ```bash
   sudo mkfs.ext4 -L datastore /dev/sdb1
   ```

2. Mount by label or UUID (more reliable):
   ```bash
   sudo mount UUID=1234-5678-90ab-cdef /mnt/data
   sudo mount LABEL=datastore /mnt/data
   ```

3. See what's mounted with custom format:
   ```bash
   mount | column -t
   ```

4. Find out which process is using a mounted filesystem:
   ```bash
   sudo lsof +f -- /mnt/data
   ```

5. Make mounting easier with entries in /etc/fstab:
   ```
   UUID=abcd-1234 /mnt/data ext4 defaults,noatime 0 2
   ```

---
