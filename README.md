# SvelteKit PWA

A [SvelteKit](https://kit.svelte.dev/) project with full **Progressive Web App (PWA)** support powered by [`@vite-pwa/sveltekit`](https://vite-pwa-org.netlify.app/frameworks/sveltekit).

## Features

- ⚡ SvelteKit + Vite
- 📦 Offline support via Workbox service worker
- 📲 Installable (Add to Home Screen)
- 🔄 Auto-updates with user prompt
- 🎨 Web App Manifest with icons
- 🔷 TypeScript support

## Getting Started

### Prerequisites

- Node.js >= 18
- npm or pnpm

### Install

```bash
npm install
```

### Development

```bash
npm run dev
```

Open [http://localhost:5173](http://localhost:5173) in your browser.

### Build

```bash
npm run build
```

### Preview Production Build

```bash
npm run preview
```

## PWA Configuration

PWA is configured in `vite.config.ts` using the `SvelteKitPWA` plugin.

| Option | Value |
|---|---|
| Register type | `autoUpdate` |
| Theme color | `#ff3e00` (Svelte orange) |
| Display mode | `standalone` |
| Icons | 192×192, 512×512 |

### Icons

Place your app icons under `static/icons/`:

```
static/
  icons/
    icon-192x192.png
    icon-512x512.png
```

> You can generate icons at [realfavicongenerator.net](https://realfavicongenerator.net) or [maskable.app](https://maskable.app).

## Project Structure

```
sveltekit-pwa/
├── src/
│   ├── app.css
│   ├── app.d.ts
│   ├── app.html
│   └── routes/
│       ├── +layout.svelte   # SW registration + update toast
│       └── +page.svelte     # Home page with install prompt
├── static/
│   └── icons/               # PWA icons
├── svelte.config.js
├── tsconfig.json
└── vite.config.ts           # PWA plugin config
```

## License

MIT
