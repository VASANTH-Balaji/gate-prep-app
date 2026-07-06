# GATE Prep App

A mobile-first React app for GATE exam preparation — daily practice, subject-wise questions, PYQ practice, aptitude, progress tracking, and resources.

## Setup

```bash
npm install
npm run dev
```

Then open the local URL shown in the terminal (defaults to http://localhost:5173).

## Build for production

```bash
npm run build
npm run preview
```

## Tech stack

- React 18 + Vite
- lucide-react (icons)
- Inline styles + Google Fonts (Space Grotesk, Inter, IBM Plex Mono) loaded at runtime
- State persisted via browser storage (see `loadState`/`saveState` in `src/App.jsx`)

## Structure

```
gate-prep-app/
├── index.html
├── package.json
├── vite.config.js
├── src/
│   ├── main.jsx
│   ├── App.jsx      # main app component (all screens/logic)
│   ├── index.css
│   └── assets/
```
