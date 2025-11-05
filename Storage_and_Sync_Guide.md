# Storage & Sync Guide for Claude Code

**The Big Question:** Where does everything live, and how do I keep it synced across multiple computers?

---

## Quick Answer: What Works Where

| Feature | Claude Code CLI | Web GUI (claude.ai) | Storage Location |
|---------|----------------|---------------------|------------------|
| **Agents** | ✅ Built-in | ❌ Not available | No storage (built into Claude Code) |
| **Skills** | ✅ Yes | ❌ Not available | `~/.claude/skills/` (per computer) |
| **Slash Commands** | ✅ Yes | ❌ Not available | `.claude/commands/` (per project) |
| **MCP Servers** | ✅ Yes | ❌ Not available | `~/.claude/config.json` (per computer) |

**Important:** Agents, Skills, Slash Commands, and MCP Servers are **Claude Code CLI features only**. They don't work in the web GUI at claude.ai.

---

## Storage Locations Explained

### 1. **Agents** - No Storage Needed! ✨

**Where:** Built into Claude Code itself
**Storage:** None - they're part of Claude Code
**Sync:** Automatic (updates with Claude Code)

```
YOU DON'T NEED TO STORE ANYTHING!

Agents are built-in features that Claude automatically uses.
When you update Claude Code, you get the latest agents.
```

**What this means:**
- Nothing to back up
- Nothing to sync
- Works the same on every computer with Claude Code installed
- Just update Claude Code to get new agent features

---

### 2. **Skills** - Global (Per Computer) 🌍

**Where:** `~/.claude/skills/` (your home directory)
**Storage:** Per computer (global settings)
**Sync:** Manual (need to sync yourself)

```
Computer 1:                Computer 2:
~/.claude/skills/          ~/.claude/skills/
├── pdf/                   ├── pdf/
├── excel/                 └── weather/
└── weather/

↑ Different on each computer unless you sync them!
```

**File Structure:**
```
~/.claude/skills/
└── my-skill-name/
    ├── skill.yaml          # Skill definition
    ├── implementation.sh   # Code that runs
    └── README.md          # Documentation
```

**How to Sync Skills Across Computers:**

**Option A: Manual Copy (Simple)**
```bash
# On Computer 1 - Package your skills
cd ~/.claude/skills/
tar -czf my-skills.tar.gz *

# Copy my-skills.tar.gz to Computer 2 (USB, cloud, email)

# On Computer 2 - Install skills
cd ~/.claude/skills/
tar -xzf my-skills.tar.gz
```

**Option B: Git Repository (Better for teams)**
```bash
# On Computer 1 - Create skills repo
cd ~/.claude/skills/
git init
git add .
git commit -m "My Claude skills"
git remote add origin https://github.com/yourusername/claude-skills.git
git push -u origin main

# On Computer 2 - Clone skills
cd ~/.claude/
rm -rf skills/  # Remove default skills folder
git clone https://github.com/yourusername/claude-skills.git skills/
```

**Option C: Symlink to Cloud Storage (Advanced)**
```bash
# Move skills to Dropbox/Google Drive
mv ~/.claude/skills ~/Dropbox/claude-skills

# Create symlink
ln -s ~/Dropbox/claude-skills ~/.claude/skills

# Now skills sync automatically via Dropbox on all computers!
```

---

### 3. **Slash Commands** - Per Project 📁

**Where:** `.claude/commands/` (in each project folder)
**Storage:** Inside your project (committed to git)
**Sync:** Automatic via git!

```
your-project/
├── .claude/
│   └── commands/
│       ├── review.md       # Code review command
│       ├── test.md         # Test generator
│       └── commit.md       # Commit message helper
├── src/
└── README.md

↑ These travel WITH your project via git!
```

**File Structure:**
```
.claude/commands/
├── mycommand.md           # Simple command
├── another-command.md     # Another command
└── README.md              # Optional: explain your commands
```

**How Slash Commands Sync (Automatically!):**

