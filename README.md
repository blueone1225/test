
<html lang="zh-TW">
<head>
  <meta charset="UTF-8">
  <title> 鑫羿文創 </title>
  <style>
    body {
      font-family: "微軟正黑體", sans-serif;
      background-color: #000000;
      color: #ffffff;
      margin: 0;
      padding: 0;
    }
    .youtube-container {
      position: relative;
      padding-bottom: 56.25%;
      height: 0;
      overflow: hidden;
    }
    .youtube-container iframe {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
    }
    .content {
      padding: 20px;
    }
    .section {
      margin-bottom: 20px;
      border: 2px solid #ff0000;
      padding: 15px;
      border-radius: 10px;
      background: #1a1a2e;
    }
    .battle-container {
      margin-top: 10px;
    }
    .victory-box {
      background-color: #300000;
      color: #ff0000;
      font-weight: bold;
      padding: 20px;
      border-radius: 20px;
      box-shadow: 0 0 20px red;
      text-align: center;
      display: none;
      margin-top: 10px;
    }
    button {
      background-color: #2b3e50;
      color: #ffffff;
      border: 2px solid #ff0000;
      padding: 10px;
      margin: 5px;
      border-radius: 8px;
      cursor: pointer;
    }
    button:hover {
      background-color: #ff4d4d;
    }
    input {
      padding: 5px;
      margin-right: 5px;
      border-radius: 5px;
      border: 1px solid #ccc;
    }
  </style>
</head>
<body>

<!-- 最上方影片 -->
<div class="youtube-container">
  
<iframe src="https://www.youtube.com/embed/_TWOsvVAXkA" title="YouTube video" frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen></iframe>




</div>

<div class="content">

  <!-- 哥吉拉系列 全新進化 -->
  <div class="section">
    <h3> □三式機龍□ 機械哥吉拉</h3>
    <div id="npcDialog">機械拉回應你：「 啊啊啊啊嗚 」</div>
    <input type="text" id="visitorInput" placeholder="跟機械拉說點什麼...">
    <button onclick="respondToVisitor()">發送</button>
  </div>

  <!-- 主戰鬥區塊 + 增加按鈕 -->
  <div id="battleArea">
    <div class="section battle-container" id="battle0">
      <h3>⚔️ 挑戰開始 </h3>
      <p><span class="enemyName">機械拉</span> 血量：<span class="enemyHP">100</span> | 玩家血量：<span class="playerHP">100</span></p>
      <button onclick="battle(this, 'attack')">攻擊</button>
      <button onclick="battle(this, 'defend')">防禦</button>
      <button onclick="battle(this, 'skill')">技能</button>
      <button onclick="deleteBlock(this)">刪除</button>
      <p class="battleLog"></p>
      <div class="victory-box">勝利！<span class="enemyName">機械拉</span> 能源不足；損毀不能移動！</div>
    </div>
  </div>

  <button onclick="addNewBattleBlock()">新增戰鬥區塊</button>

</div>

<script>
function respondToVisitor() {
  const input = document.getElementById("visitorInput").value.trim();
  if (input.length === 0) return;
  const replies = ["啊", "轟", "yeeee", "（激光射線）", "......."];
  const randomReply = replies[Math.floor(Math.random() * replies.length)];
  document.getElementById("npcDialog").innerText = `機械拉回應你：「${randomReply}」`;
  document.getElementById("visitorInput").value = "";
}

const enemyNames = ["紅蓮哥吉拉", "摩斯拉", "王者基多拉", "正宗哥吉拉", "小吉拉", "蓋亞", "固吉拉"];
let blockCount = 1;

function addNewBattleBlock() {
  const container = document.getElementById("battleArea");
  const block = document.createElement("div");
  const newEnemy = enemyNames[Math.floor(Math.random() * enemyNames.length)];
  block.className = "section battle-container";
  block.innerHTML = `
    <h3>⚔️ 新戰鬥</h3>
    <p><span class="enemyName">${newEnemy}</span> 血量：<span class="enemyHP">100</span> | 玩家血量：<span class="playerHP">100</span></p>
    <button onclick="battle(this, 'attack')">攻擊</button>
    <button onclick="battle(this, 'defend')">防禦</button>
    <button onclick="battle(this, 'skill')">技能</button>
    <button onclick="deleteBlock(this)">刪除</button>
    <p class="battleLog"></p>
    <div class="victory-box">勝利！<span class="enemyName">${newEnemy}</span> 破壞毀損不能移動；能源不足 </div>
  `;
  container.appendChild(block);
  blockCount++;
}

function deleteBlock(btn) {
  btn.parentElement.remove();
}

function battle(btn, action) {
  const section = btn.parentElement;
  const enemyHPSpan = section.querySelector(".enemyHP");
  const playerHPSpan = section.querySelector(".playerHP");
  const log = section.querySelector(".battleLog");
  const victoryBox = section.querySelector(".victory-box");

  let enemyHP = parseInt(enemyHPSpan.innerText);
  let playerHP = parseInt(playerHPSpan.innerText);
  let msg = "";

  if (action === "attack") {
    const dmg = Math.floor(Math.random() * 20 + 5);
    enemyHP -= dmg;
    msg = `你攻擊造成 ${dmg} 傷害！`;
  } else if (action === "defend") {
    msg = "你防禦了一回合。";
  } else if (action === "skill") {
    const crit = Math.random() < 0.3;
    const dmg = crit ? 50 : 25;
    enemyHP -= dmg;
    msg = `你施放技能造成 ${dmg} 傷害${crit ? "（暴擊）" : ""}`;
  }

  if (enemyHP <= 0) {
    enemyHP = 0;
    victoryBox.style.display = "block";
  }

  enemyHPSpan.innerText = enemyHP;

  const enemyAtk = Math.floor(Math.random() * 15);
  playerHP -= enemyAtk;
  if (playerHP < 0) playerHP = 0;
  playerHPSpan.innerText = playerHP;

  log.innerText = msg + `\n敵人攻擊你造成 ${enemyAtk} 傷害。`;
}
</script>

</body>
</html>
