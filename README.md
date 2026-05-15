# TokyoTrip
<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>2026 東京夢幻之旅 💜</title>
    <style>
        :root {
            --primary-color: #8A2BE2; /* 幻夢紫 */
            --secondary-color: #DDA0DD; /* 淺紫 */
            --bg-color: #F8F5FA; /* 極簡灰白紫 */
            --card-bg: #FFFFFF;
            --text-main: #333333;
            --text-light: #666666;
            --highlight-food: #FF69B4; /* 必吃美食粉色 */
            --highlight-buy: #FFA500; /* 必買橘色 */
            --highlight-alert: #E23D28; /* 重要紅色 */
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-main);
            margin: 0;
            padding: 0;
            padding-bottom: 70px; /* 給底部導覽列空間 */
            -webkit-font-smoothing: antialiased;
        }

        /* 頂部標題 */
        header {
            background: linear-gradient(135deg, var(--primary-color), #4B0082);
            color: white;
            padding: 20px 15px 15px;
            text-align: center;
            border-bottom-left-radius: 20px;
            border-bottom-right-radius: 20px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            position: sticky;
            top: 0;
            z-index: 100;
        }
        
        header h1 {
            margin: 0;
            font-size: 1.4rem;
            letter-spacing: 1px;
        }

        /* 內容區塊 */
        .container {
            padding: 15px;
            display: none; /* 預設隱藏，由 JS 控制顯示 */
        }
        .container.active {
            display: block;
            animation: fadeIn 0.3s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* 卡片設計 */
        .card {
            background-color: var(--card-bg);
            border-radius: 15px;
            padding: 15px;
            margin-bottom: 15px;
            box-shadow: 0 2px 8px rgba(138, 43, 226, 0.1);
            border-left: 5px solid var(--secondary-color);
        }

        .card h2 {
            margin-top: 0;
            font-size: 1.2rem;
            color: var(--primary-color);
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px dashed #eee;
            padding-bottom: 8px;
        }

        .weather-badge {
            font-size: 0.9rem;
            background-color: var(--bg-color);
            padding: 4px 8px;
            border-radius: 10px;
            color: var(--text-light);
        }

        .timeline-item {
            margin: 12px 0;
            padding-left: 15px;
            border-left: 2px solid var(--secondary-color);
            position: relative;
        }

        .timeline-item::before {
            content: '';
            position: absolute;
            left: -6px;
            top: 5px;
            width: 10px;
            height: 10px;
            background-color: var(--primary-color);
            border-radius: 50%;
        }

        /* 標籤設計 */
        .tag {
            display: inline-block;
            padding: 2px 6px;
            border-radius: 4px;
            font-size: 0.8rem;
            font-weight: bold;
            color: white;
            margin-right: 5px;
            margin-bottom: 5px;
        }
        .tag.food { background-color: var(--highlight-food); }
        .tag.buy { background-color: var(--highlight-buy); }
        .tag.alert { background-color: var(--highlight-alert); }
        .tag.nav { background-color: #4285F4; }

        /* 導航按鈕 */
        .btn-nav {
            display: inline-flex;
            align-items: center;
            background-color: #f0f0f0;
            color: #333;
            text-decoration: none;
            padding: 6px 12px;
            border-radius: 20px;
            font-size: 0.85rem;
            margin-top: 8px;
            box-shadow: 0 1px 3px rgba(0,0,0,0.1);
        }
        .btn-nav span { margin-right: 5px; }

        /* 底部導覽列 */
        .bottom-nav {
            position: fixed;
            bottom: 0;
            left: 0;
            width: 100%;
            background-color: white;
            display: flex;
            justify-content: space-around;
            padding: 10px 0 calc(10px + env(safe-area-inset-bottom));
            box-shadow: 0 -2px 10px rgba(0,0,0,0.05);
            border-top-left-radius: 20px;
            border-top-right-radius: 20px;
            z-index: 100;
        }

        .nav-item {
            text-align: center;
            color: var(--text-light);
            font-size: 0.8rem;
            cursor: pointer;
            flex: 1;
        }

        .nav-item.active {
            color: var(--primary-color);
            font-weight: bold;
        }

        .nav-icon {
            font-size: 1.5rem;
            display: block;
            margin-bottom: 2px;
        }

        /* 表格設計 */
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 10px;
        }
        th, td {
            text-align: left;
            padding: 10px;
            border-bottom: 1px solid #eee;
            font-size: 0.9rem;
        }
        th { color: var(--primary-color); }
    </style>
</head>
<body>

    <header>
        <h1>💜 2026 東京夢幻之旅</h1>
    </header>

    <!-- 行程頁面 -->
    <div id="itinerary" class="container active">
        <!-- Day 1 -->
        <div class="card">
            <h2>Day 1: 10/26 (一) <span class="weather-badge">☀️ 18°C</span></h2>
            <div class="timeline-item">
                <strong>下午｜抵達與中目黑</strong><br>
                12:10 抵達成田機場 ➔ 飯店放行李<br>
                <a href="https://maps.google.com/?q=D・レガーロ+市川市" target="_blank" class="btn-nav"><span>📍</span>導航至飯店</a><br>
                前往中目黑 (星巴克山手通店、小義大利 La vita)<br>
                <a href="https://maps.google.com/?q=Starbucks+Reserve+Roastery+Tokyo" target="_blank" class="btn-nav"><span>📍</span>導航星巴克</a>
            </div>
            <div class="timeline-item">
                <strong>晚上｜上野採買</strong><br>
                阿美橫町逛街 <span class="tag buy">#必買伴手禮 OS Drug / 二木的菓子</span>
            </div>
        </div>

        <!-- Day 2 -->
        <div class="card">
            <h2>Day 2: 10/27 (二) <span class="weather-badge">☁️ 17°C</span></h2>
            <div class="timeline-item">
                <strong>上午｜淺草和服</strong><br>
                江户和装工房 雅 (建議09:00首批) ➔ 淺草寺、雷門<br>
                <a href="https://maps.google.com/?q=淺草寺" target="_blank" class="btn-nav"><span>📍</span>導航淺草</a>
            </div>
            <div class="timeline-item">
                <strong>下午｜抹茶與神塔</strong><br>
                <span class="tag food">#必吃美食 Suzukien 7號濃抹茶</span><br>
                今戶神社 (招財貓/求姻緣) ➔ 東京晴空塔
            </div>
            <div class="timeline-item">
                <strong>晚餐｜深夜和牛</strong><br>
                燒肉黑田 (澀谷) <span class="tag food">#必點菜單 極厚牛舌</span><br>
                <span class="tag alert">#重要預約代號 需提前官網預約</span><br>
                <a href="https://maps.google.com/?q=焼肉黒田+渋谷" target="_blank" class="btn-nav"><span>📍</span>導航燒肉黑田</a>
            </div>
        </div>

        <!-- Day 3 & 4 -->
        <div class="card">
            <h2>Day 3-4: 迪士尼夢幻雙日 <span class="weather-badge">🏰 16°C</span></h2>
            <div class="timeline-item">
                <strong>10/28 (三)｜海洋 (Sea)</strong><br>
                開園直衝 Fantasy Springs <span class="tag buy">#必買 Duffy周邊</span>
            </div>
            <div class="timeline-item">
                <strong>10/29 (四)｜樂園 (Land)</strong><br>
                <span class="tag alert">#攻略 美女與野獸必買DPA</span><br>
                <span class="tag food">#必吃 米奇鬆餅</span>
            </div>
            <div class="timeline-item">
                <strong>🚌 交通秘訣</strong><br>
                南行德(東西線) ➔ 葛西/浦安站 ➔ 轉乘巴士直達舞濱。
            </div>
        </div>

        <!-- Day 5 -->
        <div class="card">
            <h2>Day 5: 10/30 (五) <span class="weather-badge">🌇 19°C</span></h2>
            <div class="timeline-item">
                <strong>上午｜神宮與都廳</strong><br>
                東京都廳觀景臺 (免費) ➔ 明治神宮
            </div>
            <div class="timeline-item">
                <strong>午餐｜高空燒肉</strong><br>
                敘敘苑 (東京歌劇城 53F)<br>
                <span class="tag food">#必點菜單 午間套餐</span> <span class="tag alert">#重要預約代號 確認Email窗邊席</span><br>
                <a href="https://maps.google.com/?q=敘敘苑+東京歌劇城" target="_blank" class="btn-nav"><span>📍</span>導航敘敘苑</a>
            </div>
            <div class="timeline-item">
                <strong>下午至晚上｜新宿與澀谷</strong><br>
                原宿竹下通 ➔ 伊勢丹新宿 ➔ 澀谷 SKY 夜景 ➔ 歌舞伎町<br>
                <span class="tag alert">#攻略 澀谷SKY需提早一個月購票</span>
            </div>
        </div>

        <!-- Day 6 -->
        <div class="card">
            <h2>Day 6: 10/31 (六) <span class="weather-badge">✈️ 15°C</span></h2>
            <div class="timeline-item">
                <strong>上午｜準備歸途</strong><br>
                08:15 離開飯店 ➔ 成田機場<br>
                <span class="tag alert">#注意 09:25 前須完成報到</span><br>
                免稅店 <span class="tag buy">#必買伴手禮 NY Perfect Cheese</span>
            </div>
        </div>
    </div>

    <!-- 資訊頁面 -->
    <div id="info" class="container">
        <div class="card">
            <h2>✈️ 航班資訊</h2>
            <p><strong>去程 (10/26 一)：</strong> IT280<br>08:00 高雄 (KHH) ➔ 12:10 成田 (NRT)</p>
            <p><strong>回程 (10/31 六)：</strong> IT281<br>11:25 成田 (NRT) ➔ 15:05 高雄 (KHH)</p>
        </div>

        <div class="card">
            <h2>🏨 住宿資訊</h2>
            <p><strong>D・レガーロ</strong></p>
            <p>地址：〒272-0138 Chiba, Ichikawa, Minamigyōtoku, 2-chōme−21</p>
            <a href="https://maps.google.com/?q=D・レガーロ+市川市" target="_blank" class="btn-nav"><span>📍</span>開啟地圖導航</a>
        </div>

        <div class="card">
            <h2>📞 緊急聯絡與工具</h2>
            <p>報警：110 ｜ 急救：119</p>
            <p>駐日經濟文化代表處：+81-3-3280-7811</p>
        </div>
    </div>

    <!-- 記帳/預算頁面 -->
    <div id="budget" class="container">
        <div class="card">
            <h2>💱 匯率計算</h2>
            <p>目前預估：<strong>100 日幣 (JPY) ≈ 21 台幣 (TWD)</strong></p>
        </div>

        <div class="card">
            <h2>💰 預算表 (JPY)</h2>
            <table>
                <tr>
                    <th>項目</th>
                    <th>預估</th>
                    <th>實際</th>
                </tr>
                <tr>
                    <td>餐費 (含燒肉)</td>
                    <td>60,000</td>
                    <td></td>
                </tr>
                <tr>
                    <td>交通 (儲值)</td>
                    <td>15,000</td>
                    <td></td>
                </tr>
                <tr>
                    <td>門票與體驗</td>
                    <td>25,000</td>
                    <td></td>
                </tr>
                <tr>
                    <td>購物伴手禮</td>
                    <td>50,000</td>
                    <td></td>
                </tr>
                <tr>
                    <td><strong>總預算</strong></td>
                    <td><strong>150,000</strong></td>
                    <td></td>
                </tr>
            </table>
        </div>
    </div>

    <!-- 底部導覽列 -->
    <div class="bottom-nav">
        <div class="nav-item active" onclick="switchTab('itinerary', this)">
            <span class="nav-icon">📅</span>
            行程表
        </div>
        <div class="nav-item" onclick="switchTab('info', this)">
            <span class="nav-icon">ℹ️</span>
            行前資訊
        </div>
        <div class="nav-item" onclick="switchTab('budget', this)">
            <span class="nav-icon">👛</span>
            記帳本
        </div>
    </div>

    <script>
        function switchTab(tabId, element) {
            // 隱藏所有內容
            document.querySelectorAll('.container').forEach(el => {
                el.classList.remove('active');
            });
            // 移除所有標籤的 active 狀態
            document.querySelectorAll('.nav-item').forEach(el => {
                el.classList.remove('active');
            });
            
            // 顯示選中的內容並加入 active 狀態
            document.getElementById(tabId).classList.add('active');
            element.classList.add('active');
            
            // 將畫面滾動回最上方
            window.scrollTo(0, 0);
        }
    </script>
</body>
</html>
