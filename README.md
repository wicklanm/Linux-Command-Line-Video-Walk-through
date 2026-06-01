# Linux-Command-Line-Video-Walk-through
This document summarizes the skills learned and provides a walkthrough of the Learning Linux Command Line course on LinkedIn Learning, taught by Senior Staff Instructor Scott Simpson. The course covers foundational Linux command line skills using the Bash shell and is designed for beginners, system administrators, and developers.

# Learning Linux Command Line
### LinkedIn Learning Course — Scott Simpson
**Course URL:** https://www.linkedin.com/learning/learning-linux-command-line-26594217

---

## About This Document

This document summarizes the skills I learned and provides a walkthrough of the **Learning Linux Command Line** course on LinkedIn Learning, taught by **Scott Simpson**. The course covers foundational Linux command line skills using the **Bash shell** and is designed for beginners, system administrators, and developers.

---

##  Skills Learned

### 1. Command Line Fundamentals
- Understanding the Linux command line and Bash shell
- Navigating the terminal environment
- Reading command syntax and using `man` pages
- Using command history and keyboard shortcuts

### 2. File System Navigation
- Moving through the directory tree with `cd`, `ls`, `pwd`
- Understanding absolute vs. relative paths
- Listing files with options (`ls -la`, `ls -lh`)
- Locating files with `find` and `locate`

### 3. Working with Files and Directories
- Creating, copying, moving, and deleting files (`touch`, `cp`, `mv`, `rm`)
- Creating and removing directories (`mkdir`, `rmdir`)
- Viewing file content (`cat`, `less`, `more`, `head`, `tail`)
- Editing text with **nano** and **Vim**

### 4. File Permissions & Ownership
- Understanding Linux permission model (owner, group, others)
- Reading permission strings (`rwxr-xr--`)
- Changing permissions with `chmod`
- Changing ownership with `chown` and `chgrp`
- Using octal notation for permissions

### 5. Common Command Line Tools
- **grep** — Search for patterns inside files
- **awk** — Field-based text processing
- **sed** — Stream editing and text substitution
- Combining tools for powerful text processing

### 6. Pipes & Redirection
- Chaining commands with pipes (`|`)
- Redirecting output to files (`>`, `>>`)
- Redirecting input (`<`)
- Sending errors to files (`2>`, `2>&1`)
- Using `/dev/null` to suppress output

### 7. Environment & Shell Configuration
- Understanding environment variables
- Working with the `PATH` variable
- Setting and exporting variables
- Customizing the shell with `.bashrc` and `.bash_profile`

### 8. Advanced Topics (Introduction)
- Process management (`ps`, `top`, `kill`)
- Working with archives (`tar`, `gzip`, `zip`)
- Basic system management tasks
- Scheduling tasks with `cron`

### 9. Package Management
- Installing software with `apt` (Debian/Ubuntu)
- Updating and upgrading packages
- Removing packages cleanly
- Searching for available packages

---

## Course Walkthrough

### Chapter 1 — Introduction to the Linux Command Line

The course opens by framing why the command line matters. For many tasks, it is more powerful and flexible than a graphical interface, and for system administrators it is essential.

**Key concepts covered:**
- What the Bash shell is and how it interprets commands
- The anatomy of a command: `command [options] [arguments]`
- Using `man <command>` to read the manual for any tool
- The home directory (`~`), the root directory (`/`), and how the Linux file system is organized

```bash
# Get help on any command
man ls

# Print working directory
pwd

# List files in long format with human-readable sizes
ls -lh
```

---

### Chapter 2 — Navigating the File System

Linux organizes everything into a single tree rooted at `/`. This chapter teaches navigation.

**Key concepts covered:**
- Moving between directories with `cd`
- Using `.` (current dir) and `..` (parent dir)
- Listing hidden files (those starting with `.`)
- Using tab completion to speed up typing

```bash
# Navigate to home directory
cd ~

# Go up one directory
cd ..

# List all files including hidden
ls -la

# Find files by name
find /home -name "*.txt"
```

---

### Chapter 3 — Working with Files and Directories

This chapter covers the day-to-day tasks of creating, editing, moving, and deleting files.

**Key concepts covered:**
- Creating files and directories
- Copying and moving files safely
- Removing files and directories
- Viewing file content in different ways

```bash
# Create a new empty file
touch notes.txt

# Create a directory
mkdir projects

# Copy a file
cp notes.txt notes_backup.txt

# Move (rename) a file
mv notes.txt journal.txt

# Remove a file (no recycle bin — be careful!)
rm old_file.txt

# Remove a directory and its contents
rm -rf old_folder/

# View file content page by page
less largefile.log

# View first 10 lines
head -n 10 file.txt

# View last 10 lines (useful for logs)
tail -n 10 /var/log/syslog
```

---

### Chapter 4 — Text Editors: nano and Vim

Two popular terminal-based text editors are covered. **nano** is beginner-friendly; **Vim** is powerful but has a learning curve.

**nano basics:**
```bash
nano filename.txt
# Ctrl+O  → Save
# Ctrl+X  → Exit
# Ctrl+K  → Cut line
# Ctrl+U  → Paste
```

