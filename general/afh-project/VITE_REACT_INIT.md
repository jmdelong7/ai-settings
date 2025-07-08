# Vite + React + TypeScript + Tailwind v4 Setup

## Instructions for LLM Execution

- **Report completion after each step**: Confirm what was accomplished before moving to the next step
- **Think step by step**: Process each step methodically and verify results
- **Check for existing files**: Before scaffolding, note if the current directory contains files
- **Vite compatibility check**: Before installing Tailwind, check current documentation or attempt installation first. Only add package.json overrides if specific compatibility errors occur
- **Version-specific guidance**: If errors mention Vite version incompatibility, use the package.json override pattern with the appropriate version number
- **Documentation lookup**: If Context 7 MCP tool is available and you encounter setup issues, use it to search for the latest Vite, Tailwind, Typescript, or React documentation for troubleshooting
- **Final note**: If files existed before scaffolding, mention this at the end of the setup process

## Prerequisites

- Node ≥ 20 LTS (check Vite documentation for current version requirements)
- npm (included with Node)

## 1. Scaffold Project

```bash
# Install in current directory if empty, otherwise create temp folder
npm create vite@latest . -- --template react-ts
# If current folder has files, use: npm create vite@latest temp-vite -- --template react-ts && cd temp-vite
```

## 2. Install Tailwind v4

**Check for Vite compatibility first**: The Tailwind Vite plugin may not immediately support the latest Vite versions. If you encounter compatibility errors during installation or build, add a package.json override.

**If compatibility issues arise**, add this to **package.json**:

```json
"overrides": {
  "@tailwindcss/vite": { "vite": "^X.0.0" }
}
```

_Replace `X.0.0` with your current Vite major version (e.g., `^7.0.0`, `^8.0.0`, etc.)_

Then install:

```bash
npm install @tailwindcss/vite tailwindcss
```

**Note**: Always try installation without overrides first. Only add overrides if you encounter specific compatibility errors.

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
@import 'tailwindcss';
```

**Note**: Do not add any other styles to this file. Only the import statement.

**src/main.tsx** - Add import:

```ts
import './index.css';
```

## 5. Cleanup

- Remove `public/` folder
- Remove `src/assets/` folder
- Delete any auto-generated `postcss.config.cjs`
- Remove `src/App.css`
- Update `src/App.tsx` and `src/main.tsx` to adapt to the removal of `App.css` and the `public` and `src/assets` folders
- Remove "erasableSyntaxOnly" from `tsconfig.json` & `tsconfig.node.json` if present

## 6. Update Styling

Replace any default React styling with simple Tailwind utilities:

**src/App.tsx** - Example with basic Tailwind styling:

```tsx
function App() {
  return (
    <div className="min-h-screen bg-gray-50 flex items-center justify-center">
      <div className="max-w-md mx-auto bg-white rounded-lg shadow-md p-6">
        <h1 className="text-2xl font-bold text-gray-900 mb-4">
          Vite + React + Tailwind
        </h1>
        <p className="text-gray-600 mb-4">
          Your setup is complete and ready for development.
        </p>
        <button className="bg-blue-500 hover:bg-blue-600 text-white px-4 py-2 rounded transition-colors">
          Get Started
        </button>
      </div>
    </div>
  );
}

export default App;
```

## Common Issues

| Problem                          | Solution                                                     |
| -------------------------------- | ------------------------------------------------------------ |
| Vite version compatibility error | Use package.json override with your Vite version (see above) |
| Styles don't apply               | Ensure `import "./index.css"` exists, restart dev server     |
| CLI commands fail                | Install `@tailwindcss/cli` separately if needed              |
| Setup errors or outdated info    | Use Context 7 MCP tool (if available) to search latest docs  |

## Quick Commands

```bash
# Complete setup in current directory
npm create vite@latest . -- --template react-ts
# Try installing Tailwind (add override to package.json if compatibility errors):
npm install @tailwindcss/vite tailwindcss
# Create src/index.css with @import "tailwindcss";
# Add tailwindcss() plugin to vite.config.ts
# Remove public/ and src/assets/ folders
# Update src/App.tsx with simple Tailwind styling
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
└─ package.json         ← overrides section (if needed)
```
