# TokyoTrip
<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>東京夢幻之旅 💜</title>
    <style>
        :root {
            --bg-color: #f4f0fa;
            --card-bg: #ffffff;
            --primary-dark: #2b2532; /* 酷洛米黑 */
            --primary-purple: #8a4baf; /* 幻夢紫 */
            --accent-pink: #f0a8d0; /* 童話粉 */
            --text-main: #333333;
            --text-gray: #777777;
            
            /* 標籤顏色 */
            --tag-food: #ff7b9c;
            --tag-menu: #ff9f43;
            --tag-buy: #1dd1a1;
            --tag-alert: #ff4757;
        }

        * { box-sizing: border-box; font-family: "PingFang TC", "Helvetica Neue", sans-serif; }
        
        body {
            margin: 0;
            padding: 0;
            background-color: var(--bg-color);
            color: var(--text-main);
            padding-bottom: 80px; /* 留給底部導覽列 */
        }

        /* 頂部標題列 */
        header {
            background: linear-gradient(135deg, var(--primary-dark), var(--primary-purple));
            color: white;
            padding: 20px 15px;
            text-align: center;
            border-bottom-left-radius: 24px;
            border-bottom-right-radius: 24px;
            box-shadow: 0 4px 12px rgba(138, 75, 175, 0.3);
            position: sticky;
            top: 0;
            z-index: 100;
        }

        header h1 { margin: 0; font-size: 1.5rem; letter-spacing: 2px; }

        /* 頁面切換容器 */
        .page { display: none; padding: 15px; animation: fadeIn 0.4s ease; }
        .page.active { display: block; }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* 卡片樣式 */
        .card {
            background: var(--card-bg);
            border-radius: 16px;
            padding: 18px;
            margin-bottom: 16px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
            border-left: 6px solid var(--primary-purple);
        }

        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px dashed #e0e0e0;
            padding-bottom: 10px;
            margin-bottom: 15px;
        }

        .card-header h2 { margin: 0; font-size: 1.2rem; color: var(--primary-dark); }
        .weather { font-size: 0.9rem; background: var(--bg-color); padding: 4px 10px; border-radius: 20px; color: var(--primary-purple); font-weight: bold; }

        /* 行程內容 */
        .timeline-item {
            margin-bottom: 20px;
            padding-left: 15px;
            border-left: 2px solid var(--accent-pink);
            position: relative;
        }

        .timeline-item::before {
            content: '💜';
            position: absolute;
            left: -10px;
            top: 0;
            font-size: 0.9rem;
            background: white;
        }

        .location-title { font-weight: bold; font-size: 1.1rem; margin-bottom: 5px; color: var(--primary-purple); }
        
        /* 標籤系統 */
        .tag {
            display: inline-block;
            padding: 4px 8px;
            border-radius: 6px;
            font-size: 0.75rem;
            font-weight: bold;
            color: white;
            margin: 4px 4px 4px 0;
        }
        .t-food { background-color: var(--tag-food); }
        .t-menu { background-color: var(--tag-menu); }
        .t-buy { background-color: var(--tag-buy); }
        .t-alert { background-color: var(--tag-alert); }

        .guide-text {
            font-size: 0.85rem;
            color: var(--text-gray);
            background: #fdfafb;
            padding: 8px;
            border-radius: 8px;
            margin-top: 5px;
        }

        /* 導航按鈕 (預設為自駕模式) */
        .nav-btn {
            display: inline-flex;
            align-items: center;
            background-color: var(--primary-dark);
            color: white;
            text-decoration: none;
            padding: 8px 14px;
            border-radius: 20px;
            font-size: 0.85rem;
            margin-top: 10px;
            box-shadow: 0 2px 6px rgba(0,0,0,0.2);
            transition: transform 0.1s;
        }
        .nav-btn:active { transform: scale(0.95); }
        .nav-btn span { margin-right: 6px; }

        /* 底部導覽列 */
        .bottom-nav {
            position: fixed;
            bottom: 0;
            left: 0;
            width: 100%;
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            display: flex;
            justify-content: space-around;
            padding: 12px 0;
            box-shadow: 0 -2px 15px rgba(0,0,0,0.08);
            border-top-left-radius: 20px;
            border-top-right-radius: 20px;
            z-index: 1000;
        }

        .nav-item {
            text-align: center;
            color: var(--text-gray);
            font-size: 0.75rem;
            cursor: pointer;
            flex: 1;
        }

        .nav-item.active { color: var(--primary-purple); font-weight: bold; }
        .nav-icon { font-size: 1.4rem; display: block; margin-bottom: 4px; }

        /* 工具區塊樣式 */
        .tool-box { background: #fafafa; border-radius: 12px; padding: 15px; margin-bottom: 15px; border: 1px solid #eee; }
        .input-group { display: flex; align-items: center; justify-content: space-between; margin-top: 10px; }
        input[type="number"] { width: 60%; padding: 10px; border: 1px solid #ddd; border-radius: 8px; font-size: 1rem; }
        .result-text { font-size: 1.2rem; font-weight: bold; color: var(--primary-purple); }

    </style>
</head>
<body>

    <header>
        <h1>💜 2026 東京夢幻之旅 💜</h1>
    </header>

    <!-- 頁面 1：行程卡片 -->
    <div id="page-itinerary" class="page active">
        
        <!-- Day 1 -->
        <div class="card">
            <div class="card-header">
                <h2>Day 1: 10/26 (一)</h2>
                <div class="weather">🌤 20°C</div>
            </div>
            
            <div class="timeline-item">
                <div class="location-title">✈️ 抵達與入住飯店</div>
                <div class="guide-text">從成田搭乘 Skyliner 轉總武線至南行德。先卸下行李，準備輕裝出遊！</div>
                <a href="https://www.google.com/maps/dir/?api=1&destination=D・レガーロ+Minamigyōtoku&travelmode=driving" target="_blank" class="nav-btn"><span>🚗</span>導航至飯店</a>
            </div>

            <div class="timeline-item">
                <div class="location-title">☕ 中目黑 & 上野採買</div>
                <div class="guide-text">漫步星巴克山手通店與小義大利 La vita。晚上前往上野阿美橫町大採購。</div>
                <span class="tag t-buy">必買伴手禮</span> 藥妝與零食 (二木的菓子)<br>
                <a href="https://www.google.com/maps/dir/?api=1&destination=中目黑星巴克&travelmode=driving" target="_blank" class="nav-btn"><span>🚗</span>導航至中目黑</a>
            </div>
        </div>

        <!-- Day 2 -->
        <div class="card">
            <div class="card-header">
                <h2>Day 2: 10/27 (二)</h2>
                <div class="weather">☀️ 22°C</div>
            </div>
            
            <div class="timeline-item">
                <div class="location-title">👘 淺草和服與抹茶甜點</div>
                <span class="tag t-alert">重要預約代號</span> 江户和装工房 雅<br>
                <span class="tag t-food">必吃美食</span> Suzukien 抹茶<br>
                <span class="tag t-menu">必點菜單</span> 世界最濃 7 號抹茶冰淇淋<br>
                <div class="guide-text">換上和服漫步雷門與今戶神社，感受傳統江戶風情。</div>
                <a href="https://www.google.com/maps/dir/?api=1&destination=淺草寺&travelmode=driving" target="_blank" class="nav-btn"><span>🚗</span>導航至淺草寺</a>
            </div>

            <div class="timeline-item">
                <div class="location-title">🥩 燒肉黑田 (澀谷)</div>
                <span class="tag t-food">必吃美食</span> 頂級黑毛和牛<br>
                <div class="guide-text">極致的深夜和牛饗宴，在熱鬧的澀谷區享受入口即化的美味。</div>
                <a href="https://www.google.com/maps/dir/?api=1&destination=燒肉黑田+澀谷&travelmode=driving" target="_blank" class="nav-btn"><span>🚗</span>導航至燒肉黑田</a>
            </div>
        </div>

        <!-- Day 3 & 4 -->
        <div class="card">
            <div class="card-header">
                <h2>Day 3-4: 10/28-29</h2>
                <div class="weather">🏰 21°C</div>
            </div>
            
            <div class="timeline-item">
                <div class="location-title">👑 迪士尼公主夢幻雙日</div>
                <div class="guide-text">
                    <strong>Day 3 海洋：</strong>主攻夢幻泉源，感受奇幻水都。<br>
                    <strong>Day 4 樂園：</strong>走進童話城堡，尋找迪士尼公主們的蹤跡。
                </div>
                <span class="tag t-buy">必買伴手禮</span> 達菲熊周邊、米奇造型爆米花桶<br>
                <a href="https://www.google.com/maps/dir/?api=1&destination=東京迪士尼海洋&travelmode=driving" target="_blank" class="nav-btn"><span>🚗</span>導航至迪士尼</a>
            </div>
        </div>

        <!-- Day 5 -->
        <div class="card">
            <div class="card-header">
                <h2>Day 5: 10/30 (五)</h2>
                <div class="weather">🌤 19°C</div>
            </div>
            
            <div class="timeline-item">
                <div class="location-title">🏙 神宮與高空燒肉</div>
                <div class="guide-text">早晨至明治神宮散策，午餐於歌劇城 53F 享用燒肉。</div>
                <span class="tag t-alert">重要預約代號</span> 敘敘苑 (請確認窗邊席 Email)<br>
                <span class="tag t-menu">必點菜單</span> 敘敘苑超值午間套餐<br>
                <a href="https://www.google.com/maps/dir/?api=1&destination=敘敘苑+東京歌劇城&travelmode=driving" target="_blank" class="nav-btn"><span>🚗</span>導航至敘敘苑</a>
            </div>

            <div class="timeline-item">
                <div class="location-title">🌃 澀谷 SKY 夜景</div>
                <div class="guide-text">傍晚前往原宿與新宿逛街，晚上登上澀谷 SKY 俯瞰絕美東京夜景，再至歌舞伎町散策。</div>
                <span class="tag t-alert">重要預約代號</span> 澀谷 SKY 門票憑證<br>
                <a href="https://www.google.com/maps/dir/?api=1&destination=SHIBUYA+SKY&travelmode=driving" target="_blank" class="nav-btn"><span>🚗</span>導航至澀谷SKY</a>
            </div>
        </div>

        <!-- Day 6 -->
        <div class="card">
            <div class="card-header">
                <h2>Day 6: 10/31 (六)</h2>
                <div class="weather">✈️ 18°C</div>
            </div>
            
            <div class="timeline-item">
                <div class="location-title">🎒 滿載而歸</div>
                <div class="guide-text">早上 08:15 離開飯店，務必於 09:25 前完成機場報到手續。</div>
                <span class="tag t-alert">重要預約代號</span> IT281 航班電子機票<br>
                <a href="https://www.google.com/maps/dir/?api=1&destination=成田國際機場&travelmode=driving" target="_blank" class="nav-btn"><span>🚗</span>導航至成田機場</a>
            </div>
        </div>

    </div>

    <!-- 頁面 2：其他工具區塊 -->
    <div id="page-tools" class="page">
        
        <!-- 航班與住宿 -->
        <div class="card">
            <h2>🛫 航班與住宿資訊</h2>
            <div class="tool-box">
                <strong>去程 (10/26)：</strong> IT280｜KHH 08:00 ➔ NRT 12:10<br>
                <strong>回程 (10/31)：</strong> IT281｜NRT 11:25 ➔ KHH 15:05
            </div>
            <div class="tool-box">
                <strong>🏨 D・レガーロ</strong><br>
                地址：千葉縣市川市南行德 2-21<br>
                交通：搭乘東西線至「南行德」站
            </div>
        </div>

        <!-- 匯率轉換器 -->
        <div class="card">
            <h2>💴 日幣/台幣 快速轉換器</h2>
            <div class="tool-box">
                <p style="margin-top:0; font-size:0.85rem; color:#777;">*目前以匯率 0.21 計算</p>
                <div class="input-group">
                    <input type="number" id="jpyInput" placeholder="輸入日幣金額" oninput="convertCurrency()">
                    <span class="result-text" id="twdOutput">NT$ 0</span>
                </div>
            </div>
        </div>

        <!-- 緊急聯絡電話 -->
        <div class="card">
            <h2>☎️ 緊急聯絡電話</h2>
            <div class="tool-box">
                • 報警：<a href="tel:110" style="color:var(--primary-purple); font-weight:bold;">110</a><br><br>
                • 急救/消防：<a href="tel:119" style="color:var(--primary-purple); font-weight:bold;">119</a><br><br>
                • 台北駐日經濟文化代表處：<br>
                <a href="tel:+81332807811" style="color:var(--primary-purple); font-weight:bold;">+81-3-3280-7811</a>
            </div>
        </div>

    </div>

    <!-- 底部導覽列 -->
    <div class="bottom-nav">
        <div class="nav-item active" onclick="switchTab('page-itinerary', this)">
            <span class="nav-icon">📅</span>
            行程表
        </div>
        <div class="nav-item" onclick="switchTab('page-tools', this)">
            <span class="nav-icon">🧰</span>
            實用工具
        </div>
    </div>

    <script>
        // 切換頁面功能
        function switchTab(pageId, element) {
            document.querySelectorAll('.page').forEach(page => page.classList.remove('active'));
            document.querySelectorAll('.nav-item').forEach(nav => nav.classList.remove('active'));
            
            document.getElementById(pageId).classList.add('active');
            element.classList.add('active');
            window.scrollTo(0, 0);
        }

        // 匯率轉換功能 (假設匯率為 0.21)
        function convertCurrency() {
            const jpy = document.getElementById('jpyInput').value;
            const rate = 0.21;
            if(jpy) {
                const twd = Math.round(jpy * rate);
                document.getElementById('twdOutput').innerText = `NT$ ${twd}`;
            } else {
                document.getElementById('twdOutput').innerText = `NT$ 0`;
            }
        }
    </script>
</body>
</html>
