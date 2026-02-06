# Linux Basics Cheat Sheet 🐧

A comprehensive guide to essential Linux commands for beginners. Perfect for workshop participants and students getting started with Linux!

---

## Table of Contents
- [Navigation Commands](#navigation-commands)
- [File & Directory Operations](#file--directory-operations)
- [File Viewing & Editing](#file-viewing--editing)
- [Permissions & Ownership](#permissions--ownership)
- [Process Management](#process-management)
- [System Information](#system-information)
- [Network Commands](#network-commands)
- [Package Management](#package-management)
- [Shortcuts & Tips](#shortcuts--tips)

---

## Navigation Commands

### `pwd` - Print Working Directory
Shows your current location in the filesystem.

```bash
pwd
# Output: /home/username/Documents
```

**Use Cases:**
- Verify you're in the correct directory before running commands
- Debug path-related issues in scripts

**Common Issues:**
- None! This is one of the safest commands.

---

### `ls` - List Directory Contents
Display files and directories in the current location.

```bash
ls                    # Basic listing
ls -l                 # Detailed listing (permissions, size, date)
ls -a                 # Show hidden files (starting with .)
ls -lh                # Human-readable file sizes
ls -ltr               # Sort by time, reverse order (oldest first)
```

**Use Cases:**
- Check if a file exists before creating it
- View file permissions and ownership
- Find recently modified files

**Common Issues:**
- **"Permission denied"**: You don't have access to that directory. Try with `sudo` or change directory.
- **Hidden files not showing**: Use `-a` flag to see files starting with `.`
- **Confusing output**: Use `-lh` for more readable format

---

### `cd` - Change Directory
Navigate between directories.

```bash
cd /home/username     # Absolute path
cd Documents          # Relative path
cd ..                 # Go up one level
cd ~                  # Go to home directory
cd -                  # Go to previous directory
```

**Use Cases:**
- Navigate to project folders
- Return to home directory quickly
- Move between related directories

**Common Issues:**
- **"No such file or directory"**: Path doesn't exist or typo in name (Linux is case-sensitive!)
- **Spaces in directory names**: Use quotes: `cd "My Documents"` or escape: `cd My\ Documents`
- **Permission denied**: You don't have access rights to that directory

---

## File & Directory Operations

### `mkdir` - Make Directory
Create new directories.

```bash
mkdir new_folder              # Create single directory
mkdir -p parent/child/grandchild  # Create nested directories
mkdir folder1 folder2 folder3     # Create multiple directories
```

**Use Cases:**
- Organize project structures
- Create backup directories
- Set up development environments

**Common Issues:**
- **"File exists"**: Directory already exists. Check with `ls` first.
- **"Permission denied"**: You don't have write permissions in current directory.
- **Parent doesn't exist**: Use `-p` flag to create parent directories automatically.

---

### `touch` - Create Empty File
Create a new empty file or update timestamp.

```bash
touch newfile.txt
touch file1.txt file2.txt file3.txt
```

**Use Cases:**
- Create placeholder files
- Update file modification time
- Quick file creation for testing

**Common Issues:**
- **Accidentally creating files with typos**: Always double-check spelling.
- **Permission denied**: No write access in the directory.

---

### `cp` - Copy Files/Directories
Copy files and directories from one location to another.

```bash
cp source.txt destination.txt          # Copy file
cp source.txt /path/to/directory/      # Copy to directory
cp -r directory1 directory2            # Copy directory recursively
cp -i source.txt dest.txt              # Interactive (prompt before overwrite)
cp -u source.txt dest.txt              # Copy only if source is newer
```

**Use Cases:**
- Create backups of files
- Duplicate configuration files before editing
- Copy project templates

**Common Issues:**
- **"Is a directory"**: Forgot `-r` flag when copying directories.
- **Overwriting important files**: Use `-i` (interactive) to prompt before overwriting.
- **Permission denied**: Need read access on source, write access on destination.

---

### `mv` - Move/Rename Files
Move or rename files and directories.

```bash
mv oldname.txt newname.txt             # Rename file
mv file.txt /path/to/directory/        # Move file
mv -i source.txt destination.txt       # Interactive mode
mv *.txt Documents/                    # Move all .txt files
```

**Use Cases:**
- Reorganize files
- Rename files with typos
- Move files to archive folders

**Common Issues:**
- **Accidental overwrites**: Use `-i` flag for confirmation.
- **Lost files**: `mv` doesn't create copies; the original is moved!
- **"No such file or directory"**: Destination path doesn't exist.

---

### `rm` - Remove Files/Directories
Delete files and directories permanently.

```bash
rm file.txt                   # Remove file
rm -i file.txt                # Interactive (ask before deleting)
rm -r directory/              # Remove directory recursively
rm -f file.txt                # Force removal (no confirmation)
rm *.txt                      # Remove all .txt files
```

**Use Cases:**
- Clean up temporary files
- Remove old backups
- Delete test files

**Common Issues:**
- **PERMANENT DELETION**: There's no recycle bin! Files are gone forever.
- **"Directory not empty"**: Use `-r` flag to remove directories.
- **Accidentally using wildcards**: `rm *` deletes everything! Be extremely careful.
- **Permission denied**: Need write permissions on parent directory.

⚠️ **WARNING**: Never run `rm -rf /` or `rm -rf /*` - this will delete your entire system!

---

### `rmdir` - Remove Empty Directory
Remove only empty directories.

```bash
rmdir empty_directory
```

**Use Cases:**
- Clean up empty folders safely
- Ensure directory is empty before removal

**Common Issues:**
- **"Directory not empty"**: Contains files or subdirectories. Use `rm -r` instead or clean it first.

---

## File Viewing & Editing

### `cat` - Concatenate and Display
Display file contents in terminal.

```bash
cat file.txt                          # Display file
cat file1.txt file2.txt              # Display multiple files
cat file1.txt file2.txt > merged.txt # Combine files
```

**Use Cases:**
- Quickly view small files
- Combine multiple files
- Pipe content to other commands

**Common Issues:**
- **Large files flood terminal**: Use `less` or `more` instead.
- **Binary files show gibberish**: Use file-appropriate tools.

---

### `less` - View File with Pagination
View files one page at a time.

```bash
less largefile.txt
# Press 'q' to quit, Space for next page, 'b' for previous page
# '/' to search, 'n' for next match
```

**Use Cases:**
- Read log files
- View large configuration files
- Search through documentation

**Common Issues:**
- **Don't know how to exit**: Press `q` to quit.
- **Lost in large file**: Press `g` to go to beginning, `G` to go to end.

---

### `head` - View File Beginning
Display first lines of a file.

```bash
head file.txt              # First 10 lines (default)
head -n 20 file.txt        # First 20 lines
head -n 5 *.txt            # First 5 lines of all .txt files
```

**Use Cases:**
- Preview file contents
- Check log file headers
- Verify file format

**Common Issues:**
- **Need more lines**: Adjust with `-n` flag.

---

### `tail` - View File End
Display last lines of a file.

```bash
tail file.txt              # Last 10 lines (default)
tail -n 20 file.txt        # Last 20 lines
tail -f logfile.log        # Follow file (watch in real-time)
```

**Use Cases:**
- Monitor log files in real-time (`-f`)
- Check recent entries
- Debug applications by watching logs

**Common Issues:**
- **Can't exit follow mode**: Press `Ctrl+C` to stop.
- **File not updating**: Make sure application is writing to the file.

---

### `nano` - Simple Text Editor
User-friendly terminal text editor.

```bash
nano filename.txt
# Ctrl+O to save, Ctrl+X to exit
# Ctrl+W to search, Ctrl+K to cut line
```

**Use Cases:**
- Edit configuration files
- Write quick scripts
- Make simple text changes

**Common Issues:**
- **Confused by shortcuts**: Look at the bottom of screen for hints (`^` means Ctrl).
- **Can't save**: Check file permissions.

---

### `grep` - Search Text
Search for patterns in files.

```bash
grep "search term" file.txt           # Basic search
grep -i "search" file.txt             # Case-insensitive
grep -r "search" directory/           # Recursive search
grep -n "search" file.txt             # Show line numbers
grep -v "exclude" file.txt            # Invert match (show non-matching)
```

**Use Cases:**
- Find specific errors in logs
- Search for configuration settings
- Filter command output

**Common Issues:**
- **Nothing found**: Check spelling, try `-i` for case-insensitive search.
- **Too many results**: Make search term more specific or pipe to `less`.
- **Special characters**: Escape them with `\` or use single quotes.

---

## Permissions & Ownership

### Understanding Permissions
```
-rwxr-xr--
│││││││││└─ Other: read
││││││││└── Other: no write
│││││││└─── Other: no execute
││││││└──── Group: read
│││││└───── Group: no write
││││└────── Group: execute
│││└─────── Owner: read
││└──────── Owner: write
│└───────── Owner: execute
└────────── File type (- = file, d = directory)
```

### `chmod` - Change Permissions
Modify file/directory permissions.

```bash
chmod +x script.sh              # Add execute permission
chmod 755 file.txt              # rwxr-xr-x
chmod 644 file.txt              # rw-r--r--
chmod -R 755 directory/         # Recursive
```

**Numeric Permissions:**
- 4 = read (r)
- 2 = write (w)
- 1 = execute (x)
- 7 = rwx (4+2+1)
- 6 = rw- (4+2)
- 5 = r-x (4+1)

**Use Cases:**
- Make scripts executable
- Secure sensitive files
- Fix permission issues

**Common Issues:**
- **"Permission denied" after chmod**: Check if you own the file.
- **Wrong permissions**: 755 for directories/executables, 644 for regular files.
- **Forgot recursive flag**: Use `-R` for directories.

---

### `chown` - Change Owner
Change file/directory ownership.

```bash
sudo chown username file.txt              # Change owner
sudo chown username:groupname file.txt    # Change owner and group
sudo chown -R username directory/         # Recursive
```

**Use Cases:**
- Fix ownership after sudo operations
- Transfer file ownership
- Set correct permissions for services

**Common Issues:**
- **"Operation not permitted"**: Need sudo privileges.
- **Syntax errors**: Remember format is `user:group`.

---

## Process Management

### `ps` - Process Status
Display running processes.

```bash
ps                    # Current terminal processes
ps aux                # All processes (detailed)
ps aux | grep python  # Find specific processes
```

**Use Cases:**
- Find process IDs (PIDs)
- Monitor system resources
- Identify problematic processes

**Common Issues:**
- **Too much output**: Pipe to `grep` to filter.
- **Process not showing**: Might have exited or use different flags.

---

### `top` - Task Manager
Real-time system monitor.

```bash
top
# Press 'q' to quit, 'k' to kill process
# Press 'M' to sort by memory, 'P' to sort by CPU
```

**Use Cases:**
- Monitor system performance
- Find resource-hungry processes
- Check CPU and memory usage

**Common Issues:**
- **High load**: Check which processes are using most resources.
- **Can't exit**: Press `q`.

---

### `kill` - Terminate Process
Stop running processes.

```bash
kill PID                 # Graceful termination
kill -9 PID              # Force kill
killall process_name     # Kill by name
```

**Use Cases:**
- Stop frozen applications
- End background processes
- Restart misbehaving services

**Common Issues:**
- **"No such process"**: Process already terminated or wrong PID.
- **Process won't die**: Use `kill -9` (SIGKILL) as last resort.
- **Permission denied**: Need sudo for processes owned by others.

---

### `bg` / `fg` - Background/Foreground
Manage background jobs.

```bash
command &            # Run in background
jobs                 # List background jobs
bg %1                # Resume job 1 in background
fg %1                # Bring job 1 to foreground
Ctrl+Z               # Suspend current process
```

**Use Cases:**
- Run long processes in background
- Multitask in single terminal
- Continue work while process runs

**Common Issues:**
- **Lost job**: Use `jobs` to list all background jobs.
- **Process stuck**: Bring to foreground with `fg` then `Ctrl+C`.

---

## System Information

### `uname` - System Information
Display system information.

```bash
uname -a              # All information
uname -r              # Kernel version
uname -m              # Machine architecture
```

**Use Cases:**
- Check OS version
- Verify architecture for software installation
- Debug compatibility issues

---

### `df` - Disk Free
Show disk space usage.

```bash
df                    # Basic disk usage
df -h                 # Human-readable sizes
df -h /home           # Specific partition
```

**Use Cases:**
- Check available disk space
- Find which partition is full
- Monitor storage before large operations

**Common Issues:**
- **"No space left"**: Delete unnecessary files or expand disk.
- **Confusing output**: Use `-h` flag for readable format.

---

### `du` - Disk Usage
Estimate file/directory space usage.

```bash
du -sh directory/              # Summary of directory size
du -h --max-depth=1           # Size of subdirectories (one level)
du -ah | sort -hr | head -20  # Top 20 largest items
```

**Use Cases:**
- Find what's taking up space
- Identify large directories
- Clean up disk space

**Common Issues:**
- **Too much output**: Use `--max-depth` or pipe to `head`.
- **Permission denied**: Use `sudo` for system directories.

---

### `free` - Memory Usage
Display memory information.

```bash
free                  # Memory in KB
free -h               # Human-readable
free -m               # Memory in MB
```

**Use Cases:**
- Check available RAM
- Monitor memory usage
- Diagnose performance issues

---

### `uptime` - System Uptime
Show how long system has been running.

```bash
uptime
# Output: 10:30:15 up 5 days, 3:25, 2 users, load average: 0.15, 0.10, 0.08
```

**Use Cases:**
- Check if system was recently rebooted
- View load averages
- Monitor system stability

---

## Network Commands

### `ping` - Network Connectivity
Test connection to a host.

```bash
ping google.com              # Continuous ping
ping -c 4 google.com         # 4 pings only
ping 192.168.1.1             # Ping IP address
```

**Use Cases:**
- Test internet connectivity
- Check if server is reachable
- Measure network latency

**Common Issues:**
- **Continuous ping**: Press `Ctrl+C` to stop or use `-c` flag.
- **"Network unreachable"**: Check network connection and configuration.
- **"Unknown host"**: DNS issue or wrong hostname.

---

### `ifconfig` / `ip` - Network Interfaces
Display/configure network interfaces.

```bash
ifconfig              # Show all interfaces (older)
ip addr               # Show all interfaces (modern)
ip addr show eth0     # Show specific interface
```

**Use Cases:**
- Find IP address
- Check network interface status
- Diagnose network issues

**Common Issues:**
- **"Command not found"**: Use `ip addr` instead of `ifconfig` on modern systems.
- **Interface down**: Use `sudo ip link set eth0 up` to enable.

---

### `wget` - Download Files
Download files from the web.

```bash
wget https://example.com/file.zip
wget -O custom_name.zip https://example.com/file.zip
wget -c https://example.com/largefile.iso  # Resume download
```

**Use Cases:**
- Download files from URLs
- Automate file downloads
- Retrieve web resources

**Common Issues:**
- **Certificate errors**: Use `--no-check-certificate` (not recommended for security).
- **Download interrupted**: Use `-c` to resume.
- **Permission denied**: Check write permissions in current directory.

---

### `curl` - Transfer Data
Transfer data from/to servers.

```bash
curl https://example.com                # Display webpage
curl -O https://example.com/file.zip    # Download file
curl -I https://example.com             # Show headers only
```

**Use Cases:**
- Test API endpoints
- Download files
- Check HTTP headers

**Common Issues:**
- **SSL certificate errors**: Use `-k` to skip verification (not recommended).
- **Redirect issues**: Use `-L` to follow redirects.

---

## Package Management

### Ubuntu/Debian (`apt`)

```bash
sudo apt update                    # Update package lists
sudo apt upgrade                   # Upgrade installed packages
sudo apt install package_name      # Install package
sudo apt remove package_name       # Remove package
sudo apt search keyword            # Search for packages
```

**Use Cases:**
- Install new software
- Keep system updated
- Remove unwanted applications

**Common Issues:**
- **"Unable to locate package"**: Run `sudo apt update` first.
- **Dependency errors**: Try `sudo apt --fix-broken install`.
- **"Could not get lock"**: Another package manager is running. Wait or kill the process.

---

### Red Hat/CentOS (`yum`/`dnf`)

```bash
sudo yum update                    # Update packages
sudo yum install package_name      # Install package
sudo yum remove package_name       # Remove package
sudo yum search keyword            # Search for packages
```

**Common Issues:**
- Similar to apt issues above
- **Repository errors**: Check `/etc/yum.repos.d/` configuration

---

## Shortcuts & Tips

### Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl+C` | Cancel current command |
| `Ctrl+Z` | Suspend current process |
| `Ctrl+D` | Exit terminal / End of input |
| `Ctrl+L` | Clear screen (same as `clear`) |
| `Ctrl+A` | Move to beginning of line |
| `Ctrl+E` | Move to end of line |
| `Ctrl+U` | Delete from cursor to start of line |
| `Ctrl+K` | Delete from cursor to end of line |
| `Ctrl+R` | Search command history |
| `Tab` | Auto-complete filenames/commands |
| `↑/↓` | Navigate command history |

---

### Helpful Tips

**1. Use Tab Completion**
```bash
cd Doc[Tab]  # Auto-completes to "Documents"
```

**2. Command History**
```bash
history              # View command history
!123                 # Run command #123 from history
!!                   # Run last command
!grep                # Run last command starting with "grep"
```

**3. Wildcards**
```bash
*                    # Matches any characters
?                    # Matches single character
*.txt                # All .txt files
file?.txt            # file1.txt, file2.txt, etc.
```

**4. Piping and Redirection**
```bash
command1 | command2              # Pipe output to another command
command > file.txt               # Redirect output to file (overwrite)
command >> file.txt              # Append output to file
command 2> error.log             # Redirect errors
command &> output.log            # Redirect both output and errors
```

**5. Command Chaining**
```bash
command1 && command2             # Run command2 only if command1 succeeds
command1 || command2             # Run command2 only if command1 fails
command1 ; command2              # Run both commands regardless
```

**6. Get Help**
```bash
man command                      # Manual page
command --help                   # Quick help
info command                     # Info documentation
```

---

## Common Beginner Mistakes

1. **Not using Tab completion** - Save time by letting the terminal autocomplete
2. **Ignoring case sensitivity** - `File.txt` and `file.txt` are different!
3. **Running commands without understanding** - Always know what a command does
4. **Using `rm -rf` carelessly** - Double-check before deleting
5. **Forgetting `sudo`** - Some commands need administrator privileges
6. **Not reading error messages** - They usually tell you what's wrong
7. **Working as root unnecessarily** - Use `sudo` only when needed
8. **Not backing up before editing** - `cp file.txt file.txt.bak` before editing

---

## Practice Exercises

1. Create a directory structure: `projects/web/frontend` and `projects/web/backend`
2. Create 3 empty files in frontend: `index.html`, `style.css`, `app.js`
3. Copy all files from frontend to backend
4. Find all `.js` files in the projects directory
5. Make `app.js` executable
6. View the first 5 lines of a log file
7. Search for "error" in a log file (case-insensitive)
8. Check disk space and find your largest directory

---

## Resources

- [Linux Journey](https://linuxjourney.com/) - Interactive learning
- [ExplainShell](https://explainshell.com/) - Command breakdown
- [TLDR Pages](https://tldr.sh/) - Simplified man pages
- [Linux Command Library](https://linuxcommandlibrary.com/) - Searchable commands

---

## Contributing

Found an error or want to add a command? Feel free to open an issue or submit a pull request!

---

## License

This cheat sheet is free to use and distribute. Happy learning! 🚀

---

**Pro Tip:** The best way to learn is by doing. Open a terminal and try these commands. Make mistakes in a safe environment and learn from them!
