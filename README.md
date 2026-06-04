
⚡ Fanmori-Edge ⚡
The Ultimate Optimized Worker for Cloudflare | Low Ping | Zero Buffer | Anti-Detection | Multi-Protocol

<p align="center">
<img src="https://img.shields.io/badge/Version-1.0.0-blue.svg" alt="Version">
<img src="https://img.shields.io/badge/Status-Active-success.svg" alt="Status">
<img src="https://img.shields.io/badge/Platform-Cloudflare%20Workers-F38020.svg" alt="Platform">
</p>
🌟 What is Fanmori-Edge?
Fanmori-Edge is a heavily optimized and rebranded edition of the popular Edgetunnel project, designed specifically to bypass Cloudflare's automated scanning systems while delivering the lowest possible latency and highest stability.

By implementing RAM-level caching, dynamic buffer sizing, and external UI hosting, it solves the common issues of high ping, slow site loading, and CPU limits in free-tier Cloudflare Workers.

✨ Key Advantages & Optimizations
🚀 Zero-Buffer Mode: Optimized buffer sizes (downloadGrainBytes) ensure data flows instantly without waiting to fill large chunks. Excellent for web browsing and gaming.
🛡️ Anti-Detection Architecture: Admin panel assets are hosted externally. The worker code contains no HTML forms, easily bypassing Cloudflare's proxy-detection scanners.
⚡ RAM-Level Caching: Configs, ProxyIP lists, and DNS queries are cached in memory after the first read, reducing KV reads and API calls to near zero. Drastically lowers TTFB (Time To First Byte).
🌐 Multi-Protocol Support: VLESS, Trojan, Shadowsocks over WebSocket, gRPC, and XHTTP.
🔗 **Chain Proxy
