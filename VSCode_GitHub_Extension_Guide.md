# VS Code GitHub Extension Guide

## Beginner's Glossary - VS Code GitHub Terms

### Essential Terms

**`Activity Bar`** - The vertical bar on the far left of VS Code with icons. This is where you click to access different views like Explorer, Search, Source Control, and GitHub.

**`Source Control View`** - The panel where you see your git changes (modified files, staging area, commits). Access it by clicking the branch icon in the Activity Bar or press `Cmd+Shift+G`.

**`GitHub View`** - The dedicated panel for GitHub PRs and Issues. Click the GitHub icon in the Activity Bar to see all your pull requests and issues.

**`Command Palette`** - VS Code's search bar for all commands. Press `Cmd+Shift+P` to open it and type what you want to do.

**`Inline Comments`** - Comments on specific lines of code in a PR review. They appear right next to the code line you're reviewing.

**`Working Tree`** - Your current files and changes that haven't been committed yet. Think of it as your "workspace."

**`Staging Area`** - Files you've marked to include in your next commit. Like a "shopping cart" before checkout.

**`Remote`** - The GitHub version of your repository (online). Changes need to be pushed to remote to appear on GitHub.

**`Sync`** - Pull changes from GitHub and push your changes in one action. Keeps your local code and GitHub in sync.

---

## Quick Start - First Time Setup

### Step 1: Authenticate with GitHub

```plaintext
Method 1: Automatic Prompt
- Open VS Code
- Extensions will prompt "Sign in with GitHub"
- Click "Allow" and follow browser authentication

Method 2: Manual Sign In
1. Press Cmd+Shift+P (Command Palette)
2. Type: "GitHub: Sign In"
3. Choose "Sign in with GitHub"
4. Authorize in browser
5. Return to VS Code
```

### Step 2: Verify Connection

```plaintext
1. Click Accounts icon (bottom left, person icon)
2. You should see your GitHub username
3. Click GitHub icon in Activity Bar (left sidebar)
4. You should see your PRs and Issues
```

### Step 3: Clone a Repository

```plaintext
Option 1: Command Palette
1. Press Cmd+Shift+P
2. Type: "Git: Clone"
3. Choose "Clone from GitHub"
4. Select a repository
5. Choose location to save

Option 2: Welcome Screen
1. Click "Clone Git Repository"
2. Choose "Clone from GitHub"
3. Select repository
```

---

## Interface Overview

### Activity Bar Icons (Left Sidebar)

```plaintext
📁 Explorer        - Browse files in your project
🔍 Search         - Search across all files
🌿 Source Control - Git changes, commits, sync
▶️ Run & Debug    - Run your code
📦 Extensions     - Install/manage extensions
🐙 GitHub         - Pull requests and issues view
```

### GitHub View Layout

```plaintext
PULL REQUESTS
├── Assigned to Me      - PRs you need to work on
├── Created by Me       - PRs you submitted
├── Waiting for Review  - PRs ready for your review
└── All Open           - All open PRs in repo

ISSUES
├── Assigned to Me      - Issues you're working on
├── Created by Me       - Issues you reported
└── All Open           - All open issues in repo
```

---

## Keyboard Shortcuts Reference

### Essential Shortcuts

```plaintext
NAVIGATION
Cmd+Shift+P          - Command Palette (access any command)
Cmd+Shift+G          - Open Source Control view
Cmd+Shift+E          - Open File Explorer
Cmd+P                - Quick file search/open
Cmd+Shift+F          - Search in all files
Cmd+B                - Toggle sidebar visibility

SOURCE CONTROL
Cmd+K Cmd+C          - Stage selected changes
Cmd+K Cmd+U          - Unstage selected changes
Cmd+Enter            - Commit staged changes
Cmd+Shift+K          - Delete line

GITHUB SPECIFIC
Cmd+Shift+P → "PR"   - Access all PR commands
Cmd+Shift+P → "Issue" - Access all Issue commands
Cmd+K Cmd+O          - Open file on GitHub
```

### Custom Keybindings (Optional Setup)

```json
// Add to keybindings.json (Cmd+K Cmd+S to open)
{
  "key": "cmd+shift+h",
  "command": "workbench.view.extension.github-pull-requests"
},
{
  "key": "cmd+k cmd+r",
  "command": "pr.openReview"
}
```

