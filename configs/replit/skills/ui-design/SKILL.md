---
name: ui-design
description: Designs and reviews app interfaces so they look intentionally designed rather than generic AI-generated, covering typography, colour, spacing, layout, components, states, copy, and motion. Use when building or restyling any screen, landing page, dashboard, or component, or when the user says an app looks generic, templated, or "vibe coded".
compatibility: Designed for Replit Agent. Works with any web UI stack.
metadata:
  version: "1.0"
---

# UI Design

## Scope

Use this skill before writing any UI and again before calling it done. It sets a design direction, then holds the build to it. It complements `frontend-accessibility` (WCAG compliance); this skill covers visual and interaction quality.

"Vibe coded" UI is what you get when every choice is the first default: the same gradient, the same rounded cards, the same emoji icons, the same copy. The fix is to make deliberate choices and apply them consistently, not to add decoration.

## Step 1: Set a design direction before any code

Write down, in a few lines (put them in `DESIGN.md` at the project root so later changes stay consistent):

1. **Who uses it and what they do most.** The primary task decides the layout, not the template.
2. **Tone.** Pick one or two: calm, dense and technical, editorial, playful, institutional. A finance tool and a kids' app should not look alike.
3. **One reference.** Name a real product or publication whose feel is close. Borrow principles, not pixels.
4. **Tokens.** Fonts, a colour palette, a spacing scale and a radius. Define them once (CSS variables or the theme file) and use only those.

If the user has a brand, logo, colours or screenshots, use them and skip invention. If they don't, ask one question about tone, or choose and say what you chose.

## Step 2: Apply the rules

### Typography
- Use at most two typefaces: one for headings (optional) and one for body. Load them properly and set weights deliberately.
- Don't default to the system sans for a finished product when a specific font would fit the tone.
- Build a type scale (for example 12, 14, 16, 20, 24, 32, 48) and stick to it. Body text is 16px or larger, with line height around 1.5, and line length of 60 to 75 characters.
- Create hierarchy with size and weight before colour. A page should read correctly in greyscale.

### Colour
- One accent colour, used for the primary action and key state. Neutrals do the rest.
- Build neutrals with a slight tint toward the brand hue, not pure grey or pure black on pure white.
- Avoid the default look: purple-to-blue or pink gradients, glowing orbs, neon on dark, and gradient text. Use a gradient only if the brand needs it.
- Reserve red, amber and green for status. Don't rely on colour alone to convey it.
- Check contrast: 4.5:1 for body text, 3:1 for large text and UI boundaries.

### Spacing and layout
- Use a spacing scale on a 4 or 8px base. Group related items closely and separate groups generously. Spacing communicates structure.
- Align to a grid. Left-align text by default; centre only short headings and hero copy.
- Don't centre everything or stack identical full-width sections. Vary rhythm with density, asymmetry and different section shapes.
- Design the real content widths. Cap reading width and don't stretch forms or tables to the full viewport.
- Make it responsive: check at roughly 360, 768 and 1280px wide.

### Components
- Don't wrap everything in a card with a border, shadow and rounded corners. Use whitespace, dividers or background shifts to group, and cards only for independent items.
- Pick one radius (or two) and one shadow style for the whole app. Keep shadows subtle.
- One primary button per view. Secondary actions look quieter. Destructive actions look distinct and ask for confirmation.
- Use an icon set consistently (for example Lucide or Phosphor). **Never use emoji as icons or bullets**, and don't add an icon to every heading or list item.
- Use real components for real jobs: a table for tabular data, a form with labels above inputs, a date picker for dates.

### States (where generic UI usually breaks)
Design all of these, not just the happy path:
- **Empty:** say what belongs here and offer the next action.
- **Loading:** use skeletons that match the layout; avoid layout shift.
- **Error:** say what happened and how to fix it, next to the thing that failed.
- **Disabled, hover, focus, active:** all visible. Never remove the focus outline without replacing it.
- **Long content:** long names, large numbers, many items, and no items.
- **Success:** confirm quietly, without a modal.

### Copy
- Write specific, plain labels: "Save changes", not "Submit". "Create invoice", not "Get started".
- Cut filler: "Seamless", "powerful", "revolutionary", "unlock", "elevate", "supercharge", "all-in-one". Say what the product does.
- Don't invent testimonials, logos, statistics or "trusted by" claims. Use real content or clearly marked placeholders.
- Use realistic sample data (varied names, uneven numbers), not "John Doe", "Lorem ipsum" or round figures.
- Sentence case for UI text. Avoid exclamation marks and emoji in product copy.

### Motion
- Motion explains a change (something appeared, moved or finished). It isn't decoration.
- Keep transitions to 150 to 250ms with ease-out. Animate opacity and transform only.
- No bouncing, floating, pulsing or looping effects on static content. Honour `prefers-reduced-motion`.

### Page types
- **Landing page:** lead with what it is and who it's for in the first screen, with one clear call to action. Show the product itself (a real screenshot or live demo), not abstract shapes. Skip the stock sequence of hero, three feature cards, testimonials, pricing and footer unless the content calls for it.
- **Dashboard or tool:** density is a feature. Put the most-used controls and data first, support keyboard use, and let tables sort, filter and paginate.
- **Forms:** one column, labels above fields, inline validation, clear required marking, a submit button that names the action.

## Step 3: Review before finishing

1. Work through [references/checklist.md](references/checklist.md).
2. Run the app and look at it. Check at three widths, in each state, and with real-length content. If you can't view the result, say so rather than claiming it looks right.
3. Squint test: blur the page. Is the main action and the hierarchy still clear?
4. Fix issues, then report what you changed and what you did not check.

## What to avoid doing

- Don't add features, pages or sections the user didn't ask for to make it look fuller.
- Don't restyle parts of an existing app that the user didn't mention, unless asked. Match the established design system instead.
- Don't add a new UI library when the project already has one.
