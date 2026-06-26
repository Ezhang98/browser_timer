# Timer Suite — Implementation Report

A single self-contained `index.html` (~970 lines). Double-click to open in any browser — no server, no build step, no internet needed.

## How it's built
- **One file**, no dependencies. HTML + CSS + vanilla JS.
- **Persistence:** `localStorage` (key `timerSuiteState_v1`). Intervals, saved sets, alarms (incl. per-alarm sound), theme, font, clock format, timer size, custom sound, and usage stats all survive closing/reopening the page. *(You asked about cookies — localStorage is the correct tool for a local file and was confirmed in the setup question.)*
- **Sounds:** generated live with the Web Audio API (Beep, Chime, Bell, Buzz, Triad, Blip) so nothing is downloaded. You can also upload a custom audio file in Settings; it's stored as a data URL in localStorage and appears in every sound dropdown.
- **Favicon:** an inline SVG data URI in `<head>`, so the tab icon ships inside the one file with no separate asset.

## Tabs

**Interval timer (default)** — add/remove named intervals, each with its own end sound and a duration set through a wheel picker (Hours/Minutes/Seconds). Set how many times the whole set repeats and which interval to start on. Start / Pause / Reset, a live progress bar, and current-interval / set counters. Fullscreen mode uses real browser fullscreen, mirrors the big-screen display, and has its own Start/Pause/Reset controls. The browser **tab title** live-updates with the countdown (`⏱ 00:42 · Work`, `⏸` when paused, `✓ Finished` when done) so it's visible from another tab.

**Sets** — save the current intervals + repeat count as a named set. Saved sets list with inline-editable names, a `count · duration · ×repeat` summary, Load (sends it back to the Interval tab and switches there), Delete, and drag-to-reorder via the ⠿ handle.

**Alarm** — add multiple alarms, each with a time (wheel picker), optional label, its own sound (with ▶ preview), and an on/off toggle. Times are stored internally in 24-hour form and displayed per the chosen clock format. Fires when the computer clock hits the time (checked every second); rings repeatedly with a flashing card and a Stop button (auto-stops after 60s). Existing alarm times are clickable to edit.

**Stopwatch** — multiple independent stopwatches running at once. Each has Start/Pause, Lap (newest on top), Stop (resets), and Remove. One is created on load; "+ New stopwatch" adds more.

**Settings** — timer size (Small→Huge) and font; clock format (12-hour with AM/PM, or 24-hour); ten themes with the active one highlighted; default interval sound with Preview; custom sound upload; usage stats; Reset all data.

## Wheel time picker
Shared component used by interval durations and alarm times. Each wheel is a scroll-snapping column; you can **drag** it, use the **mouse wheel/trackpad** (one step per notch), or **type** in the number field below — all kept in sync, snapping to the centered value on release. The alarm picker adds an AM/PM toggle on the side in 12-hour mode and swaps the hour wheel to 0–23 in 24-hour mode.

## Themes & fonts
Ten CSS-variable themes: Dark, Light, Cyber, Wood, Forest, Ocean, Sunset, Rosé, Midnight (AMOLED black), Matrix (green terminal). The selected theme is highlighted in Settings. Switching a theme also applies a matching font (via a `THEME_FONTS` map) and updates the font dropdown — but the choice isn't locked, so you can change the font afterward and it sticks.

## Notes & limitations

- **Browser autoplay:** audio needs one user interaction (a click) before it can play — normal browser policy. Since you start timers/alarms by clicking, this is satisfied automatically.
- **Alarms only fire while the page is open.** A closed tab can't ring. Background/inactive tabs may also throttle JS timers slightly depending on the browser.
- **Custom sounds** are stored in localStorage; very large audio files could hit the storage quota. Short clips are fine.


