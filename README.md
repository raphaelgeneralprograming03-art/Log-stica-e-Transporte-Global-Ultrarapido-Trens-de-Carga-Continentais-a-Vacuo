
<html lang="pt-BR" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MHD + SAMS | Trens de Carga Continentais a Vácuo (Hyperloop Supersônico)</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        sci: {
                            950: '#020617',
                            900: '#090d16',
                            800: '#111827',
                            700: '#1f2937',
                            cyan: '#06b6d4',
                            emerald: '#10b981',
                            amber: '#f59e0b',
                            rose: '#f43f5e',
                            purple: '#8b5cf6'
                        }
                    }
                }
            }
        }
    </script>
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;500;700&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Inter', sans-serif; }
        .font-mono { font-family: 'JetBrains Mono', monospace; }
        .glass-panel {
            background: rgba(15, 23, 42, 0.75);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(6, 182, 212, 0.2);
        }
        .glow-cyan {
            box-shadow: 0 0 25px rgba(6, 182, 212, 0.25);
        }
        .glow-emerald {
            box-shadow: 0 0 25px rgba(16, 185, 129, 0.25);
        }
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #020617;
        }
        ::-webkit-scrollbar-thumb {
            background: #1e293b;
            border-radius: 3px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #06b6d4;
        }
    </style>