```bash
# Computer 1 - Create command and push
mkdir -p .claude/commands
cat > .claude/commands/review.md << 'EOF'
Review this code for bugs and improvements.
EOF

git add .claude/
git commit -m "Add code review slash command"
git push

# Computer 2 - Get command automatically
git pull

# Now /review works on Computer 2!
```

**✅ Best Practice: Commit slash commands to git**
```bash
# Make sure .claude/ is NOT in .gitignore
git add .claude/commands/
git commit -m "Add project-specific commands"
```

**Why this is awesome:**
- Commands are version controlled
- Team members get same commands
- Commands travel with the project
- Different projects can have different commands

---

### 4. **MCP Servers** - Global (Per Computer) 🔌

**Where:** `~/.claude/config.json` (your home directory)
**Storage:** Per computer (global settings)
**Sync:** Manual (contains secrets, be careful!)

```
~/.claude/config.json

{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_TOKEN": "ghp_your_secret_token"  ⚠️ SECRET!
      }
    }
  }
}
```

**⚠️ WARNING: Contains API Keys and Secrets!**

Do NOT directly sync this file unless you know what you're doing.

**How to Sync MCP Servers Across Computers:**

**Option A: Template Config (Recommended)**
```bash
# Create a template WITHOUT secrets
# my-mcp-template.json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_TOKEN": "${GITHUB_TOKEN}"  # Placeholder
      }
    },
    "database": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres"],
      "env": {
        "DATABASE_URL": "${DATABASE_URL}"  # Placeholder
      }
    }
  }
}

# Store template in git (safe - no secrets)
git add my-mcp-template.json

# On each computer, manually set secrets:
export GITHUB_TOKEN="your-actual-token"
export DATABASE_URL="your-actual-db-url"

# Then copy template to config
cp my-mcp-template.json ~/.claude/config.json
```

**Option B: Separate Secrets File (Advanced)**
```bash
# ~/.claude/config.json (can be synced)
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "envFile": "~/.claude/secrets.env"  # Load from separate file
    }
  }
}

# ~/.claude/secrets.env (NEVER sync this!)
GITHUB_TOKEN=ghp_your_secret_token
DATABASE_URL=postgresql://...

# Add to .gitignore globally
echo "secrets.env" >> ~/.gitignore_global
```

**Option C: Environment Variables (Best for secrets)**
```bash
# Add to ~/.zshrc or ~/.bashrc on each computer
export GITHUB_TOKEN="your-token"
export DATABASE_URL="your-db-url"

# Config file references environment variables
{
  "mcpServers": {
    "github": {
      "env": {
        "GITHUB_TOKEN": "$GITHUB_TOKEN"  # Uses environment variable
      }
    }
  }
}
```

---

## Recommended Storage Strategy

### For Individual Use (You on Multiple Computers)

```
├── Cloud Storage (Dropbox/Google Drive)
│   └── claude-global/
│       ├── skills/              → Symlink to ~/.claude/skills/
│       └── mcp-template.json    → Template for ~/.claude/config.json
│
└── Git Repositories (GitHub)
    ├── project-1/
    │   └── .claude/commands/    ✅ Committed to git
    ├── project-2/
    │   └── .claude/commands/    ✅ Committed to git
    └── shared-commands/         Optional: shared commands repo
        └── commands/
```

**Setup Steps:**

```bash
# 1. Set up cloud-synced skills
mkdir -p ~/Dropbox/claude-global/skills
ln -s ~/Dropbox/claude-global/skills ~/.claude/skills

# 2. Create MCP template (without secrets)
cp ~/.claude/config.json ~/Dropbox/claude-global/mcp-template.json
# Edit mcp-template.json to remove actual tokens

# 3. For each project, commit .claude/commands/
cd your-project
git add .claude/commands/
git commit -m "Add project commands"

# 4. Set environment variables on each computer
echo 'export GITHUB_TOKEN="your-token"' >> ~/.zshrc
```

---

### For Team Use (Multiple People)

```
Git Repositories:
├── company-claude-skills/       # Shared skills
│   └── skills/
│       ├── company-api/
│       ├── deploy/
│       └── review/
│
└── your-projects/
    ├── project-a/
    │   └── .claude/commands/    # Project-specific commands
    │       ├── deploy.md        # Unique to this project
    │       └── test.md
    └── project-b/
        └── .claude/commands/
```

