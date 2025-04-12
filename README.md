
<html lang="zh-TW">
<head>
  <meta charset="UTF-8">
  <title>惡靈古堡99.0</title>
  <style>
    body {
      font-family: "微軟正黑體", sans-serif;
      background-color: #000000;
      color: #ffffff;
      padding: 20px;
      overflow: hidden;
      position: relative;
    }
    h1, h2, h3 {
      color: #ff0000;
    }
    .section {
      margin-bottom: 20px;
      border: 2px solid #ffcc80;
      padding: 15px;
      border-radius: 10px;
      background: #1a1a1a;
      position: relative;
      z-index: 5;
    }
    button {
      background-color: #1f2f47;
      color: #ffffff;
      border: 2px solid #ff0000;
      padding: 10px;
      margin: 5px;
      border-radius: 8px;
      cursor: pointer;
    }
    button:hover {
      background-color: #b71c1c;
    }
    input {
      padding: 5px;
      margin-right: 5px;
      border-radius: 5px;
      border: 1px solid #ccc;
    }
    .effect {
      position: absolute;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      pointer-events: none;
      z-index: 10;
    }
    .raindrop, .snowflake, .particle {
      position: absolute;
      border-radius: 50%;
      animation-timing-function: linear;
    }
    .raindrop {
      width: 2px;
      height: 10px;
      background: rgba(0,0,255,0.6);
      animation: drop 1s infinite;
    }
    @keyframes drop {
      0% {transform: translateY(-100px); opacity: 1;}
      100% {transform: translateY(100vh); opacity: 0;}
    }
    .snowflake {
      width: 10px;
      height: 10px;
      background: white;
      opacity: 0.8;
      animation: snow 4s linear infinite;
    }
    @keyframes snow {
      0% {transform: translateY(0px) rotate(0deg);}
      100% {transform: translateY(100vh) rotate(360deg);}
    }
    .lightning {
      background: white;
      opacity: 0.9;
      animation: flash 0.2s;
    }
    @keyframes flash {
      0%, 100% { opacity: 0; }
      50% { opacity: 1; }
    }
    .flame {
      background: radial-gradient(circle, rgba(255,100,0,0.6) 0%, rgba(255,0,0,0.3) 70%);
      animation: burn 0.5s ease-out;
    }
    @keyframes burn {
      from { transform: scale(0.5); opacity: 1; }
      to { transform: scale(2); opacity: 0; }
    }
    .vortex {
      background: radial-gradient(circle, rgba(0,255,255,0.5), transparent);
      animation: spin 1s linear infinite;
    }
    @keyframes spin {
      0% {transform: rotate(0deg);}
      100% {transform: rotate(360deg);}
    }
    .aura {
      background: radial-gradient(circle, rgba(255,255,0,0.3), transparent);
      animation: pulse 1.5s ease-in-out infinite;
    }
    @keyframes pulse {
      0%, 100% { transform: scale(1); }
      50% { transform: scale(1.2); }
    }
    .teleport {
      background: radial-gradient(circle, rgba(0,255,255,0.5), transparent);
      animation: zoom 0.6s ease-in-out;
    }
    @keyframes zoom {
      0% { transform: scale(0.5); opacity: 1; }
      100% { transform: scale(2); opacity: 0; }
    }
    .explode {
      background: radial-gradient(circle, orange, transparent);
      animation: explode 0.4s ease-out;
    }
    @keyframes explode {
      0% { transform: scale(1); opacity: 1; }
      100% { transform: scale(3); opacity: 0; }
    }
    .shake {
      animation: shake 0.3s;
    }
    @keyframes shake {
      0% { transform: translate(0, 0); }
      25% { transform: translate(-10px, 5px); }
      50% { transform: translate(10px, -5px); }
      75% { transform: translate(-5px, 5px); }
      100% { transform: translate(0, 0); }
    }
    .rune {
      background: radial-gradient(circle, rgba(128,0,255,0.3), transparent);
      animation: rotateRune 2s linear infinite;
    }
    @keyframes rotateRune {
      from { transform: rotate(0deg); }
      to { transform: rotate(360deg); }
    }
    .victory-box {
      position: absolute;
      top: 80px;
      left: 50%;
      transform: translateX(-50%);
      background-color: #ff0000;
      color: #ffffff;
      padding: 20px 30px;
      border-radius: 20px;
      box-shadow: 0 0 20px orange;
      z-index: 99;
      animation: pulse 2s infinite;
      font-size: 36px;
      font-weight: 900;
      text-align: center;
      font-family: "Microsoft JhengHei", "微軟正黑體", sans-serif;
    }
  </style>
