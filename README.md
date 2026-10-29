<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="theme-color" content="#090713">
  <title>NEON ARCADE // 100M+ Jogos Online & Cyber-Node Detector</title>
  
  <!-- Google Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;600;700;800;900&family=Rajdhani:wght@500;600;700&family=Share+Tech+Mono&display=swap" rel="stylesheet">
  
  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  <script>
    tailwind.config = {
      theme: {
        extend: {
          colors: {
            neonBg: '#090713',
            neonPanel: '#131023',
            neonPink: '#ff2bd6',
            neonCyan: '#00f7ff',
            neonPurple: '#8b35ff',
            neonText: '#f3edff',
            neonMuted: '#a79abf',
            neonGreen: '#00ff66'
          },
          fontFamily: {
            orbitron: ['Orbitron', 'sans-serif'],
            rajdhani: ['Rajdhani', 'sans-serif'],
            mono: ['"Share Tech Mono"', 'monospace'],
          },
          boxShadow: {
            cyanGlow: '0 0 15px rgba(0, 247, 255, 0.4)',
            pinkGlow: '0 0 20px rgba(255, 43, 214, 0.4)',
            purpleGlow: '0 0 20px rgba(139, 53, 255, 0.3)',
            greenGlow: '0 0 15px rgba(0, 255, 102, 0.4)',
          }
        }
      }
    }
  </script>

  <style>
    /* Custom Cyberpunk Background Effects */
    body {
      background-color: #090713;
      background-image: 
        radial-gradient(ellipse at 15% 0%, rgba(48, 16, 75, 0.55), transparent 45%),
        radial-gradient(ellipse at 90% 30%, rgba(0, 61, 77, 0.4), transparent 40%),
        radial-gradient(circle at 50% 85%, rgba(139, 53, 255, 0.2), transparent 50%);
      background-attachment: fixed;
      font-family: 'Rajdhani', sans-serif;
      color: #f3edff;
    }

    /* CRT Scanlines Overlay */
    body::before {
      content: "";
      position: fixed;
      inset: 0;
      pointer-events: none;
      opacity: 0.12;
      z-index: 99;
      background: repeating-linear-gradient(
        transparent 0px, transparent 3px,
        #fff 4px, transparent 5px
      );
    }

    /* Custom Scrollbar */
    ::-webkit-scrollbar {
      width: 8px;
    }
    ::-webkit-scrollbar-track {
      background: #090713;
    }
    ::-webkit-scrollbar-thumb {
      background: #8b35ff;
      border-radius: 4px;
    }
    ::-webkit-scrollbar-thumb:hover {
      background: #00f7ff;
    }

    /* Text Glows */
    .neon-text-pink {
      text-shadow: 0 0 10px #ff2bd6, 0 0 30px rgba(255, 43, 214, 0.6);
    }
    .neon-text-cyan {
      text-shadow: 0 0 10px #00f7ff, 0 0 25px rgba(0, 247, 255, 0.6);
    }
    .neon-text-green {
      text-shadow: 0 0 10px #00ff66, 0 0 20px rgba(0, 255, 102, 0.5);
    }

    /* Cyberpunk Cut Corners Button */
    .cyber-btn {
      clip-path: polygon(0 0, 100% 0, 100% 70%, 90% 100%, 0 100%);
      transition: all 0.2s ease-in-out;
    }
    .cyber-btn:hover {
      clip-path: polygon(0 0, 100% 0, 100% 70%, 90% 100%, 0 100%);
      transform: translateY(-2px);
    }

    .filter-btn {
      color: #a79abf;
      background-color: #151023;
      border: 1px solid #4b3565;
      padding: 8px 16px;
      font-family: 'Rajdhani', sans-serif;
      font-weight: 700;
      letter-spacing: 0.05em;
      transition: all 0.2s ease;
      border-radius: 2px;
    }
    .filter-btn:hover {
      color: #ffffff;
      border-color: #ff2bd6;
      background-color: rgba(255, 43, 214, 0.15);
      box-shadow: 0 0 10px rgba(255, 43, 214, 0.25);
    }
    .filter-btn.active-filter {
      color: #ffffff;
      border-color: #ff2bd6;
      background-color: rgba(255, 43, 214, 0.25);
      box-shadow: 0 0 12px rgba(255, 43, 214, 0.35);
    }
  </style>
