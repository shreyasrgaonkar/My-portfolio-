# Shreyas OS

A single-file interactive portfolio that looks and feels like a desktop + mobile operating system — built for **Shreyas Gaonkar** (AI / ML · Classical Vocalist).

Open `index.html` in a browser, or deploy it to GitHub Pages / Netlify / any static host.

---

## Features

- **Dual mode UI**
  - Desktop: windows, taskbar, start menu, drag / resize
  - Mobile: Pixel-style home screen, widgets, dock, app sheets
- **Apps:** About, Education, Skills, Projects, Achievements, Certifications, Music, Contact, Terminal, Settings, **Chat**
- **Themes:** RGB gaming dark mode + soft blue-gradient light mode
- **Google Search** on desktop taskbar and mobile home screen
- **Live battery %** (where the browser Battery API is available)
- **AI Chat** via Groq (API key stays on your server — visitors never enter a key)
- **Keyboard shortcuts**
  - `Ctrl + D` → Desktop
  - `Ctrl + M` → Mobile
  - `Ctrl + L` → Lock screen

---

## Quick start

1. Download or clone this repo.
2. Open `index.html` in Chrome / Edge (best support).
3. Or deploy the file to GitHub Pages / Netlify / Cloudflare Pages.

No build step. No `npm install`. One HTML file.

> **Note:** Battery % and some APIs work best on **HTTPS** or `localhost`. Opening via `file://` may limit battery and mic-related features.

---

## Project structure

```
├── index.html        # Full OS UI + CSS + JS (main deliverable)
├── groq-worker.js    # Cloudflare Worker proxy for Groq chat (optional)
└── README.md
```

Icons are **inline SVGs** inside `index.html`. There is no `icons/` folder to upload.

---

## AI Chat (Groq) setup

Visitors should **not** paste API keys. You host a small proxy once.

### 1. Get a Groq API key

- [https://console.groq.com/keys](https://console.groq.com/keys)

### 2. Deploy the Cloudflare Worker

1. [Cloudflare Dashboard](https://dash.cloudflare.com) → **Workers & Pages** → **Create** → **Worker**
2. Paste the contents of `groq-worker.js`
3. **Settings → Variables** → add secret:
   - Name: `GROQ_API_KEY`
   - Value: your Groq key
4. Deploy and copy the worker URL  
   Example: `https://shreyas-chat.your-subdomain.workers.dev`

### 3. Point the portfolio at the worker

In `index.html`, find:

```js
const CHAT_API_URL = 'https://YOUR-WORKER.workers.dev';
```

Replace with your real worker URL.

### Model

Default model in the worker:

```js
model: 'openai/gpt-oss-20b'
```

If Groq changes free-tier models, edit that string in the worker and redeploy. Alternatives that often work on free tier: `openai/gpt-oss-120b`, `groq/compound-mini`.

---

## Customization

| What | Where |
|------|--------|
| Theme colors | CSS `:root` and `:root[data-theme="light"]` in `index.html` |
| Wallpapers | `--wallpaper` / `--desktop-wallpaper` + `WALLPAPERS` JS object |
| App content | `APPS` array in `index.html` |
| Chat personality | `CHAT_SYSTEM` string in `index.html` |
| Contact links | Contact app `content` in `APPS` |

---

## Deploy (GitHub Pages)

1. Create a repo and upload **`index.html`** (and this README if you want).
2. **Settings → Pages → Deploy from branch** → `main` / root.
3. After deploy, set `CHAT_API_URL` to your HTTPS worker URL (already done if you edited before upload).

No need to upload an icons folder.

---

## Browser support

- **Recommended:** Chromium (Chrome, Edge, Brave)
- Firefox / Safari: UI works; battery API and some effects may differ
- Mobile browsers: use Mobile mode (`Ctrl+M` or narrow window)

---

## Credits

- Portfolio of **Shreyas Ranjit Gaonkar**
- AI replies powered by **Groq** (via your Cloudflare Worker)
- Optional wallpapers via Unsplash / hosted profile images

---

## License

Personal portfolio project. Reuse the OS shell idea freely; keep personal content and branding respectful of the original author.
