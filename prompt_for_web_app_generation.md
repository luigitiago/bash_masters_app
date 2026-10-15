# Prompt for AI Agent: Linux Bash Tutor & Script Generator Web App

You are an expert full-stack web developer and UI/UX designer. Your task is to build a single-file interactive web application (`index.html`) that serves as a **Linux Bash Learning, Practice, and Script Generation Assistant**. 

The app should be inspired by the provided course notes (which cover topics ranging from shell basics, terminal history, Windows/WSL setup, navigation, absolute/relative paths, to command anatomy like `echo`, `pwd`, `ls`, `cd`, `whoami`, `date`, etc.).

---

## Core Requirements & Features

### 1. Single-File Architecture (`index.html`)
- The application must be fully self-contained in a single HTML file.
- Use Tailwind CSS via CDN for a modern, responsive, dark-mode-first terminal/developer aesthetic (e.g., slate/zinc backgrounds, emerald/green accent colors for terminal text).
- Use Lucide icons or FontAwesome via CDN for clean UI icons.
- Include vanilla JavaScript for all application logic, interactivity, local storage, and tab management.

### 2. Main Navigation / Tabs
The app should feature a clean sidebar or top navigation bar with the following sections:
1. **Teoria e Appunti (Theory & Notes):** Interactive viewer based on the provided course examples (Shell vs Terminal vs Bash, History, Windows/WSL setup, Warp terminal, Navigation, Paths, Command Anatomy).
2. **Palestra di Esercizi (Practice Arena):** Interactive terminal emulator / command challenge sandbox where users test commands based on the curriculum.
3. **Generatore di Script (Script Generator):** An AI-assisted prompt builder where users select options (loops, variables, file operations) to generate clean Bash scripts with explanations.
4. **Crea Nuovi Esercizi (Exercise Generator):** A tool that generates custom Linux Bash exercises with hints, validation criteria, and difficulty levels.

---

## Detailed Section Specifications

### Section 1: Theory Viewer (`Teoria`)
- Display structured markdown-like cards or collapsible accordions based on the provided examples:
  - **Shell, Terminal e Bash:** Definitions of Shell (`bash`, `sh`, `zsh`), Terminal (`Warp`, `Xterm`), and Bash.
  - **Installazione su Windows:** Git for Windows vs WSL (`wsl --install`, `/mnt/c`).
  - **Terminali Avanzati:** Warp terminal integration notes.
  - **Primi Passi & Comandi di Orientamento:** `echo`, `pwd`, `ls` (`-l`, `-a`, `-lh`), `cd` (`..`, `~`, tab completion), Absolute vs Relative paths, and basic system info (`whoami`, `cal`, `date`, `uptime`, `uname`, `clear`).
  - **Anatomia del Comando:** Breakdown of `comando [opciones] [argumentos]`.

### Section 2: Interactive Practice Arena (`Esercizi`)
- Provide preset interactive challenges categorized by difficulty (Base, Intermedio).
- *Example Challenge 1:* "Visualizza tutti i file nella cartella corrente inclusi quelli nascosti in formato lungo human-readable." (Expected: `ls -la -h` or `ls -lah`).
- *Example Challenge 2:* "Stampa a schermo il testo 'Hola, BASH'." (Expected: `echo "Hola, BASH"`).
- Include a simulated interactive terminal input box where users type commands. The simulator should parse basic commands (`pwd`, `ls`, `echo`, `whoami`, `date`, `clear`, `cd`) against a virtual file system state and give immediate feedback or error messages.

### Section 3: Bash Script Generator (`Generatore Script`)
- A form-based builder where users can pick:
  - Script Purpose (e.g., Backup files, Process text, System monitoring, Simple loop).
  - Inputs/Arguments.
  - Output requirements.
- Generates a syntax-highlighted Bash script block with copy-to-clipboard functionality and a line-by-line explanation of what the script does.

### Section 4: AI Exercise Generator (`Crea Esercizi`)
- Lets the user pick a topic (e.g., File Navigation, String Manipulation, Conditionals) and difficulty.
- Dynamically generates a brand new exercise scenario, complete with objective, starter hint, and solution key hidden behind a "Mostra Soluzione" toggle.

---

## Design & Usability Guidelines
- **Theme:** Dark mode developer theme (Tailwind `bg-slate-900`, text `slate-100`, accents in `emerald-500` or `cyan-400`).
- **Responsiveness:** Fully responsive on desktop and mobile.
- **Persistence:** Save user progress (completed exercises, custom saved scripts) in browser `localStorage`.

Generate the complete, working, production-ready `index.html` file now.
```egon

I have created a comprehensive Markdown prompt that you can feed directly to your AI agent or coding assistant. It outlines all the architectural requirements, design principles, and specific features derived from your course notes to build the Linux Bash web application.

Let me know if you would like to refine any specific section of the prompt or need further assistance!