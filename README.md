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
        --nav-height: 80px; 
    }

    /* 核心置中修正：防止任何元素撐開寬度 */
    *, *::before, *::after { box-sizing: border-box; }

    html, body {
        margin: 0; padding: 0; width: 100%;
        overflow-x: hidden;
        background-color: var(--color-autumn-bg);
        font-family: "PingFang TC", "Microsoft JhengHei", sans-serif;
    }

    body {
        display: flex; flex-direction: column; align-items: center;
        padding-top: calc(var(--nav-height) + 40px);
        padding-bottom: 80px;
    }

    /* 楓葉容器：不影響主體排版 */
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

    /* 導覽列 */
    nav {
        position: fixed; top: 0; left: 0; width: 100%; height: var(--nav-height);
        background-color: var(--color-sumi-blue);
        display: flex; justify-content: center; align-items: center;
        z-index: 1000; box-shadow: 0 4px 10px rgba(0,0,0,0.2);
    }
    .nav-links { display: flex; gap: 18px; }
    .nav-item, .dropdown-trigger {
        color: white; text-decoration: none; font-weight: bold;
        padding: 8px 15px; border: 1px solid rgba(255,255,255,0.2); border-radius: 8px;
    }

    .dropdown { position: relative; }
    .dropdown-content {
        display: none; position: absolute; background: white; min-width: 140px;
        top: 100%; left: 50%; transform: translateX(-50%); border-radius: 8px;
        box-shadow: 0 4px 15px rgba(0,0,0,0.1);
    }
    .dropdown:hover .dropdown-content { display: block; }
    .dropdown-content a { color: var(--color-sumi-blue); padding: 12px; display: block; text-decoration: none; font-size: 0.9em; }

    /* 主容器：嚴格置中與變形修正 */
    .container {
        width: 90%; max-width: 680px; background: #fff;
        padding: 50px 40px; margin: 0 auto;
        border-radius: 12px; border-top: 12px solid var(--color-sumi-blue);
        box-shadow: 0 15px 35px rgba(0,0,0,0.05);
        position: relative; z-index: 5;
    }

    h1.site-title { color: var(--color-sumi-blue); text-align: center; letter-spacing: 6px; margin-bottom: 8px; font-size: 2.2em; }
    .site-subtitle { text-align: center; color: var(--color-sumi-green); margin-bottom: 40px; display: block; font-size: 1.1em; }

    /* 瑞克搖連結區塊 */
    .rickroll-link { text-decoration: none; display: block; width: fit-content; margin: 0 auto 45px auto; }
    .greeting-box {
        border: 2px solid var(--color-leaf-orange); border-radius: 50px;
        padding: 12px 35px; text-align: center; cursor: pointer;
        transition: 0.3s; background: white;
    }
    .greeting-box:hover { background-color: var(--color-leaf-orange); transform: scale(1.02); }
    .greeting-box span { color: var(--color-leaf-orange); font-weight: bold; }
    .greeting-box:hover span { color: white; }

    /* 內容區塊樣式 */
    h3.section-title { color: var(--color-sumi-blue); border-left: 6px solid var(--color-sky-blue); padding-left: 15px; margin-top: 45px; margin-bottom: 20px; }
    .pit-category { border-left: 3px solid var(--color-sumi-green); padding-left: 18px; margin-bottom: 28px; }
    .pit-inline-list { line-height: 1.9; word-break: break-all; color: var(--color-sumi-text); }
    
    a { color: var(--color-sumi-blue); text-decoration: none; transition: 0.2s; }
    a:hover { color: var(--color-sky-blue); }
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
    
    <a href="https://www.youtube.com/watch?v=dQw4w9WgXcQ" target="_blank" class="rickroll-link">
        <div class="greeting-box">
            <span>「相逢即是有緣。」</span>
        </div>
    </a>

    <h3 id="about" class="section-title">Ⅰ.🍂 關於我 🍂</h3>
    <ul style="list-style: none; padding-left: 5px; line-height: 2.2;">
        <li><strong>+ cn</strong> : 禾火 / 秋 / Aki</li>
        <li><strong>+✨</strong> : 10.02 天秤 | INTP</li>
        <li><strong>+✨</strong> : 羽山秋人重度依賴 🍣 (漫畫版)</li>
        <li style="color: var(--color-sumi-green);">└ 完全貓派 特別喜歡傲嬌貓塑</li>
        <li style="color: var(--color-sumi-green); font-weight: bold;">- 不拒同擔，幾乎無雷，歡迎找我聊天!</li>
    </ul>

    <h3 id="pit" class="section-title">Ⅱ. 坑</h3>
    <div id="pit-anime" class="pit-category">
        <h4>◈ 深坑 - 動漫/小說</h4>
        <div class="pit-inline-list">
            《玩偶遊戲》羽山秋人、《失憶投捕》要圭、《全知讀者視角》金獨子、《TADC》Jax、《Alien Stage》Till、《極惡》Blitzø x 親王、墨家三部曲。
        </div>
    </div>
    <div id="pit-game" class="pit-category">
        <h4>◈ 深坑 - 遊戲/VT</h4>
        <div class="pit-inline-list">
            《新世界狂歡》奧利文/八雲/艾德蒙特、Shoto、《星鐵》、《原神》、《絕區零》、《文字化化》爬爬、《輝耀姬》輝夜 x 彩P。<br>
            <strong style="color: var(--color-sky-blue);">[ 正在等待菲林斯 BJD... ]</strong>
        </div>
    </div>
    <div id="pit-retired" class="pit-category">
        <h4>◈ 淡坑 / 退坑</h4>
        <div class="pit-inline-list" style="color: #888;">
            《時光代理人》、 《世界計畫》、乙遊、FPS遊戲、咒術、鏈鋸人、NIJI EN... 《逆水寒》、《燕雲》已完全退坑
        </div>
    </div>

    <h3 id="attr" class="section-title">Ⅲ. 屬性</h3>
    <div style="padding-left: 10px; line-height: 1.8;">
        <p><strong>+ ✨</strong> : 雜食黨 但是官配 > 所有</p>
        <p><strong>+ ✨</strong> : <span style="color: var(--color-sumi-blue); font-weight: bold;">BL >> GB > BG = GL</span></p>
        <p><strong>+ ✨</strong> : [ all男主控 ]</p>
    </div>

    <h3 id="contact" class="section-title">Ⅳ. 聯絡 </h3>
    <div style="padding-left: 10px;">
        <p><a href="https://www.facebook.com/kowai.yu/" target="_blank">Facebook</a> / <a href="https://www.instagram.com/grassss_yuuuu/" target="_blank">Instagram</a></p>
        <p>Discord: traveler7378 (活躍)</p>
    </div>

    <h3 id="other" class="section-title">Ⅴ. 其他</h3>
    <div style="padding-left: 10px; line-height: 1.8;">
        <p>偶爾會開淘寶代購團。喜歡手繪 > 電繪，正在猶豫買平板還是繪圖螢幕...</p>
        <p style="color: var(--color-sumi-blue); font-weight: bold;">如果有人可以阻止我花錢，我會很感謝你的！</p>
    </div>
