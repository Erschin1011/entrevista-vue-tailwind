# Vue + Tailwind interview starter

Vue 3 + TypeScript + Vite + Tailwind CSS 4 template. It includes a small responsive task UI so you can start coding immediately and see that Vite, Vue and Tailwind are wired together.

## Requirements

- Node.js 20+
- npm

## Run

```bash
npm install
npm run dev
```

Build and preview:

```bash
npm run build
npm run preview
```

## Structure

- `src/App.vue`: starter screen; practice components, `ref`, `computed`, forms, events and list rendering
- `src/style.css`: Tailwind CSS import and global defaults
- `vite.config.ts`: Vue and Tailwind Vite plugins
- `index.html`: browser entry point

Tailwind 4 is integrated using `@tailwindcss/vite` and `@import "tailwindcss"`; no `tailwind.config.js` is required for the default setup. There is no backend in this repo. When an interview task supplies an API, add the API client in a small `src/services/` module and configure its base URL through a `VITE_API_URL` environment variable.
