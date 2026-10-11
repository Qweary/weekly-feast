# weekly-feast

A zero-dependency, single-file meal planning terminal that tracks your pantry and generates AI-powered weekly meal plans optimized for grocery store sales. Works offline, runs in any browser, no accounts or installation required. Designed for use with [Claude](https://claude.ai).

## What It Does

weekly-feast is a local-first meal planning system built around a simple loop: you tell it what's in your kitchen, it generates a prompt for Claude, Claude searches for the best grocery deals this week and matches them to recipes, and the result flows back into the app as a structured meal plan with a store-optimized shopping list.

The system tracks your pantry inventory across three tiers (shelf-stable staples, weekly perishables, and bulk items with partial quantities), manages dietary preferences and allergies, and carries your kitchen state forward week to week so the weekly update takes under two minutes. The Claude prompt is engineered to search real-time grocery ads from QFC, Kroger, Safeway, and Walmart, find matching recipes from preferred scratch-cooking sites, sequence meals by ingredient perishability, and maximize ingredient overlap across the week to minimize waste and cost.

## Getting Started

1. Download `weekly-feast.html`
2. Double-click the file to open it in your browser
3. That's it — there is no step 3

The app runs entirely in your browser from a single HTML file. No server, no build tools, no frameworks, no accounts, no internet connection required for the app itself. Your data is stored in your browser's localStorage and persists across sessions.

### Generating Your First Meal Plan

When you open the app for the first time, you'll see a default pantry and set of preferences. The recommended workflow is to go to Preferences first and set your household size, region, allergies, and dietary preferences. Then go to Pantry and adjust the default items to reflect what you actually have on hand. Run through the Weekly Review (a guided three-step flow that takes about two minutes) to confirm your pantry state. Hit Generate Prompt, copy the output, and paste it into a conversation with Claude at [claude.ai](https://claude.ai). Claude will search for current grocery deals, find matching recipes, and return a structured JSON meal plan. Copy Claude's response, go to the Import tab in the app, paste it in, and click Parse Response. The meal plan and shopping list appear on your dashboard.

### Using the Shopping List on Your Phone

The app works on mobile browsers — open the HTML file on any phone and the layout adapts with a bottom navigation bar and the shopping list displayed first. For the simplest mobile experience, use the Export List button on the dashboard, which copies a clean plain-text shopping list to your clipboard. Paste it into any notes app, text it to yourself, or share it however you prefer.

## Upgrading to a New Version

Your pantry, preferences, and plans are saved in your web browser, not inside the `weekly-feast.html` file. A newly downloaded copy is a new file, and depending on your browser it may or may not show your existing data on its own. The steps below work either way.

Do steps 1 and 2 in your **old** copy, before you move, rename, replace, or delete it.

1. **Make a backup.** Open your current copy and go to **Prefs** (the gear icon). Near the bottom, in the **Data Management** box, click **Export All Data**. You will see "Backup exported!" and a file named like `weekly-feast-backup-2026-10-10.json` will download (very old copies name it `meal-planner-backup-...json`). Note where your browser saved it, usually your Downloads folder.
2. **Copy your Special Instructions, if you use them.** Go to **Prompt** and copy the text in the **Special Instructions (optional)** box into a note or an email to yourself. Backups from many versions of the app leave this text out, so copy it by hand. If that text mentions an allergy, also add the allergy in the new copy under **Prefs**, in the **Allergies (Hard Exclusions)** box, because every backup keeps that box.
3. **Download the new version.** Download the new `weekly-feast.html` from this page and open it in the same browser you used before.
4. **Check whether your data is already there.** Look for something you added yourself: a pantry item you typed in, or your **Region** under **Prefs** (a fresh copy says "Your city, ST"). Every new copy starts with a sample pantry, so a pantry full of items does not prove it is yours.
5. **If your own data is there, do not import.** You are done. Go to **Prompt**, and if the **Special Instructions (optional)** box is empty, paste your text back in. Then skip to step 8.
6. **If you see the sample data, import your backup before you change anything.** Go to **Prefs**, and in the **Data Management** box click **Import Data**, then choose the backup file from step 1. Use this button, not the **Import** tab in the menu, which is for pasting Claude's meal plan. Importing replaces everything in the new copy, so anything you add there first will be lost.
7. **Confirm.** The app asks "This will replace ALL current data (pantry, preferences, plans, history) with the backup. Continue?" Click **OK**. A message starting with "Data restored" means it worked. Then go to **Prompt**, and if the **Special Instructions (optional)** box is empty, paste your text back in.
8. **Stop using the old file.** Once the new copy shows your data, delete the old file and keep the backup. In some browsers both copies share the same saved data, and the old file still has older food-safety rules in its prompt. After that, leave the new file's name and folder as they are. In some browsers, renaming or moving it, even to the old file's name, makes it open different saved data.

Your backup brings back your whole pantry (all three tiers, with status, quantities, par levels, units, and opened dates), your allergies, dislikes, and likes, household settings, current plan, plan history, anchor recipes, prompt template, shopping-list check-offs, and waste log (if your old version had one). The backup is a plain text file that includes your household details and allergies, so keep it somewhere private.

**If something looks different:**

- **You see "Invalid backup: missing" or "Failed to parse backup file".** You picked the wrong file. Choose the `weekly-feast-backup-...json` file from step 1.
- **A red notice says "Your custom prompt template has out-of-date food-safety rules".** If you never edited your prompt template, this is expected: your backup carried an older built-in template. Go to **Prompt**, click **Edit Template**, then click **Reset to Default**. You will see "Template reset" and the notice goes away. If you did edit your template, follow the notice's own instructions instead.
- **Your Stores box is empty or says "Store A, Store B, Store C".** Copies from before July 2026 did not save a store list. Enter yours in **Prefs** under **Stores (priority order)**.
- **A few things reset.** The plan start date goes back to today, shopping-list rows you had hidden come back, and the first-run guide or a safety notice may show once. Dismiss them as usual.
- **You already deleted or replaced the old file without a backup.** Your data is usually still in that browser. Open the new copy and check it (step 4). In Chrome, any copy of the app opened from your computer should show your data. In Firefox, your data stays with the old file's exact name and folder: save a copy of `weekly-feast.html` under the old name in the old folder, open it, and do step 1 from there. In other browsers, the Firefox approach is worth trying.
- **You moved or renamed the file later and now your data is missing or out of date.** Some browsers tie your data to the file's exact name and folder, so a moved or renamed file can open with sample data or with your data from before the upgrade. Move or rename it back to where it was and what it was called. If that is not possible, import your latest backup (steps 6 and 7).
- **You are moving to a different browser or computer.** Do steps 1 and 2 in the old browser, open the new copy in the new browser, and go straight to steps 6 and 7.
- **You use a phone or tablet.** The same steps apply. It is not known whether a new copy on a phone or tablet picks up your data on its own, so always make the backup first.

<sub>Why this is needed: the app keeps your data in your browser's storage, and browsers handle files opened from your computer differently. Some share the data with every copy of the app, others keep it tied to one exact file name and folder, and none of this is guaranteed to stay the same. A backup file works in every case.</sub>

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

Your data lives in your browser's localStorage. The Preferences screen includes Export All Data (downloads a JSON backup file) and Import Data (restores from a backup file) buttons. Use these to back up regularly, transfer your data to a different browser or computer, or recover from an accidental data loss. The backup file is a standard JSON file that includes your pantry, preferences, household config, current plan, plan history, prompt template, anchor recipes, shopping-list check-offs, waste log, and Special Instructions. Backups made by older copies of the app leave out the Special Instructions, so when you move to a new copy of the app, follow [Upgrading to a New Version](#upgrading-to-a-new-version).

### Meal Plan Intelligence

When Claude generates a plan, it sequences meals by perishability (fresh produce meals early in the week, pantry-heavy and freezer-friendly meals later), flags pantry items at risk of depletion (if the plan uses rice in four of seven dinners and your pantry says "well-stocked," it warns you), distinguishes between simple breakfasts/lunches and involved dinners, and notes when it's making quality-over-cost tradeoffs. The plan includes a confidence indicator — "normal" when at least two stores have confirmed ad data, "low" when pricing is mostly estimated.

## Project Structure

```
weekly-feast/
├── weekly-feast.html    ← the entire application
├── README.md
└── LICENSE
```

There is intentionally only one file that matters. The app is self-contained by design.

## Data Storage

All data is stored in your browser's localStorage under keys prefixed with `mp:`. The storage footprint is small — a typical setup with a full pantry, preferences, and 52 weeks of plan history uses well under 1 MB. If you want to start fresh, you can clear your browser's localStorage for the file's origin, or use the Import Data feature with a clean backup.

Note that localStorage is per-browser and per-origin. If you open the file in Chrome and then later open it in Firefox, they will have separate data stores. Use the export/import feature to transfer between browsers. To move to a newly downloaded copy of the file, see [Upgrading to a New Version](#upgrading-to-a-new-version).

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