**Vim basics:**
```bash
vim filename.txt
# i        → Enter insert mode (start typing)
# Esc      → Return to normal mode
# :w       → Save
# :q       → Quit
# :wq      → Save and quit
# :q!      → Quit without saving
# /search  → Search for text
```

---

### Chapter 5 — File Permissions

Linux enforces a permission model with three classes of users (owner, group, everyone else) and three types of access (read, write, execute).

**Reading permissions:**
```
-rwxr-xr--
Others: read only
Group: read + execute
Owner: read + write + execute
File type (- = file, d = directory)
```

**Changing permissions:**
```bash
# Give owner execute permission
chmod u+x script.sh

# Set permissions using octal notation
# 7=rwx, 5=r-x, 4=r--
chmod 754 script.sh

# Change file owner
chown alice report.txt

# Change owner and group
chown alice:developers report.txt
```

---

### Chapter 6 — Common Tools: grep, awk, sed

These three tools are workhorses of Linux text processing.

**grep — Search text:**
```bash
# Find lines containing "error" in a log file
grep "error" /var/log/syslog

# Case-insensitive search
grep -i "Error" logfile.txt

# Show line numbers
grep -n "warning" app.log

# Recursive search through directories
grep -r "TODO" ~/projects/
```

**awk — Process fields:**
```bash
# Print the first and third column from a file
awk '{print $1, $3}' data.txt

# Print lines where the second column is greater than 100
awk '$2 > 100 {print}' data.txt

# Use a custom field separator (CSV)
awk -F',' '{print $1}' file.csv
```

**sed — Stream editor:**
```bash
# Replace first occurrence of "old" with "new" on each line
sed 's/old/new/' file.txt

# Replace all occurrences (global flag)
sed 's/old/new/g' file.txt

# Edit file in place
sed -i 's/old/new/g' file.txt

# Delete lines containing a pattern
sed '/pattern/d' file.txt
```

---

### Chapter 7 — Pipes and Redirection

One of Linux's most powerful features is composing small tools into pipelines.

```bash
# Pipe: send output of one command to another
ls -la | grep ".txt"

# Count lines in a file
cat file.txt | wc -l

# Sort and remove duplicates
cat names.txt | sort | uniq

# Find top 5 largest files
du -h /home | sort -rh | head -5

# Redirect output to a file (overwrite)
ls > filelist.txt

# Append output to a file
echo "New entry" >> log.txt

# Redirect errors to a file
command 2> errors.log

# Redirect both stdout and stderr
command > output.log 2>&1
```

---

### Chapter 8 — Environment Variables and PATH

Environment variables store configuration values that the shell and programs can read.

```bash
# View all environment variables
env

# Print a specific variable
echo $HOME
echo $USER
echo $PATH

# Set a temporary variable (current session only)
MY_VAR="hello"
echo $MY_VAR

# Export a variable so child processes can see it
export MY_VAR="hello"

# Add a directory to PATH permanently (in ~/.bashrc)
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

---

### Chapter 9 — A Peek at Advanced Topics

The course introduces several topics for further exploration.

**Process management:**
```bash
# List running processes
ps aux

# Interactive process viewer
top

# Kill a process by ID
kill 1234

# Kill by name
killall firefox
```

**Archives:**
```bash
# Create a tar archive
tar -cvf archive.tar folder/

# Create a compressed archive
tar -czvf archive.tar.gz folder/

# Extract a tar.gz archive
tar -xzvf archive.tar.gz

# Zip a directory
zip -r archive.zip folder/

# Unzip
unzip archive.zip
```

**Scheduling with cron:**
```bash
# Edit the crontab
crontab -e

# Run a script every day at 2:30 AM
# 30 2 * * * /home/user/backup.sh
```

---

### Chapter 10 — Package Management

The course wraps up with installing and managing software using the `apt` package manager (Debian/Ubuntu).

```bash
# Update the package list
sudo apt update

# Upgrade installed packages
sudo apt upgrade

# Install a package
sudo apt install curl

# Remove a package
sudo apt remove curl

# Remove a package and its config files
sudo apt purge curl

# Search for a package
apt search text-editor

# Show package details
apt show vim
```

---

## 📚 Quick Reference Card

| Category | Command | Description |
|---|---|---|
| Navigation | `pwd` | Print working directory |
| Navigation | `cd <dir>` | Change directory |
| Navigation | `ls -la` | List all files with details |
| Files | `touch <file>` | Create empty file |
| Files | `cp <src> <dst>` | Copy file |
| Files | `mv <src> <dst>` | Move/rename file |
| Files | `rm <file>` | Delete file |
| Viewing | `cat <file>` | Print file content |
| Viewing | `less <file>` | Scroll through file |
| Viewing | `head / tail` | First/last lines |
| Permissions | `chmod` | Change permissions |
| Permissions | `chown` | Change ownership |
| Search | `grep <pat> <file>` | Search for pattern |
| Search | `find` | Find files |
| Processing | `awk` | Field-based processing |
| Processing | `sed` | Stream substitution |
| Redirection | `>` | Overwrite to file |
| Redirection | `>>` | Append to file |
| Redirection | `|` | Pipe between commands |
| Packages | `apt update` | Refresh package list |
| Packages | `apt install` | Install a package |

---
