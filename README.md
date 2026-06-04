# 🚀 Fanmori-Edge  
### Multi‑Protocol Edge Proxy for Cloudflare Workers

[![Deploy to Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/fanmori/fanmori-edge)  
[![License](https://img.shields.io/badge/license-MIT-blue)](LICENSE)

**Fanmori‑Edge** is a powerful, all‑in‑one proxy solution that runs on **Cloudflare Workers**.  
It supports **VLESS**, **Trojan**, **Shadowsocks (AEAD)**, **SOCKS5**, **HTTP/HTTPS CONNECT**, **TURN** and **SSTP** protocols, using **WebSocket**, **gRPC** or **XHTTP** transports.  
You can chain upstream proxies, generate client subscriptions (Clash, Sing‑box, Surge, etc.), and even use “clean IP” pools – all at Cloudflare’s edge.

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| **Multi‑protocol** | VLESS, Trojan, SS‑AEAD, SOCKS5, HTTP(S), TURN, SSTP |
| **Transports** | WebSocket, gRPC (GUN/multi), XHTTP (stream‑one) |
| **Chain proxy** | Route traffic through an upstream SOCKS5/HTTP/HTTPS/TURN/SSTP proxy |
| **Subscription** | Generate Clash, Sing‑box, Surge, Quantumult X, Loon configs |
| **Clean IP pools** | Built‑in random IP generator + external APIs (csv, txt, sub links) |
| **DNS over HTTPS** | Built‑in DoH with caching and pre‑resolve race |
| **TLS customization** | uTLS fingerprints, ECH (Encrypted Client Hello), ChaCha20 fallback |
| **Admin panel** | Password‑protected dashboard, logs, proxy health check, Cloudflare usage |
| **Fallback & load‑balance** | Multiple proxyIP entries, automatic retry, random shuffle |

---

## 📋 Prerequisites

- A **Cloudflare account** with an active domain (or you can use `*.workers.dev` subdomain).
- **Workers & Pages** service enabled (free plan works).
- A **KV Namespace** – used to store configs (`config.json`, `cf.json`, `tg.json`, `ADD.txt`).  
  Bind it to your Worker with the variable name `KV`.

---

## 🚀 Deployment – Step by Step

### 1. Create a KV Namespace
- Go to Cloudflare Dashboard → **Workers & Pages** → **KV**.
- Create a new namespace (e.g., `FANMORI_KV`).
- Note its **ID** – you will bind it to your Worker.

### 2. Create a Worker
- In the same dashboard → **Create Worker** → give it a name (e.g., `fanmori-edge`).
- Open the **Quick Edit** editor and **replace the entire content** with the code from `worker.js` (the file you have).

### 3. Bind KV to the Worker
- Go to your Worker’s **Settings** → **Variables** → **KV Namespace Bindings**.
- Click **Add binding**:
  - Variable name: `KV`
  - Select the namespace you created.
- Save.

### 4. Environment Variables (optional but recommended)
Still under **Variables** → **Environment Variables**, add any of the following:

| Variable | Description | Example |
|----------|-------------|---------|
| `ADMIN` / `PASSWORD` | Admin panel password | `mySecret123` |
| `KEY` | Access path – used for subscription | `dontchangethis` |
| `UUID` | Custom VLESS/Trojan user ID | `11111111-1111-1111-1111-111111111111` |
| `PROXYIP` | One or more upstream proxies (comma separated) | `1.2.3.4:443, 5.6.7.8:8080` |
| `HOST` | Domain(s) your Worker will answer for (used in subscription) | `example.com, sub.example.com` |
| `PATH` | Base path for WebSocket/gRPC | `/myapp` |
| `BEST_SUB` | Enable “best subscription” generator (for testing) | `true` |
| `DEBUG` | Enable debug logs | `true` |
| `PRELOAD_RACE_DIAL` | Pre‑resolve DNS and race connections | `true` |

> **Important** – If you don’t set `ADMIN`, the admin panel and proxy functions are **disabled**.

### 5. Deploy
- Click **Save and Deploy**.

Your Worker is now live at:  
`https://<your-worker-name>.<your-subdomain>.workers.dev`

---

## 🧪 First Test – Admin Panel

1. Open your Worker URL in a browser.  
   If `ADMIN` is not set, you will see a placeholder page.
2. Go to `https://.../login` – enter the password you set as `ADMIN`.
3. After login, you can:
   - View and edit `config.json` (proxy settings, subscriptions, etc.)
   - Save custom proxy IPs (`ADD.txt`)
   - Check upstream proxy health (`/admin/check?protocol=...`)
   - See logs (`/admin/log.json`)

---

## 📡 Subscription Links

Once `UUID` and `KEY` are set, your clients can use:

- **Clash** → `https://.../sub?target=clash&token=...`
- **Sing‑box** → `https://.../sub?target=singbox&token=...`
- **Mixed (standard URI)** → `https://.../sub?target=mixed&token=...`

The token is `MD5(host + UUID)`.

---

## 🧩 How It Works – Under the Hood

[```mermaid
graph LR
A[Client] -->|VLESS/Trojan/SS| B[Cloudflare Worker]
B -->|WebSocket/gRPC/XHTTP| C{Transport}
C -->|If chain proxy| D[Upstream Proxy SOCKS5/HTTP/TURN]
C -->|Direct| E[Target Server]
D --> E ]

## 🧩 How It Works – Under the Hood

1. **Client** sends a request with a special first packet (VLESS or Trojan header).  
2. **Worker** parses the header – extracts target host, port, and any early data.  
3. **Routing decision**:  
   - If `globalSOCKS5` or a domain matches the `SOCKS5白名单`, it connects through an upstream proxy.  
   - Otherwise, it tries **direct** connection with pre‑resolved DNS (race dial).  
   - On failure, it falls back to `PROXYIP` relay.  
4. **Connection** is established – the Worker then **pipes** raw TCP/UDP data between the client WebSocket/gRPC stream and the remote socket.  
5. **Subscription** endpoints read local IP pools or fetch from API, then generate protocol‑specific configs.

---

## ⚠️ Limitations

| Limitation | Explanation |
|------------|-------------|
| **UDP only for DNS** | Only UDP port 53 is supported (via DNS‑over‑TCP to 8.8.4.4). Any other UDP traffic is rejected. |
| **Worker CPU time** | Free plan has 10ms CPU time per request – heavy traffic may be limited. |
| **KV rate limits** | Free KV has 1k reads/day, 1k writes/day. Use caching to avoid exhaustion. |
| **TURN/SSTP complexity** | Those protocols require additional round trips and may be unstable over Cloudflare. |
| **IPv6** | Supported, but some upstream proxies may not handle it correctly. |
| **gRPC streaming** | Works, but error handling is limited – connections may hang if not properly closed. |

---

## 💰 Donation

If you find this project useful, consider supporting the author:

- **BTC**: `bc1q...` (not provided here – add your own)  
- **USDT (TRC20)**: `T...`  
- **GitHub Sponsor**: [Click to sponsor](https://github.com/sponsors/fanmori)

---

## 🛠️ Advanced Customization

### Using Clean IP Pools
- Edit `ADD.txt` via admin panel – each line: `IP:PORT#Remark`  
- Or use `PROXYIP` with domain names that return TXT records containing IP lists.  
- In `config.json` → `优选订阅生成` → set `local: true` to use the internal random IP generator.

### Chain Proxy via URL
Append to the WebSocket path:  
`/video/<base64_encoded_json>`

Example JSON:  
```json
{ "type": "socks5", "username": "user", "password": "pass", "hostname": "myproxy.com", "port": 1080 }
