# GitHub Commands Reference

## Beginner's Glossary - Learn These First!

### Essential Terms

**Repository (Repo)** - Like a project folder that stores all your code, files, and the history of changes. Think of it as your project's home on GitHub.

**Clone** - Making a copy of a repository from GitHub to your computer so you can work on it locally.

**Fork** - Making your own copy of someone else's repository on GitHub. It's like saying "I want to work on my own version of this project." You still have the original, but now you have your own copy you can modify without affecting the original.

**Branch** - A separate version of your code where you can make changes without affecting the main code. Like having a rough draft that doesn't mess up the final version.

**Commit** - Saving a snapshot of your changes with a description of what you changed. Like clicking "Save" but with notes about what you did.

**Push** - Sending your commits (saved changes) from your computer to GitHub so others can see them.

**Pull** - Downloading changes from GitHub to your computer to get the latest updates.

**Pull Request (PR)** - Asking the project owner to review and accept your changes. It's like saying "Hey, I made some improvements, can you add them to the main project?" Even though it says "pull," you're actually asking them to pull YOUR changes into THEIR code.

**Issue** - A way to track bugs, feature requests, or tasks. Like a to-do list item or bug report for a project.

**Merge** - Combining changes from one branch into another. When your PR gets accepted, your changes get merged into the main code.

**Squash** - Combining multiple commits into one single commit. Makes the history cleaner and easier to read.

**Rebase** - Another way to combine changes, but it rewrites history to make it look like your changes were made on top of the latest code.

**Upstream** - The original repository that you forked from. If you copied someone's project, "upstream" refers to their original version.

**Draft PR** - A pull request that's not ready for review yet. You're saying "I'm working on this, but don't review it yet."

**Release** - A specific version of your software that you're officially sharing with users (like v1.0, v2.0).

**Gist** - A simple way to share code snippets or small files. Like a mini-repository for quick sharing.

**Workflow/Actions** - Automated tasks that run when certain things happen (like running tests every time you push code).

**API** - Application Programming Interface. A way for programs to talk to GitHub automatically instead of using the website.

**SSH Key** - A secure way to connect to GitHub without typing your password every time. Like a digital key to your account.

---

## GitHub CLI (gh) - Complete Guide

### Installation & Setup

```bash
brew install gh              # Install GitHub CLI (macOS)
gh --version                 # Check installed version
gh auth login               # Login to GitHub
gh auth status              # Check authentication status
gh auth logout              # Logout from GitHub
gh auth refresh             # Refresh authentication
```

## Repository Management

### Creating Repositories

```bash
# BEGINNER: Start here to create a new project on GitHub
gh repo create                           # Interactive - asks you questions step by step
gh repo create <name>                    # Create repo with a specific name
gh repo create <name> --public           # Everyone can see it (like this one you made!)
gh repo create <name> --private          # Only you (and people you invite) can see it
gh repo create <name> --description "Description here"  # Add a description

# Create and push your current folder to GitHub in one command (what we did earlier!)
gh repo create <name> --public --source=. --remote=origin --push

# Create repo and download it to your computer immediately
gh repo create <name> --public --clone
```

### Repository Operations

```bash
# Viewing repositories
gh repo view                             # See info about the repo you're currently in
gh repo view <owner>/<repo>              # See info about any repo (ex: gh repo view microsoft/vscode)
gh repo view --web                       # Open the repo in your browser

# Listing repositories
gh repo list                             # Show all YOUR repositories
gh repo list <owner>                     # Show all repos from a specific user/organization

# Copying repositories
gh repo clone <owner>/<repo>             # Download someone's repo to your computer (ex: gh repo clone facebook/react)

# Forking - Making your own copy of someone else's project
gh repo fork                             # Copy the current repo to YOUR GitHub account
gh repo fork <owner>/<repo>              # Copy a specific repo to your account (ex: gh repo fork rails/rails)
gh repo sync                             # Update your fork with changes from the original project

# Managing your repositories
gh repo delete <owner>/<repo>            # Permanently delete a repository (careful!)
gh repo rename <new-name>                # Give your repo a different name
gh repo edit --description "New description"  # Change the description
gh repo archive <owner>/<repo>           # Put repo in read-only mode (when project is done)
```