---

## Pull Requests Workflow

### Creating a Pull Request

#### Method 1: Using Source Control View

```plaintext
1. Make changes to your code
2. Open Source Control view (Cmd+Shift+G)
3. Review changes (click files to see diffs)
4. Stage changes (+ icon next to files)
5. Write commit message in text box
6. Click ✓ (Commit) button
7. Click "Sync Changes" or push icon (↑)
8. In Source Control view, click "Create Pull Request"
9. Fill in title and description
10. Click "Create"
```

#### Method 2: Using Command Palette

```plaintext
1. Press Cmd+Shift+P
2. Type: "GitHub Pull Requests: Create Pull Request"
3. Choose base branch (usually 'main')
4. Choose compare branch (your branch)
5. Fill in title and description
6. Choose "Create" or "Create Draft"
```

#### Method 3: Using GitHub View

```plaintext
1. Click GitHub icon in Activity Bar
2. Click + icon next to "PULL REQUESTS"
3. Follow the prompts
```

### Viewing Pull Requests

```plaintext
IN GITHUB VIEW:
- Click GitHub icon in Activity Bar
- Browse PRs under different categories
- Click a PR to see details

PR DETAILS PANEL:
- Description and comments
- Changed files list
- Checks status (tests, CI/CD)
- Reviewers and assignees
- Labels and milestones

VIEW CHANGED FILES:
- Click "Changed Files" in PR detail
- Click any file to see the diff
- Green = additions, Red = deletions
```

### Reviewing Pull Requests

#### Start a Review

```plaintext
1. Click PR in GitHub view
2. Click "Checkout" to test locally (optional)
3. Click "Review Changes" button
4. Review each changed file
```

#### Add Comments to Code

```plaintext
INLINE COMMENTS:
1. Open a changed file from PR
2. Hover over line number
3. Click + icon that appears
4. Write comment
5. Choose "Add Comment" or "Start Review"

REVIEW COMMENTS:
- Single Comment: Posts immediately
- Start Review: Batch comments, submit all at once
```

#### Complete Review

```plaintext
1. After reviewing all files, click "Finish Review"
2. Choose review type:
   - Comment: Just leave feedback
   - Approve: Changes look good!
   - Request Changes: Needs fixes before merging

3. Write summary (optional)
4. Click "Submit Review"
```

### Merging Pull Requests

```plaintext
IN PR DETAIL VIEW:
1. Ensure all checks pass (green checkmarks)
2. Ensure required approvals are received
3. Click "Merge Pull Request" button
4. Choose merge method:
   - Merge Commit: Keep all commits
   - Squash and Merge: Combine into one commit
   - Rebase and Merge: Rewrite history cleanly
5. Confirm merge
6. Optionally delete branch
```

### PR Commands (Command Palette)

```plaintext
Press Cmd+Shift+P and type:

GitHub Pull Requests: Create Pull Request
GitHub Pull Requests: Checkout Pull Request
GitHub Pull Requests: View Pull Request
GitHub Pull Requests: Merge Pull Request
GitHub Pull Requests: Close Pull Request
GitHub Pull Requests: Refresh
GitHub Pull Requests: Configure Remotes
```

---

## Issues Management

### Creating an Issue

#### Method 1: From GitHub View

```plaintext
1. Click GitHub icon in Activity Bar
2. Find "ISSUES" section
3. Click + icon next to "ISSUES"
4. Fill in:
   - Title
   - Description
   - Assignees
   - Labels
   - Milestone
5. Click "Create Issue"
```

#### Method 2: From Code

```plaintext
1. Select code that has a bug
2. Right-click
3. Choose "Create Issue from Selection"
4. VS Code auto-fills with code snippet
5. Add title and description
6. Click "Create"
```

#### Method 3: Command Palette

```plaintext
1. Press Cmd+Shift+P
2. Type: "GitHub Issues: Create Issue"
3. Fill in details
```

### Viewing Issues

```plaintext
IN GITHUB VIEW:
- All your issues are listed under "ISSUES"
- Click an issue to see details
- See description, comments, labels, assignees

FILTER ISSUES:
1. Click filter icon in ISSUES section
2. Filter by:
   - Assigned to you
   - Created by you
   - Mentioned
   - Labels
   - Milestone
```

