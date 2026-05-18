---
name: dev-terminal-design-system
description: Use when building developer-facing websites, landing pages, or product sites with a dark terminal/hacker aesthetic. Provides a complete design system with ink color palette, CSS variables, utility classes, animations, and component patterns inspired by helmagent.dev.
---

# Developer Terminal Design System

## Overview

A dark-first, developer/terminal-aesthetic design system for Next.js + Tailwind CSS sites. Inspired by helmagent.dev. Features monospace typography, terminal window chrome, ink grayscale palette, blue accent color, grid backgrounds, and subtle pulse/wire animations.

Core principle: **Every element is theme-aware via CSS custom properties. Dark mode is the default; light mode is a secondary variant.**

## When to Use

- Developer tools / CLI product landing pages
- Technical product sites targeting engineers
- Any site where "terminal aesthetic" or "hacker vibes" fits the brand
- When the design brief mentions: dark theme, monospace, developer-focused, minimal, technical

## Tech Stack

| Layer | Choice | Notes |
|-------|--------|-------|
| Framework | Next.js (App Router) | `"use client"` for interactive components |
| Styling | Tailwind CSS v4 | `@import "tailwindcss"` syntax |
| Theme | next-themes | `ThemeProvider` with `defaultTheme="dark"` |
| Fonts | Geist + Geist Mono | `--font-geist-sans` / `--font-geist-mono` |
| Icons | Lucide React | Consistent icon set |
| Buttons | @base-ui/react or shadcn/ui | `nativeButton={false}` when rendering as `<a>` |

## Color System

### Ink Grayscale (primary text/UI)

| Token | Hex | Usage |
|-------|-----|-------|
| `ink-950` | `#0a0b0d` | Dark page background |
| `ink-900` | `#111214` | Card/code background |
| `ink-800` | `#191a1e` | Paper/muted background |
| `ink-700` | `#222327` | Elevated surfaces |
| `ink-600` | `#2e2f34` | Borders, dividers |
| `ink-500` | `#3e3f44` | Disabled text |
| `ink-400` | `#5a5b60` | Muted/caption text |
| `ink-300` | `#8b8c91` | Secondary text |
| `ink-200` | `#b4b5ba` | Interactive text |
| `ink-100` | `#dddee3` | Primary text (dark mode) |

### Blue Accent

| Token | Hex | Usage |
|-------|-----|-------|
| `blue` | `#3b82f6` | Primary accent, links, CTAs |
| `blue-soft` | `#60a5fa` | Hover state, soft emphasis |

### Surface Tokens (theme-aware)

| CSS Variable | Light | Dark | Usage |
|-------------|-------|------|-------|
| `--background` | `#ffffff` | `#0a0b0d` | Page background |
| `--foreground` | `#0a0b0d` | `#dddee3` | Primary text |
| `--surface-code` | `#f4f4f5` | `#111214` | Code/terminal blocks |
| `--surface-paper` | `#e4e4e7` | `#191a1e` | Secondary sections |
| `--surface-card` | `#ffffff` | `#111214` | Card backgrounds |
| `--surface-2` | `#f4f4f5` | `#191a1e` | Auxiliary surfaces |
| `--border-hair` | `rgba(0,0,0,0.08)` | `rgba(255,255,255,0.06)` | Subtle borders |
| `--border-hair-strong` | `rgba(0,0,0,0.12)` | `rgba(255,255,255,0.1)` | Emphasized borders |
| `--grid-line` | `rgba(0,0,0,0.04)` | `rgba(255,255,255,0.03)` | Grid background lines |

## CSS Utility Classes

### Borders & Surfaces

```css
.hair          { border-color: var(--border-hair); }
.hair-strong   { border-color: var(--border-hair-strong); }
.code-bg       { background: var(--surface-code); }
.paper-bg      { background: var(--surface-paper); }
.card-bg       { background: var(--surface-card); }
.surface-2     { background: var(--surface-2); }
.screen-bg     { background: var(--surface-screen); }
```

### Grid Background

```css
.grid-bg {
  background-image:
    linear-gradient(var(--grid-line) 1px, transparent 1px),
    linear-gradient(90deg, var(--grid-line) 1px, transparent 1px);
  background-size: 64px 64px;
}
.grid-fade {
  mask-image: radial-gradient(ellipse 70% 60% at 50% 40%, black 30%, transparent 100%);
}
```

### Blue Accent Utilities

```css
.bg-blue       { background-color: #3b82f6; }
.text-blue     { color: #3b82f6; }
.bg-blue-soft  { background-color: #60a5fa; }
.text-blue-soft { color: #60a5fa; }
```

