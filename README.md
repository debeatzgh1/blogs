<iframe src="https://msha.ke/debeatzgh#links-5" width="100%" height="400" frameborder="0" allowfullscreen></iframe>
  
  
            
        


<div id="firebase-mini-banner" class="firebase-node-mini">
    <div class="mini-content">
        <div class="status-indicator">
            <span class="pulse-dot"></span>
        </div>
        <div class="mini-text">
            <span class="label">Internal Build</span>
            <span class="version">v2.4-stable</span>
        </div>
    </div>
    <button onclick="openFirebaseNode()" class="mini-action-btn">
        <i class="fas fa-download"></i>
    </button>
</div>

<style>
    .firebase-node-mini {
        position: fixed;
        top: 25px;
        left: 25px; /* Positioned left to avoid clashing with the 'Suggest' button */
        width: 120px;
        height: 42px;
        background: rgba(10, 10, 12, 0.85);
        backdrop-filter: blur(12px);
        -webkit-backdrop-filter: blur(12px);
        border: 1px solid rgba(0, 242, 255, 0.2);
        border-radius: 10px;
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 0 6px 0 12px;
        z-index: 9999;
        box-shadow: 0 8px 24px rgba(0, 0, 0, 0.5);
        transition: all 0.3s ease;
    }

    .firebase-node-mini:hover {
        border-color: #00f2ff;
        transform: translateY(-3px);
    }

    .mini-content {
        display: flex;
        align-items: center;
        gap: 10px;
    }

    .status-indicator {
        position: relative;
        display: flex;
        align-items: center;
    }

    .pulse-dot {
        width: 6px;
        height: 6px;
        background: #00f2ff;
        border-radius: 50%;
        box-shadow: 0 0 8px #00f2ff;
        animation: miniPulse 2s infinite;
    }

    @keyframes miniPulse {
        0% { transform: scale(1); opacity: 1; }
        50% { transform: scale(1.5); opacity: 0.5; }
        100% { transform: scale(1); opacity: 1; }
    }

    .mini-text {
        display: flex;
        flex-direction: column;
    }

    .mini-text .label {
        font-size: 8px;
        font-weight: 900;
        text-transform: uppercase;
        color: #475569;
        letter-spacing: 1px;
    }

    .mini-text .version {
        font-size: 10px;
        font-family: monospace;
        color: #f1f5f9;
        font-weight: bold;
    }

    .mini-action-btn {
        background: #00f2ff;
        color: #000;
        border: none;
        width: 30px;
        height: 30px;
        border-radius: 8px;
        display: flex;
        align-items: center;
        justify-content: center;
        font-size: 12px;
        cursor: pointer;
        transition: 0.2s;
    }

    .mini-action-btn:hover {
        background: #fff;
        transform: scale(1.1);
    }

    /* Integration with your Master Overlay System */
</style>

<script>
    function openFirebaseNode() {
        // Using the same openLink/openFrame logic we built for your Hub
        if (typeof openLink === "function") {
            openLink('https://debeatzgh1.github.io/Home-/');
        } else if (typeof openFrame === "function") {
            openFrame('https://debeatzgh1.github.io/Home-/');
        } else {
            // Fallback for standalone use
            window.open('https://debeatzgh1.github.io/Home-/', '_blank');
        }
    }
</script>


<html lang="en">
<head>
    <style>
        :root {
            --nav-bg: rgba(13, 17, 23, 0.9);
            --nav-border: #30363d;
            --nav-accent: #58a6ff;
            --nav-hover: #1f6feb;
            --glow-color: rgba(88, 166, 255, 0.5);
        }

        /* Dock Container */
        .nav-dock {
            position: fixed;
            right: 20px;
            top: 50%;
            transform: translateY(-50%);
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 15px;
            z-index: 10000;
        }

        /* Launcher (>) */
        #nav-launcher {
            width: 38px;
            height: 38px;
            background: var(--nav-bg);
            border: 1px solid var(--nav-border);
            color: var(--nav-accent);
            border-radius: 10px;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.4rem;
            backdrop-filter: blur(8px);
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.4);
        }

        #nav-launcher.open {
            color: white;
            background: var(--nav-hover);
            border-color: var(--nav-accent);
        }

        /* Button Group */
        .nav-group {
            display: flex;
            flex-direction: column;
            gap: 10px;
            pointer-events: none;
        }

        .nav-group.active {
            pointer-events: auto;
        }

        .nav-btn {
            width: 34px;
            height: 34px;
            background: var(--nav-bg);
            border: 1px solid var(--nav-border);
            color: #c9d1d9;
            border-radius: 50%;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            opacity: 0;
            transform: scale(0.5) translateX(30px);
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            text-decoration: none;
            position: relative;
        }

        /* Active/Open State for Buttons */
        .nav-group.active .nav-btn {
            opacity: 1;
            transform: scale(1) translateX(0);
        }

        /* Heartbeat Glow Animation */
        @keyframes heartbeatGlow {
            0% { box-shadow: 0 0 0 0 var(--glow-color); transform: scale(1); }
            50% { box-shadow: 0 0 15px 5px var(--glow-color); transform: scale(1.1); }
            100% { box-shadow: 0 0 0 0 var(--glow-color); transform: scale(1); }
        }

        .heartbeat-active {
            animation: heartbeatGlow 1.2s ease-in-out 2; /* Runs twice on open */
        }

        .nav-btn:hover {
            background: var(--nav-hover);
            color: white;
            border-color: var(--nav-accent);
        }

        /* Staggered transition delays for a smooth "pop-in" effect */
        .nav-group.active .nav-btn:nth-child(1) { transition-delay: 0.1s; }
        .nav-group.active .nav-btn:nth-child(2) { transition-delay: 0.2s; }
        .nav-group.active .nav-btn:nth-child(3) { transition-delay: 0.3s; }

        .nav-btn svg { width: 18px; height: 18px; }
    </style>
