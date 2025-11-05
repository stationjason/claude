# Claude Code: Agents, Skills & Advanced Features Guide

**What is this guide?** Learn how to supercharge Claude Code with agents (AI assistants that handle complex tasks), skills (reusable capabilities), slash commands (custom shortcuts), and MCP servers (connect Claude to external tools).

---

## Table of Contents
1. [Agents - Your AI Task Runners](#agents)
2. [Skills - Reusable Capabilities](#skills)
3. [Slash Commands - Custom Shortcuts](#slash-commands)
4. [MCP Servers - External Tool Integration](#mcp-servers)
5. [Real-World Examples](#real-world-examples)
6. [Quick Reference](#quick-reference)

---

## Agents - Your AI Task Runners

### What is an Agent?

**`Agent`** - A specialized AI assistant that Claude can launch to handle specific tasks autonomously. Think of agents as mini-Claudes that are experts in particular areas.

**Real-World Analogy:** You're a manager, and agents are your specialized employees. You (Claude) delegate tasks to them:
- "Code Reviewer Agent, check this code for bugs"
- "Explorer Agent, find all the files related to authentication"
- "Test Runner Agent, run all tests and fix failures"

### Available Agent Types

Claude Code comes with several built-in agents:

#### 1. **`general-purpose`** Agent
- **What it does:** Handles complex, multi-step tasks that require research and exploration
- **When to use:** When you need to search the codebase, understand how something works, or complete tasks that require multiple steps
- **Example tasks:**
  - "Find all API endpoints in the project"
  - "Understand how authentication works in this codebase"
  - "Search for all uses of a specific function"

#### 2. **`Explore`** Agent (Fast)
- **What it does:** Quickly explores codebases to find files, search for keywords, or answer questions about structure
- **When to use:** When you need to find something quickly in the code
- **Speed levels:** `quick`, `medium`, `very thorough`
- **Example tasks:**
  - "Find all React components in src/"
  - "Where is the login function defined?"
  - "Show me all database models"

#### 3. **`Plan`** Agent (Fast)
- **What it does:** Creates detailed plans for implementing features or solving problems
- **When to use:** Before starting complex features, to map out the approach
- **Example tasks:**
  - "Plan how to add dark mode to this app"
  - "Create a step-by-step plan for implementing user authentication"
  - "How should I refactor this code to use TypeScript?"

### How to Use Agents

#### Method 1: Claude Automatically Uses Agents
Claude will automatically launch agents when appropriate. You don't need to ask explicitly.

```
You: "Find all the places where we handle user login"

Claude: [Automatically launches Explore agent to search the codebase]
```

#### Method 2: Explicitly Request an Agent
You can specifically ask for an agent if you want:

```
You: "Use the Explore agent to find all API endpoints"
You: "Launch a general-purpose agent to research how we handle errors"
```

### Agent Examples with Code

#### Example 1: Finding Code Patterns
```
Task: "Find all files that use the useState hook"

What happens:
1. Claude launches Explore agent
2. Agent searches through project files
3. Agent returns:
   - src/components/Counter.js (line 5)
   - src/components/Form.js (line 12)
   - src/pages/Dashboard.js (line 8)
4. Claude summarizes findings for you
```

#### Example 2: Understanding Complex Code
```
Task: "How does authentication work in this project?"

What happens:
1. Claude launches general-purpose agent
2. Agent explores:
   - Looks for auth-related files
   - Reads authentication middleware
   - Checks how tokens are generated
   - Traces login flow
3. Agent compiles understanding
4. Claude explains: "Authentication uses JWT tokens. When user logs in..."
```

#### Example 3: Planning a Feature
```
Task: "I want to add email notifications. Create a plan."

What happens:
1. Claude launches Plan agent
2. Agent analyzes current codebase structure
3. Agent creates step-by-step plan:
   - Step 1: Choose email service (Sendgrid, AWS SES)
   - Step 2: Add email templates
   - Step 3: Create notification service
   - Step 4: Add triggers for notifications
   - Step 5: Test email sending
4. Claude presents plan for your approval
```

### Agent Best Practices

**✅ Good Use Cases:**
- Exploring large codebases you're unfamiliar with
- Finding all instances of a pattern across many files
- Understanding how complex features work
- Planning major features before implementation
- Researching best practices for a problem

**❌ Don't Use Agents For:**
- Simple file reads (just ask Claude to read the file)
- Single file searches (use grep/search directly)
- Tasks you can explain in one sentence
- When you already know the exact file path

---

## Skills - Reusable Capabilities

### What is a Skill?

**`Skill`** - A packaged capability that gives Claude new abilities. Like installing an app on your phone that adds new features.

**Real-World Analogy:** Skills are like power-ups in a video game. Base Claude can do a lot, but skills add specialized abilities like "PDF reading" or "Excel spreadsheet editing."

### How Skills Work

Skills are installed from the Claude Code skill marketplace and live in:
```
~/.claude/skills/
```

### Common Skill Types

While the specific skills available may vary, typical skill categories include:

1. **File Format Skills**
   - PDF reading/editing
   - Excel/CSV manipulation
   - Image processing
   - Audio/video handling

2. **Development Skills**
   - Code analysis
   - Documentation generation
   - Testing frameworks
   - Deployment tools

3. **Integration Skills**
   - API connections
   - Database tools
   - Cloud services
   - Version control helpers

### How to Use Skills

#### Checking Installed Skills
```bash
# In Claude Code, ask:
"What skills do I have installed?"

# Or check the skills directory:
ls ~/.claude/skills/
```

#### Using a Skill
Claude automatically uses skills when needed, or you can explicitly invoke them:

```
You: "Read this PDF and summarize it: document.pdf"
Claude: [Uses PDF skill to read and analyze the PDF]

You: "Convert this Excel file to JSON"
Claude: [Uses spreadsheet skill to convert]
```

### Skill Examples

#### Example 1: PDF Skill
```
What it does: Read and analyze PDF files

Usage:
You: "What's in this contract.pdf file?"

Claude uses PDF skill:
1. Opens and reads PDF
2. Extracts text and structure
3. Analyzes content
4. Responds: "This is a service agreement between..."

Without skill: Claude couldn't read PDFs at all
```

#### Example 2: Spreadsheet Skill
```
What it does: Work with Excel and CSV files

Usage:
You: "Add a new column to sales.xlsx that calculates profit margin"

Claude uses spreadsheet skill:
1. Opens Excel file
2. Reads current data
3. Adds formula column: =(Revenue-Cost)/Revenue
4. Saves updated file

Without skill: Claude could only read CSV as text
```

#### Example 3: Image Analysis Skill
```
What it does: Analyze and process images

Usage:
You: "What's in this screenshot.png?"

Claude uses image skill:
1. Loads image
2. Analyzes visual content
3. Describes: "This shows a login form with email and password fields..."

Without skill: Claude couldn't process images
```

### Creating Custom Skills (Advanced)

You can create your own skills! Skills are defined in YAML files:

```yaml
# Example: Weather skill
# Location: ~/.claude/skills/weather/skill.yaml

name: weather
description: Get current weather information
version: 1.0.0

commands:
  - name: get_weather
    description: Get weather for a location
    parameters:
      location:
        type: string
        description: City name
        required: true

implementation:
  type: script
  script: ./get_weather.sh
```

Then the implementation script:
```bash
#!/bin/bash
# ~/.claude/skills/weather/get_weather.sh

LOCATION=$1
curl "https://wttr.in/$LOCATION?format=j1"
```

Now you can ask: "What's the weather in Tokyo?" and Claude uses your skill!

---

## Slash Commands - Custom Shortcuts

### What is a Slash Command?

**`Slash Command`** - Custom shortcuts you create to automate common tasks. Like keyboard shortcuts, but for AI instructions.

**Real-World Analogy:** Like speed dial on your phone. Instead of typing out a long request every time, you just type `/mycommand` and Claude knows exactly what to do.

### Where Slash Commands Live

Slash commands are stored in:
```
.claude/commands/
```

### Built-in Slash Commands

Common built-in commands:
- `/help` - Show help information
- `/clear` - Clear conversation history
- `/reset` - Reset session

### Creating Custom Slash Commands

Slash commands are simple markdown files that contain instructions for Claude.

#### Example 1: Code Review Command

Create file: `.claude/commands/review.md`
```markdown
You are doing a code review. Please:

1. Check for bugs and logic errors
2. Look for security vulnerabilities
3. Suggest performance improvements
4. Check code style and readability
5. Verify error handling

Be constructive and specific in your feedback.
```

**Usage:**
```
You: "/review src/auth.js"

Claude: [Reads review.md instructions, then reviews the file]
"I found 3 issues in src/auth.js:
1. Line 45: Password is stored in plain text (security risk)
2. Line 67: Missing error handling for database connection
3. Line 89: Variable name 'x' is not descriptive"
```

#### Example 2: Commit Message Generator

Create file: `.claude/commands/commit.md`
```markdown
Generate a git commit message based on the current changes.

Follow conventional commits format:
- type(scope): description
- Types: feat, fix, docs, style, refactor, test, chore

Keep first line under 50 characters.
Add detailed explanation if needed.
```

**Usage:**
```
You: "/commit"

Claude: [Looks at git diff, applies commit.md rules]
"Suggested commit message:

feat(auth): add password reset functionality

- Added forgot password endpoint
- Implemented email token generation
- Created password reset form component"
```

#### Example 3: Test Generator

Create file: `.claude/commands/test.md`
```markdown
Generate unit tests for the specified file or function.

Use the testing framework already in the project.
Aim for 80%+ code coverage.
Include:
- Happy path tests
- Edge cases
- Error scenarios
- Mock external dependencies
```

**Usage:**
```
You: "/test src/utils/validation.js"

Claude: [Generates comprehensive tests for the file]
```

#### Example 4: Documentation Generator

Create file: `.claude/commands/docs.md`
```markdown
Generate documentation for the specified code.

Include:
- Function/class description
- Parameters and return values
- Usage examples
- Notes about edge cases

Use JSDoc format for JavaScript, docstrings for Python, etc.
```

**Usage:**
```
You: "/docs calculateTotal function"

Claude: [Writes detailed documentation]
```

### Slash Command Best Practices

**Good Slash Commands:**
- Repetitive tasks you do often
- Complex instructions you want consistent
- Team standards (everyone uses same `/review` command)
- Project-specific workflows

**Command Ideas:**
- `/deploy` - Run deployment checklist
- `/debug` - Help troubleshoot errors
- `/optimize` - Suggest performance improvements
- `/refactor` - Modernize old code
- `/explain` - Explain code to beginners
- `/fix` - Quick bug fix with tests

---

## MCP Servers - External Tool Integration

### What is an MCP Server?

**`MCP (Model Context Protocol) Server`** - A way to connect Claude to external tools, databases, APIs, and services. It's like giving Claude superpowers to interact with the outside world.

**Real-World Analogy:** MCP servers are like plugins for Claude. Just like browser extensions add features to your browser, MCP servers add capabilities to Claude.

### What Can MCP Servers Do?

Examples of MCP server capabilities:
- Connect to databases (PostgreSQL, MySQL, MongoDB)
- Access APIs (GitHub, Slack, Google Calendar)
- Read cloud storage (AWS S3, Google Drive)
- Query analytics (Google Analytics, Mixpanel)
- Control smart home devices
- Fetch real-time data (weather, stock prices)

### MCP Server Structure

MCP servers run as separate processes that Claude communicates with:

```
You → Claude Code → MCP Server → External Service
                ↓                      ↓
           Response ← ← ← ← ← ← ← ← ←
```

### Installing MCP Servers

MCP servers are configured in Claude's settings file:
```
~/.claude/config.json
```

Example configuration:
```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_TOKEN": "your_token_here"
      }
    },
    "postgres": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres"],
      "env": {
        "DATABASE_URL": "postgresql://localhost/mydb"
      }
    }
  }
}
```

### MCP Server Examples

#### Example 1: GitHub MCP Server

**What it does:** Connect Claude to GitHub repositories

**Setup:**
```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_TOKEN": "ghp_your_token"
      }
    }
  }
}
```

**Usage:**
```
You: "List all open issues in my repositories"

Claude (using GitHub MCP):
- Connects to GitHub API via MCP server
- Fetches all repos you have access to
- Gets open issues from each
- Formats and presents the list

You: "Create a new issue in repo 'myproject' about the login bug"

Claude: [Creates issue via MCP server]
"Created issue #47: 'Fix login bug' in myproject"
```

#### Example 2: Database MCP Server

**What it does:** Query and modify databases directly

**Setup:**
```json
{
  "mcpServers": {
    "database": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres"],
      "env": {
        "DATABASE_URL": "postgresql://user:pass@localhost:5432/mydb"
      }
    }
  }
}
```

**Usage:**
```
You: "How many users are in the database?"

Claude (using Database MCP):
- Executes: SELECT COUNT(*) FROM users
- Returns: "There are 1,247 users in the database"

You: "Show me users who signed up this week"

Claude:
- Writes query: SELECT * FROM users WHERE created_at > NOW() - INTERVAL '7 days'
- Executes via MCP
- Formats results into readable table
```

#### Example 3: Slack MCP Server

**What it does:** Read and send Slack messages

**Setup:**
```json
{
  "mcpServers": {
    "slack": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-slack"],
      "env": {
        "SLACK_TOKEN": "xoxb-your-token"
      }
    }
  }
}
```

**Usage:**
```
You: "What were the last 10 messages in #engineering channel?"

Claude (using Slack MCP):
[Fetches and displays recent messages]

You: "Send a message to #general: 'Deployment complete!'"

Claude: [Sends message via MCP]
"Message sent to #general"
```

#### Example 4: File System MCP Server

**What it does:** Access files outside the project directory

**Setup:**
```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem"],
      "env": {
        "ALLOWED_DIRECTORIES": "/Users/you/Documents,/Users/you/Downloads"
      }
    }
  }
}
```

**Usage:**
```
You: "Find all PDFs in my Documents folder"

Claude (using Filesystem MCP):
[Searches allowed directories]
"Found 15 PDFs:
- /Users/you/Documents/contract.pdf
- /Users/you/Documents/resume.pdf
..."
```

### Creating Custom MCP Servers (Advanced)

You can build your own MCP servers! Here's a simple example:

**Simple Weather MCP Server (Node.js):**
```javascript
// weather-mcp-server.js
const { MCPServer } = require('@modelcontextprotocol/sdk');

const server = new MCPServer({
  name: 'weather',
  version: '1.0.0'
});

// Define a tool
server.addTool({
  name: 'get_weather',
  description: 'Get current weather for a location',
  parameters: {
    type: 'object',
    properties: {
      location: {
        type: 'string',
        description: 'City name'
      }
    }
  },
  handler: async (params) => {
    const { location } = params;
    // Call weather API
    const response = await fetch(`https://api.weather.com/v1/current?q=${location}`);
    const data = await response.json();
    return {
      temperature: data.temp,
      conditions: data.conditions,
      humidity: data.humidity
    };
  }
});

server.start();
```

**Configure in Claude:**
```json
{
  "mcpServers": {
    "weather": {
      "command": "node",
      "args": ["/path/to/weather-mcp-server.js"]
    }
  }
}
```

**Use it:**
```
You: "What's the weather in Paris?"

Claude: [Uses your custom MCP server]
"Paris is currently 18°C with partly cloudy skies and 65% humidity"
```

---

## Real-World Examples

### Scenario 1: Building a Feature with Multiple Tools

**Task:** Add a payment system to your web app

**How Claude Uses Different Features:**

```
You: "I want to add Stripe payments to my e-commerce site"

1. PLAN AGENT launches:
   - Analyzes current codebase structure
   - Creates implementation plan
   - Identifies files that need changes

2. EXPLORE AGENT searches:
   - Finds existing payment-related code
   - Locates API route files
   - Identifies database models

3. SKILLS used:
   - Documentation skill reads Stripe API docs
   - Code generation skill creates payment components

4. SLASH COMMAND:
   You: "/test payment functions"
   - Generates test cases for payment flow

5. MCP SERVER (if configured):
   - Tests Stripe API connection
   - Validates API keys
   - Checks webhook endpoints

Result: Complete payment integration with tests and documentation
```

### Scenario 2: Debugging Production Issue

**Task:** Find and fix a bug causing login failures

**Workflow:**

```
You: "Users can't log in, error says 'Invalid token'"

1. EXPLORE AGENT investigates:
   - Searches for "Invalid token" in codebase
   - Finds token validation logic
   - Traces authentication flow

2. MCP DATABASE SERVER:
   - Checks recent login attempts in database
   - Finds pattern: tokens expiring too quickly

3. You: "/review auth/tokenHandler.js"
   SLASH COMMAND executes:
   - Reviews token generation code
   - Finds bug: expiration set to 10 seconds instead of 10 hours

4. Claude fixes:
   - Changes expiration time
   - Adds unit tests
   - Updates documentation

5. You: "/commit"
   SLASH COMMAND generates:
   - Proper commit message: "fix(auth): correct token expiration time"
```

### Scenario 3: Onboarding to New Codebase

**Task:** Understand a large unfamiliar project

**Workflow:**

```
You: "I'm new to this codebase. Give me an overview."

1. EXPLORE AGENT (thorough mode):
   - Maps entire project structure
   - Identifies key files and folders
   - Finds entry points and main flows

2. GENERAL-PURPOSE AGENT:
   - Reads README and documentation
   - Analyzes package.json / dependencies
   - Understands tech stack

3. You ask specific questions:
   "How does the user registration work?"
   - Agent traces registration flow
   - Shows: Form → API → Validation → Database → Email

4. You: "/docs userService.js"
   SLASH COMMAND:
   - Generates comprehensive docs for unclear code

5. MCP GITHUB SERVER:
   - Fetches recent PRs to understand recent changes
   - Shows commit history for context

Result: Comprehensive understanding of project in minutes vs. hours
```

### Scenario 4: Automating Repetitive Tasks

**Task:** Create consistent code structure across team

**Setup Custom Tools:**

```bash
# 1. Create slash command for new React components
# .claude/commands/component.md

Create a new React component with this structure:

- Create folder: src/components/[ComponentName]
- Create files:
  - index.js (component code)
  - styles.css (component styles)
  - [ComponentName].test.js (tests)
  - README.md (usage docs)

Use functional components with hooks.
Include PropTypes.
Add basic tests.

# 2. Create slash command for API endpoints
# .claude/commands/api.md

Create a new API endpoint with this structure:

- Add route to routes/api.js
- Create controller in controllers/
- Add validation middleware
- Create tests in tests/api/
- Update API documentation

Follow RESTful conventions.
Include error handling.
```

**Usage:**

```
You: "/component UserProfile"

Claude:
1. Creates src/components/UserProfile/
2. Generates boilerplate code following team standards
3. Adds tests
4. Creates documentation

You: "/api POST /users/avatar"

Claude:
1. Adds route to express router
2. Creates avatarController.js
3. Adds validation for file upload
4. Generates tests
5. Updates API docs
```

---

## Quick Reference

### When to Use What?

| Task | Use This | Example |
|------|----------|---------|
| Find code across many files | **Explore Agent** | "Find all database queries" |
| Understand complex system | **General-Purpose Agent** | "How does auth work?" |
| Plan a big feature | **Plan Agent** | "Plan user roles feature" |
| Read special file formats | **Skills** | "Summarize this PDF" |
| Repeat common tasks | **Slash Commands** | "/review" or "/test" |
| Connect external services | **MCP Servers** | Query database, GitHub API |
| Simple task in one file | **Just Ask Claude** | "Fix this bug in auth.js" |

### Command Syntax Quick Guide

```bash
# Agents (usually automatic, but you can request)
"Use the Explore agent to find all React components"
"Launch a plan agent to design this feature"

# Skills (automatic when needed)
"Read this PDF: document.pdf"
"Convert Excel to JSON"

# Slash Commands (manual trigger)
/review src/app.js
/test components/Button
/commit
/docs myFunction

# MCP Servers (automatic when configured)
"Check GitHub issues in my repo"
"Query the database for user count"
"What's on my Google Calendar today?"
```

### File Locations Cheat Sheet

```bash
# Skills
~/.claude/skills/
~/.claude/skills/[skill-name]/skill.yaml

# Slash Commands
.claude/commands/
.claude/commands/[command-name].md

# MCP Servers Configuration
~/.claude/config.json

# Check what you have
ls ~/.claude/skills/           # Your installed skills
ls .claude/commands/            # Your custom commands
cat ~/.claude/config.json       # Your MCP servers
```

### Creating Your First Custom Tool

**Easiest Start: Slash Command**

```bash
# 1. Create commands directory in your project
mkdir -p .claude/commands

# 2. Create a simple command
cat > .claude/commands/hello.md << 'EOF'
Say "Hello! This is my first custom command!"
Then explain what you can help with.
EOF

# 3. Use it
# In Claude Code: "/hello"
```

**Next Step: Custom MCP Server**

```bash
# 1. Create simple MCP server (example: calculator)
npm init -y
npm install @modelcontextprotocol/sdk

# 2. Create server.js
# (See MCP Server section for code example)

# 3. Add to ~/.claude/config.json
# (See MCP Server configuration examples)

# 4. Restart Claude Code

# 5. Use it
# "Calculate 123 * 456 using the calculator tool"
```

---

## Tips & Best Practices

### For Agents:
✅ Let Claude decide when to use agents (usually automatic)
✅ Be specific about what you're looking for
✅ Use "thorough" mode for complex searches
❌ Don't request agents for simple tasks
❌ Don't launch multiple agents for the same task

### For Skills:
✅ Install skills you'll use frequently
✅ Keep skills updated
✅ Check skill documentation for capabilities
❌ Don't install redundant skills
❌ Don't assume skills are installed (check first)

### For Slash Commands:
✅ Create commands for repetitive tasks
✅ Use descriptive command names
✅ Include clear instructions in command files
✅ Share useful commands with your team
❌ Don't make commands too specific to one situation
❌ Don't create commands for things you rarely do

### For MCP Servers:
✅ Use official MCP servers when available
✅ Secure API tokens in environment variables
✅ Limit file system access to needed directories only
✅ Test MCP servers before relying on them
❌ Don't expose sensitive credentials in config
❌ Don't give unlimited access to external services
❌ Don't skip error handling

---

## Troubleshooting

### "Agent failed to complete task"
- Task might be too vague (be more specific)
- Codebase might be too large (narrow the scope)
- Try breaking into smaller tasks

### "Skill not found"
```bash
# Check installed skills
ls ~/.claude/skills/

# Reinstall skill if needed
claude install-skill [skill-name]
```

### "Slash command not working"
```bash
# Check command exists
ls .claude/commands/

# Verify file has .md extension
# Check file contents are valid markdown
```

### "MCP server connection failed"
```bash
# Check config file syntax
cat ~/.claude/config.json | jq .

# Test MCP server manually
node path/to/mcp-server.js

# Check environment variables are set
echo $API_TOKEN

# Restart Claude Code
```

---

## Learning Path

**Beginner:**
1. Start with slash commands (easiest to create)
2. Let Claude automatically use agents
3. Install basic skills (PDF, spreadsheet)

**Intermediate:**
4. Create custom slash commands for your workflow
5. Explicitly request specific agents
6. Install MCP servers for services you use

**Advanced:**
7. Build custom skills
8. Create custom MCP servers
9. Combine all features in complex workflows

---

**Remember:** These features make Claude Code more powerful, but you don't need to use them all at once. Start simple, add complexity as needed!

**Need Help?** Ask Claude:
- "Show me what agents are available"
- "What skills do I have installed?"
- "List my custom slash commands"
- "Help me create a slash command for [task]"
