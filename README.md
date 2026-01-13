<!DOCTYPE html>
   
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>暗棋終極自定義版</title>
    <style>
        :root { --red: #d32f2f; --black: #212121; --board: #4e342e; --cell: #d7ccc8; }
        body { font-family: "Microsoft JhengHei", sans-serif; display: flex; flex-direction: column; align-items: center; background: #f5f5f5; margin: 0; padding: 10px; touch-action: manipulation; }
        
        /* 指示框 */
        #status-bar { width: 95%; max-width: 340px; padding: 12px 0; font-size: 22px; font-weight: bold; border-radius: 12px; margin: 10px 0; text-align: center; box-shadow: 0 4px 10px rgba(0,0,0,0.2); }
        .turn-red { background: var(--red); color: white; border: 3px solid #b71c1c; }
        .turn-black { background: var(--black); color: white; border: 3px solid #000; }

        /* 響應式棋盤 */
        #board { display: grid; grid-template-columns: repeat(4, 1fr); gap: 2vw; background: var(--board); padding: 15px; border-radius: 15px; width: 90vw; max-width: 340px; box-shadow: 0 10px 30px rgba(0,0,0,0.5); }
        
        .cell {
            aspect-ratio: 1/1; background: var(--cell); border-radius: 50%;
            display: flex; justify-content: center; align-items: center;
            cursor: pointer; font-size: clamp(1.5rem, 8vw, 2.3rem); font-weight: bold;
            user-select: none; position: relative; transition: transform 0.1s;
        }

        /* 棋子背後圖片設置 */
        .covered { 
            background-image: url('https://anihk.com/cdn/shop/articles/218.jpg?v=1753970441'); 
            background-size: cover; background-position: center; border: 2px solid #3e2723; color: transparent !important;
        }

        .empty { background: rgba(0,0,0,0.2) !important; border: none; }
        .red { color: var(--red); border: 4px solid var(--red); background: white; box-shadow: inset 0 0 10px rgba(211,47,47,0.2); }
        .black { color: var(--black); border: 4px solid var(--black); background: white; box-shadow: inset 0 0 10px rgba(0,0,0,0.2); }
        .selected { outline: 5px solid #ffeb3b; outline-offset: 2px; z-index: 10; transform: scale(1.05); }

        .controls { margin-top: 20px; display: flex; gap: 10px; width: 95%; max-width: 340px; }
        button { flex: 1; padding: 15px; font-size: 16px; border-radius: 8px; border: none; background: var(--board); color: white; cursor: pointer; font-weight: bold; }
        button:active { background: #3e2723; }
    </style>
</head>
<body>
       <div id="status-bar" class="turn-yellow"> 烏薩-棋 </div> 
    <div id="status-bar" class="turn-red">紅方下子</div>
    <div id="board"></div>
    <div class="controls">
        <button onclick="resetGame()">重新開局</button>
        <button onclick="toggleMusic()">音樂播放</button>
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
            
            // 1. 翻棋
            if (p && p.isCovered) {
                p.isCovered = false;
                if (navigator.vibrate) navigator.vibrate(30);
                endTurn(); return;
            }

            // 2. 選取自己的棋子
            if (p && !p.isCovered && p.side === turn) {
                selected = (selected === i) ? null : i;
                render(); return;
            }

            // 3. 移動到空位或吃子
            if (selected !== null) {
                if (canMove(selected, i)) {
                    gameState[i] = gameState[selected];
                    gameState[selected] = null;
                    if (navigator.vibrate) navigator.vibrate(50);
                    endTurn();
                }
            }
        }

        function canMove(from, to) {
            const p1 = gameState[from], p2 = gameState[to];
            const r1 = Math.floor(from/4), c1 = from%4, r2 = Math.floor(to/4), c2 = to%4;
            const dist = Math.abs(r1-r2) + Math.abs(c1-c2);

            // 炮跳吃邏輯
            if (p1.name === '炮' || p1.name === '砲') {
                if (p2 && p1.side !== p2.side && (r1 === r2 || c1 === c2)) {
                    let count = 0, s = (r1 === r2) ? Math.min(c1, c2) : Math.min(r1, r2), e = (r1 === r2) ? Math.max(c1, c2) : Math.max(r1, r2);
                    for (let k = s + 1; k < e; k++) if (gameState[(r1 === r2) ? r1 * 4 + k : k * 4 + c1]) count++;
                    if (count === 1) return true;
                }
            }

            // 一般移動/吃子
            if (dist !== 1) return false;
            if (!p2) return true; // 移動到空位
            if (p1.side === p2.side) return false;
            if (RANK[p1.name] === 7 && RANK[p2.name] === 1) return false;
            if (RANK[p1.name] === 1 && RANK[p2.name] === 7) return true;
            return RANK[p1.name] >= RANK[p2.name];
        }

        function endTurn() { selected = null; turn = (turn === 'red') ? 'black' : 'red'; updateUI(); }
        function toggleMusic() { const m = document.getElementById('bgMusic'); m.paused ? m.play() : m.pause(); }
        resetGame();
    </script>
</body>
</html>