</head>
<body>

    <div class="nav-dock">
        <button id="nav-launcher" onclick="toggleNav()">›</button>

        <div class="nav-group" id="navGroup">
            <button class="nav-btn" onclick="window.scrollTo({top: 0, behavior: 'smooth'})">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><polyline points="18 15 12 9 6 15"></polyline></svg>
            </button>

            <a href="https://debeatzgh1.github.io/posts/" class="nav-btn">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"></path><polyline points="9 22 9 12 15 12 15 22"></polyline></svg>
            </a>

            <button class="nav-btn" onclick="window.scrollTo({top: document.body.scrollHeight, behavior: 'smooth'})">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><polyline points="6 9 12 15 18 9"></polyline></svg>
            </button>
        </div>
    </div>

    <script>
        function toggleNav() {
            const group = document.getElementById('navGroup');
            const launcher = document.getElementById('nav-launcher');
            const buttons = document.querySelectorAll('.nav-btn');
            
            const isOpen = group.classList.toggle('active');
            launcher.classList.toggle('open');
            launcher.innerText = isOpen ? '‹' : '›';

            if (isOpen) {
                // Trigger heartbeat animation on each button when opened
                buttons.forEach((btn, index) => {
                    // Slight delay before heartbeat starts to match the pop-in
                    setTimeout(() => {
                        btn.classList.add('heartbeat-active');
                    }, (index + 1) * 200);

                    // Remove class after animation ends so it can re-trigger next time
                    setTimeout(() => {
                        btn.classList.remove('heartbeat-active');
                    }, 3000);
                });
            }
        }
    </script>

</body>
</html>




<!-- Elfsight RSS Feed | RSS Feed -->
<script src="https://elfsightcdn.com/platform.js" async></script>
<div class="elfsight-app-df567ac9-59ad-42a0-9c79-0173a06788fa" data-elfsight-app-lazy></div>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Multi-Tab Launcher</title>

<script src="https://cdn.tailwindcss.com"></script>

<style>
.modal-bg{
  display:none;
  position:fixed;
  inset:0;
  background:rgba(0,0,0,.75);
  backdrop-filter:blur(6px);
  z-index:9999;
}
.modal-box{
  width:100%;
  height:100%;
  background:#fff;
  display:flex;
  flex-direction:column;
}
.tabs{
  display:flex;
  gap:6px;
  padding:10px;
  background:#0f172a;
}
.tab{
  padding:8px 14px;
  border-radius:10px;
  font-size:13px;
  font-weight:700;
  color:#cbd5f5;
  cursor:pointer;
}
.tab.active{
  background:#2563eb;
  color:#fff;
}
.controls{
  display:flex;
  gap:8px;
  padding:8px 10px;
  background:#020617;
}
.ctrl-btn{
  background:rgba(255,255,255,.15);
  color:#fff;
  padding:6px 12px;
  border-radius:8px;
  font-size:12px;
  font-weight:700;
  cursor:pointer;
}
iframe{
  flex:1;
  width:100%;
  border:none;
}
.mobile-tabs{display:none}
@media (max-width:768px){
  .tabs{display:none}
  .mobile-tabs{
    display:flex;
    justify-content:space-around;
    background:#020617;
    padding:6px 0;
  }
  .mobile-tab{
    color:#cbd5f5;
    font-size:12px;
    font-weight:700;
    padding:6px 8px;
  }
  .mobile-tab.active{
    color:#fff;
    background:#2563eb;
    border-radius:8px;
  }
}
</style>
</head>

<body class="bg-gray-100">

<header class="text-center py-12">
  <h1 class="text-3xl font-bold">AI Hub</h1>
  <p class="text-gray-600 mt-2">All your platforms in one smart workspace</p>
  <button onclick="openLauncher('wordpress')" class="mt-6 bg-blue-600 text-white px-8 py-3 rounded-xl font-bold">
    Launch Hub
  </button>
</header>

