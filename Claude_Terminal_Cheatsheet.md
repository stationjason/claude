# Claude Terminal Cheatsheet

## Navigation & Directory Operations

```bash
pwd                    # Print working directory (where am I?)
ls                     # List files in current directory
ls -la                 # List all files (including hidden) with details
cd <directory>         # Change directory
cd ..                  # Go up one directory
cd ~                   # Go to home directory
cd -                   # Go to previous directory
mkdir <name>           # Create new directory
rmdir <name>           # Remove empty directory
```

## File Operations

```bash
touch <file>           # Create new empty file
cat <file>             # Display file contents
less <file>            # View file with scrolling (q to quit)
head <file>            # Show first 10 lines
tail <file>            # Show last 10 lines
cp <source> <dest>     # Copy file
cp -r <source> <dest>  # Copy directory recursively
mv <source> <dest>     # Move or rename file
rm <file>              # Delete file
rm -rf <directory>     # Delete directory and contents (use carefully!)
open <file>            # Open file with default app (macOS)
```

## File Search & Content

```bash
find . -name "*.txt"   # Find all .txt files in current directory
grep "text" <file>     # Search for text in file
grep -r "text" .       # Search for text in all files recursively
which <command>        # Show location of command
```

## Git Commands (Essential)

### Setup & Configuration
```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
git config --list      # View your git configuration
```

### Repository Basics
```bash
git init               # Initialize new git repository
git clone <url>        # Clone remote repository
git status             # Check status of your changes
git log                # View commit history
git log --oneline      # Compact commit history
```

### Making Changes
```bash
git add <file>         # Stage specific file
git add .              # Stage all changes
git commit -m "message"    # Commit with message
git diff               # Show unstaged changes
git diff --staged      # Show staged changes
```

### Branches
```bash
git branch             # List branches
git branch <name>      # Create new branch
git checkout <branch>  # Switch to branch
git checkout -b <name> # Create and switch to new branch
git merge <branch>     # Merge branch into current branch
git branch -d <name>   # Delete branch
```

### Remote Operations
```bash
git remote -v          # Show remote repositories
git remote add origin <url>  # Add remote repository
git push               # Push commits to remote
git push -u origin main      # Push and set upstream branch
git pull               # Fetch and merge remote changes
git fetch              # Download remote changes (no merge)
```

### Undo & Reset
```bash
git restore <file>     # Discard changes in working directory
git restore --staged <file>  # Unstage file
git reset HEAD~1       # Undo last commit (keep changes)
git reset --hard HEAD~1      # Undo last commit (discard changes)
```

## GitHub CLI (gh)

### Authentication
```bash
gh auth login          # Login to GitHub
gh auth status         # Check authentication status
gh auth logout         # Logout from GitHub
```

### Repository Operations
```bash
gh repo create         # Create new repository
gh repo view           # View repository details
gh repo clone <repo>   # Clone repository
gh repo list           # List your repositories
```

### Pull Requests
```bash
gh pr create           # Create pull request
gh pr list             # List pull requests
gh pr view <number>    # View pull request
gh pr checkout <number>    # Checkout pull request locally
gh pr merge <number>   # Merge pull request
```

### Issues
```bash
gh issue create        # Create new issue
gh issue list          # List issues
gh issue view <number> # View issue details
gh issue close <number>    # Close issue
```

## Homebrew (macOS Package Manager)

```bash
brew install <package> # Install package
brew uninstall <package>   # Uninstall package
brew update            # Update Homebrew
brew upgrade           # Upgrade all packages
brew list              # List installed packages
brew search <term>     # Search for packages
brew info <package>    # Show package information
```

## System & Process Management

```bash
top                    # Show running processes
ps aux                 # List all running processes
kill <pid>             # Kill process by ID
killall <name>         # Kill process by name
df -h                  # Show disk space
du -sh <directory>     # Show directory size
whoami                 # Show current user
sudo <command>         # Run command as administrator
clear                  # Clear terminal screen
history                # Show command history
```

## Shortcuts & Tips

### Keyboard Shortcuts
```
Ctrl + C               # Cancel current command
Ctrl + D               # Exit terminal / end of file
Ctrl + L               # Clear screen (same as 'clear')
Ctrl + A               # Move to beginning of line
Ctrl + E               # Move to end of line
Ctrl + U               # Delete from cursor to beginning
Ctrl + K               # Delete from cursor to end
Ctrl + R               # Search command history
Tab                    # Auto-complete
↑ / ↓                  # Navigate command history
```

### Useful Tricks
```bash
!!                     # Run last command
!$                     # Use last argument from previous command
command &              # Run command in background
command1 && command2   # Run command2 only if command1 succeeds
command1 || command2   # Run command2 only if command1 fails
command > file         # Redirect output to file (overwrite)
command >> file        # Append output to file
```

## File Permissions (macOS/Linux)

```bash
chmod +x <file>        # Make file executable
chmod 755 <file>       # Set read/write/execute for owner, read/execute for others
chown <user> <file>    # Change file owner
ls -l                  # View file permissions
```

## Network & Download

```bash
ping <host>            # Test connection to host
curl <url>             # Download content from URL
curl -o <file> <url>   # Download and save to file
wget <url>             # Download file (may need: brew install wget)
ssh <user>@<host>      # Connect to remote server
```

## Tips for Beginners

1. **Tab completion is your friend** - Press Tab to auto-complete commands and file names
2. **Use `man <command>`** - Read manual pages for any command (q to quit)
3. **Be careful with `rm -rf`** - This permanently deletes files, no trash/recycle bin
4. **Use `git status` often** - Always check what you're about to commit
5. **Read error messages** - They usually tell you exactly what's wrong
6. **Start small** - Practice basic commands before complex operations
7. **Use `--help`** - Most commands support `command --help` for quick reference
8. **Copy-paste carefully** - Don't run commands you don't understand

## Common Workflows

### Starting a New Project with Git
```bash
mkdir my-project       # Create directory
cd my-project          # Enter directory
git init               # Initialize git
touch README.md        # Create README
git add .              # Stage files
git commit -m "Initial commit"
gh repo create         # Create GitHub repo and push
```

### Daily Git Workflow
```bash
git status             # Check current state
git add .              # Stage changes
git commit -m "Description of changes"
git push               # Push to remote
```

### Fixing a Mistake
```bash
git status             # See what's wrong
git restore <file>     # Undo changes to file
# or
git reset HEAD~1       # Undo last commit
```

---

**Pro Tip:** Keep this file handy and add your own notes as you learn!