</div>

<script>
    // 1. 自動飄落葉
    function leafFall() {
        const container = document.getElementById('leaf-container');
        if(!container) return;
        const leaf = document.createElement('div');
        leaf.className = 'leaf-fall';
        leaf.innerText = ['🍁', '🍂', '🍃'][Math.floor(Math.random()*3)];
        leaf.style.left = Math.random() * 100 + 'vw';
        const dur = Math.random() * 5 + 5;
        leaf.style.animation = `fall ${dur}s linear forwards`;
        container.appendChild(leaf);
        setTimeout(() => leaf.remove(), dur * 1000);
    }
    setInterval(leafFall, 800);

    // 2. 點擊噴發特效
    document.addEventListener('click', (e) => {
        for(let i=0; i<6; i++) {
            const l = document.createElement('div');
            l.className = 'click-leaf';
            l.innerText = '🍂';
            l.style.left = e.clientX + 'px'; l.style.top = e.clientY + 'px';
            const tx = (Math.random()-0.5)*200, ty = (Math.random()-0.5)*200;
            l.animate([
                { transform: 'translate(0,0) scale(1)', opacity: 1 },
                { transform: `translate(${tx}px, ${ty}px) scale(0) rotate(180deg)`, opacity: 0 }
            ], { duration: 800, easing: 'ease-out' });
            document.body.appendChild(l);
            setTimeout(() => l.remove(), 800);
        }
    });
</script>
</body>
</html>