<div class="modal-bg" id="modal">
  <div class="modal-box" id="modalBox">

    <!-- Desktop Tabs -->
    <div class="tabs">
      <div class="tab active" data-tab="wordpress" onclick="switchTab('wordpress')">Web</div>
      <div class="tab" data-tab="blogger" onclick="switchTab('blogger')">Blog</div>
      <div class="tab" data-tab="offers" onclick="switchTab('offers')">Offers</div>
      <div class="tab" data-tab="sign" onclick="switchTab('sign')">Sign</div>
      <div class="tab" data-tab="suggest" onclick="switchTab('suggest')">Suggest</div>
    </div>

    <!-- Controls -->
    <div class="controls">
      <div class="ctrl-btn" onclick="goBack()">⟵</div>
      <div class="ctrl-btn" onclick="goForward()">⟶</div>
      <div class="ctrl-btn" onclick="toggleFS()">⛶</div>
      <div class="ctrl-btn" onclick="closeLauncher()">✕</div>
    </div>

    <iframe id="frame"></iframe>

    <!-- Mobile Tabs (Icons open Blogspot too) -->
    <div class="mobile-tabs">
      <div class="mobile-tab active" data-tab="wordpress" onclick="switchTab('wordpress')">🌐</div>
      <div class="mobile-tab" data-tab="blogger" onclick="switchTab('blogger')">📝</div>
      <div class="mobile-tab" data-tab="offers" onclick="switchTab('offers')">🎁</div>
      <div class="mobile-tab" data-tab="sign" onclick="switchTab('sign')">✅</div>
      <div class="mobile-tab" data-tab="suggest" onclick="switchTab('suggest')">💡</div>
    </div>

  </div>
</div>

<script>
const modal = document.getElementById("modal");
const frame = document.getElementById("frame");
const tabs = document.querySelectorAll(".tab");
const mobileTabs = document.querySelectorAll(".mobile-tab");

/* ✅ CLEAN & VALID URL MAP */
const URLS = {
  wordpress: "https://debeatzgh.wordpress.com/",
  blogger: "https://debeatzgh1.blogspot.com/",
  offers: "https://msha.ke/debeatzgh/",
  sign: "https://digimartgh.blogspot.com/",
  suggest: "https://beatzde4.blogspot.com/"
};

let historyStack = [];
let historyIndex = -1;

function load(url){
  frame.src = url;
  if(historyStack[historyIndex] !== url){
    historyStack = historyStack.slice(0, historyIndex + 1);
    historyStack.push(url);
    historyIndex++;
  }
}

function openLauncher(tab){
  modal.style.display="flex";
  switchTab(tab);
}

function closeLauncher(){
  modal.style.display="none";
  frame.src="";
  historyStack=[];
  historyIndex=-1;
  if(document.fullscreenElement) document.exitFullscreen();
}

function switchTab(tab){
  tabs.forEach(t=>t.classList.remove("active"));
  mobileTabs.forEach(t=>t.classList.remove("active"));
  document.querySelectorAll(`[data-tab="${tab}"]`)
    .forEach(t=>t.classList.add("active"));
  load(URLS[tab]);
}

function goBack(){
  if(historyIndex > 0){
    historyIndex--;
    frame.src = historyStack[historyIndex];
  }
}

function goForward(){
  if(historyIndex < historyStack.length - 1){
    historyIndex++;
    frame.src = historyStack[historyIndex];
  }
}

function toggleFS(){
  const el = document.getElementById("modalBox");
  if(!document.fullscreenElement) el.requestFullscreen();
  else document.exitFullscreen();
}
</script>

</body>
</html>

<!-- Start of OpenWidget (www.openwidget.com) code -->
<script>
  window.__ow = window.__ow || {};
  window.__ow.organizationId = "8dbd48aa-17f7-49aa-b323-23eb6ad358fa";
  window.__ow.integration_name = "manual_settings";
  window.__ow.product_name = "openwidget";   
  ;(function(n,t,c){function i(n){return e._h?e._h.apply(null,n):e._q.push(n)}var e={_q:[],_h:null,_v:"2.0",on:function(){i(["on",c.call(arguments)])},once:function(){i(["once",c.call(arguments)])},off:function(){i(["off",c.call(arguments)])},get:function(){if(!e._h)throw new Error("[OpenWidget] You can't use getters before load.");return i(["get",c.call(arguments)])},call:function(){i(["call",c.call(arguments)])},init:function(){var n=t.createElement("script");n.async=!0,n.type="text/javascript",n.src="https://cdn.openwidget.com/openwidget.js",t.head.appendChild(n)}};!n.__ow.asyncInit&&e.init(),n.OpenWidget=n.OpenWidget||e}(window,document,[].slice))
</script>
<noscript>You need to <a href="https://www.openwidget.com/enable-javascript" rel="noopener nofollow">enable JavaScript</a> to use the communication tool powered by <a href="https://www.openwidget.com/" rel="noopener nofollow" target="_blank">OpenWidget</a></noscript>
<!-- End of OpenWidget code -->
