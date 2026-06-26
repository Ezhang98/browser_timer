# ⏱ Timer Suite

A single-file, offline-friendly browser app with an interval timer, alarms, and multiple stopwatches. No server, no build step, no dependencies — just open `index.html`.

**Live demo:** https://ezhang98.github.io/browser_timer/

## Features

- **Interval timer** (default tab) — add named intervals, each with its own duration and end sound, set how many times the whole set repeats, with Start/Pause/Reset, a live progress bar, and a fullscreen mode.
- **Alarms** — multiple alarms by time and label, each with an on/off toggle; rings with a flashing card and Stop button when your clock reaches the set time.
- **Stopwatches** — run several independent stopwatches at once, each with Pause, Lap, Stop, and Remove.
- **Settings** — timer size and font, five themes (Dark, Light, Cyber, Wood, Forest), built-in synthesized sounds plus custom audio upload, and usage stats.
- **Persistent** — all settings, intervals, alarms, and the custom sound are saved in `localStorage`, so they survive closing and reopening the page.

## Usage

Clone or download the repo and open `index.html` in any modern browser:

```bash
git clone https://github.com/Ezhang98/browser_timer.git
cd browser_timer
# then double-click index.html, or:
open index.html        # macOS
xdg-open index.html    # Linux
start index.html       # Windows
```

Audio requires one click first (standard browser autoplay policy) — starting a timer satisfies this automatically. Alarms only fire while the page is open.

## Hosting on GitHub Pages

Because the whole app is one static `index.html`, GitHub Pages can serve it directly:

1. Push your code to the `main` branch (already done).
2. On GitHub, go to **Settings → Pages**.
3. Under **Build and deployment → Source**, choose **Deploy from a branch**.
4. Set **Branch** to `main` and folder to `/ (root)`, then click **Save**.
5. Wait ~1 minute. Your site goes live at:

   **https://ezhang98.github.io/browser_timer/**

GitHub serves `index.html` automatically as the landing page. Every time you push to `main`, the site updates. (If it 404s at first, give it a minute and hard-refresh — the first build can lag.)

## Tech

Plain HTML, CSS, and vanilla JavaScript in one file. Sounds are generated with the Web Audio API; the favicon is an inline SVG. See [IMPLEMENTATION.md](IMPLEMENTATION.md) for design notes and limitations.

## License

[MIT](LICENSE) © 2026 Ezhang98
