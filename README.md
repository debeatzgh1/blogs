<!DOCTYPE html>
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
