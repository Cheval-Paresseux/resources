# 🐧 Linux Commands Cheat Sheet

### 📁 Navigation & Display

| Command | Description |
|---------|-------------|
| `clear` | Clear the terminal screen |
| `ls` | List files and directories in current location |
| `ls -a` | List all files including hidden ones (starting with .) |
| `ls -l` | List files with detailed information (permissions, size, date) |
| `ls -lh` | List files with human-readable file sizes |
| `pwd` | Print the current working directory path |
| `cd <directory>` | Change to specified directory |
| `cd ..` | Go up one directory level |
| `cd ~` or `cd` | Go to home directory |
| `cd -` | Go to previous directory |

### 📄 File & Directory Management

| Command | Description |
|---------|-------------|
| `mkdir <dirname>` | Create a new directory |
| `mkdir -p <path/to/nested/dirs>` | Create nested directories |
| `touch <filename>` | Create an empty file or update timestamp |
| `cp <source> <destination>` | Copy a file |
| `cp -r <source> <destination>` | Copy a directory recursively |
| `mv <source> <destination>` | Move or rename a file/directory |
| `rm <filename>` | Remove a file |
| `rm -r <dirname>` | Remove a directory and its contents recursively |
| `rm -rf <dirname>` | Force remove without prompts ⚠️ *use carefully!* |
| `rmdir <dirname>` | Remove an empty directory only |

### 👁️ Viewing & Editing Files

| Command | Description |
|---------|-------------|
| `cat <filename>` | Display entire file content |
| `less <filename>` | View file with scrolling (press `q` to quit) |
| `head <filename>` | Show first 10 lines |
| `head -n 20 <filename>` | Show first 20 lines |
| `tail <filename>` | Show last 10 lines |
| `tail -f <filename>` | Follow file updates in real-time 📊 *useful for logs* |
| `nano <filename>` | Edit file with nano text editor |
| `vim <filename>` | Edit file with vim text editor |
| `nvim <filename>` | Edit file with NeoVim text editor |
| `code <filename>` | Open file in VS Code (if installed) |

### ✏️ File Operations

| Command | Description |
|---------|-------------|
| `echo "text" > <filename>` | Overwrite file with text |
| `echo "text" >> <filename>` | Append text to file |
| `diff <file1> <file2>` | Show differences between two files |
| `cmp <file1> <file2>` | Compare two files byte by byte |
| `wc <filename>` | Count lines, words, and characters |
| `wc -l <filename>` | Count lines only |

### 🔍 Searching & Finding

| Command | Description |
|---------|-------------|
| `find <path> -name "<pattern>"` | Find files by name |
| `find . -type f -name "*.txt"` | Find all .txt files in current directory |
| `grep "<pattern>" <filename>` | Search for text pattern in file |
| `grep -r "<pattern>" <directory>` | Search recursively in directory |
| `grep -i "<pattern>" <filename>` | Case-insensitive search |
| `locate <filename>` | Quickly find file by name (uses database) |

---

### 🔒 File Permissions

| Command | Description |
|---------|-------------|
| `chmod +x <filename>` | Make file executable |
| `chmod 755 <filename>` | Set specific permissions (rwxr-xr-x) |
| `chmod -R 755 <dirname>` | Set permissions recursively |
| `chown <user>:<group> <filename>` | Change file owner |
| `ls -l` | View file permissions |

**Permission Numbers:**
- `7` = read + write + execute (rwx)
- `6` = read + write (rw-)
- `5` = read + execute (r-x)
- `4` = read only (r--)

---

### 📦 Compression & Archives

| Command | Description |
|---------|-------------|
| `tar -czf <archive.tar.gz> <files>` | Create compressed tar archive |
| `tar -xzf <archive.tar.gz>` | Extract tar.gz archive |
| `tar -xzf <archive.tar.gz> -C <path>` | Extract to specific directory |
| `zip <archive.zip> <files>` | Create zip archive |
| `zip -r <archive.zip> <directory>` | Zip a directory recursively |
| `unzip <archive.zip>` | Extract zip archive |
| `unzip -l <archive.zip>` | List contents without extracting |

