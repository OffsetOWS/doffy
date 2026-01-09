# doffy <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>QuikCharts ™ - Digital Dreams</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@400;600&display=swap');

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'IBM Plex Mono', monospace;
            background: linear-gradient(135deg, #1a0b2e 0%, #2d1b4e 25%, #1e3a5f 50%, #0f2847 75%, #1a1a2e 100%);
            color: #e0e0e0;
            overflow-x: hidden;
            position: relative;
            min-height: 100vh;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
        }

        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: 
                linear-gradient(rgba(138, 43, 226, 0.05) 1px, transparent 1px),
                linear-gradient(90deg, rgba(138, 43, 226, 0.05) 1px, transparent 1px);
            background-size: 50px 50px;
            pointer-events: none;
            z-index: 1;
        }

        .sun {
            position: fixed;
            bottom: -150px;
            left: 50%;
            transform: translateX(-50%);
            width: 350px;
            height: 350px;
            background: radial-gradient(circle, #ffd6f0 0%, #ffb3e6 30%, #ff91dc 60%, rgba(255, 145, 220, 0) 100%);
            border-radius: 50%;
            z-index: 0;
            opacity: 0.7;
        }

        .grid {
            position: fixed;
            bottom: 0;
            left: 0;
            width: 100%;
            height: 45%;
            background-image: 
                linear-gradient(rgba(255, 145, 220, 0.4) 1.5px, transparent 1.5px),
                linear-gradient(90deg, rgba(255, 145, 220, 0.4) 1.5px, transparent 1.5px);
            background-size: 60px 60px;
            transform: perspective(600px) rotateX(60deg);
            transform-origin: bottom;
            z-index: 0;
            opacity: 0.8;
        }

        .container {
            position: relative;
            z-index: 2;
            max-width: 1400px;
            margin: 0 auto;
            padding: 30px 20px;
        }

        .window {
            background: linear-gradient(to bottom, #e8e8e8 0%, #d0d0d0 100%);
            border-radius: 8px;
            border: 1px solid rgba(255, 255, 255, 0.8);
            box-shadow: 
                0 8px 32px rgba(0, 0, 0, 0.15),
                inset 0 1px 0 rgba(255, 255, 255, 0.8),
                inset 1px 0 0 rgba(255, 255, 255, 0.6),
                inset -1px 0 0 rgba(0, 0, 0, 0.1),
                inset 0 -1px 0 rgba(0, 0, 0, 0.1);
            margin-bottom: 25px;
            overflow: hidden;
        }

        .window-titlebar {
            background: linear-gradient(to bottom, #a891ff 0%, #8b6fff 100%);
            padding: 8px 12px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid rgba(0, 0, 0, 0.1);
        }

        .window-title {
            color: #ffffff;
            font-weight: 600;
            display: flex;
            align-items: center;
            gap: 10px;
            font-size: 0.95rem;
            text-shadow: 0 1px 2px rgba(0, 0, 0, 0.2);
        }

        .window-controls {
            display: flex;
            gap: 6px;
        }

        .window-button {
            width: 22px;
            height: 22px;
            background: linear-gradient(to bottom, #f0f0f0 0%, #d8d8d8 100%);
            border-radius: 3px;
            border: 1px solid rgba(0, 0, 0, 0.15);
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            font-size: 0.85rem;
            color: #555;
            box-shadow: 
                inset 0 1px 0 rgba(255, 255, 255, 0.8),
                0 1px 2px rgba(0, 0, 0, 0.1);
            transition: all 0.15s ease;
        }

        .window-button:hover {
            background: linear-gradient(to bottom, #f8f8f8 0%, #e0e0e0 100%);
        }

        .window-button:active {
            box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.2);
            transform: translateY(1px);
        }

        .window-content {
            padding: 20px;
            background: #f5f5f5;
        }

        .header {
            text-align: center;
            padding: 50px 20px 40px;
            position: relative;
        }

        .header h1 {
            font-size: 4.5rem;
            font-weight: 600;
            background: linear-gradient(135deg, #ff91dc 0%, #a891ff 25%, #7dd3fc 50%, #c89cff 75%, #ff91dc 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            background-size: 200% 200%;
            animation: gradient-shift 4s ease infinite;
            letter-spacing: 0.05em;
            filter: drop-shadow(2px 2px 4px rgba(0, 0, 0, 0.1));
        }

        @keyframes gradient-shift {
            0%, 100% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
        }

        .header-subtitle {
            font-size: 1.1rem;
            color: #6b5b95;
            margin-top: 15px;
            font-weight: 400;
        }

        .section-title {
            background: linear-gradient(to bottom, #8b6fff 0%, #7a5ee6 100%);
            padding: 10px 16px;
            margin-bottom: 18px;
            color: #ffffff;
            font-size: 1rem;
            font-weight: 600;
            border-radius: 5px;
            box-shadow: 
                0 2px 8px rgba(139, 111, 255, 0.3),
                inset 0 1px 0 rgba(255, 255, 255, 0.2);
        }

        .crypto-table {
            width: 100%;
            border-collapse: separate;
            border-spacing: 0;
            background: #ffffff;
            font-size: 0.9rem;
            border-radius: 6px;
            overflow: hidden;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
        }

        .crypto-table th {
            background: linear-gradient(to bottom, #6b5b95 0%, #5a4a7f 100%);
            color: #ffffff;
            padding: 14px 12px;
            text-align: left;
            font-weight: 600;
            font-size: 0.85rem;
            text-transform: uppercase;
            letter-spacing: 0.05em;
        }

        .crypto-table th:first-child {
            border-top-left-radius: 6px;
        }

        .crypto-table th:last-child {
            border-top-right-radius: 6px;
        }

        .crypto-table td {
            padding: 14px 12px;
            border-bottom: 1px solid #f0f0f0;
            color: #2d2d2d;
            background: #ffffff;
        }

        .crypto-table tbody tr:last-child td {
            border-bottom: none;
        }

        .crypto-table tbody tr:nth-child(even) td {
            background: #fafafa;
        }

        .crypto-table tbody tr {
            transition: all 0.2s ease;
        }

        .crypto-table tbody tr:hover td {
            background: linear-gradient(to right, #fff0fb 0%, #f0e6ff 100%);
        }

        .coin-info {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .coin-icon {
            width: 32px;
            height: 32px;
            border-radius: 50%;
            border: 2px solid #e8e8e8;
            box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
        }

        .coin-name {
            font-weight: 600;
            color: #5a4a7f;
        }

        .coin-symbol {
            color: #888;
            font-size: 0.8rem;
            margin-top: 2px;
        }

        .price-positive {
            color: #10b981;
            font-weight: 600;
        }

        .price-negative {
            color: #ef4444;
            font-weight: 600;
        }

        .loading {
            text-align: center;
            padding: 50px 20px;
            color: #2d2d2d;
            font-size: 0.95rem;
        }

        .loading-box {
            background: linear-gradient(to bottom, #e8e8e8 0%, #d0d0d0 100%);
            border-radius: 0;
            border: 2px solid;
            border-color: #dfdfdf #0a0a0a #0a0a0a #dfdfdf;
            padding: 30px 40px;
            margin: 0 auto;
            max-width: 400px;
            box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.3);
        }

        .loading-title {
            color: #000;
            font-size: 1rem;
            margin-bottom: 20px;
            font-weight: 400;
        }

        .progress-bar-container {
            background: #fff;
            border: 2px solid;
            border-color: #808080 #dfdfdf #dfdfdf #808080;
            height: 24px;
            margin-bottom: 20px;
            padding: 2px;
            box-shadow: inset 1px 1px 2px rgba(0, 0, 0, 0.2);
        }

        .progress-bar {
            height: 100%;
            background: linear-gradient(to right, #000080 0%, #0000ff 50%, #000080 100%);
            background-size: 200% 100%;
            animation: progress-slide 1.5s linear infinite;
            width: 0%;
        }

        @keyframes progress-slide {
            0% { background-position: 0% 0%; }
            100% { background-position: 200% 0%; }
        }

        .loading-buttons {
            display: flex;
            gap: 10px;
            justify-content: center;
        }

        .loading-button {
            background: linear-gradient(to bottom, #f0f0f0 0%, #d8d8d8 100%);
            border: 2px solid;
            border-color: #fff #0a0a0a #0a0a0a #fff;
            padding: 6px 20px;
            font-family: 'IBM Plex Mono', monospace;
            font-size: 0.9rem;
            cursor: not-allowed;
            color: #808080;
            min-width: 80px;
        }

        .loading-spinner {
            width: 50px;
            height: 50px;
            margin: 0 auto 20px;
            border: 4px solid #e8e8e8;
            border-top: 4px solid #a891ff;
            border-radius: 50%;
            animation: spin 1s linear infinite;
            display: none;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .button-95 {
            background: linear-gradient(to bottom, #f0f0f0 0%, #d8d8d8 100%);
            border-radius: 5px;
            border: 1px solid rgba(0, 0, 0, 0.15);
            padding: 10px 24px;
            font-family: 'IBM Plex Mono', monospace;
            font-size: 0.9rem;
            font-weight: 600;
            cursor: pointer;
            margin: 5px;
            color: #2d2d2d;
            box-shadow: 
                inset 0 1px 0 rgba(255, 255, 255, 0.8),
                0 2px 6px rgba(0, 0, 0, 0.1);
            transition: all 0.15s ease;
        }

        .button-95:hover {
            background: linear-gradient(to bottom, #f8f8f8 0%, #e0e0e0 100%);
            transform: translateY(-1px);
            box-shadow: 
                inset 0 1px 0 rgba(255, 255, 255, 0.8),
                0 4px 12px rgba(0, 0, 0, 0.15);
        }

        .button-95:active {
            box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.2);
            transform: translateY(0px);
        }

        .status-bar {
            background: linear-gradient(to bottom, #e8e8e8 0%, #d0d0d0 100%);
            border-top: 1px solid rgba(255, 255, 255, 0.5);
            padding: 10px 16px;
            display: flex;
            justify-content: space-between;
            font-size: 0.85rem;
            color: #555;
            border-radius: 0 0 8px 8px;
        }

        .status-panel {
            background: #ffffff;
            border-radius: 3px;
            border: 1px solid rgba(0, 0, 0, 0.1);
            padding: 4px 10px;
            box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.05);
        }

        .rank-badge {
            display: inline-block;
            padding: 4px 10px;
            background: linear-gradient(135deg, #ff91dc 0%, #a891ff 100%);
            color: #ffffff;
            border-radius: 4px;
            font-weight: 600;
            font-size: 0.85rem;
            box-shadow: 0 2px 6px rgba(168, 145, 255, 0.3);
        }

        .alert-box {
            background: linear-gradient(to bottom, #fff5f5 0%, #ffe8e8 100%);
            border: 1px solid #fecaca;
            border-radius: 6px;
            padding: 16px;
            margin: 20px 0;
            box-shadow: 0 2px 8px rgba(239, 68, 68, 0.1);
        }

        .alert-title {
            background: linear-gradient(to right, #ef4444 0%, #ff6b9d 100%);
            color: #ffffff;
            padding: 8px 12px;
            margin: -16px -16px 12px -16px;
            font-size: 0.9rem;
            font-weight: 600;
            display: flex;
            align-items: center;
            gap: 8px;
            border-radius: 6px 6px 0 0;
        }

        .alert-box p {
            color: #991b1b;
            font-size: 0.9rem;
            line-height: 1.6;
        }

        .floating-orb {
            position: fixed;
            width: 120px;
            height: 120px;
            border-radius: 50%;
            opacity: 0.15;
            z-index: 0;
            animation: float-orb 20s infinite ease-in-out;
        }

        .orb-1 {
            background: radial-gradient(circle, #ff91dc, transparent);
            top: 10%;
            left: 10%;
            animation-delay: 0s;
        }

        .orb-2 {
            background: radial-gradient(circle, #a891ff, transparent);
            top: 20%;
            right: 15%;
            animation-delay: 5s;
        }

        .orb-3 {
            background: radial-gradient(circle, #7dd3fc, transparent);
            bottom: 15%;
            left: 20%;
            animation-delay: 10s;
        }

        @keyframes float-orb {
            0%, 100% { transform: translate(0, 0); }
            33% { transform: translate(30px, -30px); }
            66% { transform: translate(-20px, 20px); }
        }

        .floating-emoji {
            position: fixed;
            font-size: 4rem;
            opacity: 0.25;
            z-index: 0;
            animation: swim 25s infinite ease-in-out;
            filter: drop-shadow(2px 2px 4px rgba(0, 0, 0, 0.1));
        }

        .emoji-1 {
            top: 15%;
            left: 5%;
            animation-delay: 0s;
            animation-duration: 30s;
        }

        .emoji-2 {
            top: 40%;
            right: 8%;
            animation-delay: 5s;
            animation-duration: 35s;
        }

        .emoji-3 {
            top: 65%;
            left: 15%;
            animation-delay: 10s;
            animation-duration: 28s;
        }

        .emoji-4 {
            top: 25%;
            right: 20%;
            animation-delay: 3s;
            animation-duration: 32s;
        }

        .emoji-5 {
            top: 55%;
            right: 25%;
            animation-delay: 8s;
            animation-duration: 26s;
        }

        .emoji-6 {
            top: 80%;
            left: 30%;
            animation-delay: 12s;
            animation-duration: 29s;
        }

        .emoji-7 {
            top: 10%;
            left: 40%;
            animation-delay: 15s;
            animation-duration: 33s;
        }

        .emoji-8 {
            top: 45%;
            left: 8%;
            animation-delay: 6s;
            animation-duration: 31s;
        }

        @keyframes swim {
            0%, 100% {
                transform: translate(0, 0) rotate(0deg);
            }
            25% {
                transform: translate(50px, -30px) rotate(10deg);
            }
            50% {
                transform: translate(-30px, 40px) rotate(-15deg);
            }
            75% {
                transform: translate(40px, 20px) rotate(5deg);
            }
        }

        @media (max-width: 768px) {
            .header h1 {
                font-size: 2.5rem;
            }
            
            .crypto-table {
                font-size: 0.8rem;
            }
            
            .crypto-table th,
            .crypto-table td {
                padding: 10px 8px;
            }
        }
    </style>
</head>
<body>
    <div class="sun"></div>
    <div class="grid"></div>
    
    <div class="floating-emoji emoji-1">🐋</div>
    <div class="floating-emoji emoji-2">🦈</div>
    <div class="floating-emoji emoji-3">🦐</div>
    <div class="floating-emoji emoji-4">🐋</div>
    <div class="floating-emoji emoji-5">🦈</div>
    <div class="floating-emoji emoji-6">🦐</div>
    <div class="floating-emoji emoji-7">🐋</div>
    <div class="floating-emoji emoji-8">🦐</div>

    <div class="container">
        <div class="header">
            <h1>QUIKCHARTS</h1>
            <div class="header-subtitle">∿ Digital Dreams • Cyber Reality ∿</div>
        </div>

        <div class="window">
            <div class="window-titlebar">
                <div class="window-title">
                    <span>📊</span>
                    <span>Top 20 Coins - Market Leaders</span>
                </div>
                <div class="window-controls">
                    <div class="window-button">−</div>
                    <div class="window-button">□</div>
                    <div class="window-button">×</div>
                </div>
            </div>
            <div class="window-content">
                <div class="section-title">🏆 Most Traded Cryptocurrencies</div>
                <div id="topCoinsLoading" class="loading">
                    <div class="loading-box">
                        <div class="loading-title">Loading market data...</div>
                        <div class="progress-bar-container">
                            <div class="progress-bar" style="width: 60%;"></div>
                        </div>
                        <div class="loading-buttons">
                            <button class="loading-button" disabled>Done</button>
                            <button class="loading-button" disabled>Cancel</button>
                        </div>
                    </div>
                </div>
                <table class="crypto-table" id="topCoinsTable" style="display: none;">
                    <thead>
                        <tr>
                            <th>Rank</th>
                            <th>Coin</th>
                            <th>Price</th>
                            <th>24h Change</th>
                            <th>Market Cap</th>
                            <th>Volume</th>
                        </tr>
                    </thead>
                    <tbody id="topCoinsBody"></tbody>
                </table>
            </div>
            <div class="status-bar">
                <div class="status-panel">Last Update: <span id="lastUpdate1">--:--</span></div>
                <div class="status-panel">Auto-refresh: 60 min</div>
            </div>
        </div>

        <div class="window">
            <div class="window-titlebar">
                <div class="window-title">
                    <span>📈</span>
                    <span>Volume Kings - Trading Activity</span>
                </div>
                <div class="window-controls">
                    <div class="window-button">−</div>
                    <div class="window-button">□</div>
                    <div class="window-button">×</div>
                </div>
            </div>
            <div class="window-content">
                <div class="section-title">💰 Highest Volume Traders</div>
                <div id="volumeLoading" class="loading">
                    <div class="loading-box">
                        <div class="loading-title">Analyzing volume data...</div>
                        <div class="progress-bar-container">
                            <div class="progress-bar" style="width: 60%;"></div>
                        </div>
                        <div class="loading-buttons">
                            <button class="loading-button" disabled>Done</button>
                            <button class="loading-button" disabled>Cancel</button>
                        </div>
                    </div>
                </div>
                <table class="crypto-table" id="volumeTable" style="display: none;">
                    <thead>
                        <tr>
                            <th>Rank</th>
                            <th>Coin</th>
                            <th>Price</th>
                            <th>24h Change</th>
                            <th>Volume</th>
                            <th>Market Cap</th>
                        </tr>
                    </thead>
                    <tbody id="volumeBody"></tbody>
                </table>
            </div>
            <div class="status-bar">
                <div class="status-panel">Last Update: <span id="lastUpdate2">--:--</span></div>
                <div class="status-panel">Sorted by Volume</div>
            </div>
        </div>

        <div class="window">
            <div class="window-titlebar">
                <div class="window-title">
                    <span>💎</span>
                    <span>Low Volume Perps - Hidden Opportunities</span>
                </div>
                <div class="window-controls">
                    <div class="window-button">−</div>
                    <div class="window-button">□</div>
                    <div class="window-button">×</div>
                </div>
            </div>
            <div class="window-content">
                <div class="alert-box">
                    <div class="alert-title">⚠️ High Risk Warning</div>
                    <p>Low liquidity equals high volatility. These coins have minimal trading volume. Trade perpetuals at your own risk. Not financial advice.</p>
                </div>
                <div class="section-title">🔮 Lowest Volume Perpetuals</div>
                <div id="lowVolumeLoading" class="loading">
                    <div class="loading-box">
                        <div class="loading-title">Discovering hidden opportunities...</div>
                        <div class="progress-bar-container">
                            <div class="progress-bar" style="width: 60%;"></div>
                        </div>
                        <div class="loading-buttons">
                            <button class="loading-button" disabled>Done</button>
                            <button class="loading-button" disabled>Cancel</button>
                        </div>
                    </div>
                </div>
                <table class="crypto-table" id="lowVolumeTable" style="display: none;">
                    <thead>
                        <tr>
                            <th>Rank</th>
                            <th>Coin</th>
                            <th>Price</th>
                            <th>24h Change</th>
                            <th>Volume</th>
                            <th>Market Cap</th>
                        </tr>
                    </thead>
                    <tbody id="lowVolumeBody"></tbody>
                </table>
            </div>
            <div class="status-bar">
                <div class="status-panel">Last Update: <span id="lastUpdate3">--:--</span></div>
                <div class="status-panel">Min Market Cap: $1M</div>
            </div>
        </div>

        <center style="margin: 30px 0;">
            <button class="button-95" onclick="fetchCryptoData()">🔄 Refresh All Data</button>
            <button class="button-95" onclick="alert('QuikCharts™ - Real-time cryptocurrency data with vaporwave aesthetics')">ℹ️ About</button>
            <button class="button-95" onclick="window.scrollTo({top: 0, behavior: 'smooth'})">⬆️ Back to Top</button>
        </center>

        <div class="window">
            <div class="window-titlebar">
                <div class="window-title">
                    <span>💻</span>
                    <span>System Information</span>
                </div>
                <div class="window-controls">
                    <div class="window-button">−</div>
                    <div class="window-button">□</div>
                    <div class="window-button">×</div>
                </div>
            </div>
            <div class="window-content">
                <div style="color: #555; font-size: 0.9rem; line-height: 1.8;">
                    <p>🌐 QuikCharts™ Digital Dreams Interface v2.0</p>
                    <p>📡 Real-time data via CoinGecko API</p>
                    <p>⏱️ Auto-refresh every 60 minutes</p>
                    <p>🎨 Vaporwave • Retro-futurism • Windows 95 Aesthetic</p>
                    <p>💾 Optimized for modern displays with anti-aliased rendering</p>
                    <p style="margin-top: 15px; color: #888;">© 1995-2026 QuikCharts Inc. All rights reserved.</p>
                </div>
            </div>
        </div>
    </div>

    <script>
        function formatCurrency(value) {
            if (value >= 1e9) {
                return '$' + (value / 1e9).toFixed(2) + 'B';
            } else if (value >= 1e6) {
                return '$' + (value / 1e6).toFixed(2) + 'M';
            } else if (value >= 1000) {
                return '$' + value.toLocaleString('en-US', { maximumFractionDigits: 2 });
            } else {
                return '$' + value.toFixed(6);
            }
        }

        function formatPercentage(value) {
            const formatted = value.toFixed(2);
            const className = value >= 0 ? 'price-positive' : 'price-negative';
            const arrow = value >= 0 ? '▲' : '▼';
            return `<span class="${className}">${arrow} ${value >= 0 ? '+' : ''}${formatted}%</span>`;
        }

        function createCoinRow(coin, index) {
            return `
                <tr>
                    <td><span class="rank-badge">#${index + 1}</span></td>
                    <td>
                        <div class="coin-info">
                            <img src="${coin.image}" alt="${coin.name}" class="coin-icon">
                            <div>
                                <div class="coin-name">${coin.name}</div>
                                <div class="coin-symbol">${coin.symbol.toUpperCase()}</div>
                            </div>
                        </div>
                    </td>
                    <td><strong>${formatCurrency(coin.current_price)}</strong></td>
                    <td>${formatPercentage(coin.price_change_percentage_24h || 0)}</td>
                    <td>${formatCurrency(coin.market_cap)}</td>
                    <td>${formatCurrency(coin.total_volume)}</td>
                </tr>
            `;
        }

        async function fetchCryptoData() {
            try {
                const response = await fetch(
                    'https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=250&page=1&sparkline=false'
                );
                const data = await response.json();
                
                const now = new Date();
                const timeStr = now.toLocaleTimeString();
                document.getElementById('lastUpdate1').textContent = timeStr;
                document.getElementById('lastUpdate2').textContent = timeStr;
                document.getElementById('lastUpdate3').textContent = timeStr;
                
                const topCoins = data.slice(0, 20);
                displayTopCoins(topCoins);
                
                const volumeCoins = [...data].sort((a, b) => b.total_volume - a.total_volume).slice(0, 20);
                displayVolumeCoins(volumeCoins);
                
                const lowVolumeCoins = [...data]
                    .filter(coin => coin.market_cap > 1000000)
                    .sort((a, b) => a.total_volume - b.total_volume)
                    .slice(0, 20);
                displayLowVolumeCoins(lowVolumeCoins);
                
            } catch (error) {
                console.error('Error fetching crypto data:', error);
                const errorBox = `
                    <div class="loading-box">
                        <div class="loading-title" style="color: #8b0000;">Error loading data. Please refresh.</div>
                        <div class="loading-buttons">
                            <button class="loading-button" style="cursor: pointer; color: #000;" onclick="fetchCryptoData()">Retry</button>
                            <button class="loading-button" disabled>Cancel</button>
                        </div>
                    </div>
                `;
                document.getElementById('topCoinsLoading').innerHTML = errorBox;
                document.getElementById('volumeLoading').innerHTML = errorBox;
                document.getElementById('lowVolumeLoading').innerHTML = errorBox;
            }
        }

        function displayTopCoins(coins) {
            const tbody = document.getElementById('topCoinsBody');
            tbody.innerHTML = coins.map((coin, index) => createCoinRow(coin, index)).join('');
            document.getElementById('topCoinsLoading').style.display = 'none';
            document.getElementById('topCoinsTable').style.display = 'table';
        }

        function displayVolumeCoins(coins) {
            const tbody = document.getElementById('volumeBody');
            tbody.innerHTML = coins.map((coin, index) => createCoinRow(coin, index)).join('');
            document.getElementById('volumeLoading').style.display = 'none';
            document.getElementById('volumeTable').style.display = 'table';
        }

        function displayLowVolumeCoins(coins) {
            const tbody = document.getElementById('lowVolumeBody');
            tbody.innerHTML = coins.map((coin, index) => createCoinRow(coin, index)).join('');
            document.getElementById('lowVolumeLoading').style.display = 'none';
            document.getElementById('lowVolumeTable').style.display = 'table';
        }

        fetchCryptoData();
        setInterval(fetchCryptoData, 3600000);
    </script>
</body>
</html>