### Repository Visibility

```bash
# Control who can see your repository
gh repo edit --visibility public         # Anyone can see and download your code
gh repo edit --visibility private        # Only you and invited people can see it
```

## Pull Requests (PR)

**What is a Pull Request?** When you make changes to code and want the project owner to add your changes to their project, you create a PR. It's a request saying "Please pull my changes into your code!"

### Creating Pull Requests

```bash
# BEGINNER: After you've made changes and pushed them, create a PR
gh pr create                             # Interactive - answers questions to create your PR
gh pr create --title "Title" --body "Description"  # Create PR with title and description
gh pr create --draft                     # Create a draft (not ready for review yet)
gh pr create --base develop              # Create PR to merge into a specific branch
gh pr create --web                       # Open browser to create PR (easier for beginners)
gh pr create --fill                      # Auto-fill title/description from your commits
gh pr create --assignee @me              # Assign yourself to work on it
gh pr create --reviewer <username>       # Ask someone specific to review your changes
gh pr create --label "bug,urgent"        # Tag it with labels like "bug" or "urgent"
```

### Viewing Pull Requests

```bash
# Seeing PRs in the project
gh pr list                               # Show all open (active) PRs
gh pr list --state all                   # Show ALL PRs (open, closed, merged)
gh pr list --state closed                # Show only closed PRs
gh pr list --author @me                  # Show only YOUR PRs
gh pr list --assignee @me                # Show PRs assigned to you to work on
gh pr list --label "bug"                 # Show only PRs tagged as "bug"

# Looking at a specific PR
gh pr view <number>                      # Show details of PR #number (ex: gh pr view 42)
gh pr view <number> --web                # Open PR in your browser
gh pr view <number> --comments           # Show all comments people made
gh pr diff <number>                      # Show what code changed (differences)
gh pr checks <number>                    # Show if automated tests passed/failed
```

### Managing Pull Requests

```bash
# Testing and reviewing PRs
gh pr checkout <number>                  # Download a PR to test it on your computer
gh pr edit <number>                      # Change PR title, description, etc.
gh pr ready <number>                     # Change draft PR to "ready for review"

# Reviewing someone's PR
gh pr review <number>                    # Start a review
gh pr review <number> --approve          # Approve the changes (you like them!)
gh pr review <number> --request-changes  # Ask for changes before accepting
gh pr review <number> --comment --body "LGTM"  # Leave comment (LGTM = "Looks Good To Me")

# Accepting/Merging a PR (combining the changes into main code)
gh pr merge <number>                     # Merge PR (asks how you want to merge)
gh pr merge <number> --merge             # Standard merge (keeps all commits)
gh pr merge <number> --squash            # Squash merge (combines commits into one)
gh pr merge <number> --rebase            # Rebase merge (rewrites history cleanly)
gh pr merge <number> --delete-branch     # Merge and delete the branch (cleanup)

# Managing PR status
gh pr close <number>                     # Close PR without merging (reject it)
gh pr reopen <number>                    # Reopen a closed PR
```

### PR Comments

```bash
gh pr comment <number> --body "Comment text"  # Add a comment to a PR
gh pr comment <number> --edit-last       # Edit the last comment you made
```

## Issues

**What is an Issue?** Issues are like to-do items or bug reports for a project. Found a bug? Create an issue. Want a new feature? Create an issue. It's how teams track what needs to be done.

### Creating Issues

