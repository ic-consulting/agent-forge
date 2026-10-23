# UI Design Checklist

Mark each item pass, fail, or N/A with a reason. Don't skip items silently.

## Direction
- [ ] Tone, audience and primary task are written down (`DESIGN.md`)
- [ ] Fonts, colours, spacing scale and radius are defined once and reused
- [ ] Existing brand or design system is followed where one exists

## Typography
- [ ] No more than two typefaces
- [ ] Consistent type scale; body text 16px or larger
- [ ] Hierarchy holds up in greyscale
- [ ] Line length is about 60 to 75 characters for reading text

## Colour
- [ ] One accent colour; neutrals carry the rest
- [ ] No default purple/blue gradients, glow effects or gradient text without a brand reason
- [ ] Contrast meets 4.5:1 (body) and 3:1 (large text, UI boundaries)
- [ ] Status never depends on colour alone

## Layout
- [ ] Consistent spacing scale; related items grouped
- [ ] Not everything is centred or built from identical stacked sections
- [ ] Content width is capped; works at about 360, 768 and 1280px
- [ ] No horizontal scroll or overlapping elements

## Components
- [ ] Cards used only for independent items
- [ ] One radius and one shadow style across the app
- [ ] One primary action per view
- [ ] Consistent icon set; no emoji as icons or bullets
- [ ] Correct component for each job (table, labelled form, date picker)

## States
- [ ] Empty, loading, error and success states designed
- [ ] Hover, focus, active and disabled states visible; focus outline kept
- [ ] Long text, large numbers, many items and zero items handled

## Copy and content
- [ ] Specific labels; no filler marketing words
- [ ] No invented testimonials, logos or statistics
- [ ] Realistic sample data; no lorem ipsum or "John Doe"
- [ ] Sentence case; no emoji or exclamation marks in UI copy

## Motion
- [ ] Motion has a purpose; transitions 150 to 250ms
- [ ] No decorative looping animation
- [ ] `prefers-reduced-motion` respected

## Verified
- [ ] App was run and viewed, or the report says it wasn't
