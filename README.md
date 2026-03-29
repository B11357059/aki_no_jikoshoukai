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
        --nav-height: 70px; 
    }

    /* 關鍵修正 2：設定網頁捲動偏移量，防止置中遮擋 */
    html {
        scroll-behavior: smooth; /* 平滑捲動 */
        /* 下面這行是重點：讓跳轉後的位置自動下移，空出 Nav 的高度 */
        scroll-padding-top: calc(var(--nav-height) + 15px); 
    }

    /* 核心重置：防止橫向溢出 */
    *, *::before, *::after { box-sizing: border-box; }

    body {
        margin: 0; padding: 0; width: 100%;
        overflow-x: hidden;
        background-color: var(--color-autumn-bg);
        font-family: "PingFang TC", "Microsoft JhengHei", sans-serif;
        display: flex; flex-direction: column; align-items: center;
        padding-top: calc(var(--nav-height) + 40px);
        padding-bottom: 80px;
    }

    /* 1. 導覽列 */
    nav {
        position: fixed; top: 0; left: 0; width: 100%; height: var(--nav-height);
        background-color: var(--color-sumi-blue);
        display: flex; justify-content: center; align-items: center;
        z-index: 1000; box-shadow: 0 4px 10px rgba(0,0,0,0.2);
    }
    .nav-links { display: grid; grid-template-columns: repeat(4, 1fr); gap: 8px; width: 95%; max-width: 550px; }
    .nav-item, .dropdown-trigger { color: white; text-decoration: none; font-weight: bold; padding: 10px 0; border: 1px solid rgba(255,255,255,0.2); border-radius: 8px; text-align: center; display: block; width: 100%; font-size: 0.9em; cursor: pointer; }

    /* 下拉選單 */
    .dropdown { position: relative; width: 100%; }
    .dropdown-content { display: none; position: absolute; background: white; min-width: 130px; top: 100%; left: 50%; transform: translateX(-50%); border-radius: 8px; box-shadow: 0 8px 16px rgba(0,0,0,0.15); }
    .dropdown:hover .dropdown-content { display: block; }
    .dropdown-content a { color: var(--color-sumi-blue); padding: 12px; display: block; text-decoration: none; font-size: 0.85em; font-weight: bold; text-align: center; }

    /* 2. 楓葉特效 */
    #leaf-container { position: fixed; top: 0; left: 0; width: 100vw; height: 100vh; pointer-events: none; z-index: 9999; }
    .leaf-fall, .click-leaf { position: fixed; pointer-events: none; z-index: 10000; }
    @keyframes fall { 0% { transform: translateY(-50px); opacity: 0; } 10% { opacity: 0.8; } 100% { transform: translateY(110vh) rotate(360deg); opacity: 0; } }

    /* 3. 主內容容器 */
    .container { width: 90%; max-width: 680px; background: #fff; padding: 50px 30px; margin: 0 auto; border-radius: 12px; border-top: 12px solid var(--color-sumi-blue); box-shadow: 0 15px 35px rgba(0,0,0,0.05); position: relative; z-index: 5; }
    h1.site-title { color: var(--color-sumi-blue); text-align: center; letter-spacing: 6px; margin-bottom: 8px; font-size: 2.2em; }
    .site-subtitle { text-align: center; color: var(--color-sumi-green); margin-bottom: 40px; display: block; }

    /* 瑞克搖連結 */
    .greeting-box { border: 2px solid var(--color-leaf-orange); border-radius: 50px; padding: 12px 30px; text-align: center; cursor: pointer; background: white; }
    .greeting-box span { color: var(--color-leaf-orange); font-weight: bold; }

    /* 文字內容樣式 */
    h3.section-title { color: var(--color-sumi-blue); border-left: 6px solid var(--color-sky-blue); padding-left: 15px; margin-top: 45px; margin-bottom: 20px; }
    .pit-category { border-left: 3px solid var(--color-sumi-green); padding-left: 18px; margin-bottom: 28px; }
    .pit-inline-list { line-height: 1.9; color: var(--color-sumi-text); }
</style>
</head>
<body>

<div id="leaf-container"></div>

<nav>
    <div class="nav-links">
        <a href="#about" class="nav-item">關於我</a>
        <div class="dropdown">
            <span class="dropdown-trigger">坑 ▾</span>
            <div class="dropdown-content">
                <a href="#pit-anime">動漫/小說</a>
                <a href="#pit-game">遊戲/VT</a>
                <a href="#pit-retired">淡坑/退坑</a>
            </div>
        </div>
        <a href="#attr" class="nav-item">屬性</a>
        <a href="#contact" class="nav-item">聯絡</a>
    </div>
</nav>

<div class="container">
    <h1 class="site-title">禾火人</h1>
    <span class="site-subtitle">都點進來了不看看我嗎ouo</span>
    
    <a href="https://www.youtube.com/watch?v=dQw4w9WgXcQ" target="_blank" style="text-decoration:none;">
        <div class="greeting-box"><span>「相逢即是有緣。」</span></div>
    </a>

    <h3 id="about" class="section-title">Ⅰ.🍂 關於我 🍂</h3>
    <ul style="list-style: none; padding-left: 5px; line-height: 2.2;">
        <li><strong>+ cn</strong> : 禾火 / 秋 / Aki</li>
        <li><strong>+✨</strong> : 10.02 天秤 | INTP</li>
        <li><strong>+✨</strong> : 羽山秋人重度依賴 🍣</li>
    </ul>

    <h3 id="pit" class="section-title">Ⅱ. 坑</h3>
    <div id="pit-anime" class="pit-category">
        <h4>◈ 深坑 - 動漫/小說</h4>
        <div class="pit-inline-list">《玩偶遊戲》羽山秋人、《全知讀者視角》金獨子、墨家三部曲。</div>
    </div>
    <div id="pit-game" class="pit-category">
        <h4>◈ 深坑 - 遊戲/VT</h4>
        <div class="pit-inline-list">《新世界狂歡》奧利文、《星鐵》。</div>
    </div>
    <div id="pit-retired" class="pit-category">
        <h4>◈ 淡坑 / 退坑</h4>
        <div class="pit-inline-list" style="color:#888;">《時光代理人》、《世界計畫》。</div>
    </div>

    <h3 id="attr" class="section-title">Ⅲ. 屬性</h3>
    <p><strong>+ ✨</strong> : 雜食黨 但是官配 > 所有</p>
    <p><strong>+ ✨</strong> : <span style="color:var(--color-sumi-blue); font-weight:bold;">BL >> GB</span></p>

    <h3 id="contact" class="section-title">Ⅳ. 聯絡 </h3>
    <p><a href="https://www.facebook.com/kowai.yu/" target="_blank">Facebook</a> / <a href="https://www.instagram.com/grassss_yuuuu/" target="_blank">Instagram</a></p>
</div>

<script>
    // 背景飄葉
    setInterval(() => {
        const leaf = document.createElement('div');
        leaf.className = 'leaf-fall';
        leaf.innerText = ['🍁', '🍂', '🍃'][Math.floor(Math.random()*3)];
        leaf.style.left = Math.random() * 100 + 'vw';
        const dur = Math.random() * 5 + 5;
        leaf.style.animation = `fall ${dur}s linear forwards`;
        document.getElementById('leaf-container').appendChild(leaf);
        setTimeout(() => leaf.remove(), dur * 1000);
    }, 900);

    // 點擊噴葉
    document.addEventListener('click', (e) => {
        for(let i=0; i<6; i++) {
            const l = document.createElement('div');
            l.className = 'click-leaf'; l.innerText = '🍂';
            l.style.left = e.clientX + 'px'; l.style.top = e.clientY + 'px';
            const tx = (Math.random()-0.5)*200, ty = (Math.random()-0.5)*200;
            l.animate([{ transform: 'translate(0,0) scale(1)', opacity: 1 }, { transform: `translate(${tx}px, ${ty}px) scale(0)`, opacity: 0 }], { duration: 800 });
            document.body.appendChild(l);
            setTimeout(() => l.remove(), 800);
        }
    });
</script>
</body>
</html>