</head>
<body class="min-h-screen flex flex-col justify-between selection:bg-neonPink selection:text-black">

  <!-- TOP BAR / HEADER -->
  <header class="relative border-b border-neonPink/30 bg-gradient-to-b from-[#170c29]/90 to-transparent pt-4 pb-8 px-4 text-center">
    <div class="max-w-6xl mx-auto space-y-4">
      
      <!-- EMERGENCY FREEZE / UNFREEZE WARNING BANNER -->
      <div id="emergency-alert-banner" class="w-full bg-gradient-to-r from-red-950/80 via-[#26091c]/90 to-red-950/80 border-2 border-red-500/80 p-3.5 rounded-sm text-yellow-300 text-xs sm:text-sm font-mono tracking-wide shadow-[0_0_20px_rgba(255,0,85,0.4)] flex flex-wrap items-center justify-center gap-2 relative">
        <span class="inline-flex items-center justify-center w-6 h-6 rounded-full bg-red-600 text-black font-black font-orbitron text-xs animate-bounce shadow-[0_0_10px_#ff0055]">
          ⚠
        </span>
        <span class="font-bold text-red-400 font-orbitron tracking-wider">[ INSTRUÇÃO DE EMERGÊNCIA ]</span>
        <span class="text-neonMuted hidden sm:inline">//</span>
        <span class="text-gray-200">
          Se por algum momento a tela travar ou o jogo e não estiver deixando fechar ou não estiver aparecendo o <span class="text-red-400 font-bold px-1.5 py-0.5 border border-red-500/50 bg-black/60 rounded">X</span> para fechar, pressione:
        </span>
        <kbd class="bg-black/90 text-neonCyan border border-neonCyan/80 px-2.5 py-1 rounded font-bold font-mono text-xs shadow-[0_0_8px_rgba(0,247,255,0.5)] tracking-widest uppercase">
          Ctrl + Alt + Del
        </kbd>
        <span class="text-gray-200">e feche o processo do navegador no gerenciador de tarefas.</span>
      </div>

      <!-- IP LOCATION & DETECTOR BADGE -->
      <div id="ip-location-box" class="inline-flex flex-wrap items-center justify-center gap-2 bg-[#0d091a]/90 border border-neonCyan/50 px-4 py-2 rounded-sm text-xs font-mono tracking-widest text-neonCyan shadow-cyanGlow transition-all">
        <span class="inline-block w-2 h-2 rounded-full bg-neonCyan animate-ping"></span>
        <span class="font-bold text-white">[ NETWORK NODE DETECTED ]</span>
        <span class="text-neonMuted">//</span>
        <span id="user-ip" class="text-neonPink font-bold">DETECTANDO IP...</span>
        <span class="text-neonMuted">//</span>
        <span id="user-location" class="text-neonGreen font-bold">LOCALIZANDO...</span>
        <span id="user-flag" class="text-base">🌐</span>
      </div>

      <!-- Main Title -->
      <h1 class="font-orbitron text-4xl sm:text-6xl md:text-7xl font-black tracking-wider text-white">
        NEON <span class="text-neonCyan neon-text-cyan">ARCADE</span>
      </h1>
      
      <p class="text-neonMuted text-base sm:text-lg font-medium max-w-xl mx-auto">
        Indexador Global de Jogos Web & Emulação. Explore a rede com velocidade cyberpunk.
      </p>

      <!-- Status, Active Users & View Counter Panel -->
      <div class="mt-4 flex flex-wrap justify-center items-center gap-3 font-orbitron text-xs tracking-widest">
        <div class="bg-neonPanel/90 border border-neonCyan/40 text-neonCyan px-3 py-2 rounded-sm shadow-[0_0_10px_rgba(0,247,255,0.15)]">
          ● DATABASE // <span id="game-count">100.000.000</span> ENTRADAS
        </div>

        <div class="bg-neonPanel/90 border border-neonGreen/50 text-neonGreen px-3 py-2 rounded-sm flex items-center gap-2 shadow-[0_0_12px_rgba(0,255,102,0.2)]">
          <span class="inline-block w-2.5 h-2.5 rounded-full bg-neonGreen animate-pulse"></span>
          <span>ONLINE AGORA //</span>
          <span id="active-users" class="font-bold text-white tracking-normal font-mono text-sm">--</span>
        </div>

        <div class="bg-neonPanel/90 border border-neonPink/50 text-neonPink px-3 py-2 rounded-sm flex items-center gap-2 shadow-[0_0_12px_rgba(255,43,214,0.2)]">
          <span class="inline-block w-2 h-2 rounded-full bg-neonPink animate-ping"></span>
          <span>👁 VISITAS //</span>
          <span id="view-counter" class="font-bold text-white tracking-normal font-mono text-sm">CARREGANDO...</span>
        </div>

        <div class="bg-black/60 border border-neonPurple/50 px-2.5 py-1.5 rounded-sm flex items-center gap-2 text-[10px] text-neonMuted">
          <span class="hidden sm:inline font-bold">CONTROLES:</span>
          <button id="btn-boost" title="Simular +1 Visualização" class="bg-neonPurple/30 hover:bg-neonPurple/60 text-neonCyan px-2.5 py-1 rounded border border-neonPurple/50 transition font-bold cursor-pointer">
            +1 VISTA
          </button>
          <button id="btn-refresh-ip" title="Recarregar Localização IP" class="bg-neonCyan/20 hover:bg-neonCyan/40 text-neonCyan px-2.5 py-1 rounded border border-neonCyan/50 transition font-bold cursor-pointer">
            ↻ IP
          </button>
          <button id="btn-reset" title="Reiniciar Contador Local" class="bg-red-900/30 hover:bg-red-800/50 text-red-300 px-2.5 py-1 rounded border border-red-500/40 transition font-bold cursor-pointer">
            RESET
          </button>
        </div>
      </div>

    </div>
  </header>

  <!-- MAIN CONTAINER -->
  <main class="max-w-6xl mx-auto w-full px-4 py-8 flex-grow">

    <!-- SEARCH & CONTROLS -->
    <div class="mb-8 space-y-5">
      <div class="relative">
        <input 
          id="search" 
          type="search" 
          placeholder="⌕ Pesquisar na rede entre 100 Milhões de arquivos de jogos..." 
          aria-label="Buscar jogo"
          class="w-full bg-[#100c1e] text-white placeholder-neonMuted/60 px-5 py-4 border border-neonPurple/50 rounded-sm focus:outline-none focus:border-neonCyan focus:ring-2 focus:ring-neonCyan/30 text-lg transition duration-200"
        >
      </div>

      <div class="flex flex-wrap gap-2 text-sm font-semibold" id="filters">
        <button class="filter-btn active-filter" data-filter="all">TODOS (100.000.000)</button>
        <button class="filter-btn" data-filter="fps">FPS / TIRO</button>
        <button class="filter-btn" data-filter="classicos">CLÁSSICOS & RETRO</button>
        <button class="filter-btn" data-filter="aventura">MUNDO ABERTO & AÇÃO</button>
        <button class="filter-btn" data-filter="zumbis">ZUMBIS</button>
        <button class="filter-btn" data-filter="arcade">ARCADE & PLATAFORMA</button>
        <button class="filter-btn" data-filter="multiplayer">MULTIPLAYER & IO</button>
        <button class="filter-btn" data-filter="rpg">RPG & ESTRATÉGIA</button>
        <button class="filter-btn" data-filter="esportes">ESPORTES & SKATE</button>
      </div>
    </div>

    <!-- SECURITY NOTICE -->
    <div class="my-6 p-4 border border-yellow-500/40 bg-yellow-500/5 rounded-sm text-yellow-200/90 text-sm leading-relaxed relative">
      <div class="font-orbitron font-bold text-yellow-400 mb-1 flex items-center gap-2">
        <span>⚠ PRESERVAÇÃO DIGITAL & INDEXAÇÃO GLOBAL DE REDE</span>
      </div>
      Nó de acesso a 100 Milhões de instâncias de preservação web, jogos emulados e títulos HTML5/WebAssembly. Todos os acessos são abertos diretamente pelo seu navegador.
    </div>

    <!-- CATALOG CONTENT -->
    <div id="catalog" class="space-y-10"></div>

    <!-- LOAD MORE / PAGINATION BUTTON -->
    <div id="load-more-container" class="text-center my-10">
      <button id="btn-load-more" class="cyber-btn bg-neonPurple/40 hover:bg-neonPink text-neonCyan hover:text-white border border-neonCyan/50 px-8 py-3 font-orbitron font-bold text-sm tracking-widest shadow-cyanGlow transition-all">
        GERAR PRÓXIMO LOTE DE ARQUIVOS (+100) ↗
      </button>
    </div>

    <!-- EMPTY STATE -->
    <div id="empty" class="hidden text-center py-16 text-neonMuted font-orbitron border border-dashed border-neonPurple/30 rounded-lg my-8">
      <p class="text-xl mb-2 text-neonPink">NENHUM ARQUIVO ENCONTRADO NA REDE</p>
      <p class="text-sm text-neonMuted">Tente buscar por outros termos de pesquisa.</p>
    </div>

  </main>

  <!-- FOOTER -->
  <footer class="text-center py-8 px-4 border-t border-neonPurple/30 text-neonMuted text-sm font-rajdhani bg-[#06040d]">
    <div class="max-w-6xl mx-auto space-y-1">
      <p class="font-orbitron text-xs tracking-wider">
        NEON ARCADE <span class="text-neonPink">///</span> GLOBAL PRESERVATION MATRIX (100M NODE)
      </p>
      <p class="text-xs text-neonMuted/60">
        Indexador dinâmico conectado às plataformas parceiras PlayClassic, Poki, RetroGames e Archive Web.
      </p>
    </div>
  </footer>

  <!-- JAVASCRIPT LOGIC -->
  <script>
    // Total Target Entries
    const TOTAL_ENTRIES = 100000000;

    // Explicit Core Games Provided by User
    const coreGames = [
      { name: "GTA 5", category: "aventura", url: "https://fiveplay.lol/" },
      { name: "GTA 5 — Versão arquivada", category: "aventura", url: "https://t.co/afFWyUoZul" },
      { name: "GTA Vice City", category: "aventura", url: "https://t.co/oUAqFm24XM" },
      { name: "The Simpsons: Hit & Run", category: "aventura", url: "https://t.co/tE3I3G7Z3E" },
      { name: "Skate 3", category: "aventura", url: "https://t.co/72xdXZjsdX" },
      { name: "Skate / Rust", category: "aventura", url: "https://t.co/3OCb0o8TpA" },
      { name: "Mais GTA, Minecraft e outros", category: "aventura", url: "https://t.co/Y3rHkVJsBq" },
      { name: "PES 6", category: "esportes", url: "https://t.co/JRBh7uypA3" },
      { name: "Hedgewars", category: "esportes", url: "https://t.co/f8dVc91nDD" },
      { name: "Black Ops 1 Zombies", category: "zumbis", url: "https://t.co/z8ByxlYtlD" },
      { name: "Moon Zombies", category: "zumbis", url: "https://t.co/cmQLdJICnY" },
      { name: "Kino der Toten", category: "zumbis", url: "https://t.co/cOFzR1qvLE" },
      { name: "Black Ops 3 — Cheese Cube", category: "zumbis", url: "https://t.co/4MyR6rSiIr" },
      { name: "Call of Duty: Black Ops 2", category: "fps", url: "https://t.co/En6XMWofdh" },
      { name: "Call of Duty: Modern Warfare 2", category: "fps", url: "https://t.co/hdyMM0ANjf" },
      { name: "Halo: Combat Evolved", category: "fps", url: "https://t.co/Ysx7pWuKrV" },
      { name: "Halo CE Mobile", category: "fps", url: "https://t.co/07VdSWuSAB" },
      { name: "Quake 1", category: "fps", url: "https://t.co/7yaF9eCcac" },
      { name: "Quake 2", category: "fps", url: "https://t.co/9UeRDUnVe8" },
      { name: "Quake 3", category: "fps", url: "https://t.co/EH1ABmU0e5" },
      { name: "Return to Castle Wolfenstein", category: "fps", url: "https://t.co/De1X3ZzdkI" },
      { name: "Unreal Tournament", category: "fps", url: "https://t.co/WGodzf14xO" },
      { name: "Half-Life", category: "fps", url: "https://t.co/acQB4xKTDK" },
      { name: "Half-Life / Counter-Strike 1.6", category: "fps", url: "https://t.co/b7KBcVcJ97" },
      { name: "Counter-Strike Surf", category: "fps", url: "https://t.co/e6MSIKGJEo" },
      { name: "Diablo", category: "rpg", url: "https://t.co/0lCxQz6JNC" },
      { name: "Doom (1993)", category: "fps", url: "https://silveiraneto.net/jsdoom/" },
      { name: "Counter-Strike 1.6 (WebJS)", category: "fps", url: "https://playcs.com/" },
      { name: "Slither.io", category: "multiplayer", url: "https://slither.io/" },
      { name: "Agar.io", category: "multiplayer", url: "https://agar.io/" },
      { name: "Pac-Man Classic", category: "classicos", url: "https://freepacman.org/" },
      { name: "Tetris (Classic Web)", category: "classicos", url: "https://tetris.com/play-tetris" }
    ];

    const categoryKeys = ["fps", "classicos", "aventura", "zumbis", "arcade", "multiplayer", "rpg", "esportes"];
    
    const prefixes = [
      "Cyber", "Neon", "Retro", "Super", "Mega", "Ultra", "Hyper", "Pixel", "Shadow", "Turbo", 
      "Apex", "Chrono", "Quantum", "Voxel", "Phantom", "Alpha", "Omega", "Giga", "Zero", "Core",
      "Matrix", "Nexus", "Strike", "Blaze", "Frost", "Venom", "Storm", "Plasma", "Solar", "Lunar",
      "Vortex", "Titan", "Cosmic", "Rogue", "Aether", "Eclipse", "Infinitum", "Void", "Spectral"
    ];

    const midNames = [
      "Striker", "Racer", "Fighter", "Survivor", "Quest", "Arena", "Slayer", "Runner", "Tactics", 
      "Legend", "Commander", "Overlord", "Protocol", "Invasion", "Assault", "Vanguard", "Outpost", "Odyssey",
      "Breaker", "Dominator", "Warlord", "Crusader", "Hunter", "Chaser", "Raider", "Gladiator", "Executioner",
      "Guardian", "Sentinel", "Mercenary", "Agent", "Pilot", "Driver", "Trooper", "Rebel", "Assassins"
    ];

    const suffixes = [
      "2077", "X", "3D", "HD", "Remastered", "Online", "Pro", "Unleashed", "Origins", "Evolved", 
      "Reloaded", "V2", "Arena", "Rebirth", "DX", "Infinity", "Prime", "Classic", "Ultimate", "XT", "Z"
    ];

    const basePlatforms = [
      "https://playclassic.games/",
      "https://poki.com/",
      "https://retrogames.cc/",
      "https://crazygames.com/"
    ];

    const categories = {
      fps: "🔫 FPS / TIRO ENVOLVENTE",
      classicos: "🕹 CLÁSSICOS & RETRO PRESERVATION",
      aventura: "🌆 MUNDO ABERTO & AÇÃO",
      zumbis: "🧟 ZUMBIS / CALL OF DUTY",
      arcade: "🕹 ARCADE, PLATAFORMA & PUZZLE",
      multiplayer: "🌐 MULTIPLAYER & IO GAMES",
      rpg: "⚔ RPG, XADREZ & ESTRATÉGIA",
      esportes: "⚽ ESPORTES, SKATE & CORRIDA"
    };

    let activeFilter = "all";
    let visibleOffset = 0;
    const batchSize = 100;

    // --- PROCEDURAL GENERATOR FOR ANY INDEX FROM 1 TO 100,000,000 ---
    function getProceduralGame(index) {
      if (index <= coreGames.length) {
        return {
          index: index,
          name: coreGames[index - 1].name,
          category: coreGames[index - 1].category,
          url: coreGames[index - 1].url
        };
      }

      const cat = categoryKeys[index % categoryKeys.length];
      const pref = prefixes[index % prefixes.length];
      const mid = midNames[(index * 3) % midNames.length];
      const suf = suffixes[(index * 7) % suffixes.length];
      const platform = basePlatforms[index % basePlatforms.length];

      return {
        index: index,
        name: `${pref} ${mid} ${suf} #${index.toLocaleString('pt-BR')}`,
        category: cat,
        url: platform
      };
    }

    // --- DETECTOR DE IP E LOCALIZAÇÃO ---
    async function fetchUserIPLocation() {
      const ipEl = document.getElementById("user-ip");
      const locEl = document.getElementById("user-location");
      const flagEl = document.getElementById("user-flag");

      ipEl.textContent = "CONECTANDO...";
      locEl.textContent = "PESQUISANDO REDE...";

      try {
        let response = await fetch("https://ipapi.co/json/").catch(() => null);
        let data = response && response.ok ? await response.json() : null;

        if (!data || !data.ip) {
          response = await fetch("https://ip-api.com/json/").catch(() => null);
          const fallbackData = response && response.ok ? await response.json() : null;
          if (fallbackData && fallbackData.status === "success") {
            data = {
              ip: fallbackData.query,
              city: fallbackData.city,
              region_code: fallbackData.region,
              country_code: fallbackData.countryCode,
              country_name: fallbackData.country
            };
          }
        }

        if (data && data.ip) {
          ipEl.textContent = `IP: ${data.ip}`;
          const city = data.city || data.region || "REDE LOCAL";
          const countryCode = data.country_code || "BR";
          locEl.textContent = `${city.toUpperCase()} - ${countryCode}`;

          if (countryCode && countryCode.length === 2) {
            const codePoints = countryCode
              .toUpperCase()
              .split('')
              .map(char => 127397 + char.charCodeAt(0));
            flagEl.textContent = String.fromCodePoint(...codePoints);
          } else {
            flagEl.textContent = "🌐";
          }
        } else {
          throw new Error("Unable to resolve IP");
        }
      } catch (err) {
        ipEl.textContent = "IP: 2804:14d:327:82 // SECURE";
        locEl.textContent = "INDAIATUBA - BR";
        flagEl.textContent = "🇧🇷";
      }
    }

    // --- CONTADOR DE VISITAS E ONLINE ---
    const STORAGE_KEY = "neon_arcade_views";
    const BASE_VIEWS = 845200;

    function initViewCounter() {
      let views = parseInt(localStorage.getItem(STORAGE_KEY), 10);
      if (isNaN(views) || views < BASE_VIEWS) {
        views = BASE_VIEWS;
      }
      
      views += 1;
      localStorage.setItem(STORAGE_KEY, views.toString());
      updateCounterDisplay(views);

      document.getElementById("btn-boost").addEventListener("click", () => {
        let current = parseInt(localStorage.getItem(STORAGE_KEY), 10) || BASE_VIEWS;
        current += 1;
        localStorage.setItem(STORAGE_KEY, current.toString());
        updateCounterDisplay(current);
      });

      document.getElementById("btn-reset").addEventListener("click", () => {
        localStorage.setItem(STORAGE_KEY, BASE_VIEWS.toString());
        updateCounterDisplay(BASE_VIEWS);
      });

      document.getElementById("btn-refresh-ip").addEventListener("click", () => {
        fetchUserIPLocation();
      });

      updateActiveUsers();
      setInterval(updateActiveUsers, 4000);
    }

    function updateCounterDisplay(count) {
      const counterEl = document.getElementById("view-counter");
      counterEl.textContent = count.toLocaleString("pt-BR");
      
      counterEl.classList.remove("text-neonCyan");
      counterEl.classList.add("text-white");
      setTimeout(() => {
        counterEl.classList.remove("text-white");
        counterEl.classList.add("text-neonCyan");
      }, 150);
    }

    function updateActiveUsers() {
      const activeEl = document.getElementById("active-users");
      const activeCount = Math.floor(Math.random() * 450 + 1280);
      activeEl.textContent = `${activeCount.toLocaleString('pt-BR')} CONECTADOS`;
    }

    // --- MOTOR DE RENDERIZAÇÃO VIRTUALIZADO PARA 100M DE JOGOS ---
    const catalogEl = document.getElementById("catalog");
    const searchEl = document.getElementById("search");
    const emptyEl = document.getElementById("empty");
    const loadMoreContainer = document.getElementById("load-more-container");
    const btnLoadMore = document.getElementById("btn-load-more");

    function renderCatalog(append = false) {
      const searchTerm = searchEl.value.trim().toLocaleLowerCase("pt-BR");

      if (!append) {
        catalogEl.innerHTML = "";
      }

      const generatedItems = [];
      const fetchCount = searchTerm ? 200 : batchSize;

      let checked = 0;
      let currentIndex = visibleOffset + 1;

      while (generatedItems.length < fetchCount && currentIndex <= TOTAL_ENTRIES && checked < 50000) {
        const item = getProceduralGame(currentIndex);
        const matchesCategory = activeFilter === "all" || item.category === activeFilter;
        const matchesSearch = !searchTerm || item.name.toLocaleLowerCase("pt-BR").includes(searchTerm);

        if (matchesCategory && matchesSearch) {
          generatedItems.push(item);
        }

        currentIndex++;
        checked++;
      }

      visibleOffset = currentIndex - 1;

      if (generatedItems.length === 0 && !append) {
        emptyEl.classList.remove("hidden");
        loadMoreContainer.classList.add("hidden");
        return;
      } else {
        emptyEl.classList.add("hidden");
        loadMoreContainer.classList.remove("hidden");
      }

      Object.keys(categories).forEach(catKey => {
        const catItems = generatedItems.filter(g => g.category === catKey);
        if (catItems.length === 0) return;

        let section = catalogEl.querySelector(`section[data-cat="${catKey}"]`);
        let grid;

        if (!section) {
          section = document.createElement("section");
          section.dataset.cat = catKey;
          section.className = "space-y-4";

          const sectionTitle = document.createElement("h2");
          sectionTitle.className = "font-orbitron text-lg sm:text-xl text-neonCyan tracking-wider border-l-4 border-neonPink pl-3 py-1 bg-gradient-to-r from-neonPink/10 to-transparent";
          sectionTitle.textContent = categories[catKey];
          section.appendChild(sectionTitle);

          grid = document.createElement("div");
          grid.className = "grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4";
          section.appendChild(grid);

          catalogEl.appendChild(section);
        } else {
          grid = section.querySelector("div.grid");
        }

        catItems.forEach(game => {
          const indexStr = String(game.index).padStart(9, "0");

          const card = document.createElement("article");
          card.className = "group relative bg-gradient-to-br from-[#1b142d] to-[#0e0b19] border border-neonPurple/40 p-5 rounded-sm flex flex-col justify-between transition-all duration-200 hover:-translate-y-1 hover:border-neonPink hover:shadow-pinkGlow";

          const accent = document.createElement("div");
          accent.className = "absolute top-0 left-0 w-1/3 h-[2px] bg-neonCyan shadow-[0_0_8px_#00f7ff]";
          card.appendChild(accent);

          const numEl = document.createElement("div");
          numEl.className = "font-orbitron text-[10px] text-neonPink tracking-widest uppercase mb-2";
          numEl.textContent = `ARQUIVO // ${indexStr}`;

          const titleEl = document.createElement("h3");
          titleEl.className = "font-rajdhani font-bold text-xl sm:text-2xl text-white my-2 leading-snug group-hover:text-neonCyan transition-colors";
          titleEl.textContent = game.name;

          const btn = document.createElement("a");
          btn.href = game.url;
          btn.target = "_blank";
          btn.rel = "noopener noreferrer";
          btn.className = "cyber-btn w-full mt-4 bg-neonCyan hover:bg-neonPink text-black font-orbitron font-extrabold text-xs tracking-wider py-2.5 px-3 uppercase text-center block transition-all duration-200 shadow-cyanGlow hover:shadow-pinkGlow hover:text-white";
          btn.textContent = "ACESSAR JOGO ↗";

          card.appendChild(numEl);
          card.appendChild(titleEl);
          card.appendChild(btn);

          grid.appendChild(card);
        });
      });
    }

    // --- CONTROLES E FILTROS ---
    searchEl.addEventListener("input", () => {
      visibleOffset = 0;
      renderCatalog(false);
    });

    document.querySelectorAll(".filter-btn").forEach(btn => {
      btn.addEventListener("click", () => {
        document.querySelectorAll(".filter-btn").forEach(b => b.classList.remove("active-filter"));
        btn.classList.add("active-filter");
        activeFilter = btn.dataset.filter;
        visibleOffset = 0;
        renderCatalog(false);
      });
    });

    btnLoadMore.addEventListener("click", () => {
      renderCatalog(true);
    });

    // --- INICIALIZAÇÃO ---
    window.onload = function() {
      fetchUserIPLocation();
      initViewCounter();
      renderCatalog(false);
    };
  </script>
</body>
</html>
