# ui-cloner

A Claude Code skill that analyzes UI screenshots and generates a reusable `.skill` file capturing the product's complete design system.

## What It Does

Give it screenshots of any product's UI — it extracts the full design language and packages it as a self-contained skill that anyone can use to reproduce the same UI in any tech stack.

## Installation

Copy `ui-cloner.skill` to your Claude Code skills directory:

```bash
# Project-local (recommended)
cp ui-cloner.skill .claude/skills/

# Or global
cp ui-cloner.skill ~/.claude/skills/
```

## Usage

Trigger phrases:

- \"Clone this UI\" + screenshot path(s)
- \"Copy this design\" + image directory
- \"Extract the design system from these screenshots\"
- \"Reproduce this page\"

Example:

```
Clone this UI from my screenshots: ./designs/dashboard.png ./designs/settings.png
Product name: acme-app
```

## What Gets Generated

For each run, the skill produces a `{product-name}-ui/` directory saved **inside your project** (`.claude/skills/`) by default, containing:

```
{product-name}-ui/
├── SKILL.md              # Main design system skill
└── references/
    ├── design-tokens.md  # Colors, typography, spacing, radius, shadows
    ├── components.md     # Component inventory with specs and variants
    ├── layout.md         # Page layouts, grid systems, navigation structure
    └── style-guide.md    # Visual style, interaction patterns, UX principles
```

Plus a packaged `{product-name}-ui.skill` file ready to install and share.

## Analysis Dimensions

All 5 dimensions are analyzed for every screenshot:

| Dimension | What's Extracted |
|---|---|
| Design Tokens | Colors (full palette), typography scale, spacing grid, border radius, shadows |
| Components | All UI components with variants, states, sizes, and anatomy |
| Layout Structure | Page layouts, grid system, navigation patterns, responsive breakpoints |
| Visual Style | Style category (glassmorphism/minimalism/etc.), iconography, illustration style |
| Interaction Patterns | Inferred hover/focus/loading states, animation style, feedback patterns |

## Visual Verification (Optional)

After generating the skill, you'll be asked:

> \"Would you like me to generate a sample page and compare it visually against your original screenshots?\"

If you agree, the skill will:
1. Generate a sample page using `ui-ux-pro-max`
2. Diff it against your original screenshot using visual AI comparison
3. Auto-correct any critical discrepancies in the spec files
4. Repeat until no critical differences remain

## Workflow

```
Screenshots → Analyze (×N pages) → Synthesize Design System
    → Generate skill files → Package .skill → [Visual Verify & Correct]
    → Ready to use with any tech stack
```

## Using the Generated Skill

Once installed, the generated `{product-name}-ui` skill can be used in any conversation:

```
\"Use the acme-app-ui skill to build the login page in React + Tailwind\"
\"Add a settings page that matches the acme-app-ui design system\"
\"Build a dashboard using Next.js following the acme-app-ui style\"
```

Tech stack is never locked into the skill — specify it at usage time.

## Requirements

- Claude Code with `mcp__zai-mcp-server` MCP server (for visual analysis and diffing)
- `ui-ux-pro-max` skill installed (optional, for code generation and visual verification)
- `skill-creator` skill installed (for packaging)

## File Structure

```
ui-cloner/
├── SKILL.md                        # Main skill — workflow and instructions
├── ui-cloner.skill                 # Packaged skill file
└── references/
    ├── analysis-guide.md           # Per-dimension extraction instructions
    └── skill-template.md           # Templates for generated skill files
```