### Terminal Elements

```css
.term-shadow   { box-shadow: var(--term-shadow); }
.split-window  { border-radius: 12px; border: 1px solid var(--split-border); overflow: hidden; }
.sec-tag       { font-family: monospace; font-size: 12px; letter-spacing: 0.18em; text-transform: uppercase; color: var(--sec-tag-color); }
.pull-quote    { font-size: clamp(28px, 4vw, 44px); line-height: 1.1; font-weight: 600; letter-spacing: -0.025em; }
.pull-quote em { font-style: italic; color: #3b82f6; }
```

### Animations

```css
.pulse         { /* blue breathing dot, 2s cycle */ }
.caret::after  { content: '█'; animation: blink 1s step-end infinite; }
.sse-wire      { /* horizontal wire with gradient */ }
.sse-wire-v    { /* vertical wire with gradient */ }
.sse-pulse.go-right  { animation: sse-right 2.5s ease-in-out infinite; }
.sse-pulse.go-left   { animation: sse-left 2.5s ease-in-out infinite; animation-delay: 1.2s; }
.sse-pulse.go-down   { animation: sse-down 2.5s ease-in-out infinite; }
.sse-pulse.go-up     { animation: sse-up 2.5s ease-in-out infinite; animation-delay: 1.2s; }
.reveal        { opacity: 0; transform: translateY(16px); transition: opacity 0.6s, transform 0.6s; }
.reveal.in     { opacity: 1; transform: translateY(0); }
```

### Token Highlights (terminal syntax)

```css
.tk-bin  { color: var(--tk-bin-color); }   /* command/binary */
.tk-str  { color: #3b82f6; }               /* string values */
.tk-com  { color: var(--tk-com-color); }   /* comments */
.tk-flag { color: #8b8c91; }               /* flags */
.tk-num  { color: #d97706; }               /* numbers */
```

## Component Patterns

### Navbar

```tsx
<header className="sticky top-0 z-40 backdrop-blur-md bg-background/70 border-b hair">
  <nav className="mx-auto max-w-7xl px-5 sm:px-8 h-14 flex items-center gap-6">
    {/* Logo + name */}
    {/* Right: ThemeToggle + GitHub link + CTA button */}
  </nav>
</header>
```

### Section (standard)

Every section follows this pattern:

```tsx
<section className="border-b hair">
  <div className="mx-auto max-w-7xl px-5 sm:px-8 py-20 sm:py-28">
    <p className="text-[12px] font-mono uppercase tracking-[0.18em] text-ink-400">
      <span className="sec-tag">[ 01 ] Section Name</span>
    </p>
    <h2 className="mt-2 text-[34px] sm:text-[44px] leading-[1.05] tracking-[-0.025em] font-semibold text-balance text-foreground">
      标题。
    </h2>
    <p className="mt-3 text-[15px] text-ink-300 max-w-xl">描述文字</p>
    {/* Content */}
  </div>
</section>
```

### Terminal Window (Chrome)

```tsx
<div className="split-window code-bg term-shadow overflow-hidden">
  <div className="flex items-center h-8 px-3 border-b hair">
    <div className="flex items-center gap-1.5">
      <span className="w-2.5 h-2.5 rounded-full bg-[#ff5f57]" />
      <span className="w-2.5 h-2.5 rounded-full bg-[#febc2e]" />
      <span className="w-2.5 h-2.5 rounded-full bg-[#28c840]" />
    </div>
    <span className="flex-1 text-center font-mono text-ink-400 text-[11px]">title</span>
  </div>
  <div className="px-4 py-4 font-mono text-[13px] leading-[1.7] text-ink-100">
    {/* Terminal content */}
  </div>
</div>
```

### Card Grid (with gap-px borders)

```tsx
<div className="grid md:grid-cols-3 gap-px bg-border rounded-xl overflow-hidden border hair">
  {items.map((item) => (
    <article key={item.id} className="card-bg p-6 sm:p-7">
      {/* Card content */}
    </article>
  ))}
</div>
```

### Pillar Card

```tsx
<article className="card-bg p-6 sm:p-7">
  <div className="flex items-center gap-2 text-[11px] font-mono uppercase tracking-[0.16em] text-ink-400">
    <span className="text-blue">[01]</span>
    <span className="dot" />
    tag
  </div>
  <h3 className="mt-3 text-[18px] font-semibold tracking-tight text-foreground">Title</h3>
  <p className="mt-3 text-[13.5px] leading-relaxed text-ink-300">Description</p>
  <ul className="mt-5 space-y-1.5 text-[12.5px] font-mono text-ink-300">
    <li className="flex items-start gap-2">
      <span className="text-blue mt-0.5 shrink-0">→</span>
      <span>Point</span>
    </li>
  </ul>
</article>
```