---

### 👤 User Management

| Command | Description |
|---------|-------------|
| `whoami` | Display current username |
| `id` | Show user ID and group IDs |
| `sudo adduser <username>` | Create a new user (interactive) |
| `su <username>` | Switch to another user |
| `su -` | Switch to root user |
| `exit` | Exit current user session |
| `sudo passwd <username>` | Change user password |
| `passwd` | Change your own password |

---

### 📚 Package Information

| Command | Description |
|---------|-------------|
| `whatis <command>` | Brief description of a command |
| `which <command>` | Show path to executable |
| `whereis <command>` | Show binary, source, and manual page locations |
| `man <command>` | View detailed manual page |
| `<command> --help` | Show command help information |
| `apropos <keyword>` | Search manual pages by keyword |

---

### 📦 Package Management (Debian/Ubuntu)

| Command | Description |
|---------|-------------|
| `sudo apt update` | Update package list |
| `sudo apt upgrade` | Upgrade all installed packages |
| `sudo apt install <package>` | Install a package |
| `sudo apt remove <package>` | Remove a package |
| `sudo apt search <keyword>` | Search for packages |
| `apt list --installed` | List installed packages |
| `sudo apt autoremove` | Remove unnecessary packages |

---

### 💻 System Information

| Command | Description |
|---------|-------------|
| `uname -a` | Display system information |
| `df -h` | Show disk space usage (human-readable) |
| `du -sh <directory>` | Show directory size |
| `free -h` | Display memory usage |
| `top` | Show running processes (dynamic, press `q` to quit) |
| `htop` | Enhanced process viewer 🎨 *more colorful* (if installed) |
| `ps aux` | List all running processes |
| `uptime` | Show system uptime |

---

### 🌐 Network & Downloads

| Command | Description |
|---------|-------------|
| `curl <url>` | Download or transfer data from URL |
| `curl -O <url>` | Download file with original filename |
| `wget <url>` | Download files from the web |
| `wget -c <url>` | Continue interrupted download |
| `ping <host>` | Test network connection to host |
| `ifconfig` or `ip addr` | Show network interface information |
| `netstat -tuln` | Show listening ports |

---

### ⚙️ Process Management

| Command | Description |
|---------|-------------|
| `ps aux \| grep <name>` | Find process by name |
| `kill <PID>` | Terminate process by ID |
| `kill -9 <PID>` | Force kill process |
| `killall <name>` | Terminate all processes by name |
| `bg` | Resume suspended process in background |
| `fg` | Bring background process to foreground |
| `jobs` | List background jobs |
| `<command> &` | Run command in background |

---

### ⌨️ Keyboard Shortcuts

| Shortcut | Description |
|----------|-------------|
| `Tab` | Autocomplete commands and paths |
| `Ctrl+C` | Stop current running process |
| `Ctrl+Z` | Suspend current process |
| `Ctrl+D` | Exit current shell/logout |
| `Ctrl+L` | Clear screen (alternative to `clear`) |
| `Ctrl+R` | Search command history |
| `Ctrl+A` | Move cursor to beginning of line |
| `Ctrl+E` | Move cursor to end of line |
| `Ctrl+U` | Clear line before cursor |
| `Ctrl+K` | Clear line after cursor |
| `!!` | Repeat last command |
| `sudo !!` | Run previous command with sudo |

---

### 📖 History & Aliases

| Command | Description |
|---------|-------------|
| `history` | Show command history |
| `history \| grep <term>` | Search command history |
| `!<number>` | Run command from history by number |
| `alias ll='ls -lah'` | Create command alias |
| `unalias ll` | Remove alias |
| `alias` | List all aliases |

---

**📌 Quick Reference:**
- `<something>` means replace with your value
- `|` (pipe) sends output of one command to another
- `>` redirects output to a file (overwrites)
- `>>` appends output to a file
- `&` runs command in background
- `;` runs commands sequentially
- `&&` runs next command only if previous succeeds