# Vite 7 + React + TypeScript + Tailwind v4 Setup

## Instructions for LLM Execution
- **Report completion after each step**: Confirm what was accomplished before moving to the next step
- **Think step by step**: Process each step methodically and verify results
- **Check for existing files**: Before scaffolding, note if the current directory contains files
- **Final note**: If files existed before scaffolding, mention this at the end of the setup process

## Prerequisites
- Node ≥ 20 LTS (Vite 7 requirement)
- npm (included with Node 20)

## 1. Scaffold Project
```bash
# Install in current directory if empty, otherwise create temp folder
npm create vite@latest . -- --template react-ts
# If current folder has files, use: npm create vite@latest temp-vite -- --template react-ts && cd temp-vite
```

## 2. Install Tailwind v4
The Tailwind Vite plugin doesn't officially support Vite 7 yet. Fix with package.json override:

**package.json** - Add this section:
```json
"overrides": {
  "@tailwindcss/vite": { "vite": "^7.0.0" }
}
```

Then install:
```bash
npm install @tailwindcss/vite tailwindcss
```

## 3. Configure Vite Plugin
**vite.config.ts**
```ts
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import tailwindcss from '@tailwindcss/vite';

export default defineConfig({
  plugins: [react(), tailwindcss()],
});
```

## 4. Setup CSS
**src/index.css**
```css
@import "tailwindcss";
```

**src/main.tsx** - Add import:
```ts
import "./index.css";
```

## 5. Cleanup
- Remove `public/` folder
- Remove `src/assets/` folder  
- Delete any auto-generated `postcss.config.cjs`

## Common Issues
| Problem | Solution |
|---------|----------|
| Vite 7 compatibility error | Use package.json override above |
| Styles don't apply | Ensure `import "./index.css"` exists, restart dev server |
| CLI commands fail | Install `@tailwindcss/cli` separately if needed |

## Quick Commands
```bash
# Complete setup in current directory
npm create vite@latest . -- --template react-ts
# Add override to package.json, then:
npm install @tailwindcss/vite tailwindcss
# Create src/index.css with @import "tailwindcss";
# Add tailwindcss() plugin to vite.config.ts
# Remove public/ and src/assets/ folders
npm run dev
```

## Final Structure
```
./
├─ src/
│  ├─ App.tsx
│  ├─ index.css          ← Tailwind entry
│  ├─ main.tsx           ← imports index.css
│  └─ vite-env.d.ts
├─ vite.config.ts        ← Tailwind plugin
└─ package.json         ← overrides section
```