### Button Conventions

```tsx
// Primary CTA (blue)
<Button className="bg-blue text-white hover:bg-blue-soft">Download</Button>

// Secondary (outline)
<Button variant="outline" className="border-border hover:bg-muted">Learn More</Button>

// Ghost icon button
<Button variant="ghost" size="icon" className="h-8 w-8 border hair hover:bg-muted text-ink-300">
  <Icon className="h-4 w-4" />
</Button>

// When rendering as <a>, add nativeButton={false}
<Button render={<a href="/download" />} nativeButton={false}>Download</Button>
```

### ImageLightbox

Use native `<dialog>` + `showModal()` instead of React conditional rendering. See `ImageLightbox.tsx` pattern: click opens dialog, click backdrop or X closes, body overflow managed manually.

### Footer

```tsx
<footer className="border-t hair">
  <div className="mx-auto max-w-7xl px-5 sm:px-8 py-14">
    <div className="grid grid-cols-2 sm:grid-cols-4 gap-10">
      {/* Logo column + link columns */}
    </div>
    <div className="mt-12 pt-6 border-t hair flex items-center justify-between text-[12px] font-mono text-ink-400">
      {/* Copyright */}
    </div>
  </div>
</footer>
```

## Page Structure Template

```
<html className="dark" defaultTheme="dark" enableSystem>
<body>
  <Navbar />           <!-- sticky, backdrop-blur, hair border -->
  <main>
    <Hero />           <!-- grid-bg, hero-glow, split layout -->
    <Why />            <!-- pull-quote, evidence chip -->
    <Features />       <!-- 3-col pillar cards, gap-px borders -->
    <TechStack />      <!-- architecture layer cake, SSE wires -->
    <Screenshots />    <!-- image gallery, lightbox -->
    <Privacy />        <!-- 3-col icon cards -->
    <Download />       <!-- terminal-style CTA -->
  </main>
  <Footer />           <!-- 4-col grid -->
</body>
</html>
```

## Site Config Structure

```ts
export const siteConfig = {
  name: "Product Name",
  description: "One-line description",
  tagline: "Short memorable tagline",
  url: "https://example.com",
  github: "https://github.com/org/repo",
  why: {
    quote: "Two-line pull quote.\nSecond line gets italic blue emphasis.",
    description: "Why this product exists.",
  },
  pillars: [
    { number: "01", tag: "tag", title: "Title。", description: "...", points: ["→ point"] },
  ],
  techStack: [{ name: "Tech", description: "Category" }],
  stats: [{ value: "~5MB", label: "Label" }],
  privacy: [{ title: "Title", description: "..." }],
  downloadLinks: { macOSArm: "...", macOSIntel: "...", windows: "..." },
} as const;
```

## Typography Scale

| Element | Size | Weight | Tracking |
|---------|------|--------|----------|
| Hero H1 | `40–58px` responsive | 600 | `-0.025em` |
| Section H2 | `34–44px` responsive | 600 | `-0.025em` |
| Subsection H3 | `17–18px` | 600 | `tight` |
| Body | `15–16.5px` | 400 | normal |
| Caption | `12.5–13.5px` | 400 | normal |
| Mono label | `11–12px` | 400 | `0.16–0.18em` |

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Hardcoded `text-white` / `text-black` | Use `text-foreground` (theme-aware) |
| Hardcoded border colors | Use `border hair` or `border hair-strong` |
| Non-monospace section tags | Use `.sec-tag` class |
| React conditional render for lightbox | Use native `<dialog>` + `showModal()` |
| Missing `nativeButton={false}` on `<a>` buttons | Add prop when `render={<a />}` |
| Forgetting `py-20 sm:py-28` section padding | Standard section vertical rhythm |
| Using gray-400/gray-500 instead of ink | Use ink palette for consistent grays |

## Quick Start

1. Copy `globals.css` from supporting files — it contains all CSS variables, utilities, and animations
2. Create `src/config/site.ts` using the config structure above
3. Set up `layout.tsx` with Geist fonts + ThemeProvider (`defaultTheme="dark"`)
4. Build sections following the component patterns — each section = `border-b hair` + `max-w-7xl` container
5. Use ink palette for all grays, blue accent for emphasis, `text-foreground` for all primary text

## Supporting Files

- `globals.css` — Complete CSS with all variables, utilities, and animations (copy into `src/app/globals.css`)
