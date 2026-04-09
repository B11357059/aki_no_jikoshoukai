<!DOCTYPE html>
<html lang="zh-TW">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>禾火人 /Aki/</title>
<style>
    /* 1. 希臘灰藍調 + 莫蘭迪奶茶色系核心色 */
    :root {
        --color-greece-bg: #EAEFF2; /* 莫蘭迪極淺灰藍底 */
        --color-greece-white: #FFFFFF; /* 卡片白 */
        --color-greece-blue: #5B7488; /* 核心：灰調深藍 */
        --color-greece-light-blue: #A3B5C3; /* 核心：灰調淺藍 (點綴) */
        --color-sumi-text: #2B2B2B; 
        --color-milk-tea: #DDC5A1; /* 莫蘭迪暖奶茶 */
        --color-light-brown: #CD853F; /* 莫蘭迪咖啡 */
        
        /* 重點修正：Nav 高度必須比之前更高，才能擋住那兩行字 */
        --nav-height: 100px; 
    }

    /* 核心排版與置中 */
    *, *::before, *::after { box-sizing: border-box; }

    html {
        scroll-behavior: smooth; 
        /* 關鍵修正：捲動 Offset 調更高，防止遮擋 */
        scroll-padding-top: calc(var(--nav-height) + 15px); 
    }

    body {
        margin: 0; padding: 0; width: 100%;
        overflow-x: hidden;
        background-color: var(--color-greece-bg);
        font-family: "PingFang TC", "Microsoft JhengHei", sans-serif;
        color: var(--color-sumi-text);
        display: flex; flex-direction: column; align-items: center;
        /* 重點修正：Body padding 開頭預留 Nav 高度，確保不跑版 */
        padding-top: var(--nav-height);
        padding-bottom: 80px;
    }

    /* 2. 重點修正：遮擋用實心 Nav 方塊 */
    nav {
        position: fixed; top: 0; left: 0; width: 100%; height: var(--nav-height);
        background-color: var(--color-greece-white); /* 白色背景，確保擋住字 */
        display: flex; justify-content: center; align-items: center;
        z-index: 10000; /* 保證在最上層 */
        box-shadow: 0 6px 20px rgba(0, 0, 0, 0.12); /* 強化立體感範圍框 */
        border-bottom: 1px solid var(--color-greece-light-blue); /* 希臘灰藍點綴邊框 */
        overflow: hidden; /* 防止內容跑出去 */
    }

    /* 希臘灰藍按鈕容器 (Grid 對稱排版) */
    .nav-links { 
        display: grid; 
        grid-template-columns: repeat(4, 1fr); 
        gap: 15px; /* 按鈕間距 */
        width: 90%; 
        max-width: 500px; /* 限制寬度 */
        height: 100%; /* 撐滿 Nav */
        align-items: center; /* 按鈕在卡片中置中 */
    }

    /* 希臘灰藍實心按鈕 */
    .nav-item {
        color: white; text-decoration: none; font-weight: bold;
        background-color: var(--color-greece-blue); /* 實心灰藍 */
        padding: 12px 0; border-radius: 6px;
        text-align: center; display: block; width: 100%; font-size: 0.95em;
        transition: 0.3s ease;
        box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1); /* 按鈕小立體感 */
        border: 1px solid var(--color-greece-blue);
    }
    .nav-item:hover { 
        background-color: var(--color-milk-tea); /* 懸停變莫蘭迪奶茶 */
        transform: translateY(-2px);
        box-shadow: 0 5px 12px rgba(221, 197, 161, 0.4);
        color: var(--color-greece-blue);
        border-color: var(--color-milk-tea);
    }

    /* 3. 楓葉特效容器 (在 Nav 之下) */
    #leaf-container {
        position: fixed; top: 0; left: 0; width: 100vw; height: 100vh;
        pointer-events: none; z-index: 9999;
    }
    .leaf-fall, .click-leaf { position: fixed; pointer-events: none; z-index: 10000; }
    @keyframes fall {
        0% { transform: translateY(-50px) rotate(0deg); opacity: 0; }
        10% { opacity: 0.8; }
        100% { transform: translateY(110vh) rotate(360deg); opacity: 0; }
    }

    /* 4. 主容器 (希臘極簡風) */
    .container {
        width: 90%; max-width: 800px;
        position: relative; z-index: 5;
    }

    /* 標題與副標題 (莫蘭迪色系) */
    h1.site-title { 
        color: var(--color-light-brown); text-align: center; 
        letter-spacing: 5px; margin-bottom: 5px; font-size: 2.8em; 
        text-shadow: 1px 1px 2px rgba(0,0,0,0.05);
    }

    /* 瑞克搖按鈕方塊 (莫蘭迪灰藍色) */
    .rickroll-btn {
        display: block; width: fit-content; margin: 0 auto 50px auto;
        background-color: var(--color-greece-blue); 
        color: white; text-decoration: none; font-weight: bold; font-size: 1.1em;
        padding: 12px 25px; border-radius: 50px;
        box-shadow: 0 4px 10px rgba(91, 116, 136, 0.3);
        transition: 0.3s ease; text-align: center;
    }
    .rickroll-btn:hover {
        background-color: var(--color-milk-tea); 
        transform: translateY(-2px) scale(1.03);
        box-shadow: 0 6px 15px rgba(221, 197, 161, 0.5);
    }

    /* 5. 區塊樣式：卡片雜誌風核心 */
    .section-card {
        background: var(--color-greece-white);
        border-radius: 12px;
        padding: 30px;
        margin-bottom: 35px;
        box-shadow: 0 6px 18px rgba(0,0,0,0.03);
        border-left: 8px solid var(--color-greece-light-blue); /* 希臘灰藍邊框 */
        transition: 0.3s ease;
    }
    .section-card:hover {
        transform: translateY(-5px); /* 懸停稍微浮起 */
        box-shadow: 0 10px 25px rgba(0,0,0,0.08);
    }

    h3.section-title { 
        color: var(--color-greece-blue); font-size: 1.5em; 
        margin-top: 0; margin-bottom: 25px; 
        border-bottom: 2px solid var(--color-milk-tea); padding-bottom: 10px;
    }

    /* 6. 卡片網格：【卡片雜誌風】深坑區 */
    .pit-grid {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(160px, 1fr)); /* 自動填滿網格 */
        gap: 20px;
        margin-top: 20px;
    }

    /* 【拍立得卡片】樣式 */
    .pit-card {
        background: white;
        border: 1px solid #eee;
        border-radius: 8px;
        padding: 15px;
        text-align: center;
        box-shadow: 0 2px 8px rgba(0,0,0,0.05);
        transition: 0.4s ease; /* 卡片懸停動畫核心 */
        position: relative;
        overflow: hidden;
        display: flex; flex-direction: column; justify-content: center; align-items: center; /* 讓內容置中 */
    }
    .pit-card:hover {
        transform: scale(1.1) rotate(2deg); /* 移上去放大並旋轉 */
        box-shadow: 0 12px 20px rgba(0,0,0,0.12);
        z-index: 10;
        border-color: var(--color-light-brown);
    }
    .pit-card strong { color: var(--color-greece-blue); font-size: 1.1em; margin-bottom: 5px; }
    .pit-card span { color: var(--color-sumi-text); font-size: 0.9em; display: block; margin-top: 2px; }
    
    /* 深坑卡片特殊點綴 (希臘藍) */
    .pit-card.deep-pit { border-bottom: 4px solid var(--color-greece-light-blue); }

    /* 淡坑列表樣式 */
    .retired-list {
        line-height: 2.2; color: #777;
        font-size: 0.95em;
        column-count: 2; /* 兩行顯示 */
        column-gap: 30px;
        border-top: 1px solid #eee; padding-top: 15px;
    }
    .retired-list span { color: #aaa; font-size: 0.9em; display: block; column-span: all; margin-top: 10px; } /* 特別註記跨行顯示 */

    /* 聯絡區塊 */
    a.contact-link { color: var(--color-light-brown); font-weight: bold; margin-right: 15px; text-decoration: none; }
    a.contact-link:hover { color: var(--color-greece-blue); text-decoration: underline; }

</style>
</head>
<body>

<div id="leaf-container"></div>

<nav>
    <div class="nav-links">
        <a href="#about" class="nav-item">關於我</a>
        <a href="#pit" class="nav-item">坑</a>
        <a href="#other" class="nav-item">其他</a>
        <a href="#contact" class="nav-item">聯絡</a>
    </div>
</nav>

<div class="container">
    <h1 class="site-title">禾火人</h1>
    
    <a href="https://www.youtube.com/watch?v=dQw4w9WgXcQ" target="_blank" class="rickroll-btn">
        都點進來了不看看我嗎>ouo/
    </a>
    
    <div id="about" class="section-card">
        <h3 class="section-title">I. 🍂 個人檔案</h3>
        <p style="color: var(--color-light-brown); font-weight:bold; font-size:1.1em; margin-top:0;">CN： 禾火 / 秋 / Aki</p>
        <p>INTP、10/02、天秤座♎</p>
        <p><strong>屬性:</strong> 羽山秋人重度依賴、特別喜歡傲嬌貓塑。</p>
        <p style="border-left: 3px solid var(--color-milk-tea); padding-left:10px; margin-top: 15px;">
            <strong>屬性:</strong> 雜食黨、官配派、BL >> GB > GL > BG<br>
            <strong>雷:</strong> 基本無雷 除了激進黑粉(會一直對我輸出的那種)其他都還好。
        </p>
        <p style="color: #888; font-size: 0.9em; margin-top:20px;">└ 電繪人 只畫自己喜歡的 畫的普通所以很少放圖。</p>
    </div>

    <div id="pit" class="section-card">
        <h3 class="section-title">II. 🍂 坑</h3>
        
        <h4>◈ 【深坑區】</h4>
        <div class="pit-grid">
            <div class="pit-card deep-pit">
                <strong style="display: block; margin-bottom: 5px;">
                    <span style="color: var(--color-light-brown);">✨✨✨</span>玩偶遊戲
                </strong>
                <span>羽山秋人</span>
                <span style="font-size: 0.8em; color: #aaa; margin-top: 8px; line-height: 1.4;">
                    知道為什麼我叫Aki了吧!
                </span>
            </div>
            <div class="pit-card deep-pit"><strong>極惡</strong><span>親王</span></div>
            <div class="pit-card deep-pit"><strong>Alien Stage</strong><span>Till</span></div>
            <div class="pit-card deep-pit"><strong>TADC</strong><span>Jax</span></div>
            <div class="pit-card deep-pit"><strong>文字化化</strong><span>爬爬</span></div>
            <div class="pit-card deep-pit"><strong>失憶投捕</strong><span>圭</span></div>
            <div class="pit-card deep-pit"><strong>全知讀者視角</strong><span>獨子</span></div>
            <div class="pit-card deep-pit"><strong>新世界狂歡</strong><span>奧、八 > 副團</span></div>
            <div class="pit-card deep-pit"><strong>輝耀姬</strong><span>輝夜 X 彩P</span></div>
            <div class="pit-card deep-pit"><strong>Shoto</strong></div>
        </div>

        <h4 style="margin-top:40px;">◈ 【淡坑】</h4>
        <div class="retired-list">
            《墨家三部曲》、來自新世界、時光代理人、咒術、鏈鋸、世界計畫 日服、絕區零、原神、NIJI EN、FPS類、光遇、一大堆乙遊(目前全退坑了)...
            <span>(還有一些其他沒想起來的也許之後會補上...)</span>
        </div>
    </div>

    <div id="other" class="section-card">
        <h3 class="section-title">III. 🍂 其他</h3>
        <p style="color: var(--color-greece-blue); font-weight:bold;">不是在找代購 就是在開團的路上。</p>
        <p>淘寶代購可以找我本人 ouo</p>
        <p style="margin-top:20px; border-top: 1px solid #eee; padding-top:15px; color: var(--color-light-brown);">年底前考慮要買平板還是電繪板😔</p>
    </div>

    <div id="contact" class="section-card">
        <h3 class="section-title">IV. 🍂 可以找到我的地方</h3>
        <div style="padding-left:10px; margin-top: 15px;">
            社群連結： 
            <a href="https://www.facebook.com/kowai.yu/" target="_blank" class="contact-link">FB</a> / 
            <a href="https://www.instagram.com/grassss_yuuuu/" target="_blank" class="contact-link">IG</a> / 
            <span style="color:var(--color-sumi-text); font-weight: bold; margin-left: 10px;">Discord (traveler7378)</span>
        </div>
    </div>

</div>

<script>
    // 背景飄楓葉
    setInterval(() => {
        const container = document.getElementById('leaf-container');
        if(!container) return;
        const leaf = document.createElement('div');
        leaf.className = 'leaf-fall';
        leaf.innerText = ['🍁', '🍂', '🍃'][Math.floor(Math.random()*3)];
        leaf.style.left = Math.random() * 100 + 'vw';
        const dur = Math.random() * 5 + 5;
        leaf.style.animation = `fall ${dur}s linear forwards`;
        if(leaf.innerText === '🍃') leaf.style.opacity = 0.5;
        container.appendChild(leaf);
        setTimeout(() => leaf.remove(), dur * 1000);
    }, 900);

    // 點擊噴發特效
    document.addEventListener('click', (e) => {
        if (e.target.closest('.rickroll-btn')) return;
        if (e.target.closest('nav')) return; /* 如果點擊導覽列也不觸發，增加惡整成功率 */

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