```bash
# BEGINNER: Report bugs, request features, or ask questions
gh issue create                          # Interactive - asks you what the issue is
gh issue create --title "Bug title" --body "Description"  # Create issue with details
gh issue create --label "bug,help wanted"  # Tag it (bug, feature, question, etc.)
gh issue create --assignee @me           # Assign yourself to work on it
gh issue create --assignee <username>    # Assign someone else to work on it
gh issue create --milestone "v1.0"       # Link to a project milestone/version
gh issue create --web                    # Open browser to create issue (easier)
```

### Viewing Issues

```bash
# Seeing all issues in a project
gh issue list                            # Show all open (unresolved) issues
gh issue list --state all                # Show ALL issues (open, closed)
gh issue list --state closed             # Show only resolved/closed issues
gh issue list --author @me               # Show issues YOU created
gh issue list --assignee @me             # Show issues assigned to YOU to fix
gh issue list --label "bug"              # Show only issues tagged as "bug"
gh issue list --milestone "v1.0"         # Show issues for version 1.0

# Looking at a specific issue
gh issue view <number>                   # Show details of issue #number
gh issue view <number> --web             # Open issue in browser
gh issue view <number> --comments        # Show all discussion/comments
```

### Managing Issues

```bash
# Editing issues
gh issue edit <number>                   # Edit an issue
gh issue edit <number> --title "New title"  # Change the title
gh issue edit <number> --add-label "bug"    # Add a label/tag
gh issue edit <number> --remove-label "enhancement"  # Remove a label
gh issue edit <number> --add-assignee @me   # Assign someone to work on it

# Closing/opening issues
gh issue close <number>                  # Close/resolve an issue (it's done!)
gh issue close <number> --comment "Fixed in PR #123"  # Close with explanation
gh issue reopen <number>                 # Reopen a closed issue (not actually fixed)

# Organizing issues
gh issue pin <number>                    # Pin issue to top (important!)
gh issue unpin <number>                  # Unpin issue
gh issue transfer <number> <owner>/<repo>  # Move issue to different repository
gh issue delete <number>                 # Delete issue (rare, usually just close it)
```

### Issue Comments

```bash
gh issue comment <number> --body "Comment text"  # Add comment/discussion to issue
gh issue comment <number> --edit-last    # Edit your last comment
```

## Releases

**What is a Release?** When your project reaches a milestone (like version 1.0), you create a release. It's like officially publishing a version of your software for people to download and use.

### Creating Releases

```bash
# BEGINNER: Package up a version of your project for users to download
gh release create v1.0.0                 # Create version 1.0.0
gh release create v1.0.0 --title "Version 1.0"  # Give it a friendly name
gh release create v1.0.0 --notes "Release notes here"  # Describe what's new
gh release create v1.0.0 --draft         # Create draft (not public yet)
gh release create v1.0.0 --prerelease    # Mark as beta/testing version
gh release create v1.0.0 file1.zip file2.tar.gz  # Include downloadable files
gh release create v1.0.0 --generate-notes  # Auto-create notes from commits
```

### Managing Releases

```bash
# Viewing releases
gh release list                          # Show all versions you've released
gh release view <tag>                    # Show details of a specific version
gh release view <tag> --web              # Open release page in browser

# Downloading releases
gh release download <tag>                # Download all files from a release
gh release download <tag> --pattern "*.zip"  # Download only zip files

# Editing releases
gh release edit <tag>                    # Change release details
gh release delete <tag>                  # Delete a release (careful!)
gh release upload <tag> file.zip         # Add a file to existing release
gh release delete-asset <tag> <filename>  # Remove a file from release
```

## Gists

**What is a Gist?** A quick way to share code snippets or small files without creating a full repository. Perfect for sharing examples, notes, or config files.

```bash
# BEGINNER: Share small code snippets quickly
gh gist create <file>                    # Create gist from a file
gh gist create <file> --public           # Make it public (anyone can see)
gh gist create --desc "Description"      # Add description of what it is
gh gist list                             # Show all your gists
gh gist view <id>                        # View a specific gist
gh gist edit <id>                        # Edit a gist
gh gist delete <id>                      # Delete a gist
gh gist clone <id>                       # Download a gist to your computer
```

