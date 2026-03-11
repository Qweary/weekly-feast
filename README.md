# weekly-feast

A zero-dependency, single-file meal planning terminal that tracks your pantry and generates AI-powered weekly meal plans optimized for grocery store sales. Works offline, runs in any browser, no accounts or installation required. Designed for use with [Claude](https://claude.ai).

## What It Does

weekly-feast is a local-first meal planning system built around a simple loop: you tell it what's in your kitchen, it generates a prompt for Claude, Claude searches for the best grocery deals this week and matches them to recipes, and the result flows back into the app as a structured meal plan with a store-optimized shopping list.

The system tracks your pantry inventory across three tiers (shelf-stable staples, weekly perishables, and bulk items with partial quantities), manages dietary preferences and allergies, and carries your kitchen state forward week to week so the weekly update takes under two minutes. The Claude prompt is engineered to search real-time grocery ads from QFC, Kroger, Safeway, and Walmart, find matching recipes from preferred scratch-cooking sites, sequence meals by ingredient perishability, and maximize ingredient overlap across the week to minimize waste and cost.

## Getting Started

1. Download 'weekly-feast.html`
2. Double-click the file to open it in your browser
3. That's it — there is no step 3

The app runs entirely in your browser from a single HTML file. No server, no build tools, no frameworks, no accounts, no internet connection required for the app itself. Your data is stored in your browser's localStorage and persists across sessions.

### Generating Your First Meal Plan

When you open the app for the first time, you'll see a default pantry and set of preferences. The recommended workflow is to go to Preferences first and set your household size, region, allergies, and dietary preferences. Then go to Pantry and adjust the default items to reflect what you actually have on hand. Run through the Weekly Review (a guided three-step flow that takes about two minutes) to confirm your pantry state. Hit Generate Prompt, copy the output, and paste it into a conversation with Claude at [claude.ai](https://claude.ai). Claude will search for current grocery deals, find matching recipes, and return a structured JSON meal plan. Copy Claude's response, go to Import Response in the app, paste it in, and hit Parse. The meal plan and shopping list appear on your dashboard.

### Using the Shopping List on Your Phone

The app works on mobile browsers — open the HTML file on any phone and the layout adapts with a bottom navigation bar and the shopping list displayed first. For the simplest mobile experience, use the Export List button on the dashboard, which copies a clean plain-text shopping list to your clipboard. Paste it into any notes app, text it to yourself, or share it however you prefer.

## How It Works

The system has two components that interact through structured text.

The first is the local terminal (this HTML file), which owns all persistent state: your pantry, preferences, household configuration, meal plan history, and the Claude prompt template. It doesn't connect to the internet or send data anywhere.

The second is a Claude prompt template embedded in the app. When you click Generate Prompt, the terminal serializes your current state into a detailed, optimized prompt that instructs Claude to search for current weekly grocery ads (using a three-tier search hierarchy: deal aggregator sites first, then store landing pages, then interactive circulars as a fallback), find matching recipes from preferred scratch-cooking sites (dynamically, using site-targeted search queries), cross-reference sale items against your pantry and recipes to build a perishability-sequenced meal plan, and return everything as structured JSON that the terminal can parse and display.

The prompt template is fully editable within the app if you want to customize the search strategy, add stores, change recipe sources, or adjust how Claude prioritizes cost versus quality.

### Preferred Recipe Sources

The default prompt template directs Claude to search these sites for recipes, chosen for their emphasis on from-scratch, budget-conscious cooking:

- [Graceful Little Honey Bee](https://gracefullittlehoneybee.com) — budget homestead meals
- [Scratch Pantry](https://scratchpantry.com) — from-scratch staples and pantry maximization
- [Pantry Mama](https://pantrymama.com) — sourdough and fermentation (when a starter is active)
- [Pioneer Woman](https://thepioneerwoman.com) — hearty comfort food that scales for meal prep

Claude will search other reputable cooking sites when the preferred sources don't have a good match for a particular ingredient, and will note the substitution in its narrative summary.

### Anchor Recipes

You can configure a set of fallback "anchor recipes" — known-good URLs from the preferred sites that Claude can use when its dynamic search returns thin results for a given protein or produce category. These are managed in the Preferences screen and are meant to be curated over time as you discover which recipes consistently work well for your household.

## Features

### Pantry Management

The three-tier inventory system is designed around how people actually think about their kitchen. Tier 1 covers staples like flour, rice, oil, and spices — tracked with a simple well-stocked / getting-low / out status that you cycle with a click. Tier 2 covers weekly perishables like eggs, milk, and bread — tracked with a have / don't-have toggle that resets each week. Tier 3 covers bulk items where partial quantity matters — tracked with approximate descriptors like "about half remaining" or "almost gone."

### Weekly Review

A three-step guided flow that walks you through updating your pantry state before generating a new prompt. Step 1 asks about your bulk items (the most likely to have changed), step 2 surfaces staples flagged as getting-low or out (did you restock?), and step 3 resets your weekly perishables. The whole process is designed to take under two minutes.

### Shopping List

The dashboard displays a shopping list grouped by store, with each item showing its quantity, price (color-coded green for confirmed ad pricing, amber for estimated), category badge (sale / staple / restock), and any notes from Claude. Items can be checked off as you shop (progress persists across page reloads), removed entirely if you don't need them (with an undo option to add them back), and exported as formatted plain text for use on your phone. The cost summary updates automatically when items are removed.

### Data Backup and Portability

Your data lives in your browser's localStorage. The Preferences screen includes Export All Data (downloads a JSON backup file) and Import Data (restores from a backup file) buttons. Use these to back up regularly, transfer your data to a different browser or computer, or recover from an accidental data loss. The backup file is a standard JSON file that includes your pantry, preferences, household config, current plan, plan history, prompt template, and anchor recipes.

### Meal Plan Intelligence

When Claude generates a plan, it sequences meals by perishability (fresh produce meals early in the week, pantry-heavy and freezer-friendly meals later), flags pantry items at risk of depletion (if the plan uses rice in four of seven dinners and your pantry says "well-stocked," it warns you), distinguishes between simple breakfasts/lunches and involved dinners, and notes when it's making quality-over-cost tradeoffs. The plan includes a confidence indicator — "normal" when at least two stores have confirmed ad data, "low" when pricing is mostly estimated.

## Project Structure

```
weekly-feast/
├── meal-planner.html    ← the entire application
└── README.md
```

There is intentionally only one file that matters. The app is self-contained by design.

## Data Storage

All data is stored in your browser's localStorage under keys prefixed with `mp:`. The storage footprint is small — a typical setup with a full pantry, preferences, and 52 weeks of plan history uses well under 1 MB. If you want to start fresh, you can clear your browser's localStorage for the file's origin, or use the Import Data feature with a clean backup.

Note that localStorage is per-browser and per-origin. If you open the file in Chrome and then later open it in Firefox, they will have separate data stores. Use the export/import feature to transfer between browsers.

## Customization

The prompt template and anchor recipes are both editable within the app. The prompt template uses `{{PLACEHOLDER}}` tokens that get filled in automatically from your current state — you can modify the instructions, search strategy, store list, or output format without touching the code. If you want to target different grocery stores, change the recipe source sites, or adjust how aggressively the system optimizes for cost versus quality, the template editor on the Generate Prompt screen is the place to do it.

If you modify the template and want to get back to the original, there's a "Reset to Default" button.

## Design Background

This system was designed through a multi-expert iterative process, with separate domain expertise applied at each stage: a meal planning and budget grocery expert defined the core architecture, search strategy, and recipe matching logic; a UX consultant reviewed and refined the interaction design, data model, and terminal-to-Claude interface contract; a prompt engineer optimized the Claude prompt template for search reliability, tool call budgeting, and structured output consistency; and a frontend developer built and iterated the application through several rounds of testing and refinement.

## Roadmap

Phase 1 (current) delivers the core loop: pantry tracking, prompt generation, plan import, and shopping list management.

Phase 2 (in progress) involves testing the prompt template against real weekly ad cycles across multiple weeks to tune search queries, calibrate the anchor recipe set, and validate JSON output reliability.

Phase 3 (planned) will add consumption and waste tracking, price trend analysis across weeks, seasonal awareness (learning which produce is cheapest at which times of year in your region), and the sourdough starter integration for Pantry Mama recipes once a starter is established.

## License

MIT
