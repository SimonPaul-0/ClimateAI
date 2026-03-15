# ClimateAI — Live Global Climate Operations Platform

> AI-driven climate adaptation platform with real-time sensor simulation, 11 global cities, 3D globe, and AI analyst powered by Claude.

![ClimateAI](https://img.shields.io/badge/ClimateAI-Live%20Platform-00ffe7?style=flat-square&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI+PHBhdGggZmlsbD0iIzAwZmZlNyIgZD0iTTEyIDJhMTAgMTAgMCAxIDAgMCAyMEExMCAxMCAwIDAgMCAxMiAyeiIvPjwvc3ZnPg==)
![Vercel](https://img.shields.io/badge/Deploy-Vercel-black?style=flat-square&logo=vercel)
![Three.js](https://img.shields.io/badge/Three.js-r128-black?style=flat-square&logo=three.js)

---

## 🌍 Features

- **11 Global Cities** — Chennai, Mumbai, Delhi, Kolkata, Tokyo, Jakarta, Dubai, London, New York, Miami, Sydney
- **Live 3D Globe** — Rotates to face selected city, risk zone markers pulse with live data
- **24 Live IoT Sensors** — 8 flood gauges, 8 thermal sensors, 8 energy meters per city
- **Real-Time Charts** — Flood risk trend, energy demand, temperature, rainfall, basin levels
- **Live Heatmap** — Urban heat island visualization driven by actual sensor values
- **Alert Console** — Auto-fires on threshold breaches, anomaly events, satellite passes
- **Satellite Data Feed** — Simulated MODIS, Sentinel-2, Landsat-9, INSAT-3D ingestion
- **Data Pipeline View** — Kafka → Spark → ML Engine → TimescaleDB → Dashboard throughput
- **AI Analyst** — Claude-powered chat with full live sensor context injected per query

---

## 🚀 Deploy to Vercel (3 steps)

### Option A — Vercel CLI (recommended)
```bash
# 1. Clone / download this repo
git clone https://github.com/YOUR_USERNAME/climateai.git
cd climateai

# 2. Install Vercel CLI
npm install -g vercel

# 3. Deploy
vercel --prod
```

### Option B — Vercel Dashboard (drag & drop)
1. Go to [vercel.com/new](https://vercel.com/new)
2. Import your GitHub repo **OR** drag the project folder
3. Click **Deploy** — no build settings needed

### Option C — GitHub + Vercel auto-deploy
1. Push this repo to GitHub
2. Go to vercel.com → New Project → Import from GitHub
3. Select repo → Deploy (auto-detects static HTML)

---

## 🖥️ Run Locally in VS Code

```bash
# Option 1: Live Server extension (recommended)
# Install "Live Server" by Ritwick Dey in VS Code
# Right-click index.html → "Open with Live Server"

# Option 2: Python
python -m http.server 3000
# Open http://localhost:3000

# Option 3: Node http-server
npx http-server -p 3000
# Open http://localhost:3000
```

> ⚠️ **Must use a local server** — opening `index.html` directly via `file://` will block the Google Fonts and Three.js CDN loads.

---

## 📁 Project Structure

```
climateai/
├── index.html      ← Entire app (single file, ~1400 lines)
├── vercel.json     ← Vercel deployment config
└── README.md       ← This file
```

---

## 🤖 AI Analyst Setup

The AI Analyst tab uses the Anthropic Claude API. To enable it:

1. The app calls `https://api.anthropic.com/v1/messages` directly from the browser
2. For a **production** deployment, proxy this through a backend (Next.js API route, Vercel Edge Function, etc.) to protect your API key
3. For **demo/local** use, the app will show a connection error message if no key is present — all other features work without it

### Adding a backend proxy (Vercel Edge Function)
Create `/api/chat.js`:
```js
export default async function handler(req, res) {
  const response = await fetch('https://api.anthropic.com/v1/messages', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'x-api-key': process.env.ANTHROPIC_API_KEY,
      'anthropic-version': '2023-06-01'
    },
    body: JSON.stringify(req.body)
  });
  const data = await response.json();
  res.json(data);
}
```
Then in `index.html`, change the fetch URL to `/api/chat`.

---

## 🏙️ City Profiles

| City | Flood Risk | Heat Risk | Energy Base |
|------|-----------|-----------|-------------|
| Chennai 🇮🇳 | HIGH | HIGH | 1.3 GW |
| Mumbai 🇮🇳 | CRITICAL | MEDIUM | 2.1 GW |
| Delhi 🇮🇳 | MEDIUM | CRITICAL | 3.2 GW |
| Kolkata 🇮🇳 | CRITICAL | HIGH | 1.8 GW |
| Tokyo 🇯🇵 | MEDIUM | HIGH | 4.8 GW |
| Jakarta 🇮🇩 | CRITICAL | HIGH | 2.4 GW |
| Dubai 🇦🇪 | LOW | CRITICAL | 3.8 GW |
| London 🇬🇧 | MEDIUM | LOW | 2.2 GW |
| New York 🇺🇸 | HIGH | MEDIUM | 5.1 GW |
| Miami 🇺🇸 | CRITICAL | HIGH | 1.4 GW |
| Sydney 🇦🇺 | MEDIUM | HIGH | 1.8 GW |

---

## 👥 Team

| Name | Role |
|------|------|
| Varsha Rani | UI/UX · Frontend |
| Simon Paul | Full-Stack · Systems |
| Mayank Bansal | Data Science · ML |
| Nikhilesh | Strategy · Research |

---

## 🛠️ Tech Stack

- **Frontend** — Vanilla HTML/CSS/JS (zero dependencies, no build step)
- **3D Globe** — Three.js r128
- **AI** — Anthropic Claude API (claude-sonnet-4)
- **Fonts** — Google Fonts (Orbitron, JetBrains Mono, Rajdhani)
- **Deploy** — Vercel Static

---

*Built for AI-Driven Climate Adaptation — SRM Institute of Science and Technology*
