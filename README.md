<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>暗棋終極穩定版</title>
    <style>
        :root { --red: #d32f2f; --black: #212121; --board: #5d4037; --cell: #d7ccc8; }
        body { font-family: sans-serif; display: flex; flex-direction: column; align-items: center; background: #eee; margin: 0; padding: 10px; }
        
        /* 指示框 */
        #status-bar { width: 90%; max-width: 340px; padding: 10px 0; font-size: 20px; font-weight: bold; border-radius: 8px; margin: 10px 0; text-align: center; }
        .turn-red { background: var(--red); color: white; }
        .turn-black { background: var(--black); color: white; }

        /* 響應式棋盤 */
        #board { display: grid; grid-template-columns: repeat(4, 1fr); gap: 8px; background: var(--board); padding: 12px; border-radius: 12px; width: 90vw; max-width: 340px; }
        .cell { aspect-ratio: 1/1; background: var(--cell); border-radius: 50%; display: flex; justify-content: center; align-items: center; cursor: pointer; font-size: clamp(1.5rem, 8vw, 2.2rem); font-weight: bold; user-select: none; position: relative; }
        
        /* 棋子狀態 */
        .covered { background: #a1887f !important; color: transparent !important; border: 2px dashed #3e2723; }
        .empty { background: rgba(0,0,0,0.1) !important; border: none; }
        .red { color: var(--red); border: 3px solid var(--red); background: white; }
        .black { color: var(--black); border: 3px solid var(--black); background: white; }
        .selected { outline: 5px solid #ffeb3b; z-index: 10; box-shadow: 0 0 15px #ffeb3b; }

        .controls { margin-top: 15px; display: flex; gap: 10px; width: 90%; max-width: 340px; }
        button { flex: 1; padding: 12px; font-size: 16px; border-radius: 5px; border: none; background: var(--board); color: white; cursor: pointer; }
    </style>
</head>
<body>

    <div id="status-bar" class="turn-red">紅方下子</div>
    <div id="board"></div>
    <div class="controls">
        <button onclick="resetGame()">重新開局</button>
        <button onclick="toggleMusic()">音樂</button>
    </div>

    <audio id="bgMusic" loop src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3"></audio>

    <script>
        const PIECES = ['帥','仕','仕','相','相','俥','俥','傌','傌','炮','炮','兵','兵','兵','兵','兵','將','士','士','象','象','車','車','馬','馬','砲','砲','卒','卒','卒','卒','卒'];
        const RANK = {'帥':7,'將':7,'仕':6,'士':6,'相':5,'象':5,'俥':4,'車':4,'傌':3,'馬':3,'炮':2,'砲':2,'兵':1,'卒':1};
        let gameState = [], selected = null, turn = 'red';

        function resetGame() {
            gameState = [...PIECES].sort(() => Math.random() - 0.5).map(n => ({
                name: n, side: '帥仕相俥傌炮兵'.includes(n) ? 'red' : 'black', isCovered: true
            }));
            selected = null; turn = 'red'; updateUI();
        }

        function updateUI() {
            const bar = document.getElementById('status-bar');
            bar.innerText = turn === 'red' ? '紅方下子' : '黑方下子';
            bar.className = turn === 'red' ? 'turn-red' : 'turn-black';
            render();
        }

        function render() {
            const b = document.getElementById('board'); b.innerHTML = '';
            gameState.forEach((p, i) => {
                const div = document.createElement('div');
                div.className = 'cell';
                if (!p) div.classList.add('empty');
                else if (p.isCovered) div.classList.add('covered');
                else { div.innerText = p.name; div.classList.add(p.side); }
                if (selected === i) div.classList.add('selected');
                div.onclick = () => handleClick(i);
                b.appendChild(div);
            });
        }

        function handleClick(i) {
            const p = gameState[i];
            
            // 1. 翻棋邏輯
            if (p && p.isCovered) {
                p.isCovered = false;
                if (navigator.vibrate) navigator.vibrate(30);
                endTurn(); return;
            }

            // 2. 選取邏輯
            if (p && !p.isCovered && p.side === turn) {
                selected = (selected === i) ? null : i;
                render(); return;
            }

            // 3. 移動或吃子邏輯
            if (selected !== null) {
                if (canPerformMove(selected, i)) {
                    gameState[i] = gameState[selected];
                    gameState[selected] = null;
                    if (navigator.vibrate) navigator.vibrate(50);
                    endTurn();
                }
            }
        }

        function canPerformMove(from, to) {
            const p1 = gameState[from], p2 = gameState[to];
            const r1 = Math.floor(from/4), c1 = from%4, r2 = Math.floor(to/4), c2 = t2 = to%4;
            const dist = Math.abs(r1-r2) + Math.abs(c1-c2);

            // 炮跳吃特殊邏輯
            if (p1.name === '炮' || p1.name === '砲') {
                if (p2 && p1.side !== p2.side && (r1 === r2 || c1 === c2)) {
                    let midCount = 0;
                    let s = (r1 === r2) ? Math.min(c1, c2) : Math.min(r1, r2);
                    let e = (r1 === r2) ? Math.max(c1, c2) : Math.max(r1, r2);
                    for (let k = s + 1; k < e; k++) {
                        if (gameState[(r1 === r2) ? r1 * 4 + k : k * 4 + c1]) midCount++;
                    }
                    if (midCount === 1) return true;
                }
            }

            // 一般移動到空位或吃子 (限一格)
            if (dist !== 1) return false;
            if (!p2) return true; // 空位移動
            if (p1.side === p2.side) return false; // 禁止自殘
            
            // 等級判定
            if (RANK[p1.name] === 7 && RANK[p2.name] === 1) return false; // 帥不吃卒
            if (RANK[p1.name] === 1 && RANK[p2.name] === 7) return true;  // 卒吃帥
            return RANK[p1.name] >= RANK[p2.name];
        }

        function endTurn() { selected = null; turn = (turn === 'red') ? 'black' : 'red'; updateUI(); }
        function toggleMusic() { const m = document.getElementById('bgMusic'); m.paused ? m.play() : m.pause(); }
        resetGame();
    </script>
</body>
</html>
