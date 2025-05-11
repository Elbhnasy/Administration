# 🐧 RHEL 9 & Linux Essentials - Enhanced Revision Guide

<div align="center">
  
  ![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
  ![Red Hat](https://img.shields.io/badge/Red%20Hat-EE0000?style=for-the-badge&logo=redhat&logoColor=white)
  ![Terminal](https://img.shields.io/badge/Terminal-4D4D4D?style=for-the-badge&logo=windows-terminal&logoColor=white)
  
</div>

## 📋 Quick Reference Contents
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

| Purpose | Description |
|:--------|:------------|
| ⚠️ **Fallback interface** | When GUI crashes or is unavailable |
| 🔧 **Low-level access** | Direct system maintenance without GUI overhead |
| 👥 **Multi-user sessions** | Multiple simultaneous login sessions |
| 📊 **Diagnostics** | Troubleshooting when graphical environment fails |

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
| `/bin` → `/usr/bin` | Essential commands | `ls`, `cp`, `mv`, `bash` |
| `/sbin` → `/usr/sbin` | System admin commands | `fdisk`, `mkfs`, `reboot` |
| `/lib`, `/lib64` → `/usr/lib` | Shared libraries | Libraries for `/bin` & `/sbin` |
| `/usr` | User programs | Applications, docs, most software |
| `/usr/bin` | Non-essential commands | `git`, `firefox`, `vim` |
| `/usr/sbin` | Admin commands | `useradd`, `groupadd` |

> 💡 **Pro Tip:** In RHEL 9, many traditional directories are now symbolic links to locations under `/usr`

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

| Command | Description | Example | Remember |
|:--------|:------------|:--------|:---------|
| `whoami` | Show current username | `whoami` | Who am I logged in as? |
| `id` | Display user & group IDs | `id`, `id username` | What are my privileges? |
| `su` | Switch user | `su john`, `su -` (for root) | `-` loads full environment |
| `sudo` | Execute as another user | `sudo dnf update` | Super-user do |
| `passwd` | Change password | `passwd`, `sudo passwd user` | Password management |
| `exit` | Exit current shell | `exit` | Leave current session |
| `logout` | Log out of session | `logout` | Exit login shell |

## File & Directory Navigation

| Command | Description | Example | Remember |
|:--------|:------------|:--------|:---------|
| `pwd` | Print working directory | `pwd` | Where am I now? |
| `cd` | Change directory | `cd /etc`, `cd ~`, `cd ..` | Move around filesystem |
| `ls` | List directory contents | `ls -la`, `ls /var` | Show what's here |
| `ls -l` | Long listing with details | `ls -l /etc/passwd` | Detailed view |
| `ls -a` | Show all files (inc. hidden) | `ls -a ~` | Including hidden files |
| `ls -lh` | Human-readable sizes | `ls -lh /var/log` | Readable file sizes |
| `ls -R` | Recursive listing | `ls -R /etc/ssh` | Show subdirectories too |
| `tree` | Display directory tree | `tree`, `tree -L 2` | Visual directory structure |
| `find` | Search for files | `find /home -name "*.txt"` | Locate files by criteria |

## File Operations

| Command | Description | Example | Remember |
|:--------|:------------|:--------|:---------|
| `cat` | Display file content | `cat /etc/hosts` | Con**cat**enate & display |
| `less` | View file with pagination | `less /var/log/messages` | Page through large files |
| `head` | Show first lines | `head -n 10 file.txt` | First 10 lines by default |
| `tail` | Show last lines | `tail -f /var/log/syslog` | `-f` follows new entries |
| `touch` | Create empty file | `touch newfile.txt` | Update timestamp/create file |
| `mkdir` | Create directory | `mkdir -p dir1/dir2` | `-p` creates parent dirs |
| `cp` | Copy files/directories | `cp -r source/ dest/` | `-r` copies recursively |
| `mv` | Move or rename files | `mv oldname newname` | Move or rename |
| `rm` | Remove files/directories | `rm -rf directory/` ⚠️ | **CAREFUL**: `-rf` deletes without confirmation |
| `rmdir` | Remove empty directories | `rmdir emptydir` | Only works on empty dirs |
| `chmod` | Change file permissions | `chmod 755 script.sh` | **Ch**ange **mod**e |
| `chown` | Change file owner | `chown user:group file` | **Ch**ange **own**er |

## System Information & Control

| Command | Description | Example | Remember |
|:--------|:------------|:--------|:---------|
| `uname -a` | System information | `uname -a` | Show kernel version |
| `hostname` | Show/set hostname | `hostname` | Computer's network name |
| `df -h` | Disk usage | `df -h` | **D**isk **f**ree space |
| `free -h` | Memory usage | `free -h` | RAM usage & availability |
| `top` | Process viewer | `top` | Dynamic process list |
| `htop` | Enhanced process viewer | `htop` | Better version of top |
| `ps aux` | List processes | `ps aux \| grep firefox` | Process status |
| `systemctl` | Manage systemd services | `systemctl status sshd` | Control system services |
| `journalctl` | Query systemd journal | `journalctl -u sshd` | View service logs |
| `reboot` | Restart system | `sudo reboot` | Restart computer |
| `shutdown` | Shutdown system | `sudo shutdown -h now` | Turn off computer |

## Terminal Shortcuts

| Shortcut | Action | Remember |
|:---------|:-------|:---------|
| `Ctrl + A` | Move to beginning of line | **A** = start of alphabet |
| `Ctrl + E` | Move to end of line | **E** = end |
| `Ctrl + U` | Delete from cursor to start | **U**p to start |
| `Ctrl + K` | Delete from cursor to end | **K**ill to end |
| `Ctrl + L` | Clear screen | **L** = clear |
| `Ctrl + C` | Kill current process | **C**ancel |
| `Ctrl + Z` | Suspend process | Put process to sleep/**Z**zz |
| `Ctrl + D` | Exit shell/terminate input | **D**one/exit |
| `Ctrl + R` | Search command history | **R**ecall history |
| `Tab` | Auto-complete | Save typing |
| `↑` / `↓` | Navigate history | Browse previous commands |

## Command Chaining & Redirection

| Operator | Description | Example | Remember |
|:---------|:------------|:--------|:---------|
| `cmd1 ; cmd2` | Run sequentially | `cd /tmp ; ls` | First, then second (always) |
| `cmd1 && cmd2` | Run cmd2 if cmd1 succeeds | `mkdir dir && cd dir` | AND logic - both or nothing |
| `cmd1 \|\| cmd2` | Run cmd2 if cmd1 fails | `ping -c1 server \|\| echo "down"` | OR logic - first or second |
| `cmd > file` | Redirect output (overwrite) | `ls > listing.txt` | Overwrite file |
| `cmd >> file` | Redirect output (append) | `echo "text" >> log.txt` | Append to file |
| `cmd < file` | Read input from file | `sort < unsorted.txt` | File as input |
| `cmd1 \| cmd2` | Pipe output to next command | `cat file.txt \| grep "error"` | Output becomes input |

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

| Command | Description | Example | Remember |
|:--------|:------------|:--------|:---------|
| `useradd username` | Create user | `sudo useradd john` | Bare user creation |
| `useradd -m username` | Create with home dir | `sudo useradd -m sarah` | `-m` = **m**ake home directory |
| `useradd -m -s /bin/bash user` | Create with login shell | `sudo useradd -m -s /bin/bash dave` | `-s` = set **s**hell |
| `passwd username` | Set/change password | `sudo passwd mary` | Always after user creation |
| `usermod -L username` | Lock account | `sudo usermod -L temporaryuser` | `-L` = **L**ock |
| `usermod -U username` | Unlock account | `sudo usermod -U temporaryuser` | `-U` = **U**nlock |
| `userdel username` | Delete account | `sudo userdel john` | Keeps home directory |
| `userdel -r username` | Delete account & home | `sudo userdel -r sarah` | `-r` = **r**emove files too |
| `id username` | Show IDs & groups | `id john` | IDs and group memberships |

### User Information Files

| File | Purpose | View Command | Remember |
|:-----|:--------|:-------------|:---------|
| `/etc/passwd` | User account info | `cat /etc/passwd` | Core user database |
| `/etc/shadow` | Encrypted passwords | `sudo cat /etc/shadow` | Secure password storage |
| `/etc/login.defs` | User creation defaults | `cat /etc/login.defs` | System-wide user settings |
| `/etc/skel/` | New home dir templates | `ls -la /etc/skel` | Template for new users |

## Group Management

### Core Commands

| Command | Description | Example | Remember |
|:--------|:------------|:--------|:---------|
| `groupadd groupname` | Create group | `sudo groupadd developers` | Create a new group |
| `groupmod -n newname oldname` | Rename group | `sudo groupmod -n devs developers` | `-n` = **n**ew name |
| `groupdel groupname` | Delete group | `sudo groupdel obsoletegroup` | Remove a group |
| `usermod -g group user` | Change primary group | `sudo usermod -g developers john` | `-g` = primary **g**roup |
| `usermod -a -G g1,g2 user` | Add to groups | `sudo usermod -a -G sudo,docker mary` | `-a -G` = **a**dd to **G**roups |
| `gpasswd -a user group` | Add to group | `sudo gpasswd -a john developers` | `-a` = **a**dd user |
| `gpasswd -d user group` | Remove from group | `sudo gpasswd -d john developers` | `-d` = **d**elete user |

### Group Information Files

| File | Purpose | View Command | Remember |
|:-----|:--------|:-------------|:---------|
| `/etc/group` | Group definitions | `cat /etc/group` | Group membership list |
| `/etc/gshadow` | Group passwords | `sudo cat /etc/gshadow` | Secured group info |

## Understanding File Permissions

### Permission Types Explained

| Symbol | Value | Type | File Effect | Directory Effect | Remember |
|:-------|:------|:-----|:------------|:----------------|:---------|
| `r` | 4 | Read | View contents | List contents | Read contents |
| `w` | 2 | Write | Modify | Create/delete files | Alter contents |
| `x` | 1 | Execute | Run as program | Enter directory | Run or traverse |
| `-` | 0 | None | Access denied | Access denied | No access |

### Permission Classes

| Symbol | Class | Description | Remember |
|:-------|:------|:------------|:---------|
| `u` | User | Owner | **U**ser who owns it |
| `g` | Group | Group members | **G**roup assigned to it |
| `o` | Others | Everyone else | **O**ther/all others |
| `a` | All | All users | **A**ll of the above |

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

| Command | Description | Example | Remember |
|:--------|:------------|:--------|:---------|
| `ls -l file` | Show permissions | `ls -l /etc/passwd` | Long listing includes permissions |
| `ls -ld dir` | Show dir permissions | `ls -ld /home/john` | `-d` shows directory itself |
| `chmod perm file` | Change permissions | `chmod 755 script.sh` | **Ch**ange **mod**e |
| `chown user:group file` | Change owner & group | `sudo chown john:developers file.txt` | **Ch**ange **own**er |
| `chown user file` | Change owner only | `sudo chown john file.txt` | Owner only |
| `chgrp group file` | Change group only | `sudo chgrp developers file.txt` | **Ch**ange **gr**ou**p** |

### Common Permission Values

| Numeric | Symbolic | Meaning | Typical Use | Remember |
|:--------|:---------|:--------|:------------|:---------|
| `755` | `rwxr-xr-x` | Owner all, others read/execute | Scripts, directories | Common script/directory perms |
| `700` | `rwx------` | Owner all, no others | Private scripts | Private to owner |
| `644` | `rw-r--r--` | Owner read/write, others read | Regular files | Standard file perms |
| `600` | `rw-------` | Owner read/write only | Sensitive configs | Private files |
| `444` | `r--r--r--` | Read-only for all | Reference files | Universal read-only |

### Symbolic Permission Mode

| Command | Effect | Remember |
|:--------|:-------|:---------|
| `chmod u+x file` | Add execute for owner | **u+x** = **u**ser add e**x**ecute |
| `chmod g-w file` | Remove write from group | **g-w** = **g**roup minus **w**rite |
| `chmod o=r file` | Set others to read-only | **o=r** = **o**thers set to **r**ead |
| `chmod a+r file` | Add read for all | **a+r** = **a**ll add **r**ead |
| `chmod -R g+w dir` | Recursively add group write | **-R** = **R**ecursive change |

## Special Permissions

| Command | Description | Effect | Remember |
|:--------|:------------|:-------|:---------|
| `chmod u+s file` | Set SUID | Execute as owner | **S**et **U**ser **ID** |
| `chmod 4755 file` | Set SUID (numeric) | Same as above | **4**=SUID, then normal perms |
| `chmod g+s dir` | Set SGID on directory | New files inherit group | **S**et **G**roup **ID** |
| `chmod 2775 dir` | Set SGID (numeric) | Same as `g+s` | **2**=SGID, then normal perms |
| `chmod o+t dir` | Set sticky bit | Only owner can delete files | **T**=sticky bit |
| `chmod 1777 dir` | Set sticky bit (numeric) | Same as `o+t` | **1**=sticky, then normal perms |

### Examples

- SUID: `ls -l /usr/bin/passwd` (notice the `s` in user permissions)
- SGID: `ls -ld /var/mail` (notice the `s` in group permissions)
- Sticky bit: `ls -ld /tmp` (notice the `t` in others permissions)

## Advanced Permission Topics

### Default Permissions with umask

| Command | Description | Result | Remember |
|:--------|:------------|:-------|:---------|
| `umask` | Show current umask | Typically `022` or `002` | Current permission mask |
| `umask 022` | Set umask | Files: 644, Dirs: 755 | Common server setting |
| `umask 027` | Restrictive umask | Files: 640, Dirs: 750 | More secure setting |

### Access Control Lists (ACLs)

| Command | Description | Example | Remember |
|:--------|:------------|:--------|:---------|
| `getfacl file` | Show ACLs | `getfacl /shared/project.txt` | **Get** **f**ile **ACL** |
| `setfacl -m u:user:rw file` | Add user ACL | `setfacl -m u:john:rw /shared/project.txt` | **Set** **f**ile **ACL** - **m**odify |
| `setfacl -m g:group:rx file` | Add group ACL | `setfacl -m g:devs:rx /shared/script.sh` | Add group permissions |
| `setfacl -x u:user file` | Remove user ACL | `setfacl -x u:john /shared/project.txt` | **-x** = remove |
| `setfacl -b file` | Remove all ACLs | `setfacl -b /shared/project.txt` | **-b** = remove all |

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

## 📤 Output Redirection Cheatsheet

| Command | Description | Example | Remember |
|:--------|:------------|:--------|:---------|
| `command > file` | Redirect **stdout** to file (overwrite) | `ls > filelist.txt` | Overwrite file |
| `command >> file` | Redirect **stdout** to file (append) | `echo "new line" >> notes.txt` | Add to end of file |
| `command 2> file` | Redirect **stderr** to file (overwrite) | `find / -name abc 2> errors.log` | Capture errors only |
| `command 2>> file` | Redirect **stderr** to file (append) | `gcc program.c 2>> compile_errors.log` | Add errors to log |
| `command > file 2>&1` | Redirect **both stdout and stderr** to same file | `ls -la /root > output.txt 2>&1` | Everything to one file |
| `command &> file` | Redirect both streams (shorthand, overwrite) | `find / -name "*.conf" &> results.txt` | Modern shorthand |
| `command &>> file` | Redirect both streams (shorthand, append) | `make &>> build.log` | Append everything |

## 📥 Input Redirection

| Command | Description | Example | Remember |
|:--------|:------------|:--------|:---------|
| `command < file` | Use file as **stdin** for command | `sort < unsorted.txt` | File feeds command |
| `command << MARKER` | Use here-document (multi-line input) | `cat << EOF > script.sh` | Multi-line input |
| `command <<< "string"` | Use here-string (single string input) | `grep "user" <<< "username: admin"` | String as input |

## 🔗 Pipes

| Command | Description | Example | Remember |
|:--------|:------------|:--------|:---------|
| `cmd1 \| cmd2` | Send output of cmd1 to input of cmd2 | `ls -la \| grep ".txt"` | Output becomes input |
| `cmd1 \| tee file \| cmd2` | Send output to both file and cmd2 | `ls \| tee files.txt \| grep ".log"` | T-junction for output |
| `cmd1 \|& cmd2` | Pipe both stdout and stderr | `find / -type f -name "*.conf" \|& grep -v "Permission denied"` | Pipe everything |

## 🗑️ Discard Output

| Command | Description | Example | Remember |
|:--------|:------------|:--------|:---------|
| `command > /dev/null` | Discard standard output | `apt update > /dev/null` | Send to black hole |
| `command 2> /dev/null` | Discard standard error | `find / -name core 2> /dev/null` | Hide error messages |
| `command &> /dev/null` | Discard both stdout and stderr | `wget https://example.com &> /dev/null` | Silent operation |

## Here Document Example

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

## 💡 Redirection Pro Tips

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

4. Remember the file descriptor numbers:
   - **0**: stdin
   - **1**: stdout
   - **2**: stderr

---

# 📑 File Viewing & Command Search

Commands for viewing file contents, managing output, and retrieving system/command information.

## 📄 File Viewing & Output Reference

| Command | Description | Example | Remember |
|:--------|:------------|:--------|:---------|
| `cat file` | Display entire file content | `cat /etc/hostname` | Display all at once |
| `less file` | View file with pagination & search | `less /var/log/syslog` | Best for large files |
| `more file` | View file one screen at a time | `more README.md` | One-way scrolling |
| `head file` | View first 10 lines of file | `head -n 20 large_file.txt` | Top of file |
| `tail file` | View last 10 lines of file | `tail -f /var/log/auth.log` | End of file, `-f` follows updates |
| `file filename` | Identify file type | `file unknown_file` | What kind of file is this? |
| `tee file` | Read from stdin, write to stdout & file | `ls -la | tee listing.txt` | T-junction for data |

### 📊 less Navigation Keys

| Key | Action | Remember |
|:----|:-------|:---------|
| `Space` or `Page Down` | Forward one page | Next page |
| `b` or `Page Up` | Back one page | Previous page |
| `/pattern` | Search forward for "pattern" | Find text |
| `?pattern` | Search backward for "pattern" | Find going up |
| `n` | Next search match | Next match |
| `N` | Previous search match | Previous match |
| `q` | Quit | Exit less |
| `g` | Go to first line | Top of file |
| `G` | Go to last line | Bottom of file |

## 🔍 Command & User Information

| Command | Description | Example | Remember |
|:--------|:------------|:--------|:---------|
| `w` | Show logged-in users and activity | `w` | Who is logged in and what they're doing |
| `who` | List currently logged-in users | `who -a` | Who is logged in (simpler) |
| `whoami` | Show current username | `whoami` | Who am I logged in as? |
| `id` | Show user identity and groups | `id username` | User and group IDs |
| `which command` | Show path of executable | `which python` | **Which** binary is used |
| `whatis command` | Brief description of command | `whatis grep` | **What is** this command |
| `whereis command` | Locate binary, source, manual | `whereis bash` | **Where is** everything related |
| `last` | Show login history & reboots | `last -10` | **Last** logins |
| `lastlog` | Last login time for all users | `lastlog | grep -v "Never"` | **Last log**in for everyone |
| `type command` | Show how command would be interpreted | `type ls` | Command **type** (alias, builtin, etc.) |

## 📖 Help & Documentation

| Command | Description | Example | Remember |
|:--------|:------------|:--------|:---------|
| `man command` | Display manual page | `man find` | **Man**ual page |
| `info command` | Show GNU info documentation | `info coreutils` | More detailed **info** |
| `command --help` | Brief command help | `grep --help` | Quick help |
| `apropos keyword` | Search man pages for keyword | `apropos partition` | Find commands **apropos** to a task |

---

# 💽 Partitioning & Mounting

Commands for managing disk partitions, filesystems, and mounting in Linux systems.

## 📊 Disk Usage & Space

| Command | Description | Example | Remember |
|:--------|:------------|:--------|:---------|
| `df` | Show filesystem disk space usage | `df -h` (human-readable) | **D**isk **F**ree space |
| `df -i` | Show inode usage | `df -i /home` | **I**node usage |
| `du` | Show directory space usage | `du -sh /var` | **D**isk **U**sage |
| `lsblk` | List block devices | `lsblk -f` (with filesystems) | **L**i**s**t **b**loc**k** devices |
| `ls -li` | List files with inode numbers | `

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

## 📄 Understanding /etc/fstab

The `/etc/fstab` file controls how filesystems are mounted at boot time:

```
# Device           Mount Point     FS Type   Options                     Dump  Pass
/dev/sda1          /              ext4      defaults                     0     1
/dev/sda2          /home          ext4      defaults,noatime             0     2
UUID=1234-5678     /data          xfs       defaults,nofail              0     2
LABEL=backup       /backup        ext4      defaults,noauto,user         0     0
//server/share     /mnt/share     cifs      credentials=/etc/cifs-cred   0     0
```

| Field | Description | Examples |
|:------|:------------|:---------|
| Device | Path, UUID, or LABEL | `/dev/sda1`, `UUID=1234-5678`, `LABEL=backup` |
| Mount Point | Directory | `/`, `/home`, `/mnt/data` |
| Filesystem Type | Type of filesystem | `ext4`, `xfs`, `btrfs`, `nfs`, `cifs` |
| Mount Options | Comma-separated | `defaults`, `ro`, `noatime`, `user` |
| Dump | Backup flag (0=no, 1=yes) | Usually `0` on modern systems |
| Pass | fsck order (0=skip, 1=root, 2=others) | `1` for /, `2` for others, `0` to skip |

### Common Mount Options

| Option | Description | Use Case |
|:-------|:------------|:---------|
| `defaults` | rw,suid,dev,exec,auto,nouser,async | Standard baseline |
| `noatime` | Don't update access times | Performance boost, SSD longevity |
| `ro` | Read-only | Protect from changes |
| `nofail` | Skip if device not present | Removable devices |
| `auto`/`noauto` | Mount at boot / don't mount at boot | Selective mounting |
| `user`/`nouser` | Allow/prevent regular users to mount | User access control |
| `exec`/`noexec` | Allow/prevent executable binaries | Security hardening |

## 🔍 Troubleshooting Mount Issues

| Problem | Diagnostic Command | Solution |
|:--------|:-------------------|:---------|
| Mount fails | `dmesg \| tail` | Check kernel messages for errors |
| Device not found | `lsblk`, `fdisk -l` | Verify device exists and is connected |
| Filesystem errors | `fsck /dev/sdXn` | Check and repair filesystem |
| "busy" device | `lsof +f -- /mountpoint` | Find processes using the filesystem |
| Permission denied | `ls -ld /mountpoint` | Check directory permissions |
| Wrong filesystem type | `blkid /dev/sdXn` | Verify correct filesystem type |

### Common Solutions

```bash
# Force unmount a busy filesystem
sudo umount -l /mnt/point   # Lazy unmount

# Kill all processes using a filesystem
sudo fuser -km /mnt/point   # Kill processes using mountpoint

# Remount filesystem in read-only mode (recovery)
sudo mount -o remount,ro /dev/sdXn

# Debug mount issues with verbose output
sudo mount -v /dev/sdXn /mnt/point
```

## 📦 LVM Management

Logical Volume Management (LVM) provides flexible storage management.

### 🔍 LVM Information Commands

| Command | Description | Example |
|:--------|:------------|:--------|
| `pvs` | List physical volumes | `sudo pvs` |
| `vgs` | List volume groups | `sudo vgs` |
| `lvs` | List logical volumes | `sudo lvs` |
| `pvdisplay` | Detailed PV info | `sudo pvdisplay /dev/sdb` |
| `vgdisplay` | Detailed VG info | `sudo vgdisplay vg_data` |
| `lvdisplay` | Detailed LV info | `sudo lvdisplay /dev/vg_data/lv_data` |

### 🛠️ Creating LVM Volumes

```bash
# 1. Create physical volumes
sudo pvcreate /dev/sdb /dev/sdc

# 2. Create volume group
sudo vgcreate vg_data /dev/sdb /dev/sdc

# 3. Create logical volume (50GB)
sudo lvcreate -n lv_data -L 50G vg_data

# 4. Create filesystem and mount
sudo mkfs.ext4 /dev/vg_data/lv_data
sudo mkdir -p /mnt/lvdata
sudo mount /dev/vg_data/lv_data /mnt/lvdata
```

### 🔄 LVM Resizing Operations

| Command | Description | Example |
|:--------|:------------|:--------|
| `lvextend` | Extend logical volume | `sudo lvextend -L +10G /dev/vg_data/lv_data` |
| `lvreduce` | Shrink logical volume | `sudo lvreduce -L -5G /dev/vg_data/lv_data` |
| `vgextend` | Add PV to volume group | `sudo vgextend vg_data /dev/sdd` |
| `pvmove` | Move data between PVs | `sudo pvmove /dev/sdb /dev/sdd` |
| `resize2fs` | Resize ext filesystem | `sudo resize2fs /dev/vg_data/lv_data` |
| `xfs_growfs` | Grow XFS filesystem | `sudo xfs_growfs /mnt/lvdata` |

