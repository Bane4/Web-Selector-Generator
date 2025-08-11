# README.md

## Selector Generator — Scored v2 (Non-Breaking)

Single-file web app that turns pasted HTML into **stable, minimal selectors** for Playwright, Cypress, React Testing Library, and WebdriverIO. Render your HTML, **click an element**, and copy the **Best**, **CSS**, or **XPath** selector.

---

## Features
- Render → **Click element** → get selectors instantly
- Scoring model prefers: `data-testid` → stable `#id` → **role+name** → **aria** → CSS path
- Penalizes brittle patterns (`:nth-child`, utility classes, long chains)
- Per-framework formatting (Playwright/Cypress/RTL/WDIO)
- Top alternatives with scores + reasons
- Copy buttons, bigger preview, clear pressed/hover states on buttons

---

## Quick Start
1. Open `SelectorGeneratorApp.html` in a modern browser (no build step).
2. Paste your HTML into the textarea.
3. Click **Render**.
4. In the preview, **click the exact element** you want a selector for.
5. Read **Best Selector**. Toggle options if needed.
6. Switch **Framework**/**Language** to reformat, then **Copy**.

---

## Options

| Option | Effect | When to use |
|---|---|---|
| **Avoid dynamic/utility classes** | Ignores hashy/Tailwind/Bootstrap-like classes | Default on for stability |
| **Prefer text (Playwright only)** | Adds `:has-text("…")` using accessible name | Buttons/links with reliable labels |
| **CSS full path to `<body>`** | Forces deeper chain from page root | Only if uniqueness requires ancestry |

---

## How It Chooses “Best”

**Signals (+):**
- `data-testid` (+40)
- Unique non-random `#id` (+30)
- Role + accessible name (+28)
- `aria-*` attributes (+18)
- `js-` / `qa-` classes (+14)
- Uniqueness in DOM (+8)

**Penalties (–):**
- `:nth-child` / structural index (–25)
- Utility classes (e.g., Tailwind/Bootstrap) (–12)
- XPath (–15)
- Numeric/long text (–10)
- Multiple matches (–8)
- Excess length (small)

---

## Tips
- Prefer adding `data-testid` to critical elements.
- Role+name is great for a11y and readability.
- Use **Full path** only when uniqueness requires it.

---

## Development
- Everything lives in one HTML file; works offline

---
### Summary
Adopts a scoring model to output **stable, minimal selectors**; adds click-to-select preview, clearer guidance, larger fonts, lighter accent color, button press states, and bigger preview window. Maintains existing outputs (Best/CSS/XPath) and framework formatting.

### What Changed
- **Scoring model**: prefers `data-testid` → `#id` → role+name → aria → CSS; penalizes brittle patterns
- **Alternates panel**: top 5 candidates with scores + reasons
- **Playwright XPath fix**: `page.locator("xpath=…")`
- **“Full path” toggle**: truly forces chain from `<body>`
- **Render → click** preview flow (element highlight)
- **Quick Start & Features** section (clear instructions)
- **Readability**: larger base font sizes; clearer hints/status text
- **Color**: lighter accent blue
- **Buttons**: hover + pressed feedback (shade + 1px dip)
- **Preview**: increased default height

### Why
- Reduce flaky selectors and review churn
- Make the workflow obvious (render → click → copy)
- Fix Playwright XPath runtime issue
- Improve accessibility and usability

### Testing Notes
- Verify on latest Chrome/Edge/Firefox:
  - **Best Selector** resolves to exactly one element
  - **Prefer text** only affects Playwright outputs
  - **Full path** increases CSS depth as expected
  - Playwright XPath uses `page.locator("xpath=…")`
  - Buttons show visual pressed state on `:active`
  - Preview area is larger

### Backward Compatibility
- **No breaking changes**: same three outputs; same framework/language menus
- Old behavior can be mimicked by copying CSS/XPath directly if desired

### Risks & Mitigations
- Over-reliance on text selectors → gated to Playwright + short accessible names
- Long CSS chains → length/utility penalties push toward stable attributes

### Rollback Plan
- Revert to previous commit or bypass scoring by emitting CSS output as “Best.”