## Workflows & Actions

**What are Workflows?** Automated tasks that run when something happens (like when you push code). For example: automatically run tests, check for bugs, or deploy your app. This is advanced - you probably won't need this as a beginner!

```bash
# View workflows (automation scripts)
gh workflow list                         # Show all automated workflows in the project
gh workflow view <workflow>              # See details of a specific workflow
gh workflow run <workflow>               # Manually trigger/start a workflow
gh workflow enable <workflow>            # Turn on a workflow
gh workflow disable <workflow>           # Turn off a workflow

# View workflow runs (the results of automation)
gh run list                              # Show recent workflow runs
gh run view <run-id>                     # See what happened in a specific run
gh run watch <run-id>                    # Watch a workflow run in real-time
gh run rerun <run-id>                    # Run it again
gh run cancel <run-id>                   # Stop a running workflow
gh run download <run-id>                 # Download files created by workflow
```

## Advanced GitHub Operations

### Searching

```bash
gh search repos <query>                  # Search repositories
gh search issues <query>                 # Search issues
gh search prs <query>                    # Search pull requests
gh search code <query>                   # Search code

# Examples
gh search repos "language:python stars:>1000"
gh search issues "is:open label:bug"
gh search code "import numpy"
```

### API Access

```bash
gh api repos/:owner/:repo                # Make API request
gh api repos/:owner/:repo/issues         # List issues via API
gh api graphql -f query='...'           # GraphQL query
gh api --method POST repos/:owner/:repo/issues -f title="Title"
```

### Aliases (Custom Commands)

```bash
gh alias set <alias> <expansion>         # Create alias
gh alias list                            # List aliases
gh alias delete <alias>                  # Delete alias

# Examples
gh alias set bugs 'issue list --label=bug'
gh alias set prs 'pr list --author=@me'
```

### SSH Keys

```bash
gh ssh-key list                          # List SSH keys
gh ssh-key add <file>                    # Add SSH key
gh ssh-key add <file> --title "My key"   # Add with title
gh ssh-key delete <id>                   # Delete SSH key
```

### GPG Keys

```bash
gh gpg-key list                          # List GPG keys
gh gpg-key add <file>                    # Add GPG key
gh gpg-key delete <id>                   # Delete GPG key
```

## Configuration

```bash
gh config get <key>                      # Get config value
gh config set <key> <value>              # Set config value
gh config list                           # List all config

# Examples
gh config set editor vim
gh config set git_protocol ssh
gh config set browser firefox
```

## Extensions

```bash
gh extension list                        # List installed extensions
gh extension install <repo>              # Install extension
gh extension upgrade <extension>         # Upgrade extension
gh extension upgrade --all               # Upgrade all extensions
gh extension remove <extension>          # Remove extension
gh extension create <name>               # Create new extension

# Popular extensions
gh extension install github/gh-copilot
gh extension install dlvhdr/gh-dash
```

## Useful Flags & Options

```bash
--help                                   # Show help for any command
--version                                # Show version
--repo <owner>/<repo>                    # Specify repository
--json                                   # Output as JSON
--jq <expression>                        # Filter JSON output
--web                                    # Open in browser

# Examples
gh pr list --json number,title,author
gh pr list --json number --jq '.[0].number'
gh issue view 123 --repo owner/repo
```

## Common Workflows

**BEGINNER FRIENDLY: Real-world scenarios with step-by-step instructions**

### Scenario 1: Start Working on an Issue (Fix a Bug)

**The Situation:** You see an issue (bug) in a project and want to fix it.

