# N8N Flow Documenter

A React-based tool that takes exported n8n workflow JSON and turns it into visual flow diagrams and editable documentation.

## What It Does

1. **Import n8n Flow JSON** - Paste your exported n8n workflow JSON directly, or drag-and-drop a `.json` file. The input panel validates the JSON in real-time and shows node/connection counts.

2. **Visualize the Flow** - Renders an interactive SVG diagram of your workflow nodes and connections. Nodes are color-coded by type (webhook, email, Slack, HTTP, etc.) with zoom controls and auto-fitting viewbox.

3. **Generate Documentation** - Produces human-readable documentation describing what the flow does step-by-step, including error handling and business impact. Currently uses a mock/demo output — intended to be wired to an AI backend.

4. **Edit and Export** - The generated docs open in a rich text editor with formatting toolbar (bold, italic, headings, code blocks). You can copy the output as plain text or raw HTML. A "Publish to Confluence" button is stubbed for future integration.

## Project Structure

```
n8n-flow-documenter/
├── index.html              # Entry point
├── package.json            # Dependencies and scripts
├── vite.config.js          # Vite bundler config (needs to be created)
├── tailwind.config.js      # Tailwind CSS config (needs to be created)
├── postcss.config.js       # PostCSS config (needs to be created)
└── src/
    ├── main.jsx            # React root mount
    ├── App.jsx             # Main app shell, state management, tab routing
    ├── index.css           # Global styles, Tailwind directives, scrollbars
    └── components/
        ├── Sidebar.jsx         # Left nav — switches between Input, Diagram, Docs tabs
        ├── JsonInputPanel.jsx  # JSON paste/upload with drag-and-drop and validation
        ├── FlowDiagram.jsx     # SVG-based flow visualization with zoom
        └── DocEditor.jsx       # Rich text editor with formatting toolbar and HTML preview
```

## Tech Stack

- **React 18** — UI framework
- **Vite 4** — Dev server and bundler
- **Tailwind CSS 3** — Utility-first styling
- **Lucide React** — Icon library (listed as dependency)
- **Inter + Fira Code** — Fonts loaded from Google Fonts

## Do You Need a Dev Environment?

**Yes.** This is a React project that needs to be built/served. You need:

- **Node.js** (v16 or higher) — [Download here](https://nodejs.org/)
- **npm** (comes with Node.js)

### Setup Steps

1. **Restructure the files** into the proper directory layout shown above. The current `.txt` files need to be renamed to `.jsx` and placed under `src/` and `src/components/`.

2. **Create the missing config files** that aren't included:

   **`vite.config.js`**:
   ```js
   import { defineConfig } from 'vite'
   import react from '@vitejs/plugin-react'

   export default defineConfig({
     plugins: [react()],
   })
   ```

   **`tailwind.config.js`**:
   ```js
   export default {
     content: ['./index.html', './src/**/*.{js,jsx}'],
     theme: {
       extend: {
         colors: {
           surface: {
             500: '#2d3347',
             600: '#1e2233',
             800: '#13161e',
             900: '#0d0f14',
           },
           brand: {
             400: '#8b7cf7',
             500: '#6c5ce7',
           },
           accent: {
             400: '#00cec9',
             500: '#00b894',
           },
           danger: '#d63031',
           success: '#00b894',
         },
       },
     },
     plugins: [],
   }
   ```

   **`postcss.config.js`**:
   ```js
   export default {
     plugins: {
       tailwindcss: {},
       autoprefixer: {},
     },
   }
   ```

3. **Install dependencies**:
   ```bash
   npm install
   ```

4. **Start the dev server**:
   ```bash
   npm run dev
   ```
   The app will be available at `http://localhost:5173`.

5. **Build for production** (optional):
   ```bash
   npm run build
   ```
   Output goes to `dist/` — static files you can host anywhere.

## Current Limitations

- **Doc generation is mocked** — The "Generate Docs" button currently returns a hardcoded demo. It's designed to be replaced with a real AI API call.
- **Confluence publishing is stubbed** — The button shows a "coming soon" notification.
- **No persistent storage** — Everything lives in React state; refreshing the page resets it.