### Working with Issues

```plaintext
CREATE BRANCH FROM ISSUE:
1. Open issue in GitHub view
2. Click "Start Working on Issue"
3. VS Code creates a branch automatically
4. Name format: issue-[number]-[title]

LINK COMMITS TO ISSUES:
- In commit message, use: "Fixes #123" or "Closes #123"
- Issue closes automatically when PR merges

REFERENCE ISSUES:
- In comments/PRs: Use #123 to reference issue
- VS Code auto-completes issue numbers
```

### Issue Commands (Command Palette)

```plaintext
Press Cmd+Shift+P and type:

GitHub Issues: Create Issue
GitHub Issues: Create Issue from Selection
GitHub Issues: Create Issue from Clipboard
GitHub Issues: Open Issue
GitHub Issues: Copy GitHub Permalink
GitHub Issues: Copy Issue Number
```

---

## Source Control Features

### Staging Changes

```plaintext
STAGE INDIVIDUAL FILES:
- Hover over file in Source Control view
- Click + icon to stage

STAGE ALL CHANGES:
- Click + icon next to "Changes" header

STAGE SPECIFIC LINES:
1. Open file
2. Click line numbers of changes you want
3. Right-click → "Stage Selected Ranges"

UNSTAGE:
- Click - icon to unstage files
```

### Committing Changes

```plaintext
BASIC COMMIT:
1. Stage your changes
2. Type commit message in input box
3. Press Cmd+Enter or click ✓ icon

COMMIT OPTIONS:
- Click ••• (more actions) menu
- Commit All (stage and commit everything)
- Commit Staged (only staged files)
- Commit Staged (Amend) - add to previous commit
- Undo Last Commit - revert last commit

COMMIT MESSAGE TIPS:
- Line 1: Brief summary (50 chars max)
- Line 2: Blank
- Line 3+: Detailed description
- Use "Fixes #123" to link issues
```

### Pushing & Pulling

```plaintext
SYNC CHANGES (Recommended):
- Click "Sync Changes" button
- Pulls remote changes, then pushes yours
- Safest option for beginners

PUSH ONLY:
- Click ••• menu → "Push"
- Uploads your commits to GitHub

PULL ONLY:
- Click ••• menu → "Pull"
- Downloads changes from GitHub

FETCH:
- Click ••• menu → "Fetch"
- Check for remote changes without merging
```

### Viewing Changes

```plaintext
VIEW MODIFIED FILE:
- Click file in Source Control view
- See side-by-side diff
- Left: Original, Right: Your changes

NAVIGATE CHANGES:
- F7: Next change
- Shift+F7: Previous change
- Click arrows in diff gutter

DISCARD CHANGES:
- Right-click file → "Discard Changes"
- Careful: This can't be undone!
```

### Branch Management

```plaintext
VIEW CURRENT BRANCH:
- Bottom left status bar shows branch name

SWITCH BRANCHES:
1. Click branch name in status bar
2. Choose branch from list
3. Or type to search branches

CREATE NEW BRANCH:
1. Click branch name in status bar
2. Click "+ Create new branch..."
3. Enter branch name
4. Choose to switch to it or not

PUBLISH BRANCH:
- Click publish icon (☁️↑) in Source Control view
- Uploads branch to GitHub

DELETE BRANCH:
- Click ••• menu → "Branch" → "Delete Branch"
- Choose branch to delete
```

---

## GitLens Features

**GitLens** enhances VS Code with powerful git visualization and history features.

### File Annotations

```plaintext
CURRENT LINE BLAME:
- Shows author and date at end of current line
- Automatically appears as you navigate code
- Click to see full commit details

FILE BLAME:
- Press Cmd+Shift+P → "GitLens: Toggle File Blame"
- Shows author for every line
- Hover over any line to see details

FILE HEATMAP:
- Press Cmd+Shift+P → "GitLens: Toggle File Heatmap"
- Colors show how recently lines changed
- Hot (red) = recent, Cold (blue) = old
```

### Commit History

