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
        --color-milk-gray: #BDBDBD;  
        --nav-height: 95px; 
    }

    /* 核心置中修正：確保 html 和 body 不會產生橫向捲軸 */
    html, body {
        margin: 0; padding: 0; width: 100%; overflow-x: hidden;
        background-color: var(--color-autumn-bg);
    }

    body {
        font-family: "PingFang TC", "Microsoft JhengHei", sans-serif;
        color: var(--color-sumi-text);
        padding-top: calc(var(--nav-height) + 40px);
        padding-bottom: 60px;
        display: flex; flex-direction: column; align-items: center;
    }

    /* 楓葉容器：用 fixed 定位完全抽離，不佔空間 */
    #leaf-container {
        position: fixed; top: 0; left: 0; width: 100%; height: 100%;
        pointer-events: none; z-index: 9999; overflow: hidden;
    }

    .leaf-fall { position: absolute; top: -50px; animation: fall linear infinite; user-select: none; pointer-events: none; }
    @keyframes fall {
        0% { transform: translateY(0vh) rotate(0deg); opacity: 0; }
        10% { opacity: 0.8; }
        100% { transform: translateY(110vh) rotate(360deg); opacity: 0; }
    }

    /* 點擊特效 CSS */
    .click-leaf {
        position: fixed; pointer-events: none; z-index: 10000; user-select: none; font-size: 20px;
    }

    /* 導覽列 */
    nav {
        position: fixed; top: 0; left: 0; width: 100%; height: var(--nav-height);
        background-color: var(--color-sumi-blue); color: white;
        display: flex; justify-content: center; align-items: center;
        z-index: 1000; box-shadow: 0 4px 12px rgba(0,0,0,0.15);
    }
    .nav-links { display: flex; gap: 15px; align-items: center; }
    .nav-item, .dropdown-trigger {
        color: white; text-decoration: none; font-size: 1.1em; font-weight: 900;
        padding: 8px 15px; border: 2px solid rgba(255,255,255,0.3); border-radius: 8px; cursor: pointer;
    }

    .dropdown { position: relative; display: flex; align-items: center; }
    .dropdown-content {
        display: none; position: absolute; background: white; min-width: 160px;
        box-shadow: 0px 8px 16px rgba(0,0,0,0.2); border-radius: 8px; 
        top: 100%; left: 50%; transform: translateX(-50%); z-index: 1001;
    }
    .dropdown-content a { color: var(--color-sumi-blue) !important; padding: 12px; display: block; text-decoration: none; font-weight: bold; }
    .dropdown:hover .dropdown-content { display: block; }

    /* 主容器置中：使用 margin: 0 auto 強制居中 */
    .container {
        max-width: 720px; width: 90%; background: #fff; padding: 40px;
        box-shadow: 0 10px 30px rgba(0,0,0,0.08); border-radius: 4px;
        border-top: 8px solid var(--color-sumi-blue); position: relative; z-index: 1;
        margin-left: auto; margin-right: auto; box-sizing: border-box;
    }

    h1.site-title { color: var(--color-sumi-blue); text-align: center; font-size: 2.5em; letter-spacing: 8px; margin-bottom: 5px; }
    .site-subtitle { text-align: center; font-size: 1em; color: var(--color-sumi-green); margin-bottom: 2em; display: block; }

    .greeting-box {
        cursor: pointer; border: 2px solid var(--color-leaf-orange);
        padding: 10px 30px; border-radius: 50px; margin: 0 auto 3em auto;
        width: fit-content; text-align: center; transition: 0.3s;
    }

    /* 跑馬燈 */
    .message-board { border: 3px solid var(--color-sky-blue); background-color: var(--color-milk-green); padding: 20px; border-radius: 12px; margin-top: 20px; }
    .marquee-area { background: rgba(255, 255, 255, 0.4); border-radius: 8px; margin-bottom: 15px; padding: 8px 0; overflow: hidden; }
    .marquee-line { display: flex; white-space: nowrap; animation: marquee 30s linear infinite; }
    @keyframes marquee { 0% { transform: translateX(100%); } 100% { transform: translateX(-150%); } }
    .marquee-item { display: inline-block; padding-right: 80px; color: var(--color-sumi-blue); font-weight: bold; }

    /* 表單 */
    .message-form input, .message-form textarea { width: 100%; padding: 12px; margin-bottom: 10px; border: 1px solid #ccc; border-radius: 6px; box-sizing: border-box; }
    .btn-group { display: flex; gap: 8px; }
    .submit-btn { flex: 2; background-color: var(--color-sumi-blue); color: white; border: none; padding: 12px; border-radius: 6px; font-weight: bold; cursor: pointer; }

    h3.section-title {
        color: var(--color-sumi-blue); border-left: 8px solid var(--color-sky-blue);
        padding-left: 15px; margin-top: 40px; margin-bottom: 20px;
        background: linear-gradient(to right, rgba(100, 161, 200, 0.1), transparent);
    }
    .pit-category { margin-bottom: 25px; border-left: 3px solid var(--color-sumi-green); padding-left: 15px; }
    .pit-inline-list { line-height: 1.8; word-break: break-all; }

    /* Modal */
    .modal { display: none; position: fixed; z-index: 3000; left: 0; top: 0; width: 100%; height: 100%; background-color: rgba(0,0,0,0.6); align-items: center; justify-content: center; }
    .modal-content { background: white; width: 85%; max-width: 450px; border-radius: 15px; padding: 25px; position: relative; max-height: 70vh; overflow-y: auto; }
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
    
    <div class="greeting-box">
        <h2 style="color: var(--color-leaf-orange); font-size: 1.1em; margin: 0; font-weight: normal; letter-spacing: 2px;">「相逢即是有緣。」</h2>
    </div>

    <h3 id="about" class="section-title">Ⅰ.🍂 關於我 🍂</h3>
    <ul style="list-style: none; padding-left: 5px;">
        <li><strong>+ cn</strong> : 禾火 / 秋 / Aki</li>
        <li><strong>+✨</strong> : 10.02 天秤 | INTP</li>
        <li><strong>+✨</strong> : 羽山秋人重度依賴 🍣</li>
        <li style="color: var(--color-sumi-green); font-size: 0.95em;">└ 完全貓派 特別喜歡傲嬌貓塑</li>
        <li style="margin-top:8px; color: var(--color-sumi-green); font-weight: bold;">- 不拒同擔，幾乎無雷，歡迎找我聊天!</li>
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
    <div style="padding-left: 10px;">
        <p><strong>+ ✨</strong> : 雜食黨 但是官配 > 所有</p>
        <p><strong>+ ✨</strong> : <span style="color: var(--color-sumi-blue); font-weight: bold;">BL >> GB > BG = GL</span></p>
        <p><strong>+ ✨</strong> : [ all男主控 ]</p>
    </div>

    <h3 id="message" class="section-title">Ⅳ. 留言板</h3>
    <div class="message-board">
        <div class="marquee-area"><div class="marquee-line" id="marquee-1"></div></div>
        <div class="message-form">
            <input type="text" id="user-name" placeholder="你的名字">
            <textarea id="user-msg" rows="2" placeholder="想對我說什麼？"></textarea>
            <div class="btn-group">
                <button class="submit-btn" onclick="submitMessage()">送出</button>
                <button onclick="toggleModal(true)" style="cursor:pointer; padding:10px; border-radius:6px; border:1px solid #ccc; background:white;">查看所有</button>
            </div>
        </div>
    </div>

    <div id="lobby-modal" class="modal">
        <div class="modal-content">
            <span onclick="toggleModal(false)" style="float:right; cursor:pointer; font-size:20px;">&times;</span>
            <h3 style="border-bottom: 2px solid var(--color-sky-blue); padding-bottom: 10px;">✨ 留言大廳</h3>
            <div id="full-lobby-list"></div>
        </div>
    </div>

    <h3 id="contact" class="section-title">Ⅴ. 聯絡 </h3>
    <div style="padding-left: 10px;">
        <p><a href="https://www.facebook.com/kowai.yu/" target="_blank">FACEBOOK</a> / <a href="https://www.instagram.com/grassss_yuuuu/" target="_blank">INSTAGRAM</a></p>
        <p>Discord - traveler7378 (活躍)</p>
    </div>

    <h3 id="other" class="section-title">Ⅵ. 其他</h3>
    <div style="padding-left: 10px;">
        <p>偶爾會開淘寶代購團，有需要也可以找我 我很便宜:D</p>
        <p>喜歡畫圖 (手繪 > 電繪) 正在猶豫買平板還是繪圖螢幕...</p>
        <p style="color: var(--color-sumi-blue); font-weight: bold;">如果有人可以阻止我花錢 我會很感謝你的</p>
    </div>
</div>

<script>
    // 1. 楓葉與點擊插件
    function createLeaf() {
        const leaf = document.createElement('div');
        leaf.className = 'leaf-fall';
        leaf.innerText = ['🍁', '🍂', '🍃'][Math.floor(Math.random()*3)];
        leaf.style.left = Math.random() * 100 + 'vw';
        const dur = Math.random() * 5 + 5;
        leaf.style.animationDuration = dur + 's';
        document.getElementById('leaf-container').appendChild(leaf);
        setTimeout(() => leaf.remove(), dur * 1000);
    }
    setInterval(createLeaf, 800);

    document.addEventListener('click', function(e) {
        for (let i = 0; i < 6; i++) {
            const leaf = document.createElement('div');
            leaf.className = 'click-leaf';
            leaf.style.left = e.clientX + 'px';
            leaf.style.top = e.clientY + 'px';
            leaf.innerText = ['🍂', '🍁'][Math.floor(Math.random()*2)];
            const tx = (Math.random() - 0.5) * 200 + 'px';
            const ty = (Math.random() - 0.5) * 200 + 'px';
            leaf.animate([
                { transform: 'translate(0,0) scale(1)', opacity: 1 },
                { transform: `translate(${tx}, ${ty}) scale(0) rotate(360deg)`, opacity: 0 }
            ], { duration: 800, easing: 'ease-out' });
            document.body.appendChild(leaf);
            setTimeout(() => leaf.remove(), 800);
        }
    });

    // 2. 留言板邏輯
    let msgs = [{name: "系統君", text: "相逢即是有緣！"}, {name: "秋", text: "想吃壽司 🍣"}];
    function updateMarquee() {
        const l1 = document.getElementById('marquee-1');
        let h = '';
        msgs.slice(0, 10).forEach(m => {
            h += `<span class="marquee-item">${m.name}: ${m.text}</span>`;
        });
        l1.innerHTML = h + h;
    }
    function submitMessage() {
        const n = document.getElementById('user-name').value, m = document.getElementById('user-msg').value;
        if(!n || !m) return;
        msgs.unshift({name: n, text: m}); updateMarquee();
        document.getElementById('user-name').value = ''; document.getElementById('user-msg').value = '';
    }
    function toggleModal(s) {
        document.getElementById('lobby-modal').style.display = s ? 'flex' : 'none';
        if(s) document.getElementById('full-lobby-list').innerHTML = msgs.map(m => `<div style="padding:10px; border-bottom:1px solid #eee;"><strong>${m.name}:</strong> ${m.text}</div>`).join('');
    }
    updateMarquee();
</script>
</body>
</html>