</head>
<body class="bg-sci-950 text-slate-100 min-h-screen flex flex-col overflow-x-hidden">

    <!-- Header / Navbar -->
    <header class="glass-panel border-b border-cyan-500/20 px-6 py-4 flex flex-wrap items-center justify-between gap-4 sticky top-0 z-50">
        <div class="flex items-center space-x-3">
            <div class="relative flex items-center justify-center w-10 h-10 rounded-xl bg-cyan-950 border border-cyan-500/50 glow-cyan">
                <svg class="w-6 h-6 text-cyan-400 animate-pulse" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z"/>
                </svg>
            </div>
            <div>
                <h1 class="text-lg font-bold tracking-wider text-transparent bg-clip-text bg-gradient-to-r from-cyan-400 to-emerald-400">MHD + SAMS HYPERLOOP LOGISTICS</h1>
                <p class="text-xs text-slate-400 font-mono">Trens Continentais a Vácuo & Propulsão Magnética Supersônica</p>
            </div>
        </div>

        <!-- System Status Pills -->
        <div class="flex items-center gap-3 text-xs font-mono flex-wrap">
            <div class="flex items-center gap-2 px-3 py-1.5 rounded-full bg-slate-900 border border-slate-700">
                <span id="mhd-status-dot" class="w-2.5 h-2.5 rounded-full bg-cyan-500 animate-ping"></span>
                <span>Propulsão MHD: <strong id="mhd-status-text" class="text-cyan-400">2,450 km/h (Mach 2.0)</strong></span>
            </div>
            <div class="flex items-center gap-2 px-3 py-1.5 rounded-full bg-slate-900 border border-slate-700">
                <span class="w-2.5 h-2.5 rounded-full bg-emerald-500"></span>
                <span>SAMS Suspensão: <strong id="sams-status-text" class="text-emerald-400">100% BLINDADO (0.0g)</strong></span>
            </div>
            <div class="flex items-center gap-2 px-3 py-1.5 rounded-full bg-slate-900 border border-slate-700">
                <span class="w-2.5 h-2.5 rounded-full bg-purple-500"></span>
                <span>Pressão do Vácuo: <strong class="text-purple-400">0.001 atm</strong></span>
            </div>
        </div>
    </header>

    <!-- Main Workspace -->
    <main class="flex-1 grid grid-cols-1 lg:grid-cols-12 gap-6 p-6 max-w-[1700px] mx-auto w-full">
        
        <!-- Left Sidebar: Scenarios & Controls -->
        <section class="lg:col-span-3 flex flex-col gap-6">
            
            <!-- Operational Scenario Selection -->
            <div class="glass-panel rounded-2xl p-5 shadow-xl">
                <h2 class="text-sm font-semibold tracking-wide text-cyan-400 uppercase mb-4 flex items-center gap-2">
                    <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3.055 11H5a2 2 0 012 2v1a2 2 0 002 2 2 2 0 012 2v2.945M8 3.935V5.5A2.5 2.5 0 0010.5 8h.5a2 2 0 012 2 2 2 0 104 0 2 2 0 012-2h1.064M15 20.488V18a2 2 0 012-2h3.064M21 12a9 9 0 11-18 0 9 9 0 0118 0z"/></svg>
                    Cenários de Rota e Tráfego
                </h2>
                <div class="space-y-3">
                    <button onclick="setScenario('cruise')" id="scen-cruise" class="w-full text-left p-3 rounded-xl border border-cyan-500/40 bg-cyan-500/10 transition-all hover:bg-cyan-500/20 flex items-center justify-between group">
                        <div>
                            <div class="font-semibold text-sm text-cyan-300">Cruzeiro Supersônico (Mach 2.0)</div>
                            <div class="text-xs text-slate-400">Trabalho contínuo em trilho magnético perfeito</div>
                        </div>
                        <span class="w-2 h-2 rounded-full bg-cyan-400"></span>
                    </button>
                    <button onclick="setScenario('imperfection')" id="scen-imperfection" class="w-full text-left p-3 rounded-xl border border-slate-700 bg-slate-900/60 transition-all hover:border-amber-500/40 flex items-center justify-between group">
                        <div>
                            <div class="font-semibold text-sm text-slate-200 group-hover:text-amber-300">Falha Milimétrica / Desnível</div>
                            <div class="text-xs text-slate-400">Imperfeição estrutural de 0.8 mm no trilho</div>
                        </div>
                        <span class="w-2 h-2 rounded-full bg-slate-600" id="dot-imperfection"></span>
                    </button>
                    <button onclick="setScenario('freight')" id="scen-freight" class="w-full text-left p-3 rounded-xl border border-slate-700 bg-slate-900/60 transition-all hover:border-emerald-500/40 flex items-center justify-between group">
                        <div>
                            <div class="font-semibold text-sm text-slate-200 group-hover:text-emerald-300">Carga Frágil / Órgãos Humanos</div>
                            <div class="text-xs text-slate-400">Sensibilidade máxima a solavancos (Zero G-Force)</div>
                        </div>
                        <span class="w-2 h-2 rounded-full bg-slate-600" id="dot-freight"></span>
                    </button>
                </div>
            </div>

            <!-- MHD & SAMS Control Unit -->
            <div class="glass-panel rounded-2xl p-5 shadow-xl border-cyan-500/30">
                <div class="flex items-center justify-between mb-4">
                    <h2 class="text-sm font-semibold tracking-wide text-cyan-400 uppercase flex items-center gap-2">
                        <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6V4m0 2a2 2 0 100 4m0-4a2 2 0 110 4m-6 8a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4m6 6v10m6-2a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4"/></svg>
                        Parâmetros dos Sistemas
                    </h2>
                    <span id="sys-badge" class="px-2.5 py-0.5 rounded text-xs font-mono font-bold bg-cyan-500/20 text-cyan-300 border border-cyan-500/40">ATIVO</span>
                </div>
                
                <div class="space-y-4">
                    <div class="flex items-center justify-between bg-slate-900/80 p-3 rounded-xl border border-slate-800">
                        <div>
                            <div class="text-xs font-medium text-slate-300">SAMS Suspensão Ativa</div>
                            <div class="text-[10px] text-slate-400 font-mono">Correção em milissegundos</div>
                        </div>
                        <label class="relative inline-flex items-center cursor-pointer">
                            <input type="checkbox" id="samsToggle" checked onchange="toggleSAMS()" class="sr-only peer">
                            <div class="w-11 h-6 bg-slate-700 peer-focus:outline-none rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-emerald-500"></div>
                        </label>
                    </div>

                    <div>
                        <div class="flex justify-between text-xs mb-1 font-mono">
                            <span class="text-slate-400">Velocidade da Propulsão MHD</span>
                            <span id="speed-val" class="text-cyan-400">2,450 km/h</span>
                        </div>
                        <input type="range" id="speedSlider" min="500" max="4000" step="50" value="2450" oninput="updateSpeed(this.value)" class="w-full h-2 bg-slate-800 rounded-lg appearance-none cursor-pointer accent-cyan-400">
                    </div>

                    <div>
                        <div class="flex justify-between text-xs mb-1 font-mono">
                            <span class="text-slate-400">Campo Magnético de Levitação</span>
                            <span class="text-purple-400">18.5 Tesla</span>
                        </div>
                        <input type="range" min="5" max="30" value="18" class="w-full h-2 bg-slate-800 rounded-lg appearance-none cursor-pointer accent-purple-400">
                    </div>
                </div>
            </div>

            <!-- Action Triggers -->
            <div class="glass-panel rounded-2xl p-5 shadow-xl flex flex-col gap-3">
                <h2 class="text-sm font-semibold tracking-wide text-cyan-400 uppercase mb-1">Comandos de Operação</h2>
                <button onclick="triggerRailBump()" class="w-full py-3 px-4 rounded-xl bg-gradient-to-r from-amber-600 to-rose-600 hover:from-amber-500 hover:to-rose-500 text-white font-semibold text-sm shadow-lg shadow-amber-900/30 transition-all flex items-center justify-center gap-2">
                    <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z"/></svg>
                    Simular Desnível Brusco no TrILHO
                </button>
                <button onclick="recalibrateSAMS()" class="w-full py-2.5 px-4 rounded-xl bg-slate-900 hover:bg-slate-800 border border-slate-700 text-slate-300 font-medium text-xs transition-all flex items-center justify-center gap-2">
                    <svg class="w-4 h-4 text-cyan-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15"/></svg>
                    Calibrar Sensores Piezoelétricos SAMS
                </button>
            </div>

        </section>

        <!-- Center: Canvas 2D Simulation Viewport -->
        <section class="lg:col-span-6 flex flex-col gap-6">
            <div class="glass-panel rounded-2xl p-4 shadow-2xl relative flex flex-col overflow-hidden border-cyan-500/30">
                
                <!-- Viewport Header HUD -->
                <div class="flex items-center justify-between pb-3 mb-3 border-b border-slate-800 text-xs font-mono">
                    <div class="flex items-center gap-2">
                        <span class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse"></span>
                        <span class="text-slate-300">TÚNEL DE VÁCUO CONTINENTAL - VISTA LATERAL EM TEMPO REAL</span>
                    </div>
                    <div class="flex items-center gap-4 text-slate-400">
                        <span>Mach: <strong id="hud-mach" class="text-cyan-400">Mach 2.0</strong></span>
                        <span>Força G: <strong id="hud-g" class="text-emerald-400">0.00 G</strong></span>
                    </div>
                </div>

                <!-- Canvas Container -->
                <div class="relative w-full aspect-[4/3] bg-slate-950 rounded-xl overflow-hidden border border-slate-800 shadow-inner">
                    <canvas id="simCanvas" class="w-full h-full block"></canvas>
                    
                    <!-- HUD Instructions / Legend -->
                    <div class="absolute bottom-4 left-4 pointer-events-none bg-slate-900/80 backdrop-blur-md px-3 py-2 rounded-lg border border-cyan-500/30 text-[11px] font-mono text-cyan-300 space-y-1">
                        <div>🚅 Trem Hyperloop flutuando em campo magnético MHD puro</div>
                        <div>⚡ SAMS anula qualquer imperfeição milimétrica do trilho</div>
                    </div>

                    <!-- Bump Alert Banner -->
                    <div id="bump-banner" class="absolute top-4 inset-x-4 pointer-events-none hidden transition-all duration-300">
                        <div class="bg-amber-950/90 border border-amber-500 text-amber-200 px-4 py-2 rounded-xl text-xs font-mono font-bold flex items-center justify-center gap-2 animate-bounce">
                            <svg class="w-4 h-4 text-amber-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z"/></svg>
                            IMPERFEIÇÃO DE TRILHO DETECTADA! SAMS CORRIGIU A SUSPENSÃO EM 0.3ms — CABINE INABALÁVEL!
                        </div>
                    </div>
                </div>

                <!-- Quick Metrics Bar -->
                <div class="grid grid-cols-3 gap-3 mt-4 text-center font-mono">
                    <div class="bg-slate-900/60 p-2.5 rounded-xl border border-slate-800">
                        <div class="text-[10px] text-slate-400">Estabilidade da Cabine</div>
                        <div id="metric-stability" class="text-sm font-bold text-emerald-400">100.0%</div>
                    </div>
                    <div class="bg-slate-900/60 p-2.5 rounded-xl border border-slate-800">
                        <div class="text-[10px] text-slate-400">Eficiência Energética MHD</div>
                        <div id="metric-efficiency" class="text-sm font-bold text-cyan-400">99.8%</div>
                    </div>
                    <div class="bg-slate-900/60 p-2.5 rounded-xl border border-slate-800">
                        <div class="text-[10px] text-slate-400">Integridade da Carga</div>
                        <div id="metric-cargo" class="text-sm font-bold text-purple-400">100% Protegida</div>
                    </div>
                </div>

            </div>
        </section>

        <!-- Right Sidebar: Logistics Telemetry & AI Console -->
        <section class="lg:col-span-3 flex flex-col gap-6">
            
            <!-- Logistics Telemetry -->
            <div class="glass-panel rounded-2xl p-5 shadow-xl">
                <h2 class="text-sm font-semibold tracking-wide text-cyan-400 uppercase mb-4 flex items-center gap-2">
                    <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z"/></svg>
                    Telemetria da Rota Continental
                </h2>
                <div class="space-y-3 font-mono text-xs">
                    <div class="flex justify-between items-center bg-slate-900/80 p-2.5 rounded-xl border border-slate-800">
                        <span class="text-slate-400">Rota Ativa</span>
                        <span class="text-cyan-400 font-bold">América-Europa (Trans-Atlântico)</span>
                    </div>
                    <div class="flex justify-between items-center bg-slate-900/80 p-2.5 rounded-xl border border-slate-800">
                        <span class="text-slate-400">Tempo de Viagem</span>
                        <span class="text-emerald-400 font-bold">2h 14m (Econômico)</span>
                    </div>
                    <div class="flex justify-between items-center bg-slate-900/80 p-2.5 rounded-xl border border-slate-800">
                        <span class="text-slate-400">Carga Transportada</span>
                        <span class="text-purple-400 font-bold">120 Toneladas (Alta Precisão)</span>
                    </div>
                    <div class="flex justify-between items-center bg-slate-900/80 p-2.5 rounded-xl border border-slate-800">
                        <span class="text-slate-400">Temperatura no Vácuo</span>
                        <span class="text-amber-400 font-bold">-45 °C</span>
                    </div>
                </div>
            </div>

            <!-- SAMS + MHD AI Console -->
            <div class="glass-panel rounded-2xl p-5 shadow-xl flex flex-col flex-1 min-h-[260px]">
                <h2 class="text-sm font-semibold tracking-wide text-cyan-400 uppercase mb-3 flex items-center gap-2">
                    <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 9l3 3-3 3m5 0h3M5 20h14a2 2 0 002-2V6a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"/></svg>
                    Console SAMS + MHD AI
                </h2>
                <div id="ai-console" class="flex-1 bg-slate-950/80 rounded-xl p-3 border border-slate-900 font-mono text-[11px] text-slate-300 space-y-1.5 overflow-y-auto max-h-[220px]">
                    <div class="text-slate-500">[00:00:01] Sistema de Hyperloop MHD+SAMS inicializado.</div>
                    <div class="text-cyan-400">[00:00:03] Propulsão magnética acelerando a Mach 2.0.</div>
                    <div class="text-emerald-400">[00:00:05] Suspensão SAMS ativa: anulação de tremores milimétricos em tempo real.</div>
                </div>
            </div>

        </section>

    </main>

    <!-- Footer -->
    <footer class="text-center py-4 text-xs text-slate-500 border-t border-slate-900 font-mono">
        MHD (Magnetohydrodynamic) & SAMS (Smart Active Micro-Vibration Suppression) &bull; Logística Continental Supersônica v2.4
    </footer>

    <!-- JavaScript Simulation Engine -->
    <script>
        // --- Simulation State ---
        let state = {
            scenario: 'cruise', // 'cruise', 'imperfection', 'freight'
            samsActive: true,
            trainSpeed: 2450, // km/h
            time: 0,
            bumpActive: false,
            bumpTimer: 0,
            trackOffset: 0
        };

        // DOM Elements
        const canvas = document.getElementById('simCanvas');
        const ctx = canvas.getContext('2d');
        const samsToggleEl = document.getElementById('samsToggle');
        const sysBadgeEl = document.getElementById('sys-badge');
        const bumpBannerEl = document.getElementById('bump-banner');
        const hudMachEl = document.getElementById('hud-mach');
        const hudGEl = document.getElementById('hud-g');
        const metricStabilityEl = document.getElementById('metric-stability');
        const aiConsole = document.getElementById('ai-console');

        // Audio Helper
        let audioCtx = null;
        function initAudio() {
            if (!audioCtx) audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        }

        function playBeep(freq = 440, type = 'sine', duration = 0.1) {
            try {
                initAudio();
                if (!audioCtx) return;
                const osc = audioCtx.createOscillator();
                const gain = audioCtx.createGain();
                osc.type = type;
                osc.frequency.value = freq;
                gain.gain.setValueAtTime(0.04, audioCtx.currentTime);
                gain.gain.exponentialRampToValueAtTime(0.0001, audioCtx.currentTime + duration);
                osc.connect(gain);
                gain.connect(audioCtx.destination);
                osc.start();
                osc.stop(audioCtx.currentTime + duration);
            } catch (e) {}
        }

        // Resize Canvas
        function resizeCanvas() {
            const rect = canvas.getBoundingClientRect();
            canvas.width = rect.width * window.devicePixelRatio;
            canvas.height = rect.height * window.devicePixelRatio;
            ctx.setTransform(window.devicePixelRatio, 0, 0, window.devicePixelRatio, 0, 0);
        }

        window.addEventListener('resize', resizeCanvas);

        // Control Handlers
        function setScenario(scen) {
            state.scenario = scen;
            ['cruise', 'imperfection', 'freight'].forEach(s => {
                const btn = document.getElementById(`scen-${s}`);
                if (s === scen) {
                    btn.className = "w-full text-left p-3 rounded-xl border border-cyan-500/40 bg-cyan-500/10 transition-all flex items-center justify-between group";
                } else {
                    btn.className = "w-full text-left p-3 rounded-xl border border-slate-700 bg-slate-900/60 transition-all hover:border-slate-500 flex items-center justify-between group";
                }
            });

            if (scen === 'imperfection') {
                triggerRailBump();
            } else if (scen === 'freight') {
                logAI("Cenário de Carga Sensível ativado. SAMS configurado com rigidez hiper-amortecida.");
                playBeep(520, 'triangle', 0.15);
            } else {
                logAI("Cenário de Cruzeiro Supersônico (Mach 2.0) ativado.");
                playBeep(440, 'sine', 0.1);
            }
        }

        function toggleSAMS() {
            state.samsActive = samsToggleEl.checked;
            if (state.samsActive) {
                sysBadgeEl.textContent = "ATIVO";
                sysBadgeEl.className = "px-2.5 py-0.5 rounded text-xs font-mono font-bold bg-cyan-500/20 text-cyan-300 border border-cyan-500/40";
                bumpBannerEl.classList.add('hidden');
                logAI("SAMS reativado: Suspensão piezoelétrica pronta para anular desníveis.");
                playBeep(880, 'sine', 0.2);
            } else {
                sysBadgeEl.textContent = "VULNERÁVEL";
                sysBadgeEl.className = "px-2.5 py-0.5 rounded text-xs font-mono font-bold bg-rose-500/20 text-rose-300 border border-rose-500/40";
                logAI("ALERTA: SAMS desativado! Passageiros e carga sentirão todos os solavancos dos trilhos.");
                playBeep(180, 'sawtooth', 0.3);
            }
        }

        function updateSpeed(val) {
            state.trainSpeed = parseInt(val);
            document.getElementById('speed-val').textContent = val + ' km/h';
            const mach = (val / 1225).toFixed(1);
            hudMachEl.textContent = `Mach ${mach}`;
        }

        function triggerRailBump() {
            state.bumpActive = true;
            state.bumpTimer = 60;
            bumpBannerEl.classList.remove('hidden');

            if (state.samsActive) {
                logAI("⚡ Imperfeição milimétrica no trilho! SAMS ajustou a suspensão magnética em 0.3ms. Cabine sem vibração.");
                playBeep(1200, 'square', 0.25);
            } else {
                logAI("💥 IMPACTO! Sem SAMS, o trem sofreu solavanco severo e oscilação G-Force na carga!");
                playBeep(150, 'sawtooth', 0.4);
            }

            setTimeout(() => {
                bumpBannerEl.classList.add('hidden');
                state.bumpActive = false;
            }, 2500);
        }

        function recalibrateSAMS() {
            logAI("🔄 Sensores piezoelétricos SAMS recalibrados. Resposta milimétrica em tempo real.");
            playBeep(750, 'sine', 0.2);
        }

        function logAI(message) {
            const timeStr = new Date().toTimeString().split(' ')[0];
            const div = document.createElement('div');
            div.className = "text-slate-300";
            div.innerHTML = `<span class="text-slate-500">[${timeStr}]</span> ${message}`;
            aiConsole.appendChild(div);
            aiConsole.scrollTop = aiConsole.scrollHeight;
        }

        // --- Main Animation & Simulation Loop ---
        function updateSimulation() {
            state.time += 0.04;
            state.trackOffset += (state.trainSpeed / 100);
            if (state.trackOffset > 1000) state.trackOffset = 0;

            drawCanvas();
            requestAnimationFrame(updateSimulation);
        }

        function drawCanvas() {
            const width = canvas.clientWidth;
            const height = canvas.clientHeight;
            
            ctx.clearRect(0, 0, width, height);

            // Draw Vacuum Tunnel tube interior
            const centerY = height / 2;
            const tubeRadius = 120;

            // Tunnel background gradient
            const bgGrad = ctx.createLinearGradient(0, centerY - tubeRadius, 0, centerY + tubeRadius);
            bgGrad.addColorStop(0, '#020617');
            bgGrad.addColorStop(0.5, '#091326');
            bgGrad.addColorStop(1, '#020617');
            ctx.fillStyle = bgGrad;
            ctx.fillRect(0, centerY - tubeRadius, width, tubeRadius * 2);

            // Tunnel metallic rings & glowing vacuum seal
            ctx.strokeStyle = 'rgba(6, 182, 212, 0.3)';
            ctx.lineWidth = 3;
            ctx.beginPath();
            ctx.arc(width / 2, centerY, tubeRadius, 0, Math.PI * 2);
            ctx.stroke();

            // Parallax landscape flying by outside transparent tube segments
            ctx.strokeStyle = 'rgba(16, 185, 129, 0.4)';
            ctx.lineWidth = 2;
            ctx.beginPath();
            ctx.moveTo(0, centerY + tubeRadius + 15);
            ctx.lineTo(width, centerY + tubeRadius + 15);
            ctx.stroke();

            // Magnetic levitation track line inside tube
            ctx.strokeStyle = '#8b5cf6';
            ctx.lineWidth = 4;
            ctx.beginPath();
            ctx.moveTo(0, centerY + 65);
            ctx.lineTo(width, centerY + 65);
            ctx.stroke();

            // Draw track imperfection bump if active
            let bumpOffsetY = 0;
            let cabinBumpY = 0;

            if (state.bumpActive) {
                bumpOffsetY = -12; // track goes up slightly
                if (!state.samsActive) {
                    cabinBumpY = Math.sin(state.time * 30) * 18; // violent bounce
                }
            }

            // Draw Hyperloop Train Pod in the center
            const trainWidth = 220;
            const trainHeight = 65;
            const trainX = width / 2 - trainWidth / 2;
            const trainY = centerY - 10 + cabinBumpY;

            ctx.save();
            // Train Pod body
            ctx.fillStyle = '#0f172a';
            ctx.strokeStyle = state.samsActive ? '#06b6d4' : '#f43f5e';
            ctx.lineWidth = 3;
            
            ctx.beginPath();
            ctx.roundRect(trainX, trainY, trainWidth, trainHeight, [18]);
            ctx.fill();
            ctx.stroke();

            // Aerodynamic nose cone gradient
            const noseGrad = ctx.createLinearGradient(trainX, trainY, trainX + 60, trainY);
            noseGrad.addColorStop(0, '#06b6d4');
            noseGrad.addColorStop(1, '#0f172a');
            ctx.fillStyle = noseGrad;
            ctx.beginPath();
            ctx.roundRect(trainX, trainY, 60, trainHeight, [18, 0, 0, 18]);
            ctx.fill();

            // Windows / Cargo Bay Lights
            ctx.fillStyle = 'rgba(6, 182, 212, 0.6)';
            for (let wx = trainX + 75; wx < trainX + trainWidth - 30; wx += 35) {
                ctx.fillRect(wx, trainY + 18, 20, 24);
            }

            // Magnetic levitation flux field underneath
            ctx.strokeStyle = state.samsActive ? 'rgba(16, 185, 129, 0.8)' : 'rgba(244, 63, 94, 0.8)';
            ctx.lineWidth = 2;
            ctx.beginPath();
            ctx.moveTo(trainX + 30, trainY + trainHeight);
            ctx.lineTo(trainX + trainWidth - 30, trainY + trainHeight);
            ctx.stroke();

            // SAMS active damping suspension nodes
            if (state.samsActive) {
                ctx.fillStyle = '#10b981';
                ctx.beginPath();
                ctx.arc(trainX + 50, trainY + trainHeight, 4, 0, Math.PI * 2);
                ctx.arc(trainX + trainWidth - 50, trainY + trainHeight, 4, 0, Math.PI * 2);
                ctx.fill();
            }

            ctx.restore();

            // Update UI telemetry badges dynamically
            const machVal = (state.trainSpeed / 1225).toFixed(1);
            hudMachEl.textContent = `Mach ${machVal}`;

            if (state.bumpActive && !state.samsActive) {
                metricStabilityEl.textContent = "42.5% (Instável!)";
                metricStabilityEl.className = "text-sm font-bold text-rose-400";
                hudGEl.textContent = "+2.44 G";
                hudGEl.className = "text-rose-400 font-bold";
            } else if (state.bumpActive && state.samsActive) {
                metricStabilityEl.textContent = "100.0% (Corrigido)";
                metricStabilityEl.className = "text-sm font-bold text-emerald-400";
                hudGEl.textContent = "0.00 G";
                hudGEl.className = "text-emerald-400 font-bold";
            } else {
                metricStabilityEl.textContent = "100.0%";
                metricStabilityEl.className = "text-sm font-bold text-emerald-400";
                hudGEl.textContent = "0.00 G";
                hudGEl.className = "text-emerald-400 font-bold";
            }
        }

        // Initialize on load
        window.onload = function() {
            resizeCanvas();
            updateSimulation();
        };
    </script>
</body>
</html>