```plaintext
VIEW FILE HISTORY:
1. Open a file
2. Click GitLens icon in title bar
3. Or press Cmd+Shift+P → "GitLens: Show File History"
4. See all commits that changed this file

VIEW LINE HISTORY:
1. Select a line or lines
2. Right-click → "Show Line History"
3. See commits that changed these specific lines

COMMIT DETAILS:
- Click any commit in history
- See: Author, date, message, changed files
- Click changed file to see what changed
```

### Compare Revisions

```plaintext
COMPARE FILE VERSIONS:
1. Right-click file → "Open Changes"
2. Or use GitLens history view
3. Choose commits to compare
4. See side-by-side diff

COMPARE BRANCHES:
1. Press Cmd+Shift+P
2. Type: "GitLens: Compare References"
3. Choose two branches
4. See all differences
```

### GitLens Sidebar

```plaintext
OPEN GITLENS VIEW:
- Click GitLens icon in Activity Bar
- Or press Cmd+Shift+P → "GitLens: Show GitLens"

SECTIONS:
- Commits: Recent commits in repo
- File History: History of current file
- Line History: History of selected lines
- Branches: All branches with details
- Remotes: Remote repositories
- Stashes: Saved uncommitted changes
- Tags: Version tags
- Contributors: All contributors with stats
```

### GitLens Commands

```plaintext
Press Cmd+Shift+P and type "GitLens":

GitLens: Show File History
GitLens: Show Line History
GitLens: Compare File Revisions
GitLens: Compare References (branches)
GitLens: Show Commit Graph
GitLens: Search Commits
GitLens: Open File on Remote (GitHub)
GitLens: Copy Remote File URL
```

---

## Advanced Workflows

### Scenario 1: Code Review Workflow

**The Situation:** You need to review a teammate's PR thoroughly.

```plaintext
Step 1: Find the PR
- Click GitHub icon in Activity Bar
- Find PR under "Waiting for Review"

Step 2: Checkout PR Locally
- Click the PR
- Click "Checkout" button
- PR code now on your machine

Step 3: Test the Changes
- Run the code/tests
- Verify functionality
- Check for bugs

Step 4: Review Code
- Click "Review Changes"
- Go through each changed file
- Add inline comments on specific lines

Step 5: Start a Review Session
- When you add first comment, choose "Start Review"
- This batches all comments together
- Continue adding comments

Step 6: Submit Review
- Click "Finish Review" when done
- Choose: Comment / Approve / Request Changes
- Write summary
- Submit

Step 7: Return to Your Branch
- Click branch name in status bar
- Switch back to your working branch
```

### Scenario 2: Fix a Bug and Link to Issue

**The Situation:** An issue reports a bug, you want to fix it properly.

```plaintext
Step 1: Create Branch from Issue
- Open issue in GitHub view
- Click "Start Working on Issue"
- New branch created automatically

Step 2: Fix the Bug
- Make code changes
- Test your fix
- Verify it solves the issue

Step 3: Commit with Issue Reference
- Stage changes
- Write commit message: "Fix authentication timeout. Fixes #123"
- Commit (Cmd+Enter)

Step 4: Push Changes
- Click "Sync Changes" or push icon

Step 5: Create PR
- Click "Create Pull Request" in Source Control
- Title auto-fills from commit
- Description can reference issue: "Closes #123"
- Submit PR

Step 6: When PR Merges
- Issue #123 automatically closes
- Branch can be deleted
```

### Scenario 3: Resolve Merge Conflicts

**The Situation:** You pull changes and VS Code shows merge conflicts.

```plaintext
Step 1: Identify Conflicts
- VS Code shows files with conflicts
- Files marked with ⚠️ symbol

Step 2: Open Conflicted File
- Click file in Source Control view
- Conflict markers appear:
  <<<<<<< HEAD (your changes)
  =======
  >>>>>>> branch (incoming changes)

Step 3: Resolve Each Conflict
- Click "Accept Current Change" (keep yours)
- Click "Accept Incoming Change" (use theirs)
- Click "Accept Both Changes" (keep both)
- Or manually edit to merge both

Step 4: Mark as Resolved
- After fixing all conflicts in file
- Stage the file (+ icon)
- Repeat for all conflicted files

Step 5: Complete Merge
- All conflicts resolved
- Commit the merge
- Push changes
```

### Scenario 4: Create Release from VS Code

**The Situation:** Your code is ready for v1.0 release.

