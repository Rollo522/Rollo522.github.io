# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static portfolio website for a cybersecurity graduate, deployed via GitHub Pages at `https://rollo522.github.io`. The site showcases academic research (dissertation on AI-generated phishing), professional projects (Formula Student autonomous vehicle, mobile app security), and contact information.

## Technology Stack

- **Pure HTML/CSS**: No build process or compilation required
- **TailwindCSS**: Loaded via CDN (`https://cdn.tailwindcss.com`)
- **Lucide Icons**: Loaded via CDN (`https://unpkg.com/lucide@latest`)
- **Google Fonts**: Plus Jakarta Sans (body) and JetBrains Mono (monospace/code)
- **Deployment**: GitHub Pages (auto-deploys from main branch)

## Development Workflow

### Local Development
```bash
# Open any HTML file directly in a browser
open index.html

# Or use a simple HTTP server (recommended for testing)
python3 -m http.server 8000
# Then visit http://localhost:8000
```

### Deployment
```bash
# Changes are automatically deployed when pushed to main branch
git add .
git commit -m "Description of changes"
git push origin main

# Site updates at https://rollo522.github.io within 1-2 minutes
```

## Architecture & Design System

### Page Structure
All pages follow a consistent layout pattern:
1. **Fixed background layer** (`.fixed-bg`) with parallax effect
2. **Bottom-docked navigation** (`.nav-dock`) with glass morphism
3. **Main content area** with reveal animations
4. **Lucide icon initialization** via JavaScript

### Navigation System
The site uses a persistent bottom navigation dock (inspired by macOS) that appears on all pages:
- About (`index.html`) - Landing page with hero card and skills matrix
- Dissertation (`research.html`) - Scrolling story-style research presentation
- Projects (`projects.html`) - Two-column project showcases with code samples
- Contact (`contact.html`) - Contact links and social media

Active page is indicated by red underline (`decoration-red-600 underline-offset-8`).

### Design Language
- **Color System**:
  - Primary brand: `--napier-red: #E31B23` (Edinburgh Napier University)
  - Background: `--zinc-950: #09090b` (near-black)
  - Text hierarchy: white → zinc-300 → zinc-500 → zinc-700
- **Effects**:
  - Glass morphism panels: `backdrop-filter: blur(20-30px)` with subtle borders
  - Parallax: Mouse tracking on `index.html` card (`#tilt-card`) and background
  - Reveal animations: `.reveal` class with intersection observer
- **Typography**:
  - Headers use tight tracking (`tracking-tighter`)
  - Labels use uppercase with wide tracking (`tracking-[0.3em]`)
  - Monospace elements use JetBrains Mono at 10px

### Key CSS Classes
- `.nav-dock`: Bottom navigation with blur and transparency
- `.glass-panel`: Frosted glass effect for content cards
- `.id-card`: 3D-transformable card on hover (index page)
- `.terminal-box`: Code block styling with window chrome
- `.reveal` / `.fade-in`: Scroll-triggered animations

## Images & Assets

### Required Images
- `headshot.JPEG` (770KB) - Profile photo on index.html
- `app_screenshot.png` (110KB) - Mobile app interface on projects.html
- `background.jpg` (optional) - Custom background image (falls back to Unsplash)

### Image Guidelines
- Headshot: Portrait orientation, will be displayed as square with grayscale effect
- App screenshot: 9:16 aspect ratio (mobile screen), displayed in phone frame mockup
- Background: Wide landscape (2000px+), will be darkened and blurred

## Common Modifications

### Adding a New Project (projects.html)
Projects alternate between left-image and right-image layouts using grid column ordering:
```html
<div class="grid lg:grid-cols-2 gap-20 items-center">
  <!-- Use order-1/order-2 classes to control side -->
  <div class="order-2 lg:order-1">Image/Demo</div>
  <div class="order-1 lg:order-2">Text Content</div>
</div>
```

### Updating Research Sections (research.html)
Each section uses full-viewport height (`.section-wrap`) with fade-in animations. The page uses scroll-triggered reveals via intersection observer.

### Modifying Colors
The Napier Red (`#E31B23`) is used sparingly as an accent. To change the brand color:
1. Update CSS custom property: `:root { --napier-red: #NEW_COLOR; }`
2. Update Tailwind classes: Search for `red-500`, `red-600` and replace

### Responsive Breakpoints
Tailwind's default breakpoints are used:
- `lg:` prefix applies at 1024px+ (tablet landscape and desktop)
- Most layouts stack vertically on mobile, expand to grid on desktop

## Deployment & Git

**Repository**: `https://github.com/Rollo522/Rollo522.github.io`

GitHub Pages serves the root directory directly. No build step or GitHub Actions workflow is required. The site updates automatically within 1-2 minutes of pushing to main.

## Browser Compatibility

- **Modern browsers only** (Chrome 90+, Safari 14+, Firefox 88+)
- Requires support for: `backdrop-filter`, CSS custom properties, CSS Grid, Intersection Observer API
- No polyfills or fallbacks included
