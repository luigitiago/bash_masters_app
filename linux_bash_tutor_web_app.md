<!DOCTYPE html>
<html lang="it" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Linux Bash Tutor & Script Generator</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        darker: '#090d16',
                        dark: '#0f172a',
                        card: '#1e293b',
                        terminal: '#05070b'
                    }
                }
            }
        }
    </script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts: Fira Code & Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@400;500;700&family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Inter', sans-serif; }
        .font-code { font-family: 'Fira Code', monospace; }
        /* Custom Scrollbar */
        ::-webkit-scrollbar { width: 8px; height: 8px; }
        ::-webkit-scrollbar-track { background: #0f172a; }
        ::-webkit-scrollbar-thumb { background: #334155; border-radius: 4px; }
        ::-webkit-scrollbar-thumb:hover { background: #475569; }
    </style>
</head>
<body class="bg-darker text-slate-100 min-h-screen flex flex-col selection:bg-emerald-500 selection:text-black">

    <!-- Top Navigation Header -->
    <header class="bg-dark border-b border-slate-800 sticky top-0 z-50">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <div class="flex items-center space-x-3">
                <div class="w-10 h-10 rounded-xl bg-emerald-500/10 border border-emerald-500/30 flex items-center justify-center text-emerald-400">
                    <i class="fa-solid fa-terminal text-lg"></i>
                </div>
                <div>
                    <h1 class="font-bold text-lg tracking-tight text-white flex items-center gap-2">
                        BashMaster <span class="text-xs font-semibold px-2 py-0.5 rounded-full bg-emerald-500/20 text-emerald-300 border border-emerald-500/30">Pro</span>
                    </h1>
                    <p class="text-xs text-slate-400">Guida, Palestra e Generatore Bash</p>
                </div>
            </div>

            <!-- Navigation Tabs -->
            <nav class="hidden md:flex space-x-1 bg-slate-900 p-1.5 rounded-xl border border-slate-800">
                <button onclick="switchTab('theory')" id="nav-theory" class="px-4 py-2 rounded-lg text-sm font-medium transition-all flex items-center gap-2 bg-emerald-500 text-black shadow-lg shadow-emerald-500/20">
                    <i class="fa-solid fa-book-open"></i> Teoria
                </button>
                <button onclick="switchTab('arena')" id="nav-arena" class="px-4 py-2 rounded-lg text-sm font-medium transition-all flex items-center gap-2 text-slate-400 hover:text-white hover:bg-slate-800">
                    <i class="fa-solid fa-code"></i> Palestra
                </button>
                <button onclick="switchTab('generator')" id="nav-generator" class="px-4 py-2 rounded-lg text-sm font-medium transition-all flex items-center gap-2 text-slate-400 hover:text-white hover:bg-slate-800">
                    <i class="fa-solid fa-wand-magic-sparkles"></i> Generatore Script
                </button>
                <button onclick="switchTab('exercises')" id="nav-exercises" class="px-4 py-2 rounded-lg text-sm font-medium transition-all flex items-center gap-2 text-slate-400 hover:text-white hover:bg-slate-800">
                    <i class="fa-solid fa-dumbbell"></i> Nuovi Esercizi
                </button>
            </nav>

            <!-- User Progress / Stats -->
            <div class="flex items-center space-x-3">
                <div class="hidden sm:flex items-center space-x-2 bg-slate-900 border border-slate-800 px-3 py-1.5 rounded-xl text-xs">
                    <i class="fa-solid fa-fire text-amber-400"></i>
                    <span>Completati: <strong id="completed-count" class="text-emerald-400">0</strong></span>
                </div>
            </div>
        </div>
        <!-- Mobile Navigation Bar -->
        <div class="flex md:hidden bg-slate-900 border-t border-slate-800 px-2 py-1.5 justify-around">
            <button onclick="switchTab('theory')" id="mob-nav-theory" class="p-2 rounded-lg text-xs font-medium flex flex-col items-center text-emerald-400">
                <i class="fa-solid fa-book-open text-base mb-0.5"></i> Teoria
            </button>
            <button onclick="switchTab('arena')" id="mob-nav-arena" class="p-2 rounded-lg text-xs font-medium flex flex-col items-center text-slate-400">
                <i class="fa-solid fa-code text-base mb-0.5"></i> Palestra
            </button>
            <button onclick="switchTab('generator')" id="mob-nav-generator" class="p-2 rounded-lg text-xs font-medium flex flex-col items-center text-slate-400">
                <i class="fa-solid fa-wand-magic-sparkles text-base mb-0.5"></i> Script
            </button>
            <button onclick="switchTab('exercises')" id="mob-nav-exercises" class="p-2 rounded-lg text-xs font-medium flex flex-col items-center text-slate-400">
                <i class="fa-solid fa-dumbbell text-base mb-0.5"></i> Esercizi
            </button>
        </div>
    </header>

    <!-- Main Content Container -->
    <main class="flex-1 max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-8">

        <!-- ================= SECTION 1: THEORY & NOTES ================= -->
        <section id="tab-theory" class="space-y-8">
            <div class="bg-gradient-to-r from-emerald-900/20 via-slate-900 to-slate-900 border border-emerald-500/20 p-6 rounded-2xl">
                <h2 class="text-2xl font-bold text-white mb-2 flex items-center gap-3">
                    <i class="fa-solid fa-graduation-cap text-emerald-400"></i> Appunti e Fondamenti di Bash
                </h2>
                <p class="text-slate-400 text-sm max-w-3xl">
                    Benvenuto nel corso interattivo di Bash. Qui trovi i concetti chiave relativi a Shell, Terminale, comandi di orientamento, navigazione e anatomia dei comandi.
                </p>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                <!-- Card 1: Shell, Terminale e Bash -->
                <div class="bg-card border border-slate-800 rounded-xl p-5 hover:border-slate-700 transition-all flex flex-col justify-between">
                    <div>
                        <div class="w-10 h-10 rounded-lg bg-blue-500/10 border border-blue-500/20 flex items-center justify-center text-blue-400 mb-4">
                            <i class="fa-solid fa-laptop-code"></i>
                        </div>
                        <h3 class="font-bold text-white text-lg mb-2">1. Shell, Terminale e Bash</h3>
                        <ul class="text-sm text-slate-300 space-y-2 mb-4">
                            <li><strong class="text-emerald-400">Shell:</strong> Programma che interpreta ordini scritti dall'utente (es. bash, sh, zsh).</li>
                            <li><strong class="text-emerald-400">Terminale:</strong> Interfaccia grafica o di testo per comunicare con la shell (es. Warp, Xterm).</li>
                            <li><strong class="text-emerald-400">Bash:</strong> La shell più popolare in ambienti Unix (Linux e macOS).</li>
                        </ul>
                    </div>
                    <span class="text-xs text-slate-500 font-code">configurazione/00</span>
                </div>

                <!-- Card 2: Windows & WSL -->
                <div class="bg-card border border-slate-800 rounded-xl p-5 hover:border-slate-700 transition-all flex flex-col justify-between">
                    <div>
                        <div class="w-10 h-10 rounded-lg bg-purple-500/10 border border-purple-500/20 flex items-center justify-center text-purple-400 mb-4">
                            <i class="fa-brands fa-windows"></i>
                        </div>
                        <h3 class="font-bold text-white text-lg mb-2">2. Bash su Windows & WSL</h3>
                        <p class="text-sm text-slate-300 mb-3">
                            Su Windows puoi usare <span class="text-purple-300">Git for Windows</span> (supporto limitato) oppure <strong class="text-white">WSL</strong> (Windows Subsystem for Linux) per un supporto completo.
                        </p>
                        <div class="bg-terminal p-2.5 rounded-lg font-code text-xs text-emerald-400 border border-slate-800">
                            wsl --install
                        </div>
                    </div>
                    <span class="text-xs text-slate-500 font-code mt-4">configurazione/02</span>
                </div>

                <!-- Card 3: Warp Terminal -->
                <div class="bg-card border border-slate-800 rounded-xl p-5 hover:border-slate-700 transition-all flex flex-col justify-between">
                    <div>
                        <div class="w-10 h-10 rounded-lg bg-cyan-500/10 border border-cyan-500/20 flex items-center justify-center text-cyan-400 mb-4">
                            <i class="fa-solid fa-terminal"></i>
                        </div>
                        <h3 class="font-bold text-white text-lg mb-2">3. Warp Terminal</h3>
                        <p class="text-sm text-slate-300 mb-3">
                            La moderna terminale con intelligenza artificiale integrata ideale per interagire comodamente con la shell e velocizzare lo sviluppo.
                        </p>
                    </div>
                    <span class="text-xs text-slate-500 font-code">configurazione/03</span>
                </div>

                <!-- Card 4: Primi Passi & Hola Mondo -->
                <div class="bg-card border border-slate-800 rounded-xl p-5 hover:border-slate-700 transition-all flex flex-col justify-between">
                    <div>
                        <div class="w-10 h-10 rounded-lg bg-emerald-500/10 border border-emerald-500/20 flex items-center justify-center text-emerald-400 mb-4">
                            <i class="fa-solid fa-play"></i>
                        </div>
                        <h3 class="font-bold text-white text-lg mb-2">4. Primi Passi: echo</h3>
                        <p class="text-sm text-slate-300 mb-2">Il comando <code class="text-emerald-400 font-code">echo</code> stampa testo a schermo o variabili di sistema.</p>
                        <div class="bg-terminal p-3 rounded-lg font-code text-xs text-emerald-300 space-y-1 border border-slate-800">
                            <div>echo "Hola, BASH"</div>
                            <div>echo $SHELL</div>
                        </div>
                    </div>
                    <span class="text-xs text-slate-500 font-code mt-4">primi_passi/04</span>
                </div>

                <!-- Card 5: Comandi di Orientamento -->
                <div class="bg-card border border-slate-800 rounded-xl p-5 hover:border-slate-700 transition-all flex flex-col justify-between">
                    <div>
                        <div class="w-10 h-10 rounded-lg bg-amber-500/10 border border-amber-500/20 flex items-center justify-center text-amber-400 mb-4">
                            <i class="fa-solid fa-compass"></i>
                        </div>
                        <h3 class="font-bold text-white text-lg mb-2">5. Orientamento & ls</h3>
                        <ul class="text-sm text-slate-300 space-y-1.5 mb-3">
                            <li><code class="text-amber-400 font-code">pwd</code>: Mostra directory corrente.</li>
                            <li><code class="text-amber-400 font-code">ls -l</code>: Formato lungo.</li>
                            <li><code class="text-amber-400 font-code">ls -a</code>: File nascosti.</li>
                            <li><code class="text-amber-400 font-code">ls -lh</code>: Formato human-readable.</li>
                        </ul>
                    </div>
                    <span class="text-xs text-slate-500 font-code">primi_passi/05</span>
                </div>

                <!-- Card 6: Navigazione cd -->
                <div class="bg-card border border-slate-800 rounded-xl p-5 hover:border-slate-700 transition-all flex flex-col justify-between">
                    <div>
                        <div class="w-10 h-10 rounded-lg bg-rose-500/10 border border-rose-500/20 flex items-center justify-center text-rose-400 mb-4">
                            <i class="fa-solid fa-folder-tree"></i>
                        </div>
                        <h3 class="font-bold text-white text-lg mb-2">6. Navigazione cd & Percorsi</h3>
                        <ul class="text-sm text-slate-300 space-y-1.5 mb-3">
                            <li><code class="text-rose-400 font-code">cd dir</code>: Entra nella cartella.</li>
                            <li><code class="text-rose-400 font-code">cd ..</code>: Torna al livello superiore.</li>
                            <li><code class="text-rose-400 font-code">cd ~</code>: Vai alla Home personale.</li>
                            <li><strong class="text-white">Assoluta:</strong> Parte da radice (<code class="text-rose-400 font-code">/home/user</code>).</li>
                        </ul>
                    </div>
                    <span class="text-xs text-slate-500 font-code">primi_passi/06-07</span>
                </div>
            </div>
        </section>

        <!-- ================= SECTION 2: PRACTICE ARENA (INTERACTIVE TERMINAL) ================= -->
        <section id="tab-arena" class="hidden space-y-6">
            <div class="flex flex-col md:flex-row md:items-center justify-between gap-4 bg-slate-900 border border-slate-800 p-6 rounded-2xl">
                <div>
                    <h2 class="text-2xl font-bold text-white mb-1 flex items-center gap-3">
                        <i class="fa-solid fa-code text-emerald-400"></i> Palestra di Esercizi Interattivi
                    </h2>
                    <p class="text-slate-400 text-sm">Completa le missioni scrivendo i comandi corretti nella simulazione di terminale sottostante.</p>
                </div>
                <div class="flex items-center gap-3">
                    <span id="challenge-counter" class="text-xs bg-emerald-500/20 text-emerald-300 border border-emerald-500/30 px-3 py-1.5 rounded-xl font-medium">Sfida 1 di 4</span>
                    <button onclick="nextChallenge()" class="px-4 py-2 bg-slate-800 hover:bg-slate-700 border border-slate-700 text-white rounded-xl text-xs font-medium transition-all">Prossima Sfida <i class="fa-solid fa-arrow-right ml-1"></i></button>
                </div>
            </div>

            <!-- Active Challenge Box -->
            <div class="bg-card border border-emerald-500/30 rounded-2xl p-6 shadow-xl shadow-emerald-950/20">
                <div class="flex items-start justify-between gap-4 mb-4">
                    <div>
                        <span class="text-xs uppercase tracking-wider text-emerald-400 font-semibold bg-emerald-500/10 px-2.5 py-1 rounded-lg border border-emerald-500/20" id="challenge-difficulty">Base</span>
                        <h3 class="text-lg font-bold text-white mt-2" id="challenge-title">Stampa un saluto</h3>
                        <p class="text-slate-300 text-sm mt-1" id="challenge-desc">Utilizza il comando <code class="text-emerald-400 font-code">echo</code> per stampare a schermo la scritta <code class="text-emerald-400 font-code">Hola, BASH</code>.</p>
                    </div>
                    <button onclick="toggleHint()" class="text-xs bg-slate-800 hover:bg-slate-700 text-slate-300 px-3 py-1.5 rounded-lg border border-slate-700 transition-all flex items-center gap-1.5">
                        <i class="fa-solid fa-lightbulb text-amber-400"></i> Aiuto
                    </button>
                </div>
                <div id="challenge-hint-box" class="hidden bg-slate-900 border border-amber-500/30 p-3 rounded-xl text-xs text-amber-300 font-code mb-4">
                    💡 <span id="challenge-hint-text">Digita: echo "Hola, BASH"</span>
                </div>
            </div>

            <!-- Interactive Terminal Simulator -->
            <div class="bg-terminal border border-slate-800 rounded-2xl overflow-hidden shadow-2xl">
                <!-- Terminal Header -->
                <div class="bg-slate-900/80 border-b border-slate-800 px-4 py-3 flex items-center justify-between">
                    <div class="flex items-center space-x-2">
                        <div class="w-3 h-3 rounded-full bg-rose-500"></div>
                        <div class="w-3 h-3 rounded-full bg-amber-500"></div>
                        <div class="w-3 h-3 rounded-full bg-emerald-500"></div>
                        <span class="ml-3 text-xs font-code text-slate-400">bashmaster@linux: ~/workspace</span>
                    </div>
                    <div class="text-xs text-slate-500 font-code">Warp / Bash Shell</div>
                </div>
                <!-- Terminal Output Area -->
                <div id="terminal-output" class="p-6 font-code text-sm text-slate-200 h-64 overflow-y-auto space-y-2">
                    <div class="text-slate-500">Benvenuto nella terminale Bash interattiva. Digita comandi come <span class="text-emerald-400">pwd</span>, <span class="text-emerald-400">ls</span>, <span class="text-emerald-400">echo</span> o <span class="text-emerald-400">whoami</span>.</div>
                    <div class="text-emerald-400">bashmaster@linux:~$ echo "Pronto per iniziare!"</div>
                    <div>Pronto per iniziare!</div>
                </div>
                <!-- Terminal Input Form -->
                <form id="terminal-form" onsubmit="handleTerminalSubmit(event)" class="bg-slate-900/90 border-t border-slate-800 px-4 py-3 flex items-center gap-3">
                    <span class="text-emerald-400 font-code text-sm">bashmaster@linux:~$</span>
                    <input type="text" id="terminal-input" autocomplete="off" placeholder="Scrivi un comando (es. echo 'Hola, BASH')..." class="flex-1 bg-transparent border-none outline-none font-code text-sm text-white placeholder-slate-600">
                    <button type="submit" class="px-4 py-1.5 bg-emerald-500 hover:bg-emerald-400 text-black font-semibold rounded-lg text-xs transition-all">Esegui</button>
                </form>
            </div>
        </section>

        <!-- ================= SECTION 3: BASH SCRIPT GENERATOR ================= -->
        <section id="tab-generator" class="hidden space-y-6">
            <div class="bg-slate-900 border border-slate-800 p-6 rounded-2xl">
                <h2 class="text-2xl font-bold text-white mb-1 flex items-center gap-3">
                    <i class="fa-solid fa-wand-magic-sparkles text-emerald-400"></i> Generatore di Script Bash
                </h2>
                <p class="text-slate-400 text-sm">Seleziona lo scopo e le opzioni desiderate per generare automaticamente il tuo script Bash pronto all'uso.</p>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
                <!-- Generator Controls Form -->
                <div class="bg-card border border-slate-800 rounded-2xl p-6 space-y-4 lg:col-span-1">
                    <div>
                        <label class="block text-xs font-semibold text-slate-300 uppercase tracking-wider mb-2">Tipo di Script</label>
                        <select id="script-type" onchange="generateScript()" class="w-full bg-slate-900 border border-slate-800 rounded-xl px-3 py-2.5 text-sm text-white focus:border-emerald-500 outline-none">
                            <option value="backup">Backup Automatico di File</option>
                            <option value="monitor">Controllo Risorse di Sistema</option>
                            <option value="loop">Ciclo For di Elaborazione</option>
                            <option value="userinfo">Report Informazioni Utente</option>
                        </select>
                    </div>

                    <div>
                        <label class="block text-xs font-semibold text-slate-300 uppercase tracking-wider mb-2">Parametri / Nome Cartella</label>
                        <input type="text" id="script-param" value="/var/log/backup" oninput="generateScript()" class="w-full bg-slate-900 border border-slate-800 rounded-xl px-3 py-2.5 text-sm text-white focus:border-emerald-500 outline-none">
                    </div>

                    <div>
                        <label class="block text-xs font-semibold text-slate-300 uppercase tracking-wider mb-2">Opzioni Avanzate</label>
                        <div class="space-y-2 text-sm text-slate-300">
                            <label class="flex items-center gap-2 cursor-pointer">
                                <input type="checkbox" id="opt-comments" checked onchange="generateScript()" class="rounded bg-slate-900 border-slate-700 text-emerald-500 focus:ring-0">
                                Includi commenti esplicativi
                            </label>
                            <label class="flex items-center gap-2 cursor-pointer">
                                <input type="checkbox" id="opt-strict" checked onchange="generateScript()" class="rounded bg-slate-900 border-slate-700 text-emerald-500 focus:ring-0">
                                Modalità rigida (set -e)
                            </label>
                        </div>
                    </div>

                    <button onclick="generateScript()" class="w-full py-3 bg-emerald-500 hover:bg-emerald-400 text-black font-bold rounded-xl text-sm transition-all shadow-lg shadow-emerald-500/20">
                        Rigenera Script
                    </button>
                </div>

                <!-- Generated Script Output -->
                <div class="bg-terminal border border-slate-800 rounded-2xl p-6 lg:col-span-2 flex flex-col justify-between">
                    <div>
                        <div class="flex items-center justify-between mb-4 pb-3 border-b border-slate-800">
                            <span class="text-xs font-code text-emerald-400" id="script-filename">script_backup.sh</span>
                            <button onclick="copyScript()" class="px-3 py-1.5 bg-slate-800 hover:bg-slate-700 text-slate-200 rounded-lg text-xs font-medium transition-all flex items-center gap-1.5">
                                <i class="fa-regular fa-copy"></i> Copia Codice
                            </button>
                        </div>
                        <pre id="script-output" class="font-code text-sm text-slate-200 overflow-x-auto p-2"><code>#!/bin/bash
# Script generato da BashMaster
set -e

echo "Inizio backup dei file..."
tar -czvf backup.tar.gz /var/log/backup
echo "Backup completato con successo!"</code></pre>
                    </div>

                    <div class="mt-6 pt-4 border-t border-slate-800 text-xs text-slate-400">
                        💡 <strong class="text-white">Nota:</strong> Ricordati di assegnare i permessi di esecuzione con <code class="text-emerald-400 font-code">chmod +x nome_script.sh</code> prima di eseguirlo.
                    </div>
                </div>
            </div>
        </section>

        <!-- ================= SECTION 4: EXERCISE GENERATOR ================= -->
        <section id="tab-exercises" class="hidden space-y-6">
            <div class="bg-slate-900 border border-slate-800 p-6 rounded-2xl flex flex-col md:flex-row md:items-center justify-between gap-4">
                <div>
                    <h2 class="text-2xl font-bold text-white mb-1 flex items-center gap-3">
                        <i class="fa-solid fa-dumbbell text-emerald-400"></i> Generatore di Nuovi Esercizi
                    </h2>
                    <p class="text-slate-400 text-sm">Crea sfide personalizzate per testare le tue competenze su argomenti specifici di Linux Bash.</p>
                </div>
                <button onclick="generateNewExercise()" class="px-5 py-2.5 bg-emerald-500 hover:bg-emerald-400 text-black font-bold rounded-xl text-sm transition-all shadow-lg shadow-emerald-500/20 flex items-center gap-2">
                    <i class="fa-solid fa-shuffle"></i> Genera Esercizio Casuale
                </button>
            </div>

            <!-- Dynamic Exercise Card -->
            <div class="bg-card border border-slate-800 rounded-2xl p-8 space-y-6">
                <div class="flex items-center justify-between">
                    <span id="ex-topic" class="text-xs font-semibold px-3 py-1 rounded-full bg-blue-500/20 text-blue-300 border border-blue-500/30">Navigazione & File System</span>
                    <span id="ex-diff" class="text-xs font-semibold px-3 py-1 rounded-full bg-amber-500/20 text-amber-300 border border-amber-500/30">Intermedio</span>
                </div>

                <div>
                    <h3 id="ex-title" class="text-xl font-bold text-white mb-2">Trova e elenca file nascosti con dettaglio</h3>
                    <p id="ex-desc" class="text-slate-300 text-sm leading-relaxed">Scrivi il comando corretto per visualizzare tutti i file presenti nella cartella corrente (inclusi quelli nascosti) ordinati in formato lungo human-readable.</p>
                </div>

                <div class="bg-terminal p-4 rounded-xl border border-slate-800 space-y-3">
                    <div class="text-xs font-semibold text-slate-400 uppercase tracking-wider">Soluzione Corretta (Nascosta)</div>
                    <div id="ex-solution-container" class="hidden">
                        <code id="ex-solution" class="text-emerald-400 font-code text-sm">ls -la -h</code>
                    </div>
                    <button onclick="toggleExerciseSolution()" id="ex-solution-btn" class="px-4 py-2 bg-slate-800 hover:bg-slate-700 text-slate-200 rounded-lg text-xs font-medium transition-all">
                        Mostra Soluzione
                    </button>
                </div>
            </div>
        </section>

    </main>

    <!-- Footer -->
    <footer class="bg-dark border-t border-slate-800 mt-12 py-6 text-center text-xs text-slate-500">
        BashMaster Pro — Piattaforma di apprendimento interattivo per Linux Bash & Scripting.
    </footer>

    <!-- JavaScript Application Logic -->
    <script>
        // State Management
        let completedCount = 0;
        let currentChallengeIndex = 0;

        const challenges = [
            {
                difficulty: "Base",
                title: "Stampa il tuo primo saluto",
                desc: "Utilizza il comando echo per stampare a schermo la scritta <code>Hola, BASH</code>.",
                hint: "Digita: echo \"Hola, BASH\"",
                solution: 'echo "Hola, BASH"'
            },
            {
                difficulty: "Base",
                title: "Mostra directory corrente",
                desc: "Qual è il comando fondamentale per stampare il percorso della cartella in cui ti trovi?",
                hint: "Digita: pwd",
                solution: 'pwd'
            },
            {
                difficulty: "Base",
                title: "Elenca file nascosti in formato lungo",
                desc: "Usa il comando <code>ls</code> con le opzioni adatte per visualizzare tutti i file (inclusi i nascosti) in formato lungo.",
                hint: "Digita: ls -la oppure ls -a -l",
                solution: 'ls -la'
            },
            {
                difficulty: "Intermedio",
                title: "Informazioni utente corrente",
                desc: "Mostra il nome dell'utente attualmente collegato al sistema.",
                hint: "Digita: whoami",
                solution: 'whoami'
            }
        ];

        // Tab Switching
        function switchTab(tabId) {
            const tabs = ['theory', 'arena', 'generator', 'exercises'];
            tabs.forEach(t => {
                document.getElementById(`tab-${t}`).classList.add('hidden');
                document.getElementById(`nav-${t}`).className = "px-4 py-2 rounded-lg text-sm font-medium transition-all flex items-center gap-2 text-slate-400 hover:text-white hover:bg-slate-800";
                document.getElementById(`mob-nav-${t}`).className = "p-2 rounded-lg text-xs font-medium flex flex-col items-center text-slate-400";
            });

            document.getElementById(`tab-${tabId}`).classList.remove('hidden');
            document.getElementById(`nav-${tabId}`).className = "px-4 py-2 rounded-lg text-sm font-medium transition-all flex items-center gap-2 bg-emerald-500 text-black shadow-lg shadow-emerald-500/20";
            document.getElementById(`mob-nav-${tabId}`).className = "p-2 rounded-lg text-xs font-medium flex flex-col items-center text-emerald-400";
        }

        // Challenge management
        function loadChallenge() {
            const ch = challenges[currentChallengeIndex];
            document.getElementById('challenge-difficulty').innerText = ch.difficulty;
            document.getElementById('challenge-title').innerText = ch.title;
            document.getElementById('challenge-desc').innerHTML = ch.desc;
            document.getElementById('challenge-hint-text').innerText = ch.hint;
            document.getElementById('challenge-counter').innerText = `Sfida ${currentChallengeIndex + 1} di ${challenges.length}`;
            document.getElementById('challenge-hint-box').classList.add('hidden');
        }

        function toggleHint() {
            const box = document.getElementById('challenge-hint-box');
            box.classList.toggle('hidden');
        }

        function nextChallenge() {
            currentChallengeIndex = (currentChallengeIndex + 1) % challenges.length;
            loadChallenge();
        }

        // Terminal Simulator Logic
        function handleTerminalSubmit(e) {
            e.preventDefault();
            const inputField = document.getElementById('terminal-input');
            const cmd = inputField.value.trim();
            if (!cmd) return;

            const outputDiv = document.getElementById('terminal-output');
            
            // Append user command
            outputDiv.innerHTML += `<div class="text-emerald-400">bashmaster@linux:~$ ${escapeHtml(cmd)}</div>`;
            
            let response = "";
            const currentCh = challenges[currentChallengeIndex];

            // Evaluate command
            if (cmd === 'clear') {
                outputDiv.innerHTML = `<div class="text-slate-500">Terminal pulita.</div>`;
                inputField.value = '';
                outputDiv.scrollTop = outputDiv.scrollHeight;
                return;
            } else if (cmd === 'pwd') {
                response = "/home/bashmaster/workspace";
            } else if (cmd === 'whoami') {
                response = "bashmaster";
            } else if (cmd === 'date') {
                response = new Date().toLocaleString();
            } else if (cmd.startsWith('echo ')) {
                response = cmd.substring(5).replace(/['"]/g, '');
            } else if (cmd.startsWith('ls')) {
                response = "file1.txt  file2.sh  documenti/  .config  .gitignore";
            } else if (cmd === 'uname -a' || cmd === 'uname') {
                response = "Linux bashmaster-virtual 6.5.0-generic x86_64 GNU/Linux";
            } else {
                response = `bash: ${cmd}: comando non trovato o non supportato in questa simulazione.`;
            }

            outputDiv.innerHTML += `<div>${escapeHtml(response)}</div>`;

            // Check if matches active challenge
            if (cmd === currentCh.solution || (currentCh.solution === 'ls -la' && (cmd === 'ls -l -a' || cmd === 'ls -al' || cmd === 'ls -la'))) {
                completedCount++;
                document.getElementById('completed-count').innerText = completedCount;
                outputDiv.innerHTML += `<div class="text-emerald-300 bg-emerald-950/40 p-2 rounded border border-emerald-500/30 font-semibold">🎉 Ottimo lavoro! Hai completato la sfida con successo. Passaggio alla prossima...</div>`;
                setTimeout(() => {
                    nextChallenge();
                }, 1500);
            }

            inputField.value = '';
            outputDiv.scrollTop = outputDiv.scrollHeight;
        }

        function escapeHtml(text) {
            return text.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;");
        }

        // Script Generator Logic
        function generateScript() {
            const type = document.getElementById('script-type').value;
            const param = document.getElementById('script-param').value || '/tmp';
            const comments = document.getElementById('opt-comments').checked;
            const strict = document.getElementById('opt-strict').checked;

            let code = "#!/bin/bash\n";
            if (comments) code += "# Script generato automaticamente da BashMaster Pro\n";
            if (strict) code += "set -e\n\n";

            if (type === 'backup') {
                document.getElementById('script-filename').innerText = "backup_script.sh";
                if (comments) code += "echo \"[INFO] Avvio procedura di backup per la cartella: " + param + "\"\n";
                code += "tar -czvf backup_$(date +%Y%m%d_%H%M%S).tar.gz " + param + "\n";
                if (comments) code += "echo \"[SUCCESS] Backup completato con successo!\"\n";
            } else if (type === 'monitor') {
                document.getElementById('script-filename').innerText = "system_monitor.sh";
                if (comments) code += "echo \"=== REPORT STATO SISTEMA ===\"\n";
                code += "echo \"Uptime del sistema:\"\n";
                code += "uptime\n\n";
                code += "echo \"Spazio disco disponibile:\"\n";
                code += "df -h\n";
            } else if (type === 'loop') {
                document.getElementById('script-filename').innerText = "batch_loop.sh";
                if (comments) code += "# Iterazione sui file della cartella\n";
                code += "for file in " + param + "/*; do\n";
                code += "    echo \"Elaborazione file: $file\"\n";
                code += "done\n";
            } else if (type === 'userinfo') {
                document.getElementById('script-filename').innerText = "user_report.sh";
                code += "echo \"Utente corrente: $(whoami)\"\n";
                code += "echo \"Home directory: $HOME\"\n";
                code += "echo \"Data odierna: $(date)\"\n";
            }

            document.getElementById('script-output').querySelector('code').innerText = code;
        }

        function copyScript() {
            const codeText = document.getElementById('script-output').innerText;
            navigator.clipboard.writeText(codeText);
            alert("Script copiato negli appunti!");
        }

        // Exercise Generator Logic
        const randomExercises = [
            {
                topic: "Gestione Stringhe & Variabili",
                diff: "Base",
                title: "Stampa variabile di sistema",
                desc: "Scrivi il comando per stampare il valore della variabile di ambiente che definisce la shell corrente.",
                solution: "echo $SHELL"
            },
            {
                topic: "Navigazione Avanzata",
                diff: "Base",
                title: "Torna alla directory Home",
                desc: "Qual è il comando rapido per spostarti direttamente nella tua directory personale (Home) da qualsiasi posizione?",
                solution: "cd ~"
            },
            {
                topic: "Informazioni di Sistema",
                diff: "Intermedio",
                title: "Visualizza dettagli del Kernel",
                desc: "Usa il comando <code>uname</code> con l'opzione appropriata per mostrare tutte le informazioni dettagliate del kernel e del sistema.",
                solution: "uname -a"
            }
        ];

        function generateNewExercise() {
            const rand = randomExercises[Math.floor(Math.random() * randomExercises.length)];
            document.getElementById('ex-topic').innerText = rand.topic;
            document.getElementById('ex-diff').innerText = rand.diff;
            document.getElementById('ex-title').innerText = rand.title;
            document.getElementById('ex-desc').innerHTML = rand.desc;
            document.getElementById('ex-solution').innerText = rand.solution;
            document.getElementById('ex-solution-container').classList.add('hidden');
            document.getElementById('ex-solution-btn').innerText = "Mostra Soluzione";
        }

        function toggleExerciseSolution() {
            const container = document.getElementById('ex-solution-container');
            const btn = document.getElementById('ex-solution-btn');
            container.classList.toggle('hidden');
            btn.innerText = container.classList.contains('hidden') ? "Mostra Soluzione" : "Nascondi Soluzione";
        }

        // Initial load
        loadChallenge();
    </script>
</body>
</html>