```plaintext
Step 1: Ensure Everything is Committed
- Source Control should show "No changes"
- All code pushed to GitHub

Step 2: Create Git Tag
- Press Cmd+Shift+P
- Type: "Git: Create Tag"
- Enter: v1.0.0
- Optionally add message

Step 3: Push Tag
- Press Cmd+Shift+P
- Type: "Git: Push Tags"
- Tag uploaded to GitHub

Step 4: Create Release on GitHub
- Use gh CLI or GitHub website
- Or install "GitHub Release" extension for VS Code
- gh release create v1.0.0 --generate-notes
```

### Scenario 5: Collaborative PR Review Discussion

**The Situation:** Multiple reviewers discussing changes in a PR.

```plaintext
Step 1: Open PR in VS Code
- Click PR in GitHub view
- View discussion thread

Step 2: Reply to Comments
- Click on any comment thread
- Type reply in text box
- Submit comment

Step 3: Resolve Conversations
- Click "Resolve conversation" when addressed
- Keeps discussion organized

Step 4: Request Re-review
- After making requested changes
- Click "Re-request Review" button
- Notifies reviewers

Step 5: Monitor Discussion
- Comments update in real-time
- Get notifications in VS Code
```

---

## Settings & Configuration

### Access Settings

```plaintext
1. Press Cmd+, (Command + Comma)
2. Or Cmd+Shift+P → "Preferences: Open Settings"
3. Search for setting name
```

### Essential GitHub Extension Settings

```json
// settings.json (Cmd+Shift+P → "Open Settings JSON")
{
  // GitHub Pull Requests
  "githubPullRequests.pullBranch": "never", // Don't auto-pull when checking out PR
  "githubPullRequests.createOnPublish": "ask", // Ask to create PR when publishing
  "githubPullRequests.defaultMergeMethod": "squash", // Default merge method
  "githubPullRequests.showInSCM": true, // Show in Source Control view

  // GitHub Issues
  "githubIssues.createInsertFormat": "number", // How to insert issue refs
  "githubIssues.queries": [ // Custom issue queries
    {
      "label": "My Issues",
      "query": "is:open assignee:${user}"
    },
    {
      "label": "Urgent Bugs",
      "query": "is:open label:bug label:urgent"
    }
  ],

  // Git Settings
  "git.autofetch": true, // Auto-fetch remote changes
  "git.confirmSync": false, // Don't confirm before sync
  "git.enableSmartCommit": true, // Auto-stage all files if none staged

  // GitLens Settings
  "gitlens.currentLine.enabled": true, // Show blame on current line
  "gitlens.hovers.currentLine.over": "line", // Show hover on entire line
  "gitlens.codeLens.enabled": true, // Show code lens above functions
  "gitlens.statusBar.enabled": true, // Show git info in status bar
}
```

### Notification Settings

```json
{
  "githubPullRequests.notifications": "all", // Get all PR notifications
  "githubIssues.queries": true, // Track issues
}
```

---

## Tips & Best Practices

### General Tips

1. **Use Command Palette Frequently** - Cmd+Shift+P is your best friend. Type what you want to do.

2. **Checkout PRs Locally** - Always test PRs on your machine before approving.

3. **Stage Selectively** - Don't stage everything at once. Review and stage related changes together.

4. **Write Clear Commit Messages** - First line brief, detailed explanation below if needed.

5. **Use Sync Changes** - Safer than separate push/pull, handles conflicts better.

6. **Reference Issues in Commits** - Use "Fixes #123" or "Closes #123" to auto-link.

7. **Review with Context** - Use GitLens to see file history before reviewing changes.

8. **Batch Review Comments** - Use "Start Review" to submit all comments at once.

### Keyboard Efficiency

```plaintext
MASTER THESE:
Cmd+Shift+P     - Access any command
Cmd+P           - Quick open file
Cmd+Shift+G     - Source Control
Cmd+K Cmd+O     - Open file on GitHub
F7              - Next change in diff

WORKFLOW:
1. Cmd+P (open file)
2. Make changes
3. Cmd+Shift+G (source control)
4. Review changes
5. Stage and commit
6. Sync
```

### PR Review Best Practices

1. **Check Small PRs** - Easier to review thoroughly
2. **Test, Don't Just Read** - Checkout and run the code
3. **Be Specific in Comments** - Point to exact lines, explain clearly
4. **Ask Questions** - Better to ask than assume
5. **Approve Thoughtfully** - Your approval means you trust the code

