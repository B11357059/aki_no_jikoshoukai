/* 導覽列強制對稱修正 */
    nav {
        position: fixed; top: 0; left: 0; width: 100%; height: var(--nav-height);
        background-color: var(--color-sumi-blue);
        display: flex; justify-content: center; align-items: center;
        z-index: 1000; box-shadow: 0 4px 10px rgba(0,0,0,0.2);
    }

    .nav-links { 
        display: grid; 
        grid-template-columns: repeat(4, 1fr); /* 強制平分成 4 格，每格寬度一樣 */
        gap: 10px; 
        width: 95%; 
        max-width: 600px; /* 限制總寬度，避免分太開 */
    }

    .nav-item, .dropdown-trigger {
        color: white; text-decoration: none; font-weight: bold;
        padding: 10px 0; /* 改為上下內距，左右靠 Grid 自動分配 */
        border: 1px solid rgba(255,255,255,0.2); border-radius: 8px;
        text-align: center; /* 文字強制置中 */
        display: block;
        width: 100%;
        font-size: 0.95em;
    }

    /* 下拉選單寬度修正 */
    .dropdown { position: relative; width: 100%; }
    .dropdown-content {
        display: none; position: absolute; background: white; 
        min-width: 120px; /* 縮小寬度防止撐歪 */
        top: 100%; left: 50%; transform: translateX(-50%); 
        border-radius: 8px; box-shadow: 0 4px 15px rgba(0,0,0,0.1);
    }
