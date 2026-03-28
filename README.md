<!DOCTYPE html>
<html lang="zh-TW">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>禾火人 /ouo/</title>
<style>
    :root {
        --color-autumn-bg: #F7F3E8; 
        --color-sumi-text: #2B2B2B; 
        --color-sumi-blue: #3A4F6A; 
        --color-sumi-green: #4F6353; 
        --color-sky-blue: #64A1C8;  
        --color-leaf-orange: #D48166; 
        --color-milk-green: #E8F5E9; 
        --color-nav-height: 80px; 
    }

    /* 1. 全域修正：防止寬度被撐開 */
    *, *::before, *::after {
        box-sizing: border-box;
    }

    html, body {
        margin: 0; padding: 0;
        width: 100%;
        overflow-x: hidden; /* 徹底禁止橫向捲動，防止置中偏移 */
        background-color: var(--color-autumn-bg);
        font-family: "PingFang TC", "Microsoft JhengHei", sans-serif;
    }

    body {
        display: flex;
        flex-direction: column;
        align-items: center; /* 讓所有內容在 Cross Axis 置中 */
        padding-top: calc(var(--color-nav-height) + 30px);
        padding-bottom: 60px;
    }

    /* 2. 楓葉與點擊容器：使用 fixed 且不佔空間 */
    #leaf-container {
        position: fixed; top: 0; left: 0; width: 100vw; height: 100vh;
        pointer-events: none; z-index: 9999;
    }
    .leaf-fall, .click-leaf { position: fixed; pointer-events: none; user-select: none; z-index: 10000; }
    
    @keyframes fall {
        0% { transform: translateY(-50px) rotate(0deg); opacity: 0; }
        10% { opacity: 0.8; }
        100% { transform: translateY(110vh) rotate(360deg); opacity: 0; }
    }

    /* 3. 導覽列修正：確保內容也置中 */
    nav {
        position: fixed; top: 0; left: 0; width: 100%; height: var(--color-nav-height);
        background-color: var(--color-sumi-blue);
        display: flex; justify-content: center; align-items: center;
        z-index: 1000; box-shadow: 0 4px 10px rgba(0,0,0,0.2);
    }
    .nav-links { display: flex; gap: 15px; }
    .nav-item, .dropdown-trigger {
        color: white; text-decoration: none; font-weight: bold; font-size: 1.05em;
        padding: 8px 12px; border: 1px solid rgba(255,255,255,0.3); border-radius: 6px;
    }

    .dropdown { position: relative; }
    .dropdown-content {
        display: none; position: absolute; background: white; min-width: 140px;
        top: 100%; left: 50%; transform: translateX(-50%); border-radius: 8px;
    }
    .dropdown:hover .dropdown-content { display: block; }
    .dropdown-content a { color: var(--color-sumi-blue); padding: 12px; display: block; text-decoration: none; }

    /* 4. 主容器修正：這是最容易歪掉的地方 */
    .container {
        width: 90%;
        max-width: 700px;
        background: #fff;
        padding: 40px 30px;
        margin: 0 auto; /* 強制左右 margin 相等 */
        border-radius: 8px;
        border-top: 10px solid var(--color-sumi-blue);
        box-shadow: 0 10px 30px rgba(0,0,0,0.1);
        position: relative;
        z-index: 5;
    }

    h1.site-title { color: var(--color-sumi-blue); text-align: center; letter-spacing: 5px; margin-bottom: 5px; }
    .site-subtitle { text-align: center; color: var(--color-sumi-green); margin-bottom: 30px; display: block; }

    .greeting-box {
    .greeting-box {
    border: 2px solid var(--color-leaf-orange); 
    border-radius: 50px;
    padding: 10px 25px; 
    margin: 0 auto 40px auto; 
    width: fit-content;
    text-align: center; 
    cursor: pointer;
    transition: 0.3s; /* 讓變色效果更平滑 */
}

.greeting-box:hover {
    background-color: var(--color-leaf-orange); /* 移上去背景變橘色 */
}

.greeting-box:hover span {
    color: white !important; /* 移上去文字變白色 */
}
        border: 2px solid var(--color-leaf-orange); border-radius: 50px;
        padding: 10px 25px; margin: 0 auto 40px auto; width: fit-content;
        text-align: center; cursor: pointer;
    }

    /* 留言板與跑馬燈 */
    .message-board { background: var(--color-milk-green); padding: 20px; border-radius: 12px; border: 2px solid var(--color-sky-blue); }
    .marquee-area { background: #fff; overflow: hidden; margin-bottom: 15px; border-radius: 6px; padding: 10px 0; }
    .marquee-line { display: flex; white-space: nowrap; animation: marquee 25s linear infinite; }
    @keyframes marquee { 0% { transform: translateX(100%); } 100% { transform: translateX(-150%); } }
    .marquee-item { padding-right: 60px; font-weight: bold; color: var(--color-sumi-blue); }

    .message-form input, .message-form textarea { width: 100%; padding: 10px; margin-bottom: 10px; border: 1px solid #ddd; border-radius: 5px; }
    .submit-btn { width: 100%; background: var(--color-sumi-blue); color: #fff; border: none; padding: 12px; border-radius: 6px; font-weight: bold; cursor: pointer; }

    h3.section-title { color: var(--color-sumi-blue); border-left: 6px solid var(--color-sky-blue); padding-left: 15px; margin-top: 40px; }
    .pit-category { border-left: 3px solid var(--color-sumi-green); padding-left: 15px; margin-bottom: 25px; }
    .pit-inline-list { line-height: 1.8; word-break: break-all; }
</style>
</head>
<body>

<a href="https://www.youtube.com/watch?v=dQw4w9WgXcQ" target="_blank" style="text-decoration: none;">
    <div class="greeting-box">
        <span style="color: var(--color-leaf-orange); font-weight: bold;">「相逢即是有緣。」</span>
    </div>
</a>

<nav>
    <div class="nav-links">
        <a href="#about" class="nav-item">關於我</a>
        <div class="dropdown">
            <span class="dropdown-trigger">坑 ▾</span>
            <div class="dropdown-content">
                <a href="#pit-anime">動漫/小說</a>
                <a href="#pit-game">遊戲/VT</a>
                <a href="#pit-retired">退坑</a>
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
    
    <div class="greeting-box">
        <span style="color: var(--color-leaf-orange); font-weight: bold;">「相逢即是有緣。」</span>
    </div>

    <h3 id="about" class="section-title">Ⅰ.🍂 關於我 🍂</h3>
    <ul style="list-style: none; padding-left: 5px; line-height: 2;">
        <li><strong>+ cn</strong> : 禾火 / 秋 / Aki</li>
        <li><strong>+✨</strong> : 10.02 天秤 | INTP</li>
        <li><strong>+✨</strong> : 羽山秋人重度依賴 🍣 (漫畫版)</li>
        <li style="color: var(--color-sumi-green);">└ 完全貓派 特別喜歡傲嬌貓塑</li>
    </ul>

    <h3 id="pit" class="section-title">Ⅱ. 坑</h3>
    <div id="pit-anime" class="pit-category">
        <h4>◈ 深坑 - 動漫/小說</h4>
        <div class="pit-inline-list">
            《玩偶遊戲》羽山秋人、《失憶投捕》要圭、《全知讀者視角》金獨子、《TADC》Jax、《Alien Stage》Till、《極惡》Blitzø x 親王、《時光代理人》光 x 時、墨家三部曲。
        </div>
    </div>
    <div id="pit-game" class="pit-category">
        <h4>◈ 深坑 - 遊戲/VT</h4>
        <div class="pit-inline-list">
            《新世界狂歡》奧利文/八雲/艾德蒙特、Shoto、《星鐵》、《原神》、《絕區零》、《文字化化》爬爬、《輝耀姬》輝夜 x 彩P。<br>
            <strong style="color: var(--color-sky-blue);">[ 正在等待菲林斯 BJD... ]</strong>
        </div>
    </div>

    <h3 id="attr" class="section-title">Ⅲ. 屬性</h3>
    <p><strong>+ ✨</strong> : 雜食黨 但是官配 > 所有</p>
    <p><strong>+ ✨</strong> : <span style="color: var(--color-sumi-blue); font-weight: bold;">BL >> GB > BG = GL</span></p>

    <h3 id="message" class="section-title">Ⅳ. 留言板</h3>
    <div class="message-board">
        <div class="marquee-area"><div class="marquee-line" id="marquee-list"></div></div>
        <input type="text" id="user-name" placeholder="你的名字">
        <textarea id="user-msg" rows="2" placeholder="跟我說說話(❁´◡`❁)"></textarea>
        <button class="submit-btn" onclick="addMsg()">送出留言</button>
    </div>

    <h3 id="contact" class="section-title">Ⅴ. 聯絡 </h3>
    <p><a href="https://www.facebook.com/kowai.yu/" target="_blank">Facebook</a> / <a href="https://www.instagram.com/grassss_yuuuu/" target="_blank">Instagram</a></p>
    <p>Discord: traveler7378</p>

    <h3 id="other" class="section-title">Ⅵ. 其他</h3>
    <p>偶爾會開淘寶代購團。喜歡手繪 > 電繪，正在猶豫買平板還是繪圖螢幕... 如果有人可以阻止我花錢，我會很感謝你的！</p>
</div>

<script>
    // 楓葉下落
    function leafFall() {
        const leaf = document.createElement('div');
        leaf.className = 'leaf-fall';
        leaf.innerText = ['🍁', '🍂', '🍃'][Math.floor(Math.random()*3)];
        leaf.style.left = Math.random() * 100 + 'vw';
        const dur = Math.random() * 5 + 5;
        leaf.style.animation = `fall ${dur}s linear forwards`;
        document.getElementById('leaf-container').appendChild(leaf);
        setTimeout(() => leaf.remove(), dur * 1000);
    }
    setInterval(leafFall, 800);

    // 點擊噴葉子
    document.addEventListener('click', (e) => {
        for(let i=0; i<6; i++) {
            const l = document.createElement('div');
            l.className = 'click-leaf';
            l.innerText = '🍂';
            l.style.left = e.clientX + 'px'; l.style.top = e.clientY + 'px';
            const tx = (Math.random()-0.5)*200, ty = (Math.random()-0.5)*200;
            l.animate([
                { transform: 'translate(0,0) scale(1)', opacity: 1 },
                { transform: `translate(${tx}px, ${ty}px) scale(0)`, opacity: 0 }
            ], { duration: 800 });
            document.body.appendChild(l);
            setTimeout(() => l.remove(), 800);
        }
    });

    // 留言板
    let data = [{n: "系統", t: "歡迎來到禾火人的空間！"}, {n: "秋", t: "今天想吃壽司🍣"}];
    function render() {
        document.getElementById('marquee-list').innerHTML = data.map(i => `<span class="marquee-item">${i.n}: ${i.t}</span>`).join('') + 
        data.map(i => `<span class="marquee-item">${i.n}: ${i.t}</span>`).join('');
    }
    function addMsg() {
        const n = document.getElementById('user-name').value, t = document.getElementById('user-msg').value;
        if(!n || !t) return;
        data.unshift({n, t}); render();
        document.getElementById('user-name').value = ''; document.getElementById('user-msg').value = '';
    }
    render();
</script>
</body>
</html>
