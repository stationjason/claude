# Web App Prompt Template for Claude

**How to use this template:** Copy the template below, fill in your specific details, and give it to Claude. The more specific you are, the better results you'll get!

---

## Complete Prompt Template (Copy This!)

```
I want you to build a [TYPE OF WEB APP] called "[APP NAME]".

## Project Overview
[Describe what your app does in 2-3 sentences. Be clear about the main purpose.]

Example:
This is a task management app that helps users track their daily to-dos.
Users can create, edit, and delete tasks, mark them as complete, and organize
them by categories. It should be simple and easy to use.


## Target Users
[Who will use this? Beginners? Professionals? Kids? This helps Claude make
appropriate design decisions.]

Example:
- Primary users: Busy professionals who need quick task tracking
- Secondary users: Students managing homework assignments
- Should be usable by anyone with basic computer skills


## Technical Stack
[Tell Claude what technologies to use. If you don't know, just say "use modern
best practices" or specify what you're familiar with.]

**Frontend:**
- [Framework: React, Vue, vanilla JavaScript, etc.]
- [Styling: CSS, Tailwind, Bootstrap, etc.]
- [Any specific libraries you want]

**Backend:**
- [Node.js, Python/Flask, PHP, etc. OR say "no backend needed"]
- [Database: PostgreSQL, MongoDB, SQLite, or "none"]

**Deployment/Hosting:**
- [Where will this run? Local only? Deploy to Vercel/Netlify? Or "not sure yet"]

Example:
Frontend: React with Tailwind CSS for styling
Backend: Node.js with Express (simple REST API)
Database: SQLite (keep it simple, local file storage)
Hosting: I want to run it locally for now, but make it easy to deploy later


## Core Features (Must-Have)
[List the essential features your app MUST have. Number them for clarity.]

Example:
1. User can add a new task with title and description
2. User can mark tasks as complete/incomplete
3. User can delete tasks
4. Tasks are saved so they persist when page refreshes
5. User can filter tasks by: All, Active, Completed
6. Display task count (e.g., "5 tasks remaining")


## Nice-to-Have Features (Optional)
[Features you want if there's time, but not critical for first version.]

Example:
1. Ability to set due dates on tasks
2. Color-code tasks by priority (high, medium, low)
3. Search/filter tasks by keyword
4. Export tasks to a text file
5. Dark mode toggle


## Design Preferences
[Describe how you want it to look. Include examples if possible.]

**Style:**
- [Modern, minimal, playful, professional, etc.]
- [Color scheme preferences]
- [Any specific design inspiration?]

**Layout:**
- [Single page? Multiple pages? Sidebar navigation?]
- [Mobile-friendly? Desktop-only?]

Example:
Style: Clean and minimal, inspired by Apple's design language
Colors: Use a blue color scheme (primary: #3B82F6, background: white/light gray)
Layout: Single page app with sidebar for categories and main area for task list
Mobile: Must be fully responsive and work well on phones


## User Flow
[Describe step-by-step how a user will interact with your app. This is VERY
helpful for Claude to understand your vision.]

Example:
1. User opens the app and sees a list of existing tasks (or empty state if first time)
2. User clicks "Add Task" button at the top
3. A form appears with fields for: task title (required), description (optional), category dropdown
4. User fills out form and clicks "Save"
5. New task appears at the top of the list
6. User can click checkbox next to task to mark it complete (adds strikethrough)
7. User can click trash icon to delete a task (shows confirmation dialog)
8. User can use filter buttons at the top to view: All, Active, or Completed tasks


## File Structure
[If you have preferences about how files should be organized. Optional - Claude
can decide if you don't specify.]

Example:
project/
├── frontend/
│   ├── src/
│   │   ├── components/     # Reusable UI components
│   │   ├── pages/          # Main page components
│   │   ├── utils/          # Helper functions
│   │   └── App.js          # Main app component
│   └── public/
├── backend/
│   ├── routes/             # API endpoints
│   ├── models/             # Database models
│   └── server.js           # Main server file
└── README.md


## Specific Requirements/Constraints
[Any technical requirements, limitations, or preferences Claude should know about.]

Example:
- I'm running on an older Mac, so keep dependencies lightweight
- I prefer functional React components (not class components)
- Add clear comments in the code so I can learn from it
- Use semantic HTML for accessibility
- No authentication needed for v1 - single user app
- Data should persist in local storage (or database if using backend)


## What I Need From You
[Tell Claude exactly what deliverables you want.]

Example:
1. Complete source code for frontend and backend
2. README file with:
   - How to install dependencies
   - How to run the app locally
   - Brief explanation of the project structure
3. Comments in code explaining key functions
4. Basic error handling (e.g., form validation, empty states)
5. Instructions for how to add new features later


## Things to Avoid
[Optional: Specify what you DON'T want.]

Example:
- Don't use TypeScript (I'm not familiar with it yet)
- Don't add user authentication yet (save for v2)
- Don't use complicated state management libraries (keep it simple)
- Avoid external APIs or paid services


## Success Criteria
[How will you know if the app is successful? What should it accomplish?]

Example:
The app is successful if:
1. I can add, complete, and delete tasks without errors
2. My tasks are still there when I close and reopen the browser
3. The app looks good on both desktop and mobile
4. Someone with no coding knowledge could use it easily
5. The code is clean enough that I can modify it later


## Questions for Claude
[If you're unsure about anything, ask Claude for recommendations.]

Example:
- What's the best database choice for this project given my requirements?
- Should I use a framework or vanilla JavaScript for something this simple?
- Do I need a backend at all, or can this work with just frontend + local storage?
- What's the easiest way to deploy this once it's done?

```

