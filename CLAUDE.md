# AIVerify website

Static HTML site for useaiverify.app. Six pages, each with its own inline
`<style>` block. Shared color system lives in `theme.css`.

## Color system (canonical)

All colors go through the CSS custom properties in `theme.css`. No hardcoded
hex or rgba values in page styles, inline styles, or SVG attributes. If a
new color is needed, add a variable to `theme.css` first.

| Role | Variable | Code | Contrast on bg |
|---|---|---|---|
| Accent (ice cyan) | `--accent` | `#5fb9c9` | 8.7:1 |
| Accent hover | `--accent-hover` | `#79c6d4` | 10.2:1 |
| Accent tint, backgrounds | `--accent-tint` | `rgba(95,185,201,0.12)` | — |
| Accent border | `--accent-border` | `rgba(95,185,201,0.3)` | — |
| Text on accent buttons and badges | `--on-accent` | `#0a2127` | 7.4:1 on accent |
| Flagged as AI (dusty rose) | `--verdict-ai` | `#cf5a68` | 5.0:1 |
| Uncertain / manipulated (amber) | `--verdict-uncertain` | `#e08a3c` | 7.4:1 |
| Clear / human (sage) | `--verdict-human` | `#6aae7c` | 7.5:1 |
| Background | `--bg` | `#090a0c` | — |
| Surface, cards and nav | `--surface` | `#0f1114` | — |
| Border | `--border` | `#1f2328` | — |
| Border strong / hover | `--border-strong` | `#2b3138` | — |
| Text | `--text` | `#e6eaec` | 16.4:1 |
| Muted text | `--text-muted` | `#98a2a8` | 7.6:1 |
| Faint text (smallest readable) | `--text-faint` | `#79838b` | 5.1:1 |
| Disabled / decorative only | `--text-disabled` | `#4a525a` | 2.5:1 |

```css
:root {
  --bg: #090a0c;
  --surface: #0f1114;
  --border: #1f2328;
  --border-strong: #2b3138;
  --text: #e6eaec;
  --text-muted: #98a2a8;
  --text-faint: #79838b;      /* smallest readable text */
  --text-disabled: #4a525a;   /* disabled states and decoration only, never content */
  --accent: #5fb9c9;
  --accent-hover: #79c6d4;
  --accent-tint: rgba(95, 185, 201, 0.12);
  --accent-border: rgba(95, 185, 201, 0.3);
  --on-accent: #0a2127;
  --verdict-ai: #cf5a68;
  --verdict-uncertain: #e08a3c;
  --verdict-human: #6aae7c;
}
```

`theme.css` also defines derived values (verdict tints and borders, nav
backdrop, shadows, mockup window-chrome dots). Use those rather than
re-deriving them.

## Rules

### Verdict badges
- Background is the verdict color at 12% alpha, border at 35% alpha. Use the
  `--verdict-*-tint` and `--verdict-*-border` variables.
- Every verdict always shows icon + word, never color alone:
  cross "AI-generated", question mark "Uncertain", check "Human".
- Use the shared `.verdict` component from `theme.css`:

```html
<span class="verdict ai">
  <svg class="verdict-icon" viewBox="0 0 24 24"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg>
  AI-generated
</span>
<span class="verdict uncertain">
  <svg class="verdict-icon" viewBox="0 0 24 24"><path d="M9 9a3 3 0 1 1 4 2.8c-.7.4-1 1-1 1.7V15"/><line x1="12" y1="19" x2="12" y2="19"/></svg>
  Uncertain
</span>
<span class="verdict human">
  <svg class="verdict-icon" viewBox="0 0 24 24"><polyline points="20 6 9 17 4 12"/></svg>
  Human
</span>
```

### Text on accent
- Any element filled with `--accent` (primary buttons, the pricing badge)
  uses `--on-accent` for its text. Never white.
- Hover on accent-filled elements changes the fill to `--accent-hover`,
  not opacity.

### Faint vs disabled
- `--text-faint` is the minimum for readable text: footer text, notes,
  captions, mockup labels.
- `--text-disabled` is for disabled states and decoration only: inactive
  plan features and their cross icons, decorative marks. Never for content
  the reader needs to read.
