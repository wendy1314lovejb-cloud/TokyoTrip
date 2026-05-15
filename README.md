<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <title>2026 東京夢幻之旅 💜</title>
    <style>
        :root {
            --primary-color: #9370DB;
            --secondary-color: #8A2BE2;
            --bg-color: #F8F4FF;
            --card-bg: #FFFFFF;
            --text-main: #333333;
            --text-light: #666666;
            --tag-food: #FFE4E1;
            --tag-food-text: #D2691E;
            --tag-buy: #E6E6FA;
            --tag-buy-text: #4B0082;
            --safe-area-bottom: env(safe-area-inset-bottom);
        }

        * {
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent; /* 移除手機點擊藍色高亮 */
        }

        body {
            margin: 0;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "PingFang TC", "Hiragino Sans GB", "Microsoft JhengHei", sans-serif;
            background-color: var(--bg-color);
            color: var(--text-main);
            line-height: 1.5;
            overflow-x: hidden;
            overscroll-behavior-y: none; /* 防止手機下拉重整干擾體驗 */
            padding-bottom: calc(90px + var(--safe-area-bottom)); 
        }

        .header {
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            color: white;
            padding: calc(20px + env(safe-area-inset-top)) 15px 20px;
            text-align: center;
            position: sticky;
            top: 0;
            z-index: 100;
            box-shadow: 0 2px 10px rgba(138, 43, 226, 0.15);
            border-bottom-left-radius: 20px;
            border-bottom-right-radius: 20px;
        }

        .header h1 { margin: 0; font-size: 1.25rem; font-weight: 600; letter-spacing: 0.5px; }

        .container { padding: 12px; width: 100%; max-width: 500px; margin: 0 auto; }

        .tab-content { display: none; animation: slideIn 0.3s ease-out; }
        .tab-content.active { display: block; }

        @keyframes slideIn { 
            from { opacity: 0; transform: translateY(15px); } 
            to { opacity: 1; transform: translateY(0); } 
        }

        .card {
            background: var(--card-bg);
            border-radius: 18px;
            padding: 16px;
            margin-bottom: 12px;
            box-shadow: 0 4px 15px rgba(147, 112, 219, 0.06);
            border-left: 5px solid var(--primary-color);
        }

        .card-title {
            font-size: 1.05rem;
            font-weight: 700;
            color: var(--secondary-color);
            margin: 0 0 10px 0;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .weather {
            font-size: 0.8rem;
            color: var(--text-light);
            background: #F3F0F7;
            padding: 8px 12px;
            border-radius: 10px;
            margin-bottom: 12px;
            display: block;
            width: 100%;
        }

        ul { padding-left: 18px; margin: 10px 0; color: var(--text-light); }
        li { margin-bottom: 10px; font-size: 0.92rem; }
        strong { color: var(--text-main); }

        .tag {
            display: inline-block;
            padding: 3px 8px;
            border-radius: 8px;
            font-size: 0.72rem;
            font-weight: 600;
            margin: 4px 4px 0 0;
        }
        .tag.food { background: var(--tag-food); color: var(--tag-food-text); }
        .tag.buy { background: var(--tag-buy); color: var(--tag-buy-text); }
        .tag.story { background: #FFF0F5; color: #C71585; }

        .nav-btn-link {
            background-color: var(--primary-color);
            color: white;
            text-decoration: none;
            padding: 8px 16px;
            border-radius: 12px;
            font-size: 0.85rem;
            display: inline-flex;
            align-items: center;
            margin-top: 10px;
            transition: transform 0.1s;
        }
        .nav-btn-link:active { transform: scale(0.96); }

        /* 底部導覽列 - 優化手機手勢 */
        .bottom-nav {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            background: rgba(255, 255, 255, 0.9);
            backdrop-filter: blur(15px);
            -webkit-backdrop-filter: blur(15px);
            display: flex;
            justify-content: space-around;
            padding: 10px 0 calc(10px + var(--safe-area-bottom));
            box-shadow: 0 -5px 20px rgba(0,0,0,0.05);
            z-index: 1000;
        }

        .nav-item {
            background: none;
            border: none;
            font-size: 0.7rem;
            color: #BDBDBD;
            cursor: pointer;
            display: flex;
            flex-direction: column;
            align-items: center;
            flex: 1;
            transition: color 0.2s;
        }

        .nav-item.active { color: var(--secondary-color); font-weight: 700; }
        .nav-icon { font-size: 1.4rem; margin-bottom: 2px; }

        /* 工具與表格優化 */
        table { width: 100%; border-collapse: separate; border-spacing: 0; border: 1px solid #eee; border-radius: 12px; overflow: hidden; }
        th, td { padding: 12px; text-align: left; font-size: 0.85rem; border-bottom: 1px solid #eee; }
        th { background-color: #F9F7FF; color: var(--secondary-color); width: 35%; }

        .converter-box { border: 2px solid var(--primary-color); }
        .converter-input { 
            padding: 12px; 
            font-size: 1.2rem; 
            width: 80%; 
            border: 1px solid #ddd; 
            border-radius: 12px; 
            margin: 10px 0; 
            text-align: center;
            appearance: none;
        }
    </style>
</head>
<body>

    <div class="header">
        <h1>💜 2026 東京夢幻之旅</h1>
    </div>

    <div class="container">
        <!-- 行程分頁 (同原內容但結構優化) -->
        <div id="tab-itinerary" class="tab-content active">
            <div class="card">
                <div class="card-title">Day 1: 啟程浪漫 <span>10/26 Mon</span></div>
                <div class="weather">⛅ 15°C - 21°C | 適合紫色外套</div>
                <ul>
                    <li><strong>🚆 交通：</strong>12:10 抵成田機場 ➔ Skyliner至船橋 ➔ 南行德</li>
                    <li><strong>📍 景點：中目黑 Starbucks</strong>
                        <br><a href="https://maps.google.com/?q=星巴克臻選東京烘焙工坊" target="_blank" class="nav-btn-link">📍 打開地圖</a>
                        <br><span class="tag story">💡 全球六間之一</span> <span class="tag food">😋 推薦 Princi 麵包</span>
                    </li>
                </ul>
            </div>
            
            <div class="card">
                <div class="card-title">Day 2: 淺草和服 <span>10/27 Tue</span></div>
                <div class="weather">🌤️ 14°C - 20°C | 穿和服的好天氣</div>
                <ul>
                    <li><strong>👘 體驗：江户和装工房 雅</strong></li>
                    <li><strong>📍 景點：淺草寺、雷門</strong>
                        <br><span class="tag food">😋 炸饅頭、No.7 抹茶冰</span>
                    </li>
                    <li><strong>🥩 晚餐：燒肉黑田 (澀谷)</strong>
                        <br><a href="https://maps.google.com/?q=燒肉黑田+澀谷" target="_blank" class="nav-btn-link">🥩 導航去吃肉</a>
                    </li>
                </ul>
            </div>

            <div class="card">
                <div class="card-title">Day 3 & 4: 迪士尼雙樂園</div>
                <div class="weather">☀️ 晴朗 | 記得帶行動電源</div>
                <ul>
                    <li><strong>🎢 10/28 Sea:</strong> 夢幻泉鄉必搶 DPA</li>
                    <li><strong>🏰 10/29 Land:</strong> 美女與野獸城堡</li>
                </ul>
            </div>

            <div class="card">
                <div class="card-title">Day 5: 澀谷絕景 <span>10/30 Fri</span></div>
                <ul>
                    <li><strong>📍 景點：明治神宮 ➔ 澀谷 SKY</strong></li>
                    <li><strong>🛍️ 逛街：原宿 ➔ 伊勢丹新宿</strong></li>
                </ul>
            </div>
        </div>

        <!-- 工具分頁 -->
        <div id="tab-tools" class="tab-content">
            <div class="card">
                <div class="card-title">✈️ 航班與住宿</div>
                <table>
                    <tr><th>去程</th><td>IT280 08:00</td></tr>
                    <tr><th>回程</th><td>IT281 11:25</td></tr>
                    <tr><th>住宿</th><td>D Regalo (南行德)</td></tr>
                </table>
            </div>
            <div class="card" style="text-align: center;">
                <a href="https://maps.app.goo.gl/6ouHWvNahBLUjwXb6" target="_blank" class="nav-btn-link" style="width: 100%; justify-content: center; background: #6A5ACD;">🏠 一鍵導航回飯店</a>
            </div>
            <div class="card">
                <div class="card-title">📞 緊急電話</div>
                <ul style="list-style: none; padding: 0;">
                    <li>🚑 救護車：<a href="tel:119">119</a></li>
                    <li>👮 報警：<a href="tel:110">110</a></li>
                </ul>
            </div>
        </div>

        <!-- 預算分頁 -->
        <div id="tab-budget" class="tab-content">
            <div class="card converter-box" style="text-align: center;">
                <div class="card-title" style="justify-content: center;">💱 匯率換算 (0.215)</div>
                <input type="number" id="jpyInput" class="converter-input" placeholder="輸入日幣金額" oninput="calcCurrency()">
                <div style="font-size: 1.3rem; font-weight: 800; color: var(--secondary-color); margin-top: 10px;">
                    ≈ NT$ <span id="twdOutput">0</span>
                </div>
            </div>
        </div>
    </div>

    <!-- 底部導覽 -->
    <div class="bottom-nav">
        <button class="nav-item active" onclick="switchTab('tab-itinerary', this)">
            <span class="nav-icon">📅</span>
            <span>行程</span>
        </button>
        <button class="nav-item" onclick="switchTab('tab-tools', this)">
            <span class="nav-icon">🛠️</span>
            <span>工具</span>
        </button>
        <button class="nav-item" onclick="switchTab('tab-budget', this)">
            <span class="nav-icon">💰</span>
            <span>預算</span>
        </button>
    </div>

    <script>
        function switchTab(tabId, btnElement) {
            document.querySelectorAll('.tab-content').forEach(tab => tab.classList.remove('active'));
            document.querySelectorAll('.nav-item').forEach(btn => btn.classList.remove('active'));
            document.getElementById(tabId).classList.add('active');
            btnElement.classList.add('active');
            window.scrollTo({ top: 0, behavior: 'smooth' });
            
            // 手機震動反饋 (若瀏覽器支援)
            if (navigator.vibrate) navigator.vibrate(5);
        }

        function calcCurrency() {
            const jpy = document.getElementById('jpyInput').value;
            const rate = 0.215;
            const twd = Math.round(jpy * rate);
            document.getElementById('twdOutput').innerText = twd.toLocaleString();
        }
    </script>
</body>
</html>