</head>
<body>

<div class="section">
  <h3>喪屍 吼叫</h3>
  <div id="npcDialog">喪屍回應你：「hey hey stranger 」</div>
  <input type="text" id="visitorInput" placeholder="跟喪屍說點什麼...">
  <button onclick="respondToVisitor()">發送</button>
</div>

<div class="section">
  <h3>⚔️ 來一下</h3>
  <p>喪屍血量：<span id="enemyHP">100</span> | 玩家血量：<span id="playerHP">100</span></p>
  <button onclick="battle('attack')">攻擊</button>
  <button onclick="battle('defend')">防禦</button>
  <button onclick="battle('skill')">技能</button>
  <p id="battleLog"></p>
</div>

<div id="effectContainer" class="effect"></div>

<script>
let playerHP = 100, enemyHP = 100;

function respondToVisitor() {
  const input = document.getElementById("visitorInput").value.trim();
  if (input.length === 0) return;
  const replies = ["啦。", "哈～", "蛤", "eeeee.", "laaaaaaaa。"];
  const randomReply = replies[Math.floor(Math.random() * replies.length)];
  document.getElementById("npcDialog").innerText = `喪屍回應你：「${randomReply}」`;
  document.getElementById("visitorInput").value = "";
  triggerRandomEffect();
}

function battle(action) {
  const log = document.getElementById("battleLog");
  let msg = "";
  if (action === "attack") {
    const dmg = Math.floor(Math.random() * 20 + 5);
    enemyHP -= dmg;
    msg = `你攻擊喪屍造成 ${dmg} 傷害！`;
    triggerEffect("flame");
  } else if (action === "defend") {
    msg = "你進入防禦姿態，減少下一次傷害。";
    triggerEffect("aura");
  } else if (action === "skill") {
    const crit = Math.random() < 0.3;
    const dmg = crit ? 50 : 25;
    enemyHP -= dmg;
    msg = `你使用技能造成 ${dmg} 傷害${crit ? "（暴擊！）" : ""}`;
    triggerEffect("rune");
  }

  document.getElementById("enemyHP").innerText = Math.max(0, enemyHP);

  if (enemyHP <= 0) {
    showVictory();
    return;
  }

  const enemyAtk = Math.floor(Math.random() * 15);
  playerHP -= enemyAtk;
  document.getElementById("playerHP").innerText = Math.max(0, playerHP);
  log.innerText = msg + `\n喪屍攻擊你造成 ${enemyAtk} 傷害！`;
  triggerRandomEffect();
}

function triggerRandomEffect() {
  const effects = ["raindrop", "snowflake", "flame", "lightning", "vortex", "aura", "teleport", "explode", "shake", "rune"];
  const choice = effects[Math.floor(Math.random() * effects.length)];
  triggerEffect(choice);
}

function triggerEffect(type) {
  const container = document.getElementById("effectContainer");
  container.innerHTML = "";
  if (["raindrop", "snowflake", "particle"].includes(type)) {
    for (let i = 0; i < 40; i++) {
      const drop = document.createElement("div");
      drop.className = type;
      drop.style.left = Math.random() * 100 + "vw";
      drop.style.top = Math.random() * -100 + "px";
      container.appendChild(drop);
    }
  } else {
    const effect = document.createElement("div");
    effect.className = type;
    effect.style.width = "100vw";
    effect.style.height = "100vh";
    container.appendChild(effect);
    if (type === "shake") document.body.classList.add("shake");
  }
  setTimeout(() => {
    document.body.classList.remove("shake");
    container.innerHTML = "";
  }, 1000);
}

function showVictory() {
  const victoryBox = document.createElement("div");
  victoryBox.className = "victory-box";
  victoryBox.textContent = "勝利！喪屍不動了！";
  document.body.appendChild(victoryBox);
  triggerEffect("explode");
}
</script>
</body>
</html>
