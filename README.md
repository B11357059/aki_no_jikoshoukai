# aki_no_jikoshoukai[index.html](https://github.com/user-attachments/files/26326229/index.html)
<!DOCTYPE html>
<html lang="zh-TW">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>禾火人 /ouo/</title>
<style>

/* 點擊噴發葉子的基礎樣式 */
.click-leaf {
    position: fixed;
    pointer-events: none; /* 確保不會擋到下方的按鈕 */
    z-index: 10000;       /* 確保在最上層 */
    user-select: none;
    font-size: 20px;
    will-change: transform, opacity;
}

/* 噴發動畫：隨機位移與縮小消失 */
@keyframes leaf-burst {
    0% {
        transform: translate(-50%, -50%) scale(1) rotate(0deg);
        opacity: 1;
    }
    100% {
        /* 位移與旋轉由 JS 動態設定，這裡設定基礎結束狀態 */
        transform: translate(var(--tx), var(--ty)) scale(0) rotate(var(--tr));
        opacity: 0;
    }
}

    :root {
        --color-autumn-bg: #F7F3E8; 
        --color-sumi-text: #2B2B2B; 
        --color-sumi-blue: #3A4F6A; 
        --color-sumi-green: #4F6353; 
        --color-sky-blue: #64A1C8;  
        --color-leaf-orange: #D48166; 
        --color-milk-green: #E8F5E9; 
        --color-milk-gray: #BDBDBD;  
        --nav-height: 95px; 
    }

    html { scroll-behavior: smooth; scroll-padding-top: calc(var(--nav-height) + 20px); }

    /* 修正置中問題：確保 body 依然是 flex 且不被側邊擠壓 */
    body {
        background-color: var(--color-autumn-bg); color: var(--color-sumi-text);
        font-family: "PingFang TC", "Microsoft JhengHei", sans-serif;
        margin: 0; padding-top: calc(var(--nav-height) + 40px); padding-bottom: 60px;
        display: flex; flex-direction: column; align-items: center; 
        overflow-x: hidden; position: relative; width: 100%;
    }

    /* 楓葉容器：固定定位，不佔據空間 */
    #leaf-container {
        position: fixed; top: 0; left: 0; width: 100vw; height: 100vh;
        pointer-events: none; z-index: 9999; overflow: hidden;
    }
    .leaf-fall { position: absolute; top: -50px; animation: fall linear infinite; user-select: none; }
    @keyframes fall {
        0% { transform: translateY(0vh) rotate(0deg) translateX(0px); opacity: 0; }
        10% { opacity: 0.8; }
        100% { transform: translateY(110vh) rotate(360deg) translateX(100px); opacity: 0; }
    }

    /* 導覽列 */
    nav {
        position: fixed; top: 0; width: 100%; height: var(--nav-height);
        background-color: var(--color-sumi-blue); color: white;
        display: flex; justify-content: center; align-items: center;
        z-index: 1000; box-shadow: 0 4px 12px rgba(0,0,0,0.15);
    }
    .nav-links { display: flex; gap: 15px; align-items: center; }
    .nav-item, .dropdown-trigger {
        color: white; text-decoration: none; font-size: calc(1.1em + 3px); 
        font-weight: 900; padding: 8px 15px; border: 2px solid rgba(255,255,255,0.3); 
        border-radius: 8px; cursor: pointer; transition: 0.3s;
    }
    .nav-item:hover, .dropdown:hover .dropdown-trigger { border-color: var(--color-sky-blue); color: var(--color-sky-blue); }

    .dropdown { position: relative; display: flex; align-items: center; }
    .dropdown-content {
        display: none; position: absolute; background: white; min-width: 200px;
        box-shadow: 0px 8px 16px rgba(0,0,0,0.2); border-radius: 8px; 
        top: 80%; left: 50%; transform: translateX(-50%); z-index: 1001;
    }
    .dropdown-content a { color: var(--color-sumi-blue) !important; padding: 15px; display: block; text-decoration: none; font-weight: bold; }
    .dropdown:hover .dropdown-content { display: block; }

    /* 主容器：確保左右 margin 為 auto 實現置中 */
    .container {
        max-width: 720px; width: 90%; background: #fff; padding: 50px;
        box-shadow: 0 10px 30px rgba(0,0,0,0.08); border-radius: 4px;
        border-top: 8px solid var(--color-sumi-blue); position: relative; z-index: 1;
        margin: 0 auto;
    }

    h1.site-title { color: var(--color-sumi-blue); text-align: center; font-size: 2.8em; letter-spacing: 8px; margin-bottom: 5px; }
    .site-subtitle { text-align: center; font-size: 1em; color: var(--color-sumi-green); margin-bottom: 1.5em; display: block; }

    .greeting-box {
        cursor: pointer; border: 2px solid var(--color-leaf-orange);
        padding: 10px 30px; border-radius: 50px; margin: 0 auto 3.5em auto;
        width: fit-content; text-align: center; transition: 0.3s;
    }
    .greeting-box:hover { background: var(--color-autumn-bg); transform: scale(1.05); }

    /* 跑馬燈 */
    .message-board { border: 3px solid var(--color-sky-blue); background-color: var(--color-milk-green); padding: 25px; border-radius: 12px; margin-top: 20px; }
    .marquee-area { background: rgba(255, 255, 255, 0.4); border-radius: 8px; margin-bottom: 20px; padding: 10px 0; overflow: hidden; border: 1px solid rgba(100, 161, 200, 0.2); }
    .marquee-line { display: flex; white-space: nowrap; margin: 5px 0; animation: marquee 35s linear infinite; }
    .marquee-line.reverse { animation: marquee-reverse 35s linear infinite; }
    @keyframes marquee { 0% { transform: translateX(100%); } 100% { transform: translateX(-150%); } }
    @keyframes marquee-reverse { 0% { transform: translateX(-150%); } 100% { transform: translateX(100%); } }
    .marquee-item { display: inline-block; padding-right: 120px; color: var(--color-sumi-blue); font-weight: bold; }

    /* 留言表單 */
    .message-form input, .message-form textarea { width: 100%; padding: 12px; margin-bottom: 15px; border: 1px solid #ccc; border-radius: 6px; box-sizing: border-box; }
    .btn-group { display: flex; gap: 10px; }
    .submit-btn { flex: 2; background-color: var(--color-sumi-blue); color: white; border: none; padding: 12px; border-radius: 6px; font-weight: bold; cursor: pointer; }
    .view-all-btn { flex: 1; background-color: white; color: var(--color-sumi-blue); border: 2px solid var(--color-sumi-blue); padding: 12px; border-radius: 6px; font-weight: bold; cursor: pointer; }

    /* Modal */
    .modal { display: none; position: fixed; z-index: 3000; left: 0; top: 0; width: 100%; height: 100%; background-color: rgba(0,0,0,0.6); backdrop-filter: blur(5px); align-items: center; justify-content: center; }
    .modal-content { background: white; width: 85%; max-width: 500px; border-radius: 15px; padding: 30px; position: relative; max-height: 70vh; overflow-y: auto; }
    .close-modal { position: absolute; right: 20px; top: 15px; font-size: 24px; cursor: pointer; color: #aaa; }

    /* 區塊樣式 */
    h3.section-title {
        color: var(--color-sumi-blue); border-left: 8px solid var(--color-sky-blue);
        padding-left: 18px; margin-top: 50px; margin-bottom: 25px;
        background: linear-gradient(to right, rgba(100, 161, 200, 0.1), transparent); font-size: 1.4em;
    }
    .pit-category { margin-bottom: 30px; border-left: 3px solid var(--color-sumi-green); padding-left: 20px; }
    .pit-inline-list { line-height: 1.8; }
</style>
</head>
<body>

<div id="leaf-container"></div>

<nav>
    <div class="nav-links">
        <a href="#about" class="nav-item">關於我</a>
        <div class="dropdown">
            <div class="dropdown-trigger">坑 ▾</div>
            <div class="dropdown-content">
                <a href="#pit-anime">動漫/小說</a>
                <a href="#pit-game">遊戲/VT</a>
                <a href="#pit-retired">淡坑/退坑</a>
            </div>
        </div>
        <a href="#attr" class="nav-item">屬性</a>
        <a href="#message" class="nav-item">留言</a>
        <a href="#contact" class="nav-item">聯絡</a>
    </div>
</nav>

<div class="container">
    <h1 class="site-title">禾火人</h1>
    <span class="site-subtitle">都點進來了不看看我嗎ouo</span>
    
    <div class="greeting-box" onclick="handleInteraction(event)">
        <h2 style="color: var(--color-leaf-orange); font-size: 1.2em; margin: 0; font-weight: normal; letter-spacing: 3px; pointer-events: none;">「相逢即是有緣。」</h2>
    </div>

    <h3 id="about" class="section-title">Ⅰ.🍂 關於我 🍂</h3>
    <ul style="list-style: none; padding-left: 10px;">
        <li><strong>+ cn</strong> : 禾火 / 秋 / Aki</li>
        <li><strong>+✨</strong> : 10.02 天秤 | INTP</li>
        <li><strong>+✨</strong> : 羽山秋人重度依賴 🍣</li>
        <li style="color: var(--color-sumi-green); font-size: 0.95em;">└ 完全貓派 特別喜歡傲嬌貓塑</li>
        <li style="margin-top:10px; color: var(--color-sumi-green); font-weight: bold;">- 不拒同擔，幾乎無雷，本人很好相處可以多找我聊天!</li>
    </ul>

    <h3 id="pit" class="section-title">Ⅱ. 坑 </h3>
    <div id="pit-anime" class="pit-category">
        <h4>◈ 深坑 - 動漫/小說</h4>
        <div class="pit-inline-list">
            《玩偶遊戲》羽山秋人、《失憶投捕》要圭、《全知讀者視角》金獨子、《TADC》Jax、《Alien Stage》Till、《極惡》Blitzø x 親王、《時光代理人》光 x 時、墨家三部曲。
        </div>
    </div>
    <div id="pit-game" class="pit-category">
        <h4>◈ 深坑 - 遊戲/VT</h4>
        <div class="pit-inline-list">
            《新世界狂歡》奧利文/八雲/艾德蒙特、Shoto、《星鐵》、《原神》、《絕區零》、《文字化化》爬爬、《輝耀姬》輝夜 x 彩P。
            <br><span style="color: var(--color-sky-blue); font-weight: bold;">[ 正在等待菲林斯 BJD... ]</span>
        </div>
    </div>
    <div id="pit-retired" class="pit-category">
        <h4>◈ 淡坑 / 退坑</h4>
        <div class="pit-inline-list" style="color: #888;">
            《世界計畫》、乙遊、FPS遊戲、咒術、鏈鋸人、NIJI EN... 《逆水寒》、《燕雲》已完全退坑
        </div>
    </div>

    <h3 id="attr" class="section-title">Ⅲ. 屬性</h3>
    <div style="padding-left: 15px;">
        <p><strong>+ ✨</strong> : 雜食黨 但是官配 > 所有</p>
        <p><strong>+ ✨</strong> : <span style="color: var(--color-sumi-blue); font-weight: bold;">BL >> GB > BG = GL</span></p>
        <p><strong>+ ✨</strong> : [ all男主控 ]</p>
    </div>

    <h3 id="message" class="section-title">Ⅳ. 留言板</h3>
    <div class="message-board">
        <div class="marquee-area"><div class="marquee-line" id="marquee-1"></div><div class="marquee-line reverse" id="marquee-2"></div></div>
        <div class="message-form">
            <input type="text" id="user-name" placeholder="你的名字">
            <textarea id="user-msg" rows="3" placeholder="想對我說什麼？"></textarea>
            <div class="btn-group">
                <button class="submit-btn" onclick="submitMessage()">送出留言</button>
                <button class="view-all-btn" onclick="toggleModal(true)">查看所有</button>
            </div>
        </div>
    </div>

    <div id="lobby-modal" class="modal">
        <div class="modal-content">
            <span class="close-modal" onclick="toggleModal(false)">&times;</span>
            <h3 style="border-bottom: 2px solid var(--color-sky-blue); padding-bottom: 10px;">✨ 留言大廳</h3>
            <div id="full-lobby-list"></div>
        </div>
    </div>

    <h3 id="contact" class="section-title">Ⅴ. 聯絡 </h3>
    <div style="padding-left: 15px;">
        <p><a href="https://www.facebook.com/kowai.yu/" target="_blank">FACEBOOK</a> / <a href="https://www.instagram.com/grassss_yuuuu/" target="_blank">INSTAGRAM</a></p>
        <p>Discord - traveler7378 (活躍)</p>
    </div>

    <h3 id="other" class="section-title">Ⅵ. 其他</h3>
    <div style="padding-left: 15px;">
        <p>偶爾會開淘寶代購團，有需要也可以找我 我很便宜:D</p>
        <p>喜歡畫圖 (手繪 > 電繪) 正在猶豫買平板還是繪圖螢幕...</p>
        <p style="color: var(--color-sumi-blue); font-weight: bold;">如果有人可以阻止我花錢 我會很感謝你的</p>
    </div>
</div>

<script>
    // 楓葉與互動邏輯
    function createLeaf() {
        const leaf = document.createElement('div');
        leaf.className = 'leaf-fall';
        const types = ['🍁', '🍂', '🍃'];
        leaf.innerText = types[Math.floor(Math.random()*types.length)];
        leaf.style.left = Math.random() * 100 + 'vw';
        const duration = Math.random() * 5 + 5;
        leaf.style.animationDuration = duration + 's';
        document.getElementById('leaf-container').appendChild(leaf);
        setTimeout(() => leaf.remove(), duration * 1000);
    }
    setInterval(createLeaf, 700);

    function handleInteraction(e) {
        for(let i=0; i<8; i++) {
            const leaf = document.createElement('div');
            leaf.style.position = 'fixed'; leaf.style.left = e.clientX + 'px'; leaf.style.top = e.clientY + 'px';
            leaf.innerText = '🍂'; leaf.style.pointerEvents = 'none';
            leaf.animate([{ transform: 'translate(0,0) scale(1)', opacity: 1 }, 
            { transform: `translate(${(Math.random()-0.5)*300}px, ${(Math.random()-0.5)*300}px) scale(0)`, opacity: 0 }], { duration: 1000 });
            document.body.appendChild(leaf);
            setTimeout(() => leaf.remove(), 1000);
        }
    }

    // 留言板邏輯
    let msgs = [{name: "系統君", text: "相逢即是有緣！"}, {name: "秋", text: "想吃壽司 🍣"}, {name: "Yu", text: "BL >> GB > BG = GL 哦～"}];
    function updateMarquee() {
        const l1 = document.getElementById('marquee-1'), l2 = document.getElementById('marquee-2');
        let h1 = '', h2 = '';
        msgs.slice(0, 10).forEach((m, i) => {
            const item = `<span class="marquee-item">${m.name}: ${m.text}</span>`;
            if(i % 2 === 0) h1 += item; else h2 += item;
        });
        l1.innerHTML = h1 + h1; l2.innerHTML = h2 + h2;
    }
    function submitMessage() {
        const n = document.getElementById('user-name').value, m = document.getElementById('user-msg').value;
        if(!n || !m) return alert("要填名字跟內容喔！");
        msgs.unshift({name: n, text: m}); updateMarquee();
        document.getElementById('user-name').value = ''; document.getElementById('user-msg').value = '';
    }
    function toggleModal(s) {
        document.getElementById('lobby-modal').style.display = s ? 'flex' : 'none';
        if(s) document.getElementById('full-lobby-list').innerHTML = msgs.map(m => `<div style="padding:10px; border-bottom:1px solid #eee;"><strong>${m.name}:</strong> ${m.text}</div>`).join('');
    }
    updateMarquee();

// 點擊噴發落葉插件
document.addEventListener('click', function(e) {
    // 一次噴出的葉子數量
    const leafCount = 8; 
    const leafTypes = ['🍂', '🍁', '🍃'];

    for (let i = 0; i < leafCount; i++) {
        const leaf = document.createElement('div');
        leaf.className = 'click-leaf';
        leaf.innerText = leafTypes[Math.floor(Math.random() * leafTypes.length)];

        // 設定初始點擊位置
        leaf.style.left = e.clientX + 'px';
        leaf.style.top = e.clientY + 'px';

        // 隨機生成噴發的方向與旋轉角度 (透過 CSS 變數傳遞)
        const tx = (Math.random() - 0.5) * 300 + 'px'; // 左右位移距離
        const ty = (Math.random() - 0.5) * 300 + 'px'; // 上下位移距離
        const tr = (Math.random() * 720 - 360) + 'deg'; // 旋轉角度

        leaf.style.setProperty('--tx', tx);
        leaf.style.setProperty('--ty', ty);
        leaf.style.setProperty('--tr', tr);

        // 設定動畫時間與特效
        leaf.style.animation = `leaf-burst ${Math.random() * 0.5 + 0.8}s cubic-bezier(0.1, 0.5, 0.3, 1) forwards`;

        document.body.appendChild(leaf);

        // 動畫結束後移除元素，維持網頁效能
        leaf.addEventListener('animationend', () => {
            leaf.remove();
        });
    }
});

</script>
</body>
</html>
