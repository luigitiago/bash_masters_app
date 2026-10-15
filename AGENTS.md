# AGENTS.md

## What this repo is
Single-file static web app: an interactive Linux/Bash tutor ("BashMaster"). No build system, no package manager, no tests, no git.

- `index.html` — **the app and the only source of truth.** All HTML, CSS (Tailwind utility classes + one inline `<style>`) and vanilla JS live here.
- `prompt_for_web_app_generation.md` — original spec/prompt (reference only).
- `linux_bash_tutor_web_app.md` — **NOT markdown.** Despite the extension it contains a complete *older* HTML prototype of this same app. It is superseded; do not treat it as docs and do not "fix" the app there.

## Hard constraints
- Keep everything in **one file**. Do not split into modules, add a bundler, or introduce npm dependencies. Styling is Tailwind via CDN with a custom theme in the first `<script>` (`tailwind.config`, colors: `darker/dark/card/terminal`).
- Loaded from CDNs (needs network): Tailwind, FontAwesome 6.5.1, Google Fonts (Inter + Fira Code). There is no offline/vendored copy.
- UI text is Italian. Keep new user-facing strings in Italian.
- There are exactly **2 `<script>` blocks**; the app logic is the **last** one (index `-1` when extracting).

## Verify changes (there is no test runner)
1. Syntax-check the app script:
   ```bash
   python3 -c "import re;open('/tmp/app.js','w').write(re.findall(r'<script>(.*?)</script>',open('index.html').read(),re.S)[-1])"
   node --check /tmp/app.js
   ```
2. Open in a browser: `xdg-open index.html`. The folder is not a served app; opening the file directly is the intended flow.
3. For terminal-engine logic you can stub `document`/`localStorage`/`Blob` and `new Function(code)` the extracted script, but strip the trailing `init();` and the `terminal-input` keydown listener (both touch the DOM) before evaluating.

## App architecture gotchas
- **Terminal simulator, not a real shell.** `runCommand(raw)` handles single commands; pipes (`|`) are only handled by `runPipeline()`, which is invoked from `handleTerminalSubmit()`. If you add commands, wire them into `runCommand` and the `help`/`man` lists.
- Virtual filesystem is a plain JS object tree `fs`; `HOME = /home/bashmaster`, cwd starts at `~/workspace`. Path helpers: `resolvePath`, `getNode`, `displayPath`.
- Challenges are validated by `check(cmd, ctx)` functions. The active list is `getChallenges()` = built-in `CHALLENGES` **plus** `customChallenges` (auto-generated from user study material). Always consider both.
- Study material (`state.materials`) feeds three places at once via `afterMaterialChange()`: theory cards, palestra challenges, and quiz questions. When changing material logic, keep all three in sync.
- All persistence is `localStorage` under key **`bashmaster.v2`** (`STORAGE_KEY`). If you change the state shape, handle its absence defensively; `resetProgress()` intentionally preserves `state.materials`.
- Tailwind classes are applied by string concatenation in JS (e.g. nav active/inactive states in `setNavClass`). Editing one class list usually means editing the matching string too.