```bash
# Step 1: Look at the issue to understand what needs fixing
gh issue view 123                        # Read issue #123

# Step 2: Create a new branch for your changes (don't work on main!)
git checkout -b fix-issue-123            # Create branch named "fix-issue-123"

# Step 3: Fix the bug in your code editor...

# Step 4: Save your changes to git
git add .                                # Stage all your changes
git commit -m "Fix issue #123"           # Commit with a message

# Step 5: Upload your changes to GitHub
git push -u origin fix-issue-123         # Push your branch to GitHub

# Step 6: Create a Pull Request asking to merge your fix
gh pr create --fill                      # Create PR (auto-fills from commits)
```

### Scenario 2: Review & Merge Someone's PR (You're the Project Owner)

**The Situation:** Someone submitted changes and you need to review and accept them.

```bash
# Step 1: See what PRs are waiting for review
gh pr list                               # Show all open pull requests

# Step 2: Look at a specific PR
gh pr view 45                            # Read details of PR #45

# Step 3: Test the changes on your computer
gh pr checkout 45                        # Download and test PR #45 locally

# Step 4: Looks good? Approve it!
gh pr review 45 --approve                # Approve the changes

# Step 5: Merge it into your main code and cleanup
gh pr merge 45 --squash --delete-branch  # Merge, squash commits, delete branch
```

### Scenario 3: Create Your First Release

**The Situation:** Your project is ready for version 1.0!

```bash
# Step 1: Create a version tag
git tag v1.0.0                           # Mark this point as version 1.0.0

# Step 2: Push the tag to GitHub
git push --tags                          # Upload tag to GitHub

# Step 3: Create official release on GitHub
gh release create v1.0.0 --generate-notes  # Create release with auto-generated notes
```

### Scenario 4: Quick Status Check (What am I working on?)

**The Situation:** You want to see all your current work.

```bash
gh pr status                             # See YOUR pull requests and their status
gh issue status                          # See issues you created or are assigned to
gh run list --limit 5                    # See recent automated test runs
```

### Scenario 5: Contribute to Someone Else's Project

**The Situation:** You found a cool project and want to contribute!

```bash
# Step 1: Fork the project (make your own copy)
gh repo fork owner/project --clone       # Fork and download to your computer

# Step 2: Create a branch for your changes
cd project                               # Go into the project folder
git checkout -b my-new-feature           # Create a branch

# Step 3: Make your changes in your code editor...

# Step 4: Save and push your changes
git add .
git commit -m "Add awesome new feature"
git push -u origin my-new-feature

# Step 5: Create PR to the original project
gh pr create --fill                      # Request they add your changes
```

## Tips & Best Practices

1. **Use `--web` flag** - Quickly open things in browser when needed
2. **Set up aliases** - Create shortcuts for frequently used commands
3. **Use `--fill`** - Auto-populate PR descriptions from commits
4. **Check `gh status`** - Quick overview of your PRs and issues
5. **Use JSON output** - Pipe results to other tools with `--json`
6. **Enable shell completion** - Run `gh completion -s zsh` or `gh completion -s bash`

---

## For Absolute Beginners: Start Here!

**The 10 commands you'll use 90% of the time:**

```bash
# Working with repositories
gh repo create --public              # Create a new project on GitHub
gh repo view --web                   # Open your project in browser
gh repo clone owner/repo             # Download someone's project

# Checking what's going on
gh repo list                         # See all your projects
gh pr list                           # See all pull requests
gh issue list                        # See all issues/bugs

# Creating stuff
gh issue create --web                # Report a bug or request a feature (in browser - easier!)
gh pr create --web                   # Create pull request (in browser - easier!)

# Quick status
gh pr status                         # See your pull requests
gh issue status                      # See your issues
```

**Remember:**
- Use `--web` flag to open things in your browser (easier when starting out!)
- `gh <command> --help` shows help for any command
- When in doubt, the interactive modes (just `gh pr create` without flags) will ask you questions

---

**Quick Reference Card:**
```bash
gh repo view --web        # Open repo in browser
gh pr create --fill       # Create PR from commits
gh issue create           # Create new issue
gh pr checkout 123        # Test PR locally
gh pr merge 123           # Merge PR
```
