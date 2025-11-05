# GitHub Commands Reference

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
gh repo create                           # Interactive repo creation
gh repo create <name>                    # Create repo with name
gh repo create <name> --public           # Create public repository
gh repo create <name> --private          # Create private repository
gh repo create <name> --description "Description here"

# Create and initialize
gh repo create <name> --public --source=. --remote=origin --push

# Clone during creation
gh repo create <name> --public --clone
```

### Repository Operations

```bash
gh repo view                             # View current repository
gh repo view <owner>/<repo>              # View specific repository
gh repo view --web                       # Open repository in browser
gh repo list                             # List your repositories
gh repo list <owner>                     # List repositories for user/org
gh repo clone <owner>/<repo>             # Clone repository
gh repo fork                             # Fork current repository
gh repo fork <owner>/<repo>              # Fork specific repository
gh repo sync                             # Sync fork with upstream
gh repo delete <owner>/<repo>            # Delete repository
gh repo rename <new-name>                # Rename repository
gh repo edit --description "New description"  # Edit repository details
gh repo archive <owner>/<repo>           # Archive repository
```

### Repository Visibility

```bash
gh repo edit --visibility public         # Make repository public
gh repo edit --visibility private        # Make repository private
```

## Pull Requests

### Creating Pull Requests

```bash
gh pr create                             # Interactive PR creation
gh pr create --title "Title" --body "Description"
gh pr create --draft                     # Create draft PR
gh pr create --base develop              # Create PR against specific branch
gh pr create --web                       # Create PR in browser
gh pr create --fill                      # Use commit info for PR
gh pr create --assignee @me              # Assign to yourself
gh pr create --reviewer <username>       # Request specific reviewer
gh pr create --label "bug,urgent"        # Add labels
```

### Viewing Pull Requests

```bash
gh pr list                               # List open PRs
gh pr list --state all                   # List all PRs
gh pr list --state closed                # List closed PRs
gh pr list --author @me                  # List your PRs
gh pr list --assignee @me                # List PRs assigned to you
gh pr list --label "bug"                 # Filter by label
gh pr view <number>                      # View PR details
gh pr view <number> --web                # Open PR in browser
gh pr view <number> --comments           # View with comments
gh pr diff <number>                      # View PR diff
gh pr checks <number>                    # View PR status checks
```

### Managing Pull Requests

```bash
gh pr checkout <number>                  # Checkout PR locally
gh pr edit <number>                      # Edit PR
gh pr ready <number>                     # Mark draft PR as ready
gh pr review <number>                    # Review PR
gh pr review <number> --approve          # Approve PR
gh pr review <number> --request-changes  # Request changes
gh pr review <number> --comment --body "LGTM"
gh pr merge <number>                     # Merge PR (interactive)
gh pr merge <number> --merge             # Merge with merge commit
gh pr merge <number> --squash            # Squash and merge
gh pr merge <number> --rebase            # Rebase and merge
gh pr merge <number> --delete-branch     # Delete branch after merge
gh pr close <number>                     # Close PR
gh pr reopen <number>                    # Reopen closed PR
```

### PR Comments

```bash
gh pr comment <number> --body "Comment text"
gh pr comment <number> --edit-last       # Edit your last comment
```

## Issues

### Creating Issues

```bash
gh issue create                          # Interactive issue creation
gh issue create --title "Bug title" --body "Description"
gh issue create --label "bug,help wanted"
gh issue create --assignee @me           # Assign to yourself
gh issue create --assignee <username>    # Assign to specific user
gh issue create --milestone "v1.0"       # Assign to milestone
gh issue create --web                    # Create issue in browser
```

### Viewing Issues

```bash
gh issue list                            # List open issues
gh issue list --state all                # List all issues
gh issue list --state closed             # List closed issues
gh issue list --author @me               # List your issues
gh issue list --assignee @me             # List issues assigned to you
gh issue list --label "bug"              # Filter by label
gh issue list --milestone "v1.0"         # Filter by milestone
gh issue view <number>                   # View issue details
gh issue view <number> --web             # Open issue in browser
gh issue view <number> --comments        # View with comments
```

### Managing Issues

```bash
gh issue edit <number>                   # Edit issue
gh issue edit <number> --title "New title"
gh issue edit <number> --add-label "bug"
gh issue edit <number> --remove-label "enhancement"
gh issue edit <number> --add-assignee @me
gh issue close <number>                  # Close issue
gh issue close <number> --comment "Fixed in PR #123"
gh issue reopen <number>                 # Reopen closed issue
gh issue pin <number>                    # Pin issue
gh issue unpin <number>                  # Unpin issue
gh issue transfer <number> <owner>/<repo>  # Transfer issue
gh issue delete <number>                 # Delete issue
```

### Issue Comments

```bash
gh issue comment <number> --body "Comment text"
gh issue comment <number> --edit-last    # Edit your last comment
```

## Releases

### Creating Releases

```bash
gh release create v1.0.0                 # Create release
gh release create v1.0.0 --title "Version 1.0"
gh release create v1.0.0 --notes "Release notes here"
gh release create v1.0.0 --draft         # Create draft release
gh release create v1.0.0 --prerelease    # Mark as pre-release
gh release create v1.0.0 file1.zip file2.tar.gz  # Upload assets
gh release create v1.0.0 --generate-notes  # Auto-generate notes
```

### Managing Releases

```bash
gh release list                          # List releases
gh release view <tag>                    # View release details
gh release view <tag> --web              # Open release in browser
gh release download <tag>                # Download release assets
gh release download <tag> --pattern "*.zip"  # Download specific files
gh release edit <tag>                    # Edit release
gh release delete <tag>                  # Delete release
gh release upload <tag> file.zip         # Upload asset to release
gh release delete-asset <tag> <filename>  # Delete asset
```

## Gists

```bash
gh gist create <file>                    # Create gist from file
gh gist create <file> --public           # Create public gist
gh gist create --desc "Description"      # Add description
gh gist list                             # List your gists
gh gist view <id>                        # View gist
gh gist edit <id>                        # Edit gist
gh gist delete <id>                      # Delete gist
gh gist clone <id>                       # Clone gist
```

## Workflows & Actions

```bash
gh workflow list                         # List workflows
gh workflow view <workflow>              # View workflow details
gh workflow run <workflow>               # Trigger workflow
gh workflow enable <workflow>            # Enable workflow
gh workflow disable <workflow>           # Disable workflow