**Team Setup:**

```bash
# 1. Each person clones company skills
git clone https://github.com/company/claude-skills.git ~/.claude/skills

# 2. Each person sets their own secrets
# (Don't share tokens! Everyone has their own)
export GITHUB_TOKEN="your-personal-token"

# 3. Projects have shared commands (in git)
cd your-project
git pull  # Gets team's commands automatically

# 4. Update skills when team adds new ones
cd ~/.claude/skills
git pull
```

---

## File Location Summary

### What's Global (Per Computer):

```bash
~/.claude/
├── config.json          # MCP servers config (contains secrets!)
├── skills/              # Skills folder (can sync)
└── cache/               # Claude's cache (don't sync)

# On Mac/Linux: ~/.claude/
# On Windows: %USERPROFILE%\.claude\
```

### What's Per Project:

```bash
your-project/
├── .claude/
│   └── commands/        # Slash commands (commit to git!)
├── src/
└── README.md
```

---

## Syncing Checklist

### Setting Up New Computer:

```bash
# ✅ Step 1: Install Claude Code
# (Agents come automatically)

# ✅ Step 2: Set up Skills (if you have custom ones)
cd ~/.claude/
git clone https://github.com/yourusername/claude-skills.git skills/
# OR: Copy from cloud storage

# ✅ Step 3: Set up MCP Servers
cp ~/your-backup/mcp-template.json ~/.claude/config.json
# Then add your API keys/secrets

# ✅ Step 4: Clone your projects
git clone https://github.com/yourusername/your-project.git
cd your-project
# Slash commands come with the project automatically!

# ✅ Step 5: Set environment variables (for MCP secrets)
echo 'export GITHUB_TOKEN="your-token"' >> ~/.zshrc
echo 'export DATABASE_URL="your-db"' >> ~/.zshrc
source ~/.zshrc
```

---

## Quick Commands to Check Your Setup

```bash
# Where are my skills?
ls ~/.claude/skills/

# Where is my MCP config?
cat ~/.claude/config.json

# What slash commands does this project have?
ls .claude/commands/

# Check if everything is working
claude --version                    # Claude Code installed?
ls ~/.claude/skills/                # Skills present?
cat ~/.claude/config.json | jq .    # MCP config valid?
ls .claude/commands/*.md            # Project commands present?
```

---

## Best Practices Summary

### ✅ DO:

- **Commit `.claude/commands/` to git** (travels with project)
- **Back up skills folder** to cloud or git
- **Use environment variables for secrets** (in MCP config)
- **Create MCP config templates** (without actual tokens)
- **Document your custom commands** (so you remember what they do)

### ❌ DON'T:

- **Don't commit API tokens to git** (use environment variables)
- **Don't sync `~/.claude/cache/`** (it's just temporary data)
- **Don't share your config.json directly** (contains secrets)
- **Don't forget to gitignore secrets.env** (if you use that approach)

---

## TL;DR - Simple Strategy

**For most people, this is all you need:**

1. **Agents:** Built-in, nothing to do ✅
2. **Skills:** Rare to customize, use defaults ✅
3. **Slash Commands:** Commit to git with your project ✅
4. **MCP Servers:** Set up once per computer manually ✅

**On new computer:**
```bash
# Install Claude Code
# Clone your projects (git pull gets commands automatically)
# Set your API keys as environment variables
# Done!
```

---

## Need Help?

**Check your current setup:**
```
Ask Claude: "Show me my current storage setup"
```

**See what you have:**
```bash
# Skills
ls -la ~/.claude/skills/

# Commands in current project
ls -la .claude/commands/

# MCP config
cat ~/.claude/config.json
```

**Start fresh:**
```bash
# Back up first!
cp -r ~/.claude/ ~/claude-backup/

# Then reset
rm -rf ~/.claude/
# Claude Code will recreate defaults
```

---

**Remember:** Most users only need to commit `.claude/commands/` to git for their projects. Skills and MCP servers are advanced features you may never need!