---

## Example: Complete Filled-Out Prompt

Here's what a complete prompt looks like:

```
I want you to build a recipe organizer web app called "My Recipe Box".

## Project Overview
This is a personal recipe management app where users can save their favorite
recipes, organize them by category (breakfast, lunch, dinner, desserts), and
search through them easily. It's like a digital recipe box that replaces the
old paper recipe cards.

## Target Users
- Home cooks who want to digitize their recipe collection
- Should be simple enough for non-technical users (like my mom!)
- Age range: 30-70 years old

## Technical Stack
Frontend: React with Tailwind CSS
Backend: Node.js with Express
Database: MongoDB (I want to learn it)
Hosting: Deploy to Vercel (frontend) and Render (backend)

## Core Features (Must-Have)
1. Add a new recipe with: title, ingredients list, instructions, prep time, cook time, servings
2. View all recipes in a card/grid layout with photo placeholder
3. Click on recipe card to view full recipe details
4. Edit existing recipes
5. Delete recipes (with confirmation)
6. Organize recipes by category (Breakfast, Lunch, Dinner, Desserts, Snacks)
7. Search recipes by name or ingredient
8. Recipes persist in database

## Nice-to-Have Features (Optional)
1. Upload recipe photos
2. Print recipe in a clean format
3. Mark recipes as favorites
4. Add tags (e.g., "quick", "vegetarian", "kid-friendly")
5. Share recipe via unique link
6. Import recipe from URL (scrape website)

## Design Preferences
Style: Warm and inviting, like a cozy kitchen. Think Pinterest aesthetic.
Colors: Warm oranges/yellows for accents, cream/beige backgrounds, brown for text
Layout:
- Homepage: Grid of recipe cards (3 per row on desktop, 1 on mobile)
- Recipe detail: Clean, readable layout with large text for instructions
- Sidebar with category filters
Mobile: Must work perfectly on phones since people use them in the kitchen

## User Flow
1. User lands on homepage showing all recipes in grid layout
2. User clicks "Add Recipe" button in top right
3. Form opens with fields for all recipe details
4. User fills out form (title and ingredients are required, rest optional)
5. User clicks Save - recipe card appears in grid
6. User clicks on any recipe card to view full details
7. On detail page, user sees Edit and Delete buttons
8. User can click category filters in sidebar to show only recipes in that category
9. User can type in search bar to filter recipes in real-time

## File Structure
Keep it organized but simple:
- frontend/ (React app)
- backend/ (Express API)
- Separate README for each

## Specific Requirements/Constraints
- Add lots of comments - I'm still learning React
- Use functional components with hooks
- Make forms accessible (proper labels, keyboard navigation)
- Handle empty states (e.g., "No recipes yet! Add your first recipe")
- Validate forms (don't let users save recipe without a title)
- Show loading states when fetching from API
- Graceful error handling (show user-friendly error messages)

## What I Need From You
1. Complete working code
2. Clear README with setup instructions
3. Example seed data (5-10 sample recipes) so I can test it
4. Comments explaining the code structure
5. List of npm packages used and why

## Things to Avoid
- No user authentication (just one user - me)
- Don't use TypeScript yet
- Keep external dependencies minimal
- No complicated build setups

## Success Criteria
Success means:
1. I can add my mom's 50+ recipes and easily find them later
2. The app is fast and doesn't lag
3. It looks professional enough to show off to friends
4. My non-technical family could use it if I shared it
5. Code is clean enough for me to add features later

## Questions for Claude
- Should I use MongoDB Atlas (cloud) or local MongoDB?
- What's the best way to structure the ingredients list (array vs. text field)?
- Any recommendations for making this more maintainable?
```

---

## Quick Tips for Writing Good Prompts