gh run list                              # List workflow runs
gh run view <run-id>                     # View run details
gh run watch <run-id>                    # Watch run in real-time
gh run rerun <run-id>                    # Re-run workflow
gh run cancel <run-id>                   # Cancel workflow run
gh run download <run-id>                 # Download artifacts
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

### Start Working on an Issue

```bash
gh issue view 123                        # View issue details
git checkout -b fix-issue-123            # Create branch
# Make changes...
git add .
git commit -m "Fix issue #123"
git push -u origin fix-issue-123
gh pr create --fill                      # Create PR
```

### Review & Merge PR

```bash
gh pr list                               # See open PRs
gh pr view 45                            # View PR details
gh pr checkout 45                        # Test locally
gh pr review 45 --approve               # Approve PR
gh pr merge 45 --squash --delete-branch  # Merge and cleanup
```

### Create Release from Tag

```bash
git tag v1.0.0                           # Create tag
git push --tags                          # Push tag
gh release create v1.0.0 --generate-notes  # Create release
```

### Quick Status Check

```bash
gh pr status                             # Your PR status
gh issue status                          # Your issue status
gh run list --limit 5                    # Recent workflow runs
```

## Tips & Best Practices

1. **Use `--web` flag** - Quickly open things in browser when needed
2. **Set up aliases** - Create shortcuts for frequently used commands
3. **Use `--fill`** - Auto-populate PR descriptions from commits
4. **Check `gh status`** - Quick overview of your PRs and issues
5. **Use JSON output** - Pipe results to other tools with `--json`
6. **Enable shell completion** - Run `gh completion -s zsh` or `gh completion -s bash`

---

**Quick Reference Card:**
```bash
gh repo view --web        # Open repo in browser
gh pr create --fill       # Create PR from commits
gh issue create           # Create new issue
gh pr checkout 123        # Test PR locally
gh pr merge 123           # Merge PR
```
