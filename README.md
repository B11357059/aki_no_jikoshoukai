<script>
    // 1. 基礎資料初始化
    let msgs = [
        {name: "系統君", text: "相逢即是有緣！"}, 
        {name: "秋", text: "想吃壽司 🍣"}, 
        {name: "Yu", text: "BL >> GB > BG = GL 哦～"}
    ];

    // 2. 跑馬燈邏輯
    function updateMarquee() {
        const l1 = document.getElementById('marquee-1'), l2 = document.getElementById('marquee-2');
        if(!l1 || !l2) return;
        let h1 = '', h2 = '';
        msgs.slice(0, 10).forEach((m, i) => {
            const item = `<span class="marquee-item">${m.name}: ${m.text}</span>`;
            if(i % 2 === 0) h1 += item; else h2 += item;
        });
        l1.innerHTML = h1 + h1; 
        l2.innerHTML = h2 + h2;
    }

    // 3. 留言送出
    function submitMessage() {
        const n = document.getElementById('user-name').value, m = document.getElementById('user-msg').value;
        if(!n || !m) return alert("要填名字跟內容喔！");
        msgs.unshift({name: n, text: m}); 
        updateMarquee();
        document.getElementById('user-name').value = ''; 
        document.getElementById('user-msg').value = '';
        alert("留言成功！");
    }

    // 4. 背景自動飄落葉
    function createLeaf() {
        const container = document.getElementById('leaf-container');
        if(!container) return;
        const leaf = document.createElement('div');
        leaf.className = 'leaf-fall';
        const types = ['🍁', '🍂', '🍃'];
        leaf.innerText = types[Math.floor(Math.random()*types.length)];
        leaf.style.left = Math.random() * 100 + 'vw';
        const duration = Math.random() * 5 + 5;
        leaf.style.animationDuration = duration + 's';
        container.appendChild(leaf);
        setTimeout(() => leaf.remove(), duration * 1000);
    }
    setInterval(createLeaf, 700);

    // 5. 點擊全域噴葉子插件
    document.addEventListener('click', function(e) {
        const leafCount = 6; 
        const types = ['🍂', '🍁'];
        for (let i = 0; i < leafCount; i++) {
            const leaf = document.createElement('div');
            leaf.className = 'click-leaf'; // 確保 CSS 有定義這個 class
            leaf.style.position = 'fixed';
            leaf.style.left = e.clientX + 'px';
            leaf.style.top = e.clientY + 'px';
            leaf.innerText = types[Math.floor(Math.random() * types.length)];
            const tx = (Math.random() - 0.5) * 200 + 'px';
            const ty = (Math.random() - 0.5) * 200 + 'px';
            leaf.animate([
                { transform: 'translate(0,0) scale(1)', opacity: 1 },
                { transform: `translate(${tx}, ${ty}) scale(0)`, opacity: 0 }
            ], { duration: 800 });
            document.body.appendChild(leaf);
            setTimeout(() => leaf.remove(), 800);
        }
    });

    // 6. 彈窗控制
    function toggleModal(s) {
        document.getElementById('lobby-modal').style.display = s ? 'flex' : 'none';
        if(s) document.getElementById('full-lobby-list').innerHTML = msgs.map(m => `<div style="padding:10px; border-bottom:1px solid #eee;"><strong>${m.name}:</strong> ${m.text}</div>`).join('');
    }

    // 初始化執行
    updateMarquee();
</script>
