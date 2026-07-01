# Portfolio — YuRi

> A portfolio of self-hosted technical decks, powered by Reveal.js and published through GitHub Pages.

[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-Live-brightgreen)](https://mybotagent.github.io/hermes-architecture-deck/)
[![Reveal.js](https://img.shields.io/badge/Reveal.js-5.1-blue)](https://revealjs.com/)
[![Design](https://img.shields.io/badge/Design-Apple%20inspired-000000)](https://www.apple.com)

## 🎯 What this is

A multi-deck portfolio for technical presentation work. Each deck lives in its own folder, has its own slide source, and is independently navigable.

- **No build step** — static HTML, vanilla CSS, plain Markdown
- **Keyboard-driven** — Reveal.js with `←` `→` `↑` `↓` `F` `ESC` `S`
- **Apple-inspired** — SF Pro, dark mode, single accent color, generous whitespace
- **GitHub Pages hosted** — push to `main`, served at `https://<owner>.github.io/<repo>/`

## 📁 Structure

```
hermes-architecture-deck/
├── index.html              # Portfolio homepage (this entry point)
├── decks/                  # One folder per deck
│   └── hermes-architecture/
│       ├── index.html      # Deck entry point
│       ├── slides/         # Markdown slides
│       │   ├── 00-hero.md
│       │   ├── 01-*.md
│       │   └── ...
│       ├── APPLE-DESIGN.md # Design reference (Apple system)
│       └── README.md       # Deck-specific notes
├── assets/
│   └── css/
│       ├── portfolio.css   # Homepage styling
│       └── deck.css        # Deck styling (shared)
└── README.md               # You are here
```

## 🚀 Adding a new deck

1. **Create the folder** under `decks/`
   ```bash
   mkdir -p decks/my-new-deck/slides
   ```

2. **Copy the entry point** from `decks/hermes-architecture/index.html` — adjust:
   - `<title>` and meta description
   - The `<section data-markdown="slides/XX.md">` references
   - Any deck-specific CSS imports

3. **Write slides** as Markdown files in `decks/my-new-deck/slides/`
   - Use `---` as horizontal slide separator
   - Use `----` as vertical (nested) separator
   - Available CSS classes: `.tldr`, `.flow-tree`, `.small`, `.big`, `.section-hero`

4. **Add a card to the homepage** (`index.html`) under `.deck-grid`:
   ```html
   <a class="deck-card" href="decks/my-new-deck/">
     <div class="deck-thumb">
       <span class="deck-thumb-glyph">XX</span>
       <span class="deck-thumb-label">Short tagline</span>
     </div>
     <div class="deck-body">
       <p class="deck-tag">Status</p>
       <h3 class="deck-title">Deck title</h3>
       <p class="deck-desc">One-paragraph description.</p>
       <span class="deck-cta">View deck</span>
     </div>
   </a>
   ```

5. **Push to `main`** — GitHub Pages rebuilds automatically (legacy mode).

## ⌨️ Keyboard shortcuts (in any deck)

| Key | Action |
|---|---|
| `←` `→` | Next / previous slide |
| `↑` `↓` | Vertical slide |
| `Space` | Next |
| `ESC` | Overview |
| `F` | Fullscreen |
| `S` | Speaker notes |
| `B` | Pause (black screen) |

## 🛠 Tech stack

- **[Reveal.js 5.1](https://revealjs.com/)** — slide engine (CDN)
- **[GitHub Pages](https://pages.github.com/)** — static hosting (legacy mode)
- **No build step** — edit and push
- **Apple-inspired CSS** — SF Pro stack, single accent, dark canvas

## 🎨 Design system

Each deck uses `assets/css/deck.css`, which implements an Apple-inspired dark theme:

- **Background**: pure black (`#000000`)
- **Primary accent**: `#2997ff` (Apple Blue on dark)
- **Body text**: `#ffffff` with `#86868b` for muted
- **Type**: SF Pro Display for headings, SF Pro Text for body
- **Cards**: 22px radius, subtle shadow on hover, 0.3s ease transitions
- **Sections**: 1px hairlines, generous padding, no decorative gradients

Reference the Apple design guide at `decks/hermes-architecture/APPLE-DESIGN.md` (generated via `npx getdesign@latest add apple`).

## 📜 License

MIT

## 🤖 Credits

Generated and maintained by Hermes Agent.