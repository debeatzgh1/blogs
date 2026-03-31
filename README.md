
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DeBeatzGH | AI Tech Hub</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    
    <style>
        :root {
            --nav-bg: rgba(13, 17, 23, 0.95);
            --nav-border: #30363d;
            --nav-accent: #00f2ff;
            --cyber-cyan: #00f2ff;
        }

        body { background: #0d1117; color: #f1f5f9; font-family: 'Plus Jakarta Sans', sans-serif; margin: 0; }

        /* --- 1. FIREBASE INTERNAL BUILD BANNER (Top-Left) --- */
        .firebase-node-mini {
            position: fixed; top: 25px; left: 25px;
            width: 160px; height: 45px;
            background: rgba(10, 10, 12, 0.85); backdrop-filter: blur(12px);
            border: 1px solid rgba(0, 242, 255, 0.2); border-radius: 12px;
            display: flex; align-items: center; justify-content: space-between;
            padding: 0 8px 0 12px; z-index: 9999;
            box-shadow: 0 8px 24px rgba(0, 0, 0, 0.5); transition: 0.3s;
        }
        .firebase-node-mini:hover { border-color: var(--cyber-cyan); transform: translateY(-2px); }
        
        .pulse-dot {
            width: 8px; height: 8px; background: var(--cyber-cyan);
            border-radius: 50%; box-shadow: 0 0 10px var(--cyber-cyan);
            animation: miniPulse 2s infinite; margin-right: 10px;
        }
        @keyframes miniPulse { 0%, 100% { opacity: 1; transform: scale(1); } 50% { opacity: 0.5; transform: scale(1.3); } }

        /* --- 2. MULTI-TAB MODAL SYSTEM --- */
        #hub-modal {
            display: none; position: fixed; inset: 0;
            background: rgba(0,0,0,0.9); backdrop-filter: blur(8px); z-index: 10000;
        }
        .modal-box { width: 100%; height: 100%; display: flex; flex-direction: column; }
        
        .tabs-header { 
            display: flex; justify-content: space-between; align-items: center;
            background: #0f172a; padding: 10px 20px; border-bottom: 1px solid #1e293b;
        }
        .tab-group { display: flex; gap: 8px; }
        .tab { 
            padding: 8px 16px; border-radius: 8px; font-size: 12px; font-weight: 700; 
            color: #94a3b8; cursor: pointer; transition: 0.2s; background: #1e293b;
        }
        .tab.active { background: #2563eb; color: #fff; box-shadow: 0 0 15px rgba(37, 99, 235, 0.4); }

        .ctrl-group { display: flex; gap: 10px; }
        .ctrl-btn { color: #fff; cursor: pointer; font-size: 18px; opacity: 0.7; transition: 0.2s; }
        .ctrl-btn:hover { opacity: 1; color: var(--cyber-cyan); }

        /* --- 3. NAVIGATION DOCK (Right) --- */
        .nav-dock {
            position: fixed; right: 20px; top: 50%; transform: translateY(-50%);
            display: flex; flex-direction: column; align-items: center; gap: 15px; z-index: 9998;
        }
        .nav-btn {
            width: 40px; height: 40px; background: var(--nav-bg); border: 1px solid var(--nav-border);
            color: #fff; border-radius: 50%; display: flex; align-items: center; justify-content: center;
            cursor: pointer; transition: 0.3s;
        }
        .nav-btn:hover { border-color: var(--nav-accent); background: #1f6feb; }
    </style>
</head>
<body>

    <div id="firebase-mini-banner" class="firebase-node-mini">
        <div style="display:flex; align-items:center;">
            <span class="pulse-dot"></span>
            <div style="display:flex; flex-direction:column;">
                <span style="font-size:7px; font-weight:900; color:#64748b; text-transform:uppercase;">Build Status</span>
                <span style="font-size:10px; font-family:monospace; font-weight:bold;">v2.4-STABLE</span>
            </div>
        </div>
        <button onclick="openTabHub('wordpress')" style="background:var(--cyber-cyan); border:none; width:28px; height:28px; border-radius:6px; cursor:pointer;">
            <i class="fas fa-rocket" style="font-size:12px;"></i>
        </button>
    </div>

    <div class="nav-dock">
        <button class="nav-btn" onclick="window.scrollTo({top: 0, behavior: 'smooth'})"><i class="fas fa-chevron-up"></i></button>
        <button class="nav-btn" onclick="openTabHub('blogger')"><i class="fas fa-blog"></i></button>
        <button class="nav-btn" onclick="window.scrollTo({top: document.body.scrollHeight, behavior: 'smooth'})"><i class="fas fa-chevron-down"></i></button>
    </div>

    <div class="p-10 text-center mt-20">
        <h1 class="text-4xl font-black text-white">AI PRODUCT LAB</h1>
        <p class="text-gray-400 mt-4">System Online. All Gist Nodes active.</p>
        <iframe src="https://msha.ke/debeatzgh#links-5" width="100%" height="500" class="mt-10 rounded-2xl border-2 border-gray-800"></iframe>
    </div>

    <div id="hub-modal">
        <div class="modal-box" id="modalContainer">
            <div class="tabs-header">
                <div class="tab-group">
                    <div class="tab active" data-id="wordpress" onclick="switchTab('wordpress')">Web Hub</div>
                    <div class="tab" data-id="blogger" onclick="switchTab('blogger')">Tech Blog</div>
                    <div class="tab" data-id="suggest" onclick="switchTab('suggest')">Suggestions</div>
                </div>
                <div class="ctrl-group">
                    <i class="fas fa-expand ctrl-btn" onclick="toggleFull()"></i>
                    <i class="fas fa-times ctrl-btn" onclick="closeHub()" style="font-size:24px;"></i>
                </div>
            </div>
            <iframe id="hub-frame" src="" style="flex:1; width:100%; border:none; background:#fff;"></iframe>
        </div>
    </div>

    <script>
        const URLS = {
            wordpress: "https://debeatzgh.wordpress.com/",
            blogger: "https://debeatzgh1.blogspot.com/",
            suggest: "https://beatzde4.blogspot.com/"
        };

        function openTabHub(key) {
            document.getElementById('hub-modal').style.display = 'block';
            switchTab(key);
        }

        function closeHub() {
            document.getElementById('hub-modal').style.display = 'none';
            document.getElementById('hub-frame').src = "";
        }

        function switchTab(key) {
            // Update UI
            document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
            document.querySelector(`[data-id="${key}"]`).classList.add('active');
            // Load URL
            document.getElementById('hub-frame').src = URLS[key];
        }

        function toggleFull() {
            const el = document.getElementById('modalContainer');
            if (!document.fullscreenElement) el.requestFullscreen();
            else document.exitFullscreen();
        }
    </script>

</body>
</html>