### Workflow Optimization

```plaintext
MORNING ROUTINE:
1. Open VS Code
2. Check GitHub view for new PRs/Issues
3. Sync your branches (fetch all)
4. Review notifications

BEFORE COMMITTING:
1. Review all changes in Source Control
2. Check you're on the right branch
3. Stage only related changes together
4. Write clear commit message
5. Sync to push

BEFORE CREATING PR:
1. Ensure all tests pass
2. Review your own changes first
3. Write descriptive title
4. Add detailed description
5. Link related issues
6. Choose reviewers wisely
```

---

## Troubleshooting

### Authentication Issues

**Problem:** "Not authenticated with GitHub"

```plaintext
Solution:
1. Press Cmd+Shift+P
2. Type: "GitHub: Sign Out"
3. Sign out completely
4. Type: "GitHub: Sign In"
5. Re-authenticate in browser
```

### PRs Not Showing

**Problem:** Can't see any PRs in GitHub view

```plaintext
Solution:
1. Check you're signed in (Accounts icon)
2. Click refresh icon in GitHub view
3. Press Cmd+Shift+P → "GitHub Pull Requests: Configure Remotes"
4. Ensure correct repository is selected
```

### Checkout Failed

**Problem:** Can't checkout PR locally

```plaintext
Solution:
1. Ensure you have no uncommitted changes
   - Commit or stash your changes first
2. Ensure correct branch permissions
3. Try: Press Cmd+Shift+P → "Git: Fetch"
4. Then retry checkout
```

### Sync Conflicts

**Problem:** "Cannot sync, you have conflicts"

```plaintext
Solution:
1. Open Source Control view
2. Files with conflicts marked with ⚠️
3. Click each conflicted file
4. Resolve conflicts (accept changes)
5. Stage resolved files
6. Commit the merge
7. Now you can sync
```

### Extension Not Working

**Problem:** GitHub extension not functioning

```plaintext
Solution:
1. Check extension is enabled:
   - Click Extensions icon
   - Search "GitHub Pull Requests"
   - Should say "Enabled"
2. Reload VS Code:
   - Cmd+Shift+P → "Developer: Reload Window"
3. Check for updates:
   - Extensions → Update available
4. Reinstall if needed:
   - Uninstall → Restart → Reinstall
```

### Performance Issues

**Problem:** VS Code slow with GitHub extension

```plaintext
Solution:
1. Reduce query frequency:
   - Settings → Search "githubPullRequests"
   - Increase "Pull Request: Background Refresh Interval"
2. Disable GitLens features:
   - Settings → Search "gitlens"
   - Disable "Current Line Blame" if not needed
3. Close unused repositories:
   - File → Close Folder
   - Only work on one repo at a time
```

---

## Quick Reference Card

### Essential Commands (Cmd+Shift+P)

```plaintext
PULL REQUESTS:
- GitHub Pull Requests: Create Pull Request
- GitHub Pull Requests: Checkout Pull Request
- GitHub Pull Requests: Review Changes

ISSUES:
- GitHub Issues: Create Issue
- GitHub Issues: Create Issue from Selection

GIT:
- Git: Clone
- Git: Create Branch
- Git: Checkout to...
- Git: Push
- Git: Pull
- Git: Sync

GITLENS:
- GitLens: Show File History
- GitLens: Compare File Revisions
- GitLens: Open File on Remote
```

### Quick Actions

```plaintext
IN EXPLORER:
- Right-click file → "Open Changes"
- Right-click file → "Open File on GitHub"

IN EDITOR:
- Right-click line → "Copy GitHub Permalink"
- Select code → Right-click → "Create Issue from Selection"

IN SOURCE CONTROL:
- Click + to stage file
- Click - to unstage file
- Click ↻ next to file to discard changes
```

### Status Bar Info

```plaintext
Bottom Status Bar Shows:
[Branch Name] - Current git branch (click to switch)
[↓ ↑] - Incoming/outgoing commits (click to sync)
[⚠ Errors] - Workspace errors
[GitLens] - Current line git blame
```

---

## Resources & Extensions

### Official Documentation

