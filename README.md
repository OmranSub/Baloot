<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="بلوت">
<meta name="theme-color" content="#0a0a0f">
<title>بلوت</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@300;400;500;700;900&display=swap" rel="stylesheet">
<style>
  :root {
    --gold: #c9a84c;
    --gold-light: #e8c97a;
    --gold-dim: #7a5e25;
    --bg: #0a0a0f;
    --bg2: #111118;
    --bg3: #1a1a24;
    --surface: #16161f;
    --surface2: #1e1e2a;
    --text: #f0ead8;
    --text2: #8a8070;
    --text3: #4a4440;
    --border: rgba(201,168,76,0.15);
    --border2: rgba(201,168,76,0.3);
  }

  * { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }

  html, body {
    height: 100%;
    background: var(--bg);
    color: var(--text);
    font-family: 'Tajawal', sans-serif;
    overflow: hidden;
  }

  .app {
    height: 100dvh;
    display: flex;
    flex-direction: column;
    max-width: 480px;
    margin: 0 auto;
    position: relative;
  }

  .bg-ornament {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 600px;
    height: 600px;
    opacity: 0.03;
    pointer-events: none;
    z-index: 0;
  }

  .header {
    position: relative;
    z-index: 1;
    text-align: center;
    padding: 1.2rem 1rem 0.8rem;
    border-bottom: 0.5px solid var(--border);
    flex-shrink: 0;
  }

  .header-title {
    font-size: 28px;
    font-weight: 900;
    letter-spacing: 0.05em;
    background: linear-gradient(135deg, var(--gold-light), var(--gold), var(--gold-dim));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .header-sub {
    font-size: 11px;
    color: var(--text3);
    font-weight: 300;
    letter-spacing: 0.15em;
    margin-top: 2px;
  }

  .board {
    position: relative;
    z-index: 1;
    display: grid;
    grid-template-columns: 1fr 1px 1fr;
    flex: 1;
    overflow: hidden;
  }

  .divider-line {
    background: var(--border);
    position: relative;
  }

  .divider-line::before {
    content: '';
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 6px;
    height: 6px;
    border-radius: 50%;
    background: var(--gold-dim);
  }

  .team {
    display: flex;
    flex-direction: column;
    padding: 1rem 0.8rem 0.5rem;
    overflow: hidden;
  }

  .team-name {
    font-size: 22px;
    font-weight: 700;
    text-align: center;
    color: var(--gold);
    margin-bottom: 0.8rem;
    letter-spacing: 0.05em;
  }

  .score-input {
    width: 100%;
    background: var(--surface);
    border: 0.5px solid var(--border);
    border-radius: 10px;
    color: var(--text);
    font-family: 'Tajawal', sans-serif;
    font-size: 20px;
    font-weight: 500;
    text-align: center;
    padding: 10px 8px;
    outline: none;
    transition: border-color 0.2s, box-shadow 0.2s;
    -moz-appearance: textfield;
    appearance: textfield;
    margin-bottom: 0.8rem;
  }

  .score-input::-webkit-outer-spin-button,
  .score-input::-webkit-inner-spin-button { -webkit-appearance: none; }

  .score-input:focus {
    border-color: var(--gold-dim);
    box-shadow: 0 0 0 3px rgba(201,168,76,0.1);
  }

  .total-block {
    background: var(--surface);
    border: 0.5px solid var(--border);
    border-radius: 12px;
    padding: 0.6rem;
    text-align: center;
    margin-bottom: 0.8rem;
  }

  .total-label {
    font-size: 10px;
    color: var(--text3);
    letter-spacing: 0.12em;
    font-weight: 300;
    margin-bottom: 2px;
  }

  .total-num {
    font-size: 36px;
    font-weight: 900;
    color: var(--gold);
    line-height: 1;
  }

  .total-num.bump { animation: bump 0.25s ease; }

  @keyframes bump {
    0% { transform: scale(1); }
    50% { transform: scale(1.18); }
    100% { transform: scale(1); }
  }

  .progress-bar-wrap {
    height: 3px;
    background: var(--bg3);
    border-radius: 2px;
    margin-top: 6px;
    overflow: hidden;
  }

  .progress-bar {
    height: 100%;
    background: linear-gradient(90deg, var(--gold-dim), var(--gold));
    border-radius: 2px;
    transition: width 0.4s cubic-bezier(0.34, 1.56, 0.64, 1);
    width: 0%;
  }

  .history-label {
    font-size: 10px;
    color: var(--text3);
    letter-spacing: 0.1em;
    margin-bottom: 4px;
    text-align: center;
    font-weight: 300;
  }

  .history-scroll {
    flex: 1;
    overflow-y: auto;
    scrollbar-width: none;
    padding-bottom: 0.5rem;
  }

  .history-scroll::-webkit-scrollbar { display: none; }

  .history-item {
    text-align: center;
    font-size: 14px;
    font-weight: 400;
    color: var(--text2);
    padding: 5px 0;
    border-bottom: 0.5px solid var(--border);
    animation: slideIn 0.2s ease;
  }

  .history-item:last-child { border-bottom: none; }

  @keyframes slideIn {
    from { opacity: 0; transform: translateY(-6px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* Single add button row pinned at bottom */
  .add-row {
    position: relative;
    z-index: 2;
    flex-shrink: 0;
    padding: 0.75rem 1.5rem calc(0.75rem + env(safe-area-inset-bottom));
    border-top: 0.5px solid var(--border);
    background: var(--bg);
  }

  .add-btn {
    width: 100%;
    padding: 15px;
    background: linear-gradient(135deg, var(--gold-dim), var(--gold));
    border: none;
    border-radius: 14px;
    color: #0a0a0f;
    font-family: 'Tajawal', sans-serif;
    font-size: 18px;
    font-weight: 700;
    cursor: pointer;
    transition: transform 0.1s, opacity 0.15s;
    letter-spacing: 0.05em;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
  }

  .add-btn:active {
    transform: scale(0.97);
    opacity: 0.85;
  }

  /* Win overlay */
  .overlay {
    position: fixed;
    inset: 0;
    background: rgba(5,5,10,0.85);
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 100;
    backdrop-filter: blur(6px);
    -webkit-backdrop-filter: blur(6px);
    animation: fadeIn 0.3s ease;
  }

  .overlay.hidden { display: none; }

  @keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
  }

  .modal {
    background: var(--bg2);
    border: 0.5px solid var(--border2);
    border-radius: 20px;
    padding: 2rem 1.8rem;
    text-align: center;
    max-width: 300px;
    width: 88%;
    animation: popIn 0.35s cubic-bezier(0.34, 1.56, 0.64, 1);
  }

  @keyframes popIn {
    from { opacity: 0; transform: scale(0.8); }
    to { opacity: 1; transform: scale(1); }
  }

  .modal-icon {
    font-size: 48px;
    margin-bottom: 0.8rem;
    animation: spinIn 0.6s ease 0.3s both;
  }

  @keyframes spinIn {
    from { transform: rotate(-20deg) scale(0.5); opacity: 0; }
    to { transform: rotate(0) scale(1); opacity: 1; }
  }

  .modal-title {
    font-size: 13px;
    color: var(--text3);
    letter-spacing: 0.15em;
    font-weight: 300;
    margin-bottom: 0.4rem;
  }

  .modal-winner {
    font-size: 32px;
    font-weight: 900;
    color: var(--gold);
    margin-bottom: 0.4rem;
  }

  .modal-sub {
    font-size: 13px;
    color: var(--text2);
    margin-bottom: 1.5rem;
    font-weight: 300;
  }

  .new-game-btn {
    width: 100%;
    padding: 13px;
    background: linear-gradient(135deg, var(--gold-dim), var(--gold));
    border: none;
    border-radius: 12px;
    color: #0a0a0f;
    font-family: 'Tajawal', sans-serif;
    font-size: 16px;
    font-weight: 700;
    cursor: pointer;
    transition: transform 0.1s, opacity 0.15s;
    letter-spacing: 0.05em;
  }

  .new-game-btn:active { transform: scale(0.96); opacity: 0.85; }

  .install-banner {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    background: var(--bg2);
    border-top: 0.5px solid var(--border);
    padding: 0.8rem 1rem;
    display: flex;
    align-items: center;
    gap: 10px;
    z-index: 50;
    animation: slideUp 0.3s ease;
  }

  .install-banner.hidden { display: none; }

  @keyframes slideUp {
    from { transform: translateY(100%); }
    to { transform: translateY(0); }
  }

  .install-text { flex: 1; font-size: 12px; color: var(--text2); line-height: 1.4; }
  .install-text strong { color: var(--gold); font-weight: 500; display: block; font-size: 13px; }

  .install-dismiss {
    background: none;
    border: none;
    color: var(--text3);
    font-size: 18px;
    cursor: pointer;
    padding: 4px;
  }
</style>
</head>
<body>

<svg class="bg-ornament" viewBox="0 0 200 200" fill="none" xmlns="http://www.w3.org/2000/svg">
  <path d="M100 10 L190 55 L190 145 L100 190 L10 145 L10 55 Z" stroke="white" stroke-width="1" fill="none"/>
  <path d="M100 30 L170 67 L170 133 L100 170 L30 133 L30 67 Z" stroke="white" stroke-width="0.5" fill="none"/>
  <path d="M100 50 L150 78 L150 122 L100 150 L50 122 L50 78 Z" stroke="white" stroke-width="0.5" fill="none"/>
  <circle cx="100" cy="100" r="40" stroke="white" stroke-width="0.5" fill="none"/>
  <circle cx="100" cy="100" r="5" fill="white"/>
</svg>

<div class="app">
  <div class="header">
    <div class="header-title">بـلـوت</div>
    <div class="header-sub">أول من يصل إلى ١٥٢ يفوز</div>
  </div>

  <div class="board">
    <div class="team">
      <div class="team-name">لنا</div>
      <input class="score-input" id="input1" type="number" inputmode="numeric" pattern="[0-9]*" placeholder="٠" min="0">
      <div class="total-block">
        <div class="total-label">المجموع</div>
        <div class="total-num" id="total1">0</div>
        <div class="progress-bar-wrap"><div class="progress-bar" id="bar1"></div></div>
      </div>
      <div class="history-label">السجل</div>
      <div class="history-scroll"><div id="history1"></div></div>
    </div>

    <div class="divider-line"></div>

    <div class="team">
      <div class="team-name">لهم</div>
      <input class="score-input" id="input2" type="number" inputmode="numeric" pattern="[0-9]*" placeholder="٠" min="0">
      <div class="total-block">
        <div class="total-label">المجموع</div>
        <div class="total-num" id="total2">0</div>
        <div class="progress-bar-wrap"><div class="progress-bar" id="bar2"></div></div>
      </div>
      <div class="history-label">السجل</div>
      <div class="history-scroll"><div id="history2"></div></div>
    </div>
  </div>

  <div class="add-row">
    <button class="add-btn" onclick="addScores()">
      <span style="font-size:22px; line-height:1;">+</span>
      <span>أضف النقاط</span>
    </button>
  </div>
</div>

<div class="overlay hidden" id="overlay">
  <div class="modal">
    <div class="modal-icon">🏆</div>
    <div class="modal-title">الفائز</div>
    <div class="modal-winner" id="winner-name"></div>
    <div class="modal-sub" id="winner-sub"></div>
    <button class="new-game-btn" onclick="newGame()">لعبة جديدة</button>
  </div>
</div>

<div class="install-banner hidden" id="install-banner">
  <div class="install-text">
    <strong>ثبّت التطبيق</strong>
    اضغط على مشاركة ثم "إضافة إلى الشاشة الرئيسية"
  </div>
  <button class="install-dismiss" onclick="dismissInstall()">✕</button>
</div>

<script>
var scores = [0, 0];
var histories = [[], []];
var WIN = 152;

function addScores() {
  var v1 = parseInt(document.getElementById('input1').value);
  var v2 = parseInt(document.getElementById('input2').value);
  var valid1 = !isNaN(v1) && v1 >= 0;
  var valid2 = !isNaN(v2) && v2 >= 0;
  if (!valid1 && !valid2) return;

  if (valid1) {
    histories[0].push(v1);
    scores[0] += v1;
    document.getElementById('input1').value = '';
    renderTeam(0);
  }
  if (valid2) {
    histories[1].push(v2);
    scores[1] += v2;
    document.getElementById('input2').value = '';
    renderTeam(1);
  }

  var winner = null;
  if (scores[0] >= WIN && scores[1] >= WIN) {
    winner = scores[0] >= scores[1] ? 1 : 2;
  } else if (scores[0] >= WIN) {
    winner = 1;
  } else if (scores[1] >= WIN) {
    winner = 2;
  }
  if (winner !== null) setTimeout(function() { showWinner(winner); }, 200);
}

function renderTeam(idx) {
  var t = idx + 1;
  var totalEl = document.getElementById('total' + t);
  totalEl.textContent = scores[idx];
  totalEl.classList.remove('bump');
  void totalEl.offsetWidth;
  totalEl.classList.add('bump');
  var pct = Math.min((scores[idx] / WIN) * 100, 100);
  document.getElementById('bar' + t).style.width = pct + '%';
  var hist = document.getElementById('history' + t);
  var item = document.createElement('div');
  item.className = 'history-item';
  item.textContent = histories[idx][histories[idx].length - 1];
  hist.insertBefore(item, hist.firstChild);
}

function showWinner(team) {
  var name = team === 1 ? 'لنا' : 'لهم';
  document.getElementById('winner-name').textContent = name;
  document.getElementById('winner-sub').textContent = 'وصل إلى ' + scores[team - 1] + ' نقطة 🎉';
  document.getElementById('overlay').classList.remove('hidden');
}

function newGame() {
  scores = [0, 0];
  histories = [[], []];
  document.getElementById('overlay').classList.add('hidden');
  for (var t = 1; t <= 2; t++) {
    document.getElementById('total' + t).textContent = '0';
    document.getElementById('bar' + t).style.width = '0%';
    document.getElementById('history' + t).innerHTML = '';
  }
}

document.getElementById('input1').addEventListener('keydown', function(e) { if (e.key === 'Enter') addScores(); });
document.getElementById('input2').addEventListener('keydown', function(e) { if (e.key === 'Enter') addScores(); });

setTimeout(function() {
  var isIOS = /iphone|ipad|ipod/i.test(navigator.userAgent);
  var isStandalone = window.navigator.standalone;
  var dismissed = localStorage.getItem('baloot-install-dismissed');
  if (isIOS && !isStandalone && !dismissed) {
    document.getElementById('install-banner').classList.remove('hidden');
  }
}, 3000);

function dismissInstall() {
  document.getElementById('install-banner').classList.add('hidden');
  localStorage.setItem('baloot-install-dismissed', '1');
}

if ('serviceWorker' in navigator) {
  var swCode = "const CACHE='baloot-v1';self.addEventListener('install',e=>{e.waitUntil(caches.open(CACHE).then(c=>c.addAll(['./'])))});self.addEventListener('fetch',e=>{e.respondWith(caches.match(e.request).then(r=>r||fetch(e.request)))});";
  var blob = new Blob([swCode], { type: 'application/javascript' });
  navigator.serviceWorker.register(URL.createObjectURL(blob)).catch(function(){});
}
</script>
</body>
</html>
