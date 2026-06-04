<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fanmori-Edge - The Ultimate Optimized Worker</title>
    <style>
        :root {
            --bg-color: #0d1117;
            --card-bg: #161b22;
            --border-color: #30363d;
            --text-main: #c9d1d9;
            --text-muted: #8b949e;
            --accent-blue: #58a6ff;
            --accent-green: #3fb950;
            --accent-red: #f85149;
            --accent-purple: #bc8cff;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-main);
            line-height: 1.6;
            padding: 20px;
        }

        .container {
            max-width: 900px;
            margin: 0 auto;
        }

        header {
            text-align: center;
            padding: 60px 0;
            border-bottom: 1px solid var(--border-color);
            margin-bottom: 40px;
        }

        h1 {
            font-size: 3rem;
            background: linear-gradient(to right, var(--accent-blue), var(--accent-purple));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 10px;
        }

        .subtitle {
            font-size: 1.2rem;
            color: var(--text-muted);
        }

        .badges {
            margin-top: 20px;
            display: flex;
            justify-content: center;
            gap: 10px;
            flex-wrap: wrap;
        }

        .badge {
            background-color: var(--card-bg);
            border: 1px solid var(--border-color);
            padding: 5px 12px;
            border-radius: 20px;
            font-size: 0.85rem;
            font-weight: bold;
        }

        section {
            margin-bottom: 50px;
        }

        h2 {
            font-size: 1.8rem;
            color: var(--accent-blue);
            border-bottom: 1px solid var(--border-color);
            padding-bottom: 10px;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .card-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
        }

        .card {
            background-color: var(--card-bg);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            padding: 20px;
            transition: transform 0.2s, border-color 0.2s;
        }

        .card:hover {
            transform: translateY(-3px);
            border-color: var(--accent-blue);
        }

        .card h3 {
            color: var(--accent-green);
            margin-bottom: 10px;
            font-size: 1.1rem;
        }

        .card.warning h3 {
            color: var(--accent-red);
        }

        .card p {
            color: var(--text-muted);
            font-size: 0.95rem;
        }

        .steps {
            counter-reset: step;
        }

        .step {
            background-color: var(--card-bg);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            padding: 20px;
            margin-bottom: 15px;
            position: relative;
            padding-left: 60px;
        }

        .step::before {
            counter-increment: step;
            content: counter(step);
            position: absolute;
            left: 15px;
            top: 15px;
            font-size: 1.5rem;
            font-weight: bold;
            color: var(--accent-purple);
        }

        code {
            background-color: rgba(110, 118, 129, 0.4);
            padding: 0.2em 0.4em;
            margin: 0;
            font-size: 85%;
            border-radius: 6px;
            font-family: monospace;
        }

        .var-table {
            width: 100%;
            border-collapse: collapse;
            background-color: var(--card-bg);
            border-radius: 8px;
            overflow: hidden;
        }

        .var-table th, .var-table td {
            border: 1px solid var(--border-color);
            padding: 12px;
            text-align: left;
        }

        .var-table th {
            background-color: #1c2128;
            color: var(--accent-blue);
        }

        /* Donate Section */
        .donate-section {
            text-align: center;
            background: linear-gradient(145deg, #1c2128, #161b22);
            border: 1px solid var(--accent-purple);
            border-radius: 12px;
            padding: 40px 20px;
            margin-top: 50px;
        }

        .donate-section h2 {
            border: none;
            justify-content: center;
            color: var(--accent-purple);
        }

        .crypto-box {
            background-color: var(--bg-color);
            padding: 15px;
            border-radius: 8px;
            display: inline-block;
            margin-top: 20px;
            text-align: left;
            border: 1px solid var(--border-color);
        }

        .wallet-row {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-top: 5px;
        }

        .wallet-address {
            color: #fff;
            font-family: monospace;
            font-size: 0.9rem;
            background: #2d333b;
            padding: 8px;
            border-radius: 4px;
        }

        .copy-btn {
            background-color: var(--accent-purple);
            color: #fff;
            border: none;
            padding: 8px 15px;
            border-radius: 4px;
            cursor: pointer;
            font-weight: bold;
            transition: opacity 0.2s;
        }

        .copy-btn:hover { opacity: 0.8; }

        .donate-links {
            margin-top: 30px;
            display: flex;
            justify-content: center;
            gap: 15px;
            flex-wrap: wrap;
        }

        .donate-link {
            background-color: #FFDD00;
            color: #000;
            text-decoration: none;
            padding: 10px 25px;
            border-radius: 8px;
            font-weight: bold;
            transition: transform 0.2s;
        }

        .donate-link:hover { transform: scale(1.05); }

        footer {
            text-align: center;
            margin-top: 50px;
            padding-top: 20px;
            border-top: 1px solid var(--border-color);
            color: var(--text-muted);
            font-size: 0.9rem;
        }
    </style>
</head>
<body>

<div class="container">
    <header>
        <h1>Fanmori-Edge</h1>
        <p class="subtitle">The Ultimate Optimized VLESS/Trojan/SS Worker for Cloudflare</p>
        <div class="badges">
            <span class="badge" style="color: var(--accent-green);">● Active</span>
            <span class="badge" style="color: var(--accent-blue);">Version 1.0.0</span>
            <span class="badge" style="color: var(--accent-purple);">Zero-Buffer Mode</span>
        </div>
    </header>

    <!-- FEATURES -->
    <section>
        <h2>✨ Advantages & Features</h2>
        <div class="card-grid">
            <div class="card">
                <h3>🚀 Low Ping / Zero Buffer</h3>
                <p>Optimized with dynamic buffer sizing and RAM caching for KV. Ensures the lowest possible TTFB for flawless web browsing and gaming.</p>
            </div>
            <div class="card">
                <h3>🛡️ Anti-Detection Panel</h3>
                <p>Admin panel assets are loaded externally to bypass Cloudflare's automated proxy-detection scanners and save CPU time.</p>
            </div>
            <div class="card">
                <h3>🌐 Multi-Protocol</h3>
                <p>Supports VLESS, Trojan, and Shadowsocks over WebSocket, gRPC, and XHTTP. Full
