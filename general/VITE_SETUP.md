# Vite 7 + React + TypeScript + Tailwind v4 — **Zero‑Boilerplate Quick‑Start**

> Repeatable checklist that captures all the snags we hit and how to solve them. Copy‑paste at will.

---

## 0  Prerequisites

| Tool     | Version                         |
| -------- | ------------------------------- |
| **Node** | ≥ 20 LTS (Vite 7 drops Node 18) |
| **npm**  | comes with Node 20              |

---

## 1  Scaffold the project

```bash
npm create vite@latest my-app -- --template react-ts
cd my-app
```

This gives you Vite 7, React, React‑DOM, TypeScript, JSX transform, ESLint, and the default file layout (see tree below).

---

## 2  Install Tailwind v4 + Vite plugin (Vite 7‑first)

Tailwind’s Vite plugin (`@tailwindcss/vite@4.1.10`) **still lists Vite 5/6 in its peer‑range**, so npm will refuse to marry it with Vite 7 out of the box. Use one of the up‑to‑date paths below—both keep you on the latest Vite.

| Path                            | When to choose                                                          | Commands                              |
| ------------------------------- | ----------------------------------------------------------------------- | ------------------------------------- |
| **Override path (recommended)** | You want the official plugin today with a stable, deterministic install | 1⃣ Add to `package.json` → \`\`\`json |
| "overrides": {                  |                                                                         |                                       |

```
"@tailwindcss/vite": { "vite": "^7.0.0" }
```

} \`\`\`  2⃣ `npm install` | | **Grab unreleased plugin** | You like a perfectly clean dependency tree & don’t mind tracking HEAD | `npm i -D tailwindlabs/[email protected] tailwindcss` |

> **Why not just **``**?** Works in a pinch but the override is deterministic—CI, teammates, and future installs all behave the same.

---

## 3  Add Tailwind to the build

**vite.config.ts**

```ts
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import tailwindcss from '@tailwindcss/vite';

export default defineConfig({
  plugins: [react(), tailwindcss()],
});
```

---

## 4  Minimal stylesheet (CSS‑first model)

Create **src/index.css** and import Tailwind plus any tokens:

```css
@import "tailwindcss";

@theme {
  --brand: #1e40af;  /* indigo‑800 */
  --radius: 0.75rem; /* lg */
}
```

Then, in **src/main.tsx**:

```ts
import "./index.css";
```

No `tailwind.config.js` is required in v4—the `@theme{}` and `@config{}` at‑rules live right in your CSS. Delete any auto‑generated `postcss.config.cjs`; the Vite plugin bypasses PostCSS.

---

---

## 7  Common issues & fixes

| Symptom                                              | Root cause                                                         | Fix                                                                                                     |
| ---------------------------------------------------- | ------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------- |
| ``                                                   | `@tailwindcss/vite` peer‑depends on Vite 5/6                       | Apply *override path* (or use the unreleased plugin)                                                    |
| ``\*\* → “could not determine executable to run”\*\* | Tailwind CLI split into `@tailwindcss/cli`; `init` command retired | Usually you *don’t* need a CLI. If you do, `npm i -D @tailwindcss/cli` and run `npx @tailwindcss/cli …` |
| **Styles don’t apply**                               | CSS file not imported; class typo; server cache                    | Ensure `import "./index.css";` exists and restart `npm run dev`                                         |

---

## 8  Project tree after setup

```
my-app/
├─ dist/                  (prod build)
├─ node_modules/
├─ src/
│  ├─ App.css
│  ├─ App.tsx
│  ├─ index.css           ← Tailwind entry
│  ├─ main.tsx            ← imports index.css
│  └─ vite-env.d.ts
├─ vite.config.ts         ← Tailwind plugin wired here
├─ package.json
└─ tsconfig.*.json
```

*(Matches the screenshot you shared.)*



- Remove public folder in root and assets folder in src

---

## 9  Further reading / quick search terms

| Topic                     | Search phrase                  |
| ------------------------- | ------------------------------ |
| Tailwind v4 release notes | `Tailwind CSS v4 announcement` |
| CSS‑first theming         | `Tailwind @theme at‑rule`      |
| Vite 7 migration guide    | `Vite 7 release blog`          |
| Tailwind × Vite plugin    | `@tailwindcss/vite github`     |

Consult the official docs for the most current commands; CLI flags change fastest.

---

**Repeatable punch‑list (TL;DR)**

```bash
# 1  Scaffold
npm create vite@latest my-app -- --template react-ts && cd my-app
# 2  Handle Vite‑plugin mismatch
## Override path (recommended)
#   add overrides → package.json, then:
npm install
# 3  Create src/index.css with "@import 'tailwindcss';"
# 4  Add plugin line to vite.config.ts
```

Keep this doc in your repo root (e.g. `SETUP.md`) so any LLM—or future you—can bootstrap the stack without tripping over the same road‑blocks.