- [GitHub Pull Requests Extension Docs](https://code.visualstudio.com/docs/editor/github)
- [GitLens Documentation](https://gitlens.amod.io/)
- [VS Code Git Tutorial](https://code.visualstudio.com/docs/editor/versioncontrol)

### Complementary Extensions

```plaintext
HIGHLY RECOMMENDED:
- GitHub Pull Requests and Issues (github.vscode-pull-request-github)
- GitLens (eamodio.gitlens)
- GitHub Actions (github.vscode-github-actions)
- GitHub Copilot (github.copilot) - If subscribed

USEFUL ADDITIONS:
- Git Graph (mhutchie.git-graph) - Visual git history
- Git History (donjayamanne.githistory) - View git log
- GitHub Repositories (github.remotehub) - Browse repos without cloning
```

### Install Extensions

```bash
# Via VS Code:
# Cmd+Shift+X → Search extension name → Install

# Via CLI:
~/.local/bin/code --install-extension github.vscode-pull-request-github
~/.local/bin/code --install-extension eamodio.gitlens
~/.local/bin/code --install-extension mhutchie.git-graph
~/.local/bin/code --install-extension github.vscode-github-actions
```

---

## Beginner's 10-Minute Quick Start

**Your first 10 minutes with GitHub in VS Code:**

### 1. Sign In (1 minute)
```plaintext
- Click Accounts icon (bottom left)
- Sign in with GitHub
- Authorize in browser
```

### 2. Clone a Repo (2 minutes)
```plaintext
- Cmd+Shift+P → "Git: Clone"
- Choose "Clone from GitHub"
- Pick a repo, choose location
```

### 3. Make a Change (2 minutes)
```plaintext
- Open a file, make small change
- Save file (Cmd+S)
```

### 4. Commit Change (3 minutes)
```plaintext
- Cmd+Shift+G (Source Control)
- Click + to stage file
- Type commit message
- Press Cmd+Enter
- Click "Sync Changes"
```

### 5. Explore GitHub View (2 minutes)
```plaintext
- Click GitHub icon in Activity Bar
- See your PRs and Issues
- Click a PR to explore details
```

**Congratulations!** You've completed your first GitHub workflow in VS Code!

---

## Cheat Sheet for Daily Use

```plaintext
┌─────────────────────────────────────────────────────────┐
│  VS CODE GITHUB DAILY CHEAT SHEET                       │
├─────────────────────────────────────────────────────────┤
│  START OF DAY                                           │
│  • Cmd+Shift+G → Check for changes                     │
│  • Click branch name → Ensure on correct branch        │
│  • Click sync (↓↑) → Get latest changes                │
│  • Click GitHub icon → Check PRs/Issues assigned       │
├─────────────────────────────────────────────────────────┤
│  MAKING CHANGES                                         │
│  • Make edits → Save (Cmd+S)                           │
│  • Cmd+Shift+G → Review changes                        │
│  • Click + → Stage files                               │
│  • Type message → Commit (Cmd+Enter)                   │
│  • Click "Sync Changes"                                │
├─────────────────────────────────────────────────────────┤
│  CREATE PR                                              │
│  • Source Control → "Create Pull Request"              │
│  • Fill title & description                            │
│  • Link issues with "Fixes #123"                       │
│  • Choose reviewers → Create                           │
├─────────────────────────────────────────────────────────┤
│  REVIEW PR                                              │
│  • GitHub view → Click PR                              │
│  • Click "Checkout" → Test locally                     │
│  • Click "Review Changes"                              │
│  • Add comments on lines                               │
│  • "Finish Review" → Approve/Request Changes           │
├─────────────────────────────────────────────────────────┤
│  CREATE ISSUE                                           │
│  • Select code → Right-click                           │
│  • "Create Issue from Selection"                       │
│  • Or: GitHub view → + icon in ISSUES                  │
├─────────────────────────────────────────────────────────┤
│  WHEN STUCK                                             │
│  • Cmd+Shift+P → Type what you want to do              │
│  • "Developer: Reload Window" to restart               │
│  • Check Output panel (View → Output) for errors       │
└─────────────────────────────────────────────────────────┘
```

---

**Remember:** The Command Palette (Cmd+Shift+P) is your superpower. When in doubt, open it and type what you want to do in plain English!