### ✅ DO:
- **Be specific** - "I want a blue button" is better than "make it look nice"
- **Give examples** - Show Claude similar apps you like
- **Explain WHY** - "I want dark mode because users will use this at night"
- **Mention your skill level** - "I'm a beginner, please add comments"
- **Prioritize features** - Separate "must-have" from "nice-to-have"

### ❌ DON'T:
- Be vague - "Make it look good" doesn't help
- Assume Claude knows your preferences - be explicit
- Skip the user flow - Claude needs to understand how users interact with your app
- Forget about constraints - mention OS, budget, hosting limitations
- Request everything at once - start with core features, iterate later

---

## Template Variations for Different Project Types

### Simple Single-Page App (No Backend)
```
I want a [TYPE] app that runs entirely in the browser.

Stack: HTML, CSS, JavaScript (or React if you prefer)
Data Storage: Browser's localStorage
Hosting: I'll open the HTML file locally (or use GitHub Pages)

Features:
[List your features...]
```

### API-Only Backend (No Frontend)
```
I want to build a REST API for [PURPOSE].

Stack: Node.js + Express + PostgreSQL
No frontend needed - I'll test with Postman

Endpoints needed:
- GET /api/items - list all items
- POST /api/items - create item
- PUT /api/items/:id - update item
- DELETE /api/items/:id - delete item

[More details...]
```

### Full-Stack with Authentication
```
I want a full-stack [TYPE] app with user accounts.

Users should be able to:
- Sign up with email and password
- Log in and log out
- Each user sees only their own data

Stack: [Your choices]
Auth: Use JWT or sessions (your recommendation?)

[More details...]
```

---

## Before You Start: Checklist

Before giving your prompt to Claude, make sure you've answered:

- [ ] What does my app DO? (Can I explain it in one sentence?)
- [ ] Who is it FOR? (Target audience)
- [ ] What are the 3-5 CORE features? (Must-haves)
- [ ] What should it LOOK like? (Design direction)
- [ ] What tech should it USE? (Or should Claude decide?)
- [ ] Where will it RUN? (Local? Deployed? What OS?)
- [ ] How will users INTERACT with it? (Step-by-step flow)
- [ ] What is my SKILL level? (So Claude can adjust complexity)

---

## After Claude Builds Your App

### What to Do Next:
1. **Test everything** - Try to break it! Click all buttons, try invalid inputs
2. **Read the code** - Understand what Claude built
3. **Ask questions** - "Why did you use X instead of Y?"
4. **Request improvements** - "Can you add error handling for Z?"
5. **Iterate** - "Now add feature X from my nice-to-have list"

### Good Follow-Up Prompts:
- "Add comments explaining the X function"
- "The button should be bigger - make it 200px wide"
- "Add a loading spinner when data is fetching"
- "Can you refactor this to be more efficient?"
- "Add error handling for when the API fails"
- "Make the mobile version look better"

---

## Real-World Example Prompts

### Example 1: Learning Project
```
I want to build a simple calculator app to practice JavaScript.

I'm a beginner learning web development. Please build a basic calculator that:
- Has buttons for numbers 0-9 and operators (+, -, ×, ÷)
- Shows the current calculation in a display area
- Has equals button to show result
- Has clear button to reset

Stack: Pure HTML, CSS, JavaScript (no frameworks - I want to learn basics)
Design: Make it look like an iPhone calculator
What I need: Lots of comments explaining how JavaScript handles the calculations

Please keep it simple and educational!
```

### Example 2: Business Tool
```
I want to build an invoice generator for my freelance business.

I need to create professional invoices quickly. The app should:
- Let me input client info, my info, and line items (description, quantity, price)
- Calculate totals automatically
- Generate a PDF I can email to clients
- Save invoice data so I can reference it later

Stack: React frontend, Node.js backend, SQLite database
Design: Professional and clean - black text on white background
Hosting: I'll run locally on my Mac

Must be fast and reliable - I use this for real clients!
```

### Example 3: Fun Side Project
```
I want to build a "mood tracker" app just for fun.

Users can log their mood each day by clicking an emoji (😊 😐 😢 😡 😴).
Show a calendar view of the month with the mood emoji on each day.
Display simple stats like "You were happy 60% of this month!"

Stack: Whatever you think is easiest and most fun to build
Design: Colorful and playful
Storage: Local storage is fine

This is just for me to learn and experiment. Feel free to suggest cool features!
```

---

**Remember:** The better your prompt, the better Claude's result. Spend time on the prompt - it's worth it!

---

## Need Help?

If you're stuck, try this starter prompt:

```
I want to build a web app but I'm not sure how to describe it. Let me tell you
what I want it to do, and can you ask me clarifying questions to help me build
a better prompt?

Here's my basic idea: [Your rough idea]
```

Claude will ask you the right questions to help you flesh out your idea!
