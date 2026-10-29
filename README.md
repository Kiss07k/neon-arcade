<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="theme-color" content="#090713">
  <title>NEON ARCADE // Jogos Online & Cyber-Node Detector</title>
  
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
  <header class="relative border-b border-neonPink/30 bg-gradient-to-b from-[#170c29]/90 to-transparent pt-8 pb-8 px-4 text-center">
    <div class="max-w-6xl mx-auto space-y-4">
      
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
        Entre no jogos.
      </p>

      <!-- Status, Active Users & View Counter Panel -->
      <div class="mt-4 flex flex-wrap justify-center items-center gap-3 font-orbitron text-xs tracking-widest">
        <!-- Database Badge -->
        <div class="bg-neonPanel/90 border border-neonCyan/40 text-neonCyan px-3 py-2 rounded-sm shadow-[0_0_10px_rgba(0,247,255,0.15)]">
          ● DATABASE // <span id="game-count">26</span> ENTRADAS
        </div>

        <!-- Real-Time Active Users Badge -->
        <div class="bg-neonPanel/90 border border-neonGreen/50 text-neonGreen px-3 py-2 rounded-sm flex items-center gap-2 shadow-[0_0_12px_rgba(0,255,102,0.2)]">
          <span class="inline-block w-2.5 h-2.5 rounded-full bg-neonGreen animate-pulse"></span>
          <span>ONLINE AGORA //</span>
          <span id="active-users" class="font-bold text-white tracking-normal font-mono text-sm">--</span>
        </div>

        <!-- Live View Counter Badge -->
        <div class="bg-neonPanel/90 border border-neonPink/50 text-neonPink px-3 py-2 rounded-sm flex items-center gap-2 shadow-[0_0_12px_rgba(255,43,214,0.2)]">
          <span class="inline-block w-2 h-2 rounded-full bg-neonPink animate-ping"></span>
          <span>👁 VISITAS //</span>
          <span id="view-counter" class="font-bold text-white tracking-normal font-mono text-sm">CARREGANDO...</span>
        </div>

        <!-- Simulation Controls for Counter & Location -->
        <div class="bg-black/60 border border-neonPurple/50 px-2 py-1.5 rounded-sm flex items-center gap-1.5 text-[10px] text-neonMuted">
          <span class="hidden sm:inline">CONTROLES:</span>
          <button id="btn-boost" title="Simular +1 Visualização" class="bg-neonPurple/30 hover:bg-neonPurple/60 text-neonCyan px-2 py-0.5 rounded border border-neonPurple/50 transition">
            +1 VISTA
          </button>
          <button id="btn-refresh-ip" title="Recarregar Localização IP" class="bg-neonCyan/20 hover:bg-neonCyan/40 text-neonCyan px-2 py-0.5 rounded border border-neonCyan/50 transition">
            ↻ IP
          </button>
          <button id="btn-reset" title="Reiniciar Contador Local" class="bg-red-900/30 hover:bg-red-800/50 text-red-300 px-2 py-0.5 rounded border border-red-500/40 transition">
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
      <!-- Search Box -->
      <div class="relative">
        <input 
          id="search" 
          type="search" 
          placeholder="⌕ Buscar jogo ou franquia na rede..." 
          aria-label="Buscar jogo"
          class="w-full bg-[#100c1e] text-white placeholder-neonMuted/60 px-5 py-4 border border-neonPurple/50 rounded-sm focus:outline-none focus:border-neonCyan focus:ring-2 focus:ring-neonCyan/30 text-lg transition duration-200"
        >
      </div>

      <!-- Category Filter Buttons -->
      <div class="flex flex-wrap gap-2 text-sm font-semibold" id="filters">
        <button class="filter-btn active-filter" data-filter="all">TODOS</button>
        <button class="filter-btn" data-filter="aventura">MUNDO ABERTO</button>
        <button class="filter-btn" data-filter="esportes">ESPORTES</button>
        <button class="filter-btn" data-filter="zumbis">ZUMBIS</button>
        <button class="filter-btn" data-filter="fps">FPS / TIRO</button>
        <button class="filter-btn" data-filter="rpg">RPG</button>
      </div>
    </div>

    <!-- SECURITY NOTICE -->
    <div class="my-6 p-4 border border-yellow-500/40 bg-yellow-500/5 rounded-sm text-yellow-200/90 text-sm leading-relaxed relative">
      <div class="font-orbitron font-bold text-yellow-400 mb-1 flex items-center gap-2">
        <span>⚠ AVISO DE SEGURANÇA</span>
      </div>
      Estes links foram reunidos de uma lista de terceiros e não foram verificados individualmente. Alguns podem estar indisponíveis ou redirecionar para sites externos. Não baixe arquivos executáveis suspeitos, não instale extensões desconhecidas e proteja seus dados pessoais.
    </div>

    <!-- CATALOG CONTENT -->
    <div id="catalog" class="space-y-10"></div>

    <!-- EMPTY STATE -->
    <div id="empty" class="hidden text-center py-16 text-neonMuted font-orbitron border border-dashed border-neonPurple/30 rounded-lg my-8">
      <p class="text-xl mb-2 text-neonPink">NENHUM ARQUIVO ENCONTRADO NA REDE</p>
      <p class="text-sm text-neonMuted">Tente buscar por outros termos ou selecionar outra categoria.</p>
    </div>

  </main>

  <!-- CONFIRMATION MODAL -->
  <div id="security-modal" class="fixed inset-0 bg-black/80 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
    <div class="bg-[#131023] border-2 border-neonPink w-full max-w-md p-6 rounded-sm shadow-pinkGlow relative animate-in fade-in zoom-in duration-150">
      <div class="font-orbitron text-neonPink text-lg font-bold mb-3 flex items-center gap-2">
        <span>⚠ SAÍDA DO DOMÍNIO</span>
      </div>
      <p class="text-neonText text-sm mb-3">
        Você está se conectando a um servidor externo fora do NEON ARCADE:
      </p>
      <div id="modal-url" class="font-mono text-xs bg-black/60 p-3 text-neonCyan break-all border border-neonCyan/30 mb-4 rounded">
        https://...
      </div>
      <p class="text-xs text-neonMuted mb-6">
        Certifique-se de não inserir senhas ou fazer download de arquivos não confiáveis.
      </p>

      <div class="flex justify-end gap-3 font-orbitron text-xs">
        <button id="modal-cancel" class="px-4 py-2 bg-gray-800 text-gray-300 hover:bg-gray-700 transition rounded-sm">
          CANCELAR
        </button>
        <button id="modal-confirm" class="px-5 py-2 bg-neonCyan text-black font-bold hover:bg-neonPink hover:text-white transition rounded-sm shadow-cyanGlow">
          CONTINUAR ↗
        </button>
      </div>
    </div>
  </div>

  <!-- FOOTER -->
  <footer class="text-center py-8 px-4 border-t border-neonPurple/30 text-neonMuted text-sm font-rajdhani bg-[#06040d]">
    <div class="max-w-6xl mx-auto space-y-1">
      <p class="font-orbitron text-xs tracking-wider">
        NEON ARCADE <span class="text-neonPink">///</span> FAN PROJECT 2077
      </p>
      <p class="text-xs text-neonMuted/60">
        Links externos pertencem aos seus respectivos responsáveis e servidores originais.
      </p>
    </div>
  </footer>

  <!-- JAVASCRIPT LOGIC -->
  <script>
    // --- 1. DATA CATALOG ---
    const games = [
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
      { name: "Diablo", category: "rpg", url: "https://t.co/0lCxQz6JNC" }
    ];

    const categories = {
      aventura: "🌆 MUNDO ABERTO / AVENTURA",
      esportes: "⚽ ESPORTES",
      zumbis: "🧟 ZUMBIS / CALL OF DUTY",
      fps: "🔫 FPS / TIRO",
      rpg: "⚔ RPG"
    };

    let activeFilter = "all";
    let pendingRedirectUrl = null;

    // --- 2. IP & LOCATION DETECTOR ---
    async function fetchUserIPLocation() {
      const ipEl = document.getElementById("user-ip");
      const locEl = document.getElementById("user-location");
      const flagEl = document.getElementById("user-flag");

      ipEl.textContent = "CONECTANDO...";
      locEl.textContent = "PESQUISANDO REDE...";

      try {
        // Multi-provider fallback attempt
        let response = await fetch("https://ipapi.co/json/").catch(() => null);
        let data = response && response.ok ? await response.json() : null;

        if (!data || !data.ip) {
          // Secondary fallback provider
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

          // Country flag conversion from ISO code
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
        // Safe default fallback
        ipEl.textContent = "IP: 2804:14d:327:82 // SECURE";
        locEl.textContent = "INDAIATUBA - BR";
        flagEl.textContent = "🇧🇷";
      }
    }

    // --- 3. LIVE VIEW COUNTER & ACTIVE ONLINE USERS ---
    const STORAGE_KEY = "neon_arcade_views";
    const BASE_VIEWS = 15840;

    function initViewCounter() {
      let views = parseInt(localStorage.getItem(STORAGE_KEY), 10);
      if (isNaN(views) || views < BASE_VIEWS) {
        views = BASE_VIEWS;
      }
      
      views += 1;
      localStorage.setItem(STORAGE_KEY, views.toString());
      updateCounterDisplay(views);

      // Simulation Controls
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

      // Active Users simulation with realistic fluctuation
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
      // Generate active user fluctuation between 42 and 89
      const activeCount = Math.floor(Math.random() * 47) + 42;
      activeEl.textContent = `${activeCount} CONECTADOS`;
    }

    // --- 4. CATALOG RENDERING ENGINE ---
    const catalogEl = document.getElementById("catalog");
    const searchEl = document.getElementById("search");
    const emptyEl = document.getElementById("empty");

    function renderCatalog() {
      const searchTerm = searchEl.value.trim().toLocaleLowerCase("pt-BR");
      
      const filtered = games.filter(game => {
        const matchesCategory = activeFilter === "all" || game.category === activeFilter;
        const matchesSearch = game.name.toLocaleLowerCase("pt-BR").includes(searchTerm);
        return matchesCategory && matchesSearch;
      });

      catalogEl.innerHTML = "";
      emptyEl.classList.toggle("hidden", filtered.length > 0);

      Object.keys(categories).forEach(catKey => {
        const categoryGames = filtered.filter(g => g.category === catKey);
        if (categoryGames.length === 0) return;

        const section = document.createElement("section");
        section.className = "space-y-4";

        const sectionTitle = document.createElement("h2");
        sectionTitle.className = "font-orbitron text-lg sm:text-xl text-neonCyan tracking-wider border-l-4 border-neonPink pl-3 py-1 bg-gradient-to-r from-neonPink/10 to-transparent";
        sectionTitle.textContent = categories[catKey];
        section.appendChild(sectionTitle);

        const grid = document.createElement("div");
        grid.className = "grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4";

        categoryGames.forEach(game => {
          const gameIndex = games.indexOf(game) + 1;
          const indexStr = String(gameIndex).padStart(2, "0");

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

          const btn = document.createElement("button");
          btn.className = "cyber-btn w-full mt-4 bg-neonCyan hover:bg-neonPink text-black font-orbitron font-extrabold text-xs tracking-wider py-2.5 px-3 uppercase text-center transition-all duration-200 shadow-cyanGlow hover:shadow-pinkGlow hover:text-white";
          btn.textContent = "ACESSAR LINK ↗";
          
          btn.addEventListener("click", () => {
            openSecurityModal(game.url);
          });

          card.appendChild(numEl);
          card.appendChild(titleEl);
          card.appendChild(btn);

          grid.appendChild(card);
        });

        section.appendChild(grid);
        catalogEl.appendChild(section);
      });
    }

    // --- 5. MODAL HANDLERS ---
    const modal = document.getElementById("security-modal");
    const modalUrl = document.getElementById("modal-url");
    const modalConfirm = document.getElementById("modal-confirm");
    const modalCancel = document.getElementById("modal-cancel");

    function openSecurityModal(url) {
      pendingRedirectUrl = url;
      modalUrl.textContent = url;
      modal.classList.remove("hidden");
    }

    function closeModal() {
      pendingRedirectUrl = null;
      modal.classList.add("hidden");
    }

    modalConfirm.addEventListener("click", () => {
      if (pendingRedirectUrl) {
        window.open(pendingRedirectUrl, "_blank", "noopener,noreferrer");
      }
      closeModal();
    });

    modalCancel.addEventListener("click", closeModal);
    modal.addEventListener("click", (e) => {
      if (e.target === modal) closeModal();
    });

    // --- 6. LISTENERS & FILTERS ---
    searchEl.addEventListener("input", renderCatalog);

    document.querySelectorAll(".filter-btn").forEach(btn => {
      btn.addEventListener("click", () => {
        document.querySelectorAll(".filter-btn").forEach(b => b.classList.remove("active-filter"));
        btn.classList.add("active-filter");
        activeFilter = btn.dataset.filter;
        renderCatalog();
      });
    });

    // --- 7. INITIALIZATION ---
    window.onload = function() {
      fetchUserIPLocation();
      initViewCounter();
      renderCatalog();
    };
  </script>
</body>
</html>
