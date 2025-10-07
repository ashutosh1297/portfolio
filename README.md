# Ashutosh Sharma — Terminal Portfolio

This repository contains a single-page, front-end "terminal" portfolio for Ashutosh Sharma. It's a playful, minimal, and fully client-side experience that mimics a shell-like interface where visitors can read about work, education, languages, frameworks, and download a resume.

It is implemented with vanilla HTML/CSS/JavaScript — no frameworks or build steps required. The page works with in-memory fallbacks for file content and will also attempt to fetch `.txt` files from the same directory when served over HTTP.

## Features

- Terminal-like UI with a titlebar and resizable panel.
- Native text input caret and keyboard-driven command interface.
- Built-in commands: `help`, `clear`, `ls`, `cat <filename>`, `exit` (and `quit`/`close`).
- Persistent command history (stored in `localStorage`) and Up/Down navigation.
- Tab-completion for base commands and a static file list.
- Landing overlay with name, social links (LinkedIn, GitHub, Email), and two action buttons:
  - "Go to console" — reveal the terminal and focus the input.
  - "Download Resume" — triggers a download of `resume.pdf`.
- `cat` attempts to fetch files from the server and falls back to included in-memory text constants for offline/file:// usage.
- Printed file output supports simple role/header highlighting and linkification.

## Files in this repo

- `index.html` — the entire application (UI, styles, and logic).
- `work.txt`, `education.txt`, `languages.txt`, `frameworks.txt`, `projects.txt` — content files that can be shown via `cat` (or fetched by the page when served).
- `resume.pdf` — the downloadable resume (expected in the same folder).
- `README.md` — this file.

## How to run locally

Serving the folder over a small HTTP server is recommended so `fetch()` works for `cat <filename>` and resume downloads. From the project root:

```bash
python3 -m http.server 8000
# or (if you prefer Node):
# npx http-server -p 8000
```

Then open http://localhost:8000 in your browser.

You can also open `index.html` directly via `file://`, but the page will fall back to in-memory text for `cat` and resume downloads may behave differently depending on the browser's local-file handling.

## Commands

- `help` — show available commands and tips.
- `clear` — clear the visible terminal output (history preserved).
- `ls` — list available files.
- `cat <filename>` — show file contents. Supported names (fallback): `work.txt`, `education.txt`, `languages.txt`, `frameworks.txt`, `projects.txt`, `resume.pdf` (download).
- `exit`, `quit`, `close` — return to the landing overlay (clears visible output, preserves history).

## Development notes

- All logic lives in `index.html`. It's intentionally small and dependency-free for portability.
- Command history is saved to `localStorage` under `portfolio_terminal_history_v1`.
- The `FILE_LIST` and `BASE_COMMANDS` arrays are static for Tab completion. If you'd like dynamic completion from the directory, we can add a simple endpoint or a build step.
- The `catFile()` function will `fetch()` files from the server; if the fetch fails, it uses a fallback mapping of in-memory strings defined in the script.
- Styles are inlined in `index.html` for simplicity. If you want to split into separate CSS/JS files, I can scaffold that.

## Accessibility

- Buttons and interactive controls use semantic elements (`button`) and have accessible labels where appropriate.
- The overlay is marked with `role="dialog"` and `aria-modal="true"`.
- Keyboard navigation: focus is automatically moved to the input when the console opens; Escape hides the overlay.

## Suggestions / Next steps

- Persist the terminal size across reloads (store width/height in `localStorage`).
- Improve Tab completion with case-insensitive matching and cycling through multiple matches.
- Add unit tests for the command parsing logic (small JS test harness).
- Extract JS into a separate module and add a minimal build/test pipeline if you plan to extend the project.

If you'd like, I can implement any of these follow-ups now. Want me to make the `Download Resume` button visually secondary (outline) or hide the overlay after download?  