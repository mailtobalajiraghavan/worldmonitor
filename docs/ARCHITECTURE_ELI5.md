# World Monitor — Explain Like I'm 5 🧒

> Every system, tool, and technology used in World Monitor — explained so simply a five-year-old could get it. For each one: **What is it?** · **Why does World Monitor use it?** · **How does it help?**

---

## Table of Contents

1. [The Big Picture](#1-the-big-picture--what-is-world-monitor)
2. [TypeScript](#2-typescript--the-language)
3. [Vite](#3-vite--the-builder)
4. [No Framework (Vanilla)](#4-no-framework--why-no-react-or-vue)
5. [Vercel Edge Functions](#5-vercel-edge-functions--the-helpers-in-the-sky)
6. [Upstash Redis](#6-upstash-redis--the-memory-jar)
7. [Service Worker (Workbox)](#7-service-worker-workbox--the-offline-buddy)
8. [IndexedDB](#8-indexeddb--the-toy-box-in-your-browser)
9. [Tauri](#9-tauri--the-desktop-wrapper)
10. [MapLibre GL JS](#10-maplibre-gl-js--the-map)
11. [deck.gl](#11-deckgl--the-3d-map-layer)
12. [D3.js (SVG Fallback)](#12-d3js--the-backup-map)
13. [ONNX Runtime & Transformers.js](#13-onnx-runtime--transformersjs--the-brain-in-your-browser)
14. [Web Workers](#14-web-workers--the-background-helper)
15. [RSS Feeds](#15-rss-feeds--the-news-firehose)
16. [ACLED](#16-acled--the-conflict-database)
17. [UCDP](#17-ucdp--the-university-conflict-tracker)
18. [GDELT](#18-gdelt--the-everything-database)
19. [Finnhub](#19-finnhub--the-stock-ticker)
20. [Yahoo Finance](#20-yahoo-finance--the-free-stock-charts)
21. [CoinGecko](#21-coingecko--the-crypto-price-tracker)
22. [FRED](#22-fred--the-governments-data-vault)
23. [Polymarket](#23-polymarket--the-prediction-market)
24. [OpenSky Network](#24-opensky-network--the-airplane-radar)
25. [Wingbits](#25-wingbits--the-premium-airplane-radar)
26. [AIS Relay](#26-ais-relay--the-ship-tracker)
27. [NASA FIRMS](#27-nasa-firms--the-fire-spotter-from-space)
28. [USGS](#28-usgs--the-earthquake-detector)
29. [NOAA](#29-noaa--the-weather-and-climate-monitor)
30. [Groq](#30-groq--the-fast-ai-brain)
31. [OpenRouter](#31-openrouter--the-backup-ai-brain)
32. [Cloudflare Radar](#32-cloudflare-radar--who-lost-their-internet)
33. [Cyber Threat Feeds](#33-cyber-threat-feeds--the-bad-guy-watchlist)
34. [Status Pages](#34-status-pages--is-the-internet-broken)
35. [UNHCR & Humanitarian APIs](#35-unhcr--humanitarian-apis--who-needs-help)
36. [World Bank & EIA](#36-world-bank--eia--the-economy-scorecards)
37. [Hacker News & GitHub](#37-hacker-news--github--the-tech-news-feeds)
38. [The 5-Tier Caching System](#38-the-5-tier-caching-system--dont-ask-twice)
39. [Circuit Breakers](#39-circuit-breakers--the-safety-switch)
40. [The Variant System](#40-the-variant-system--three-apps-in-one)
41. [The Panel System](#41-the-panel-system--lego-blocks-for-dashboards)
42. [Signal Aggregator](#42-signal-aggregator--connecting-the-dots)
43. [Clustering & Classification](#43-clustering--classification--sorting-the-news)

---

## 1. The Big Picture — What IS World Monitor?

Imagine you have a **magical window** that shows you everything happening in the world, all at once. Earthquakes shaking. Planes flying. Ships sailing. Stock markets going up and down. Wars happening. Internet going out in countries. AI companies launching new things.

That's World Monitor.

It's a **website** (and a **desktop app**) that pulls information from **38 different sources** — like 38 different TV channels — and shows it all on one screen with a big interactive globe.

**Think of it like this:** You know how a weather app checks the weather from satellites and shows it to you? World Monitor does that, but instead of just weather, it checks **everything** — conflicts, markets, fires, earthquakes, ships, planes, cyber attacks, refugee data, tech news — and shows it all on a single dashboard with a map.

### The Simple Version of How It Works

```
📡 38 Data Sources (news, conflicts, markets, fires, planes, ships...)
    ↓
☁️ Helper servers in the cloud (one for each data source)
    ↓
💾 Memory jar (so we don't keep asking the same question)
    ↓
🌐 Your browser (where the magic happens)
    ↓
🧠 AI brain IN your browser (sorts, classifies, summarises)
    ↓
🗺️ Beautiful map + 44 dashboard panels
```

---

## 2. TypeScript — The Language

### What is it?
TypeScript is like **English with grammar rules**. Regular JavaScript is like talking to your friends — you can say whatever and they'll probably understand. TypeScript is like writing an essay — there are strict rules about what goes where.

### Why does World Monitor use it?
World Monitor handles **60+ different data types** — earthquakes, flights, stock prices, news articles, military vessels. Each one has different fields (an earthquake has a magnitude, a flight has an altitude, a stock has a price). TypeScript makes sure you never accidentally put an earthquake's magnitude where a stock's price should go.

### How does it help?
Without TypeScript, imagine having 44 panels each showing different data, and accidentally showing ship coordinates where stock prices should be. TypeScript catches these mistakes **before anyone sees them**. It's like a spell-checker, but for data.

---

## 3. Vite — The Builder

### What is it?
When you write code for a website, browsers can't read your raw files directly. You need a **builder** that packages everything up. Vite is that builder — and it's *really* fast.

### Why does World Monitor use it?
Imagine you're building a house with 500 pieces of wood. The old builders (like Webpack) would look at ALL 500 pieces every time you changed one. Vite is smarter — it only looks at the ONE piece you changed. This means when a developer makes a change, they see the result in **under a second** instead of waiting 10-30 seconds.

### How does it help?
- **Fast development:** Changes appear instantly
- **Small final product:** Vite removes any code that's not actually used (called "tree-shaking" — like shaking a tree and only keeping the fruit that falls)
- **The final bundle is ~800 KB** — that's smaller than a single photo on your phone

---

## 4. No Framework — Why No React or Vue?

### What is it?
Most websites use a "framework" — a pre-built set of tools. React (by Facebook), Vue, Angular (by Google) — these are like IKEA furniture kits. World Monitor instead builds everything from **raw wood** (vanilla TypeScript).

### Why does World Monitor use it?
This is the **biggest and most unusual decision** in the entire project. Here's why:

🏠 **Imagine you're decorating 44 rooms in a house.**

With React, every time you change ONE room, React would walk through ALL 44 rooms to check if anything else needs changing. That's called "reconciliation." With 44 panels updating at different speeds from 38 data sources, React would be constantly walking around checking rooms for no reason.

Without React, when you change Room 7, you just... change Room 7. Nobody walks anywhere else. It's faster because **you only touch what you need to touch.**

### How does it help?
1. **Speed** — No wasted work checking rooms that didn't change
2. **Size** — React alone would add ~45 KB to the download. That's 5% of the entire app just for a framework
3. **No surprises** — Some frameworks do things automatically that are hard to predict. Vanilla code does exactly what you write, nothing more
4. **The map** — The 3D globe uses WebGL (graphic card rendering). Frameworks fight with WebGL because both want to control the screen. Without a framework, there's no fight

---

## 5. Vercel Edge Functions — The Helpers in the Sky

### What is it?
Imagine you want to check the news from 38 different newspapers. Instead of calling each newspaper yourself, you have a **personal assistant** who sits between you and all the newspapers. You tell the assistant "get me the news," and the assistant calls all 38 newspapers, organizes the answers, and gives you a clean summary.

That's what Vercel Edge Functions are. They're **little helper programs** that run in the cloud.

### Why does World Monitor use it?
Three big reasons:

1. **You can't call some APIs from a browser.** Some data sources (like ACLED for conflict data) have secret API keys. If you put the key in the browser, anyone could steal it. The Edge Function holds the key safely.

2. **The helpers are EVERYWHERE.** "Edge" means they run in data centers all around the world. If you're in India, your request goes to a server in India, not California. This shaves off 50-200 milliseconds per request.

3. **No servers to maintain.** Traditional backends are like owning a restaurant — you pay rent even when no one's eating. Edge Functions are like a food truck — you only pay when someone orders.

### How does it help?
- 60+ endpoints (that's 60 different helpers for different data types)
- Secret API keys stay hidden
- Runs close to the user = faster
- Costs $0/month on the free tier

---

## 6. Upstash Redis — The Memory Jar

### What is it?
Imagine you ask your mom "What's for dinner?" and she says "Pasta." If you ask again 5 minutes later, she shouldn't have to go check the kitchen again — she already knows. She **remembers** the answer.

Redis is a **super-fast memory**. It remembers answers to questions so you don't have to ask the original source again.

"Upstash" is a specific company that runs Redis in a way that works with serverless helpers (Edge Functions). Normal Redis needs a permanent phone connection. Upstash Redis works with quick text messages (REST API) — which is the only way serverless helpers can communicate.

### Why does World Monitor use it?
World Monitor checks 38 data sources, some every 15 seconds. Without a memory jar:
- The ACLED conflict API would be called thousands of times a day (they'd block us)
- Users would wait 2-5 seconds for every panel to load
- API rate limits (rules about how often you can ask) would be hit immediately

### How does it help?
- **First user asks** → takes 2 seconds to get earthquake data from USGS
- **Next 100 users ask within 5 minutes** → takes 50 milliseconds (instant) because it's in the memory jar
- Saves money (fewer API calls = free tier lasts longer)
- Prevents getting blocked by data sources

---

## 7. Service Worker (Workbox) — The Offline Buddy

### What is it?
A Service Worker is like a **little librarian** that lives in your browser. When you visit a website, the librarian makes copies of important files. Later, if the internet goes out, the librarian can show you the copies instead.

**Workbox** is a toolkit by Google that makes building this librarian easier.

### Why does World Monitor use it?
Two reasons:

1. **Offline support.** The desktop app (Tauri) should work even without internet. The librarian serves the last-known data when offline.

2. **Speed.** If you visited World Monitor 5 minutes ago, the librarian already has the page's code. It loads from your hard drive (instant) instead of downloading it again.

### How does it help?
- App loads faster on repeat visits
- Works offline on desktop (shows last-known data)
- Reduces network requests (saves bandwidth, especially on mobile)

---

## 8. IndexedDB — The Toy Box in Your Browser

### What is it?
Every browser has a hidden storage space called IndexedDB. Think of it like a **toy box** under your bed — you can put things in and take them out, and they stay there even if you close your bedroom door (refresh the page) or turn off the lights (close the browser).

Unlike cookies (tiny, text-only), IndexedDB can store **megabytes** of structured data.

### Why does World Monitor use it?
World Monitor stores two important things:

1. **Baselines** — "What's normal?" If flights over Eastern Europe are usually 200/day, and today there are 800, that's a spike. To know it's a spike, you need to remember what "normal" looks like. That's stored in IndexedDB.

2. **Snapshots** — Every so often, the app takes a "photo" of the entire dashboard state. This allows **time-travel playback** — slide a timeline back and see what the world looked like 6 hours ago.

### How does it help?
- Anomaly detection: "This is 3x higher than normal!" (z-score > 2.5 = spike)
- Time travel: Replay past dashboard states
- Survives refresh — your baselines don't reset when you reload the page
- 7-day retention for snapshots

---

## 9. Tauri — The Desktop Wrapper

### What is it?
Tauri takes a website and wraps it into a **desktop application** — like putting a picture in a frame. You can double-click it on your computer just like Word or Chrome.

You might have heard of Electron (what VS Code, Slack, and Discord use). Tauri is similar but **much smaller** — a Tauri app is 5-10x smaller than an Electron app because it uses your computer's built-in browser engine instead of bundling its own copy of Chrome.

### Why does World Monitor use it?
1. **Smaller download.** Nobody wants to download a 200 MB app for a dashboard. Tauri keeps it under 20 MB.

2. **OS Keychain.** Your computer has a **secret vault** (Keychain on Mac, Credential Manager on Windows). Tauri can store API keys there instead of in a config file that anyone could read.

3. **Node.js Sidecar.** Tauri can run a small helper server on your machine (port 46123). This means the app can work completely offline because the caching layer runs locally instead of in the cloud.

### How does it help?
- Desktop app for Windows, Mac, Linux
- API keys stored in your OS's built-in vault (not hackable text files)
- Fully offline mode with local caching
- 5-10x smaller than Electron

---

## 10. MapLibre GL JS — The Map

### What is it?
MapLibre is an **interactive map library** — like Google Maps, but free and open-source. It draws maps using vector tiles (mathematical descriptions of roads, borders, and water) instead of image tiles (pre-drawn pictures). This makes it crisp at any zoom level.

"GL" means it uses your **graphics card** (GPU) to draw — the same hardware that runs video games. This makes it buttery smooth even with thousands of data points.

### Why does World Monitor use it?
Google Maps costs money at scale. MapLibre is free. Period. But it's also:
- Extremely customizable (World Monitor uses a dark theme map)
- Supports region highlighting, click events, popups
- Handles vector tiles efficiently

### How does it help?
- Free forever (no per-request billing like Google Maps)
- Smooth panning and zooming on the dark-themed globe
- Foundation layer that everything else draws on top of

---

## 11. deck.gl — The 3D Map Layer

### What is it?
If MapLibre is the **paper map**, deck.gl is what lets you **stack holographic layers on top**. It draws thousands of points, arcs, heatmaps, and 3D hexagons using your GPU (graphics card).

Made by Uber for visualizing millions of trip data points, it's designed for exactly this use case: lots of data points on a map.

### Why does World Monitor use it?
World Monitor needs to show:
- 200+ military flights as moving dots
- 1000+ ship positions with wake trails
- Fire hotspots as heat blobs
- Cable routes as glowing lines
- Conflict zones as pulsing polygons

Drawing all of these with regular HTML/SVG would crash the browser. deck.gl draws them all on the GPU at 60 frames per second.

### How does it help?
- 35+ data layers simultaneously without lag
- 3D globe with rotating perspective
- GPU-accelerated = smooth even with thousands of points
- Supports hover/click interactions on every single point

---

## 12. D3.js — The Backup Map

### What is it?
D3 is a **drawing library** for the web. Unlike deck.gl (which uses the GPU), D3 draws using SVG — which is like using a pencil and paper instead of a 3D printer.

### Why does World Monitor use it?
Not everyone has a powerful computer. If your GPU can't handle deck.gl (old laptops, some tablets, most phones), the app falls back to D3's simpler SVG map. It's not as pretty, but it **works everywhere**.

```
If (your device has a good GPU) → use deck.gl (3D, beautiful)
If (no GPU or mobile) → use D3 (flat, simpler, but works)
```

### How does it help?
- **Nobody gets a broken app.** Even an old phone gets a working map.
- Graceful degradation — the experience degrades, but it never crashes

---

## 13. ONNX Runtime & Transformers.js — The Brain in Your Browser

### What is it?
These are **AI/ML engines that run inside your browser** — no cloud server needed.

**ONNX Runtime:** A universal format for AI models. Think of it like MP3 for music — any player can play it. ONNX runs AI models on any device.

**Transformers.js:** Hugging Face's library that brings AI models (the same ones that power ChatGPT-like tools) directly into your browser using WebAssembly and WebGL.

### Why does World Monitor use it?
World Monitor needs AI for:
- **Summarizing** dozens of news articles into one-paragraph summaries
- **Classifying** events by threat level (critical, high, medium, low, info)
- **Extracting** entity names (countries, companies, commodities) from text
- **Computing embeddings** (turning text into numbers) for smart clustering

Normally you'd pay a cloud AI service for this. By running it IN the browser:

1. **Costs $0** — no cloud GPU bills
2. **Works offline** — the desktop app can summarize news without internet
3. **Privacy** — your data never leaves your computer

### How does it help?
- Free AI features (cloud ML would cost hundreds per month at this scale)
- Offline intelligence pipeline
- This is the **third fallback** in the AI chain: Groq → OpenRouter → Browser ML

---

## 14. Web Workers — The Background Helper

### What is it?
Your browser normally runs everything on a **single thread** — like having one person doing all the cooking, cleaning, and shopping. A Web Worker is like **hiring a second person** who works in the background.

### Why does World Monitor use it?
The ML models (from section 13) are computationally heavy. If they ran on the main thread, the map would freeze and buttons wouldn't respond while the AI is thinking. By putting ML in a Web Worker, the AI "thinks" in the background while the UI stays smooth.

### How does it help?
- **No UI freezing** — the map still spins, panels still update, you can still click things while AI is analyzing 200 news articles
- Clean separation — ML code is isolated, can't crash the main app

---

## 15. RSS Feeds — The News Firehose

### What is it?
RSS is a **really old internet standard** (from 1999!) that lets websites publish their articles in a machine-readable list. Instead of visiting 150 different news websites, your app can just check their RSS feeds — like having 150 newspapers delivered to your door every morning.

### Why does World Monitor use it?
World Monitor monitors **~150 news domains** — AP, Reuters, AFP, BBC, Al Jazeera, defense publications, tech media, OSINT blogs, financial outlets, and more. RSS is:
- **Free** — no API key needed
- **Universal** — almost every news site has one
- **Standardized** — same format everywhere

### How does it help?
- One endpoint (`/api/rss-proxy`) fetches any feed
- Per-feed circuit breaker (if one feed breaks, the other 149 keep working)
- 5-minute cache per feed
- The clustering system groups headlines from different sources about the same story

---

## 16. ACLED — The Conflict Database

### What is it?
ACLED (Armed Conflict Location & Event Data) is the world's most **comprehensive conflict database**. A team of researchers manually reviews news reports and codes every battle, protest, riot, and act of violence against civilians — with exact dates and GPS coordinates.

### Why does World Monitor use it?
If you want to know "Where are conflicts happening right now?", ACLED is the **gold standard**. No other source has the same combination of:
- Global coverage (every country)
- Event-level granularity (not just "there's a war in Syria" but "a battle occurred at 36.2°N, 37.1°E on March 5")
- Rigorous validation (human researchers verify each event)

### How does it help?
- Powers the conflict panels showing battles, riots, protests
- Provides data for the signal aggregator (correlating conflicts with other events)
- GPS coordinates are plotted directly on the map as colored markers
- **Severity: 🔴 HIGH** — if ACLED goes down, conflict panels are blank

---

## 17. UCDP — The University Conflict Tracker

### What is it?
UCDP (Uppsala Conflict Data Program) is run by a Swedish university. Like ACLED, it tracks conflicts, but with a **more academic approach** — longer historical depth, strict definitions of "armed conflict" (25+ battle deaths per year).

### Why does World Monitor use it?
ACLED and UCDP complement each other:
- **ACLED:** More recent data, more event types, faster updates
- **UCDP:** Longer history, stricter definitions, state-based vs non-state categorization

Using both means World Monitor gets both **speed** (ACLED) and **depth** (UCDP).

### How does it help?
- Feeds the UCDP Events Panel with historical conflict data
- 24-hour cache (data updates slowly — it's academic research, not breaking news)
- If ACLED goes down, UCDP still provides partial conflict coverage

---

## 18. GDELT — The Everything Database

### What is it?
GDELT (Global Database of Events, Language, and Tone) is the **world's largest open database of human events**. It processes news from virtually every country in 65+ languages, every 15 minutes. It doesn't just track articles — it extracts events, people, organizations, themes, and emotional tone.

### Why does World Monitor use it?
Two specific APIs:
- **DOC 2.0:** Full-text search across global news. "Show me everything about Taiwan in the last 24 hours."
- **GEO 2.0:** Geographic heatmaps. "Where in the world are the most articles about 'military' right now?"

GDELT is the only free source that provides this kind of **global, real-time, geographic news intelligence**.

### How does it help?
- Powers the GDELT Intelligence Panel (real-time global news analysis)
- Geographic heatmaps layered on the globe
- Free, no API key needed
- Updates every 15 minutes

---

## 19. Finnhub — The Stock Ticker

### What is it?
Finnhub provides **real-time stock market data** — prices, changes, company info, ETF data. It has a free tier with an API key.

### Why does World Monitor use it?
It's the **only reliable free stock API** with decent rate limits (60 requests/minute). Alternatives like Alpha Vantage have much stricter limits (5/minute).

### How does it help?
- Powers the Market Panel with live stock quotes
- Feeds into ETF Flows panel
- Part of the Macro Signals composite (stock trends = one signal)
- CDN-cached for 60 seconds (stocks don't need sub-second updates for a dashboard)

---

## 20. Yahoo Finance — The Free Stock Charts

### What is it?
Yahoo Finance has an **undocumented, unofficial** API endpoint that returns chart/sparkline data for any stock or index. It's not an official API — Yahoo doesn't advertise it — but it works.

### Why does World Monitor use it?
It's the **only free source** for intraday OHLCV (Open, High, Low, Close, Volume) data for international stock indices. Finnhub covers US stocks well, but for the Nikkei, DAX, FTSE, and 42 other country indices, Yahoo is the only free option.

### How does it help?
- 42 country stock indices on a single panel
- Sparkline mini-charts showing price trends
- **Risk:** Could break any time since it's unofficial (World Monitor caches aggressively as insurance)

---

## 21. CoinGecko — The Crypto Price Tracker

### What is it?
CoinGecko is a **free crypto market data provider**. It covers thousands of cryptocurrencies with prices, market caps, volume, and sparkline data.

### Why does World Monitor use it?
It's free and comprehensive. The main alternatives (CoinMarketCap) require paid API access for the same features.

### How does it help?
- Powers the Crypto Panel
- Feeds into Stablecoin Panel (tracking USDT/USDC peg deviations)
- Part of the Macro Signals composite (crypto market cap = one signal)
- Rate limits fluctuate (10-30/min) so aggressive caching is essential

---

## 22. FRED — The Government's Data Vault

### What is it?
FRED (Federal Reserve Economic Data) is the US Federal Reserve's **public data warehouse**. It has 800,000+ data series — treasury yields, unemployment rates, CPI, GDP, interest rates, and basically every economic number the government tracks.

### Why does World Monitor use it?
For macro-economic indicators, FRED is the **primary authoritative source**. When World Monitor shows "10-Year Treasury Yield: 4.25%", that number comes directly from the Federal Reserve.

### How does it help?
- Powers the Economic Indicators panel
- Key input for the Macro Signals composite (treasury yields, fed funds rate)
- 1-hour cache (economic data updates on the Fed's schedule, not in real-time)

---

## 23. Polymarket — The Prediction Market

### What is it?
Polymarket is a **prediction market** where people bet real money on future events. "Will there be a ceasefire in Ukraine by June?" — if the market price is $0.30, that roughly means a 30% probability.

### Why does World Monitor use it?
Prediction markets are remarkably good at **aggregating crowd knowledge**. When thousands of people put money on the line, the resulting probabilities tend to be more accurate than expert polls. It's like asking "what does the crowd think will happen?"

### How does it help?
- Powers the Predictions Panel showing live market odds
- Filtered for geopolitical and election-related markets
- Free public API, no key needed

---

## 24. OpenSky Network — The Airplane Radar

### What is it?
OpenSky is a **volunteer-run network** of ADS-B receivers around the world. Every commercial and military aircraft broadcasts its position via ADS-B (Automatic Dependent Surveillance-Broadcast). OpenSky collects these signals and makes them available via API.

### Why does World Monitor use it?
It's the **only free source** for real-time global flight data. World Monitor uses it specifically to track **military aircraft** — fighters, bombers, tankers, AWACS — by matching callsign patterns against a known-patterns database.

### How does it help?
- Military flights plotted on the map in real-time
- Feeds into Theater Posture Analysis ("activity in EUCOM theater: ELEVATED")
- Part of the Signal Aggregator (military flights near a conflict zone = higher convergence score)
- CDN-cached for just 15 seconds (flight positions change rapidly)

---

## 25. Wingbits — The Premium Airplane Radar

### What is it?
Wingbits is a **commercial ADS-B data provider** with higher-fidelity coverage in specific regions where OpenSky has gaps.

### Why does World Monitor use it?
OpenSky's free tier has tight limits (100 requests/day anonymously) and coverage gaps. Wingbits fills those gaps with **premium data**.

### How does it help?
- Higher fidelity in some regions (better military aircraft identification)
- **This is one of only 2 paid APIs** in the entire system
- Optional — the app works without it, just with slightly less complete flight data

---

## 26. AIS Relay — The Ship Tracker

### What is it?
Every large ship broadcasts its position via AIS (Automatic Identification System) — like an airplane's ADS-B but for ships. A "relay" is a custom-hosted server that listens to these signals and forwards them.

### Why does World Monitor use it?
Ship tracking is critical for monitoring:
- Military vessels (aircraft carriers, destroyers, submarines when they surface)
- Ships going "dark" (turning off AIS near sensitive areas — very suspicious)
- Chokepoint traffic (Strait of Hormuz, Suez Canal, Malacca Strait)

### How does it help?
- Maritime tracking layer on the map
- Vessel positions updated every 4-8 seconds
- Detects "dark" ships (AIS gap detection)
- **Severity: 🔴 HIGH** — if it goes down, the entire maritime layer disappears

---

## 27. NASA FIRMS — The Fire Spotter from Space

### What is it?
NASA's Fire Information for Resource Management System uses **satellites** (MODIS and VIIRS instruments) to detect fires anywhere on Earth. Every time a satellite passes over a fire, it records the location, brightness, and intensity.

### Why does World Monitor use it?
Satellite fire detection enables a type of intelligence that's otherwise impossible:
- Detect wildfires in remote areas with no news coverage
- Spot artillery/bombing fires in conflict zones (fires in Syrian desert = possible airstrike)
- Correlate fires with other signals (fires + military flights + internet outage = something is happening)

### How does it help?
- Satellite Fires Panel showing global hotspots
- Fires plotted as heat blobs on the map
- Part of the Signal Aggregator (fires in conflict zones raise the convergence score)
- CSV format parsed server-side into structured data

---

## 28. USGS — The Earthquake Detector

### What is it?
The US Geological Survey runs a **global seismograph network** that detects earthquakes. Their GeoJSON feed provides real-time data on earthquakes above magnitude 4.5 anywhere in the world.

### Why does World Monitor use it?
1. It's the most reliable earthquake data source in the world
2. It's completely free, no API key needed
3. Data is already in GeoJSON format (perfect for mapping)
4. USGS regenerates the feed every 5 minutes

### How does it help?
- Earthquake markers on the map (color-coded by magnitude)
- Population exposure analysis ("500,000 people live within 50km of this quake")
- Used alongside WorldPop data to calculate human impact

---

## 29. NOAA — The Weather and Climate Monitor

### What is it?
NOAA (National Oceanic and Atmospheric Administration) tracks **global climate patterns** — temperature anomalies, precipitation changes, extreme weather trends.

### Why does World Monitor use it?
Climate data is a slow-moving but critical signal. When a region's temperature anomaly is +5°C above baseline, that's a drought indicator. Combined with conflict data, it can predict instability (drought → food scarcity → unrest).

### How does it help?
- Climate Anomaly Panel showing 15 global zones
- Temperature and precipitation deviation from baselines
- 6-hour cache (climate data is monthly resolution, not hourly)

---

## 30. Groq — The Fast AI Brain

### What is it?
Groq is an AI inference company that built custom hardware (LPU — Language Processing Unit) specifically to run language models. It's **dramatically faster** than GPU-based inference — responses in 100-500ms instead of 2-5 seconds.

### Why does World Monitor use it?
Groq is the **primary AI engine** for:
- Summarizing news articles (turn 2000-word articles into 2-sentence summaries)
- Classifying events by threat level (is this news critical, high, medium, or low priority?)
- Generating country intelligence briefs ("What's happening in Iran right now?")

It uses an OpenAI-compatible API, so switching between models is easy.

### How does it help?
- Ultra-fast summaries (100ms vs 5 seconds on other providers)
- Free tier available
- If it goes down → falls back to OpenRouter → then to browser-based ML
- **It's the first stop in a 3-tier AI fallback chain**

---

## 31. OpenRouter — The Backup AI Brain

### What is it?
OpenRouter is an **AI aggregator** — it routes your request to whichever AI model you choose from dozens of providers (Mistral, Meta, Google, Anthropic). Some models are free.

### Why does World Monitor use it?
It's the **backup plan** for when Groq hits rate limits. OpenRouter provides access to free-tier models like `mistral-7b-instruct:free`. It's slower than Groq but still cloud-based (unlike browser ML).

### How does it help?
- Second fallback in the AI chain (Groq → **OpenRouter** → Browser ML)
- Access to free models from multiple providers
- Shared cache key with Groq summaries — if Groq already summarized something, OpenRouter doesn't redo it (and vice versa)

---

## 32. Cloudflare Radar — Who Lost Their Internet?

### What is it?
Cloudflare handles ~20% of all internet traffic. Their Radar product monitors internet health globally — detected outages, cable cuts, government shutdowns.

### Why does World Monitor use it?
When a country's internet goes dark, that's a **massive intelligence signal**:
- Government-ordered shutdowns (censorship, coup, unrest)
- Submarine cable cuts (undersea warfare or accident)
- Infrastructure failure (cyberattack, natural disaster)

Cloudflare is the most authoritative source for this because they literally see the internet traffic disappear.

### How does it help?
- Internet Outage layer on the map
- Part of the Signal Aggregator (outage + protests + military = high convergence)
- **Requires enterprise API token** — optional enhancement
- Without it, the app misses internet outages (but everything else works fine)

---

## 33. Cyber Threat Feeds — The Bad Guy Watchlist

### What is it?
Five separate sources that track malicious activity on the internet:

| Feed | What It Tracks |
|---|---|
| **Feodo Tracker** | Command & Control (C2) servers used by botnets |
| **URLhaus** | URLs distributing malware |
| **C2IntelFeeds** | Community-reported malicious IPs |
| **AlienVault OTX** | Indicators of Compromise (IoCs) from security researchers |
| **AbuseIPDB** | IP reputation scores (how evil is this IP?) |

### Why does World Monitor use it?
By aggregating five independent threat feeds, World Monitor builds a more complete picture of the **cyber threat landscape** than any single source provides. Each source catches things the others miss.

### How does it help?
- All five sources merged into a single `/api/cyber-threats` endpoint
- Each threat IP is geolocated and plotted on the map
- **Every source is independently optional** — if one feed goes down, the other four keep working
- Severity: ⚪ Minimal for each individual feed (one missing is barely noticeable)

---

## 34. Status Pages — Is the Internet Broken?

### What is it?
Major internet services (AWS, GitHub, Cloudflare, Stripe, etc.) publish their operational status on public status pages (usually `status.service.com`). World Monitor checks **33 of these** automatically.

### Why does World Monitor use it?
When AWS goes down, half the internet goes down. When Cloudflare goes down, 20% of websites stop working. Knowing which services are degraded is critical intelligence for the tech variant.

### How does it help?
- Service Status Panel showing 33 major services at a glance
- Checks every 60 seconds
- Individual circuit breaker per service (one broken status page doesn't block the others)
- Services monitored: AWS, Azure, GCP, GitHub, Cloudflare, Stripe, Vercel, Datadog, PagerDuty, Twilio, Heroku, Atlassian, npm, PyPI, OpenAI, Anthropic...

---

## 35. UNHCR & Humanitarian APIs — Who Needs Help?

### What is it?
Three sources for humanitarian data:

| Source | What It Provides |
|---|---|
| **UNHCR** | Refugee and displaced population counts by country/year |
| **HDX HAPI** | OCHA's Humanitarian Data Exchange — food security, operational presence |
| **WorldPop** | Population density estimates for any location |

### Why does World Monitor use it?
The humanitarian angle answers questions like:
- "How many refugees has this conflict produced?"
- "How many people live within 50km of this earthquake?"
- "Which countries have the highest food insecurity right now?"

### How does it help?
- Displacement Panel (refugee flows visualized)
- Population Exposure Panel ("earthquake hit 50km from 2.3 million people")
- Long cache TTLs (24h for UNHCR, 7 days for WorldPop) because this data changes slowly

---

## 36. World Bank & EIA — The Economy Scorecards

### What is it?
- **World Bank:** Development indicators for every country (GDP, population, poverty rates)
- **EIA:** US Energy Information Administration (petroleum, natural gas, electricity production/consumption)

### Why does World Monitor use it?
Economic context matters:
- GDP per capita helps assess a country's resilience to shocks
- Energy data shows supply chain vulnerabilities (oil production drops = price spikes)

### How does it help?
- Economic data enriches country intelligence briefs
- Energy data feeds into commodities analysis
- 24-hour cache for World Bank, CDN cache for EIA

---

## 37. Hacker News & GitHub — The Tech News Feeds

### What is it?
- **Hacker News:** Y Combinator's tech news forum (the front page of the tech world)
- **GitHub:** Trending repositories show what developers are building right now

### Why does World Monitor use it?
For the **tech variant**, these are equivalent to what ACLED is for the full variant — the primary sources showing "what's happening right now in tech."

### How does it help?
- Hacker News powers the tech news feed panel
- GitHub trending shows emerging tools, frameworks, AI models
- GitHub falls back from API to HTML scraping if the token is missing (or rate limited at 60 requests/hour)

---

## 38. The 5-Tier Caching System — Don't Ask Twice

### What is it?
Remember the memory jar (Redis)? World Monitor actually has **FIVE** memory jars stacked on top of each other, each for a different purpose:

```
You ask for earthquake data:
  ↓
Tier 5: Persistent cache (Tauri disk / localStorage)
  → "I saved this yesterday. Here." ← Last resort, possibly stale
  ↓ miss
Tier 4: IndexedDB (baselines + snapshots)
  → "I have yesterday's baseline for comparison."
  ↓ miss
Tier 3: Service Worker (Workbox)
  → "I cached this 2 minutes ago. Here!" ← Fastest (on-device)
  ↓ miss
Tier 2: CDN (Vercel CDN)
  → "Someone else asked 30 seconds ago. Here." ← Shared across all users
  ↓ miss
Tier 1: Redis (Upstash)
  → "The API response from 5 minutes ago. Here." ← Server-side
  ↓ miss
Origin: Actually call the USGS earthquake API
```

### Why does World Monitor use it?
With 38 data sources polled at different intervals, without aggressive caching:
- API rate limits would be exceeded in minutes
- Every panel would take 2-5 seconds to load
- The app would be slow, expensive, and fragile

### How does it help?
- Most requests NEVER reach the original API (cache hit rate > 90%)
- Sub-100ms response times for cached data
- Offline support (Tier 3-5 work without internet)
- Rate limit protection (even if thousands of users are active)

---

## 39. Circuit Breakers — The Safety Switch

### What is it?
In your house, if there's an electrical overload, a circuit breaker **trips** to prevent a fire. Instead of everything blowing up, the one affected circuit shuts off and the rest of the house keeps working.

World Monitor has the same concept for API calls.

### Why does World Monitor use it?
If GDELT suddenly starts returning errors, without a circuit breaker:
1. Every request would wait 30 seconds, then fail
2. The retry logic would keep trying, wasting resources
3. The entire app would slow down waiting for GDELT

With a circuit breaker:
1. After 3 failures, the circuit "opens" (stops trying)
2. The panel shows "temporarily unavailable"
3. After 5 minutes, it tries ONE request. If it works, the circuit "closes" (normal operation resumes)

### How does it help?
- **One broken API can't crash the whole app**
- Each RSS feed has its own circuit breaker
- 5-minute cooldown before retrying
- The other 37 data sources keep working while one is down

---

## 40. The Variant System — Three Apps in One

### What is it?
World Monitor is actually **THREE different products** built from the same code:

| Variant | URL | Focus |
|---|---|---|
| **Full** | worldmonitor.app | Everything: conflicts, military, OSINT, markets |
| **Tech** | tech.worldmonitor.app | AI, startups, cybersecurity, developer tools |
| **Finance** | finance.worldmonitor.app | Markets, trading, central banks, macro indices |

### Why does World Monitor use it?
Building three separate apps would mean maintaining three copies of the same code. Since 80% of the functionality is shared (maps, caching, panels, news), the author built ONE codebase with a variant switch:

```
"What variant am I?"
  → Check localStorage (can switch at runtime)
  → Check VITE_VARIANT env var (set at deploy time)
  → Default to 'full'
```

### How does it help?
- One codebase, three products
- At build time, Vite **tree-shakes** unused variant code (the tech variant doesn't ship finance panel code)
- Users can switch variants from settings without redeploying

---

## 41. The Panel System — LEGO Blocks for Dashboards

### What is it?
Each panel is like a **LEGO block**. The base class (`Panel.ts`, 420 lines) provides the frame (header, collapse button, loading spinner, error state, count badge), and each specific panel fills in the content.

Think of it like a picture frame — the frame is the same for all panels, but the picture inside is different.

### Why does World Monitor use it?
With 44 panels, you don't want to rebuild the header, loading state, error state, and collapse button 44 times. The author centralised all of this into one `Panel` base class, so each specific panel only needs to define "what goes inside."

### How does it help?
- **Consistency:** All 44 panels look and behave the same way
- **Drag and reorder:** Users can rearrange panels like moving apps on a phone
- **Toggle on/off:** Each panel can be hidden from settings
- **Persistent:** Your layout and preferences survive page refresh
- **New panels are easy:** Creating a new panel is just extending the base class and filling the content

---

## 42. Signal Aggregator — Connecting the Dots

### What is it?
The Signal Aggregator is like a **detective** that watches 7 different clue streams and says "Hey, these clues all point to the same country — something might be going on there."

The 7 signal types:
1. 🌐 Internet outages
2. ✈️ Military flights
3. 🚢 Military vessels
4. ✊ Protests
5. 📡 AIS disruptions (ships going dark)
6. 🔥 Satellite fires
7. 📊 Temporal anomalies (something 3x higher than normal)

### Why does World Monitor use it?
**No single signal means much on its own.** Military flights happen every day. Protests happen every day. Fires happen every day. But when you see military flights AND internet outage AND protests AND satellite fires in the **same country, on the same day** — that's a strong signal that something significant is happening.

This is called **multi-signal convergence**, and it's the core intelligence concept of World Monitor.

### How does it help?
- Calculates a **convergence score** per country
- Monitors 6 regions: Middle East, East Asia, South Asia, Eastern Europe, North Africa, Sahel
- High convergence scores drive the AI Insights panel (the AI writes a brief explaining what's happening)
- This is what turns World Monitor from "38 separate data feeds" into an actual **intelligence platform**

---

## 43. Clustering & Classification — Sorting the News

### What is it?
When 150 news sources all report the same story, you don't want 150 separate items. **Clustering** groups similar headlines together. **Classification** assigns a threat level.

### Why does World Monitor use it?

**Clustering works in two stages:**

1. **Jaccard similarity** (fast, always available):
   - Takes the words from each headline
   - Compares them: "How many words do these two headlines share?"
   - If they share enough words (> threshold), they're the same story
   - Example: "Russia fires missiles at Ukraine" and "Ukraine hit by Russian missile attack" → same cluster

2. **Semantic clustering** (smarter, needs ML):
   - Takes the Jaccard clusters and computes "meaning embeddings"
   - Two headlines might use completely different words but mean the same thing
   - Merges clusters whose meanings are > 75% similar
   - Only activates when 5+ initial clusters exist (not worth the compute for fewer)

**Classification assigns threat levels:**
- 🔴 Critical — mass casualty event, nuclear incident, major cyberattack
- 🟠 High — military escalation, significant conflict, major infrastructure failure
- 🟡 Medium — notable political event, moderate unrest, financial disruption
- 🟢 Low — routine political news, minor incidents
- ℹ️ Info — general news, no threat implication

### How does it help?
- 150 articles about the same story become ONE cluster with a "from 47 sources" badge
- Each cluster gets a threat level so the most important stories float to the top
- The velocity metric shows if a story is "rising" (more sources per hour = breaking news)

---

## Summary — The Whole System in One Picture

```
🌍 THE WORLD (conflicts, markets, fires, ships, planes, weather, cyber...)
     ↓
📡 38 DATA SOURCES (ACLED, OpenSky, USGS, Finnhub, RSS, NASA, Groq, ...)
     ↓
☁️  60+ EDGE FUNCTIONS (proxy, normalize, cache, rate-limit)
     ↓
💾 5-TIER CACHE (Redis → CDN → Service Worker → IndexedDB → Disk)
     ↓
🌐 BROWSER (TypeScript SPA, no framework, class-based components)
     ↓
🧮 PROCESSING (cluster → classify → entity-extract → score)
     ↓
🧠 AI (Groq → OpenRouter → Browser Transformers.js)
     ↓
🗺️ DISPLAY (deck.gl 3D globe + 44 configurable panels)
     ↓
👤 USER (sees the world, all at once)
```

Every system in this document exists because it solves a **specific problem**. Nothing is here "just because." The author built a dashboard that tracks the entire world in real-time, for $0/month in API costs, that works offline, runs AI locally in your browser, and degrades gracefully when any of its 38 data sources goes down.

> **Part 1 stats:** ~7,200 words · 43 systems explained · ELI5 format.

---

# Part 2 — Deep Dives Into the Internals 🔬

Now that you know WHAT each system is, let's look at HOW they work together under the hood — still explained like you're five.

---

## 44. How Data Models Work — The Shape of Everything

### What is it?
Every piece of data in World Monitor has a **shape** — a definition that says "an earthquake must have a magnitude, a location, and a time." In code, these shapes are called **interfaces** (TypeScript) or **types**.

Imagine a **cookie cutter** — the cutter defines the shape, and every cookie (data item) must fit that shape. There are 60+ cookie cutters in World Monitor.

### Why does it matter?
Without shapes, you'd have chaos. Imagine a pile of 10,000 data items — some are earthquakes, some are stock prices, some are news articles. If they didn't have defined shapes, the app couldn't tell them apart. It would try to plot a stock price on the map (stock prices don't have lat/lon!) and crash.

### The major shape families:

**News family:**
```
NewsItem → gets clustered into → ClusteredEvent → gets scored with → VelocityMetrics
```
A news item is a single article. Multiple articles about the same story become a cluster. The cluster gets a velocity score ("is this story growing or dying?").

**Military family:**
```
MilitaryFlight (fighters, bombers, AWACS, drones)
MilitaryVessel (carriers, destroyers, submarines)
ConflictZone (active battle areas with polygon boundaries)
```

**Infrastructure family:**
```
UnderseaCable (fiber optic cables under the ocean)
Pipeline (oil and gas pipelines)
InternetOutage (countries or regions losing internet)
NuclearFacility (power plants, research reactors)
```

**Market family:**
```
MarketData (symbol, price, change, sparkline)
GulfInvestment (sovereign wealth fund investments)
```

**Signal family:**
```
GeoSignal → grouped into → CountrySignalCluster → rolled up into → RegionalConvergence → summarized as → SignalSummary
```

### The lifecycle of a data item:
```
🌐 External API returns raw JSON
  ↓
☁️ Edge Function normalizes it into the correct shape
  ↓
💾 Cache stores the shaped data
  ↓
🌐 Browser receives it and validates the shape
  ↓
🧮 Processing enriches it (add threat level, entity tags, velocity)
  ↓
🗺️ Display renders it in the correct panel and/or map layer
```

---

## 45. Anatomy of an Edge Function — What Happens in Those 60+ Files

### What is it?
Each file in the `api/` directory is a standalone Edge Function. Think of each one as a **translator** sitting in the cloud between you and a data source.

### A typical Edge Function does these 7 steps:

```
1. 🚦 CORS check — "Are you allowed to ask me?"
2. 🏎️ Rate limit — "Have you asked too many times?"
3. 💾 Cache check — "Do I already know the answer?"
4. 🔑 Auth — "Let me add the API key you don't have"
5. 📡 Fetch — Actually call the external API
6. 🔄 Transform — Convert the response into a clean shape
7. 💾 Cache save — Remember this answer for next time
```

**Step 1 (CORS):** The browser says "I'm from worldmonitor.app." The Edge Function checks: "Is that on my list of allowed domains?" If not, it rejects the request. This stops random websites from stealing our API endpoints.

**Step 3 (Cache check):** Before calling the external API, the function asks Redis: "Do you have a recent answer for this?" If Redis says yes, the function returns it immediately. The external API is never even contacted. This is why most requests take 50ms instead of 2 seconds.

**Step 4 (Auth):** The ACLED API requires an API key and email. The browser doesn't have these (exposing them would be a security hole). The Edge Function has them as environment variables and adds them to the request.

**Step 6 (Transform):** Some APIs return messy data. Yahoo Finance returns nested XML with inconsistent field names. NOAA returns CSV files. The Edge Function cleans this up into a consistent JSON shape that the browser can trust.

### What "edge" actually means:
Regular servers run in ONE location (say, Virginia). If you're in Tokyo, your request travels to Virginia and back — 200ms round trip. Edge Functions run in **300+ locations worldwide**. If you're in Tokyo, the function runs in Tokyo. The data still needs to come from the external API, but the function itself is right next to you.

---

## 46. The Panel Lifecycle — Birth, Life, and Death of a Panel

### What is it?
Every panel goes through a **lifecycle** — it's created, it shows loading, it gets data, it updates, and (if the user hides it) it's destroyed. Understanding this lifecycle is key to understanding how World Monitor works.

### The lifecycle in 8 steps:

**1. Birth (Construction)**
When the app starts, it reads the variant config: "Full variant = 37 panels." For each panel, it calls `new ConflictPanel()` or `new MarketPanel()` etc. The constructor creates the DOM elements (the actual HTML on screen).

**2. Registration**
The panel registers itself with `App.ts`: "Hi, I'm the earthquake panel. My ID is `earthquakes`. I need data from `/api/earthquakes`."

**3. Grid Placement**
The panel is placed into the CSS grid. Its position comes from: (a) saved order in localStorage, or (b) default order from the variant config. `live-news` is always first. `monitors` is always last.

**4. Loading State**
`showLoading()` replaces the panel content with a spinner. The user sees a panel-shaped box with a spinning circle.

**5. Data Fetch**
`loadAllData()` fires ALL panel data requests in parallel. Not one-by-one — all 37 at once. Each panel's data comes back at its own speed (earthquakes in 200ms, ACLED in 500ms, AI summary in 2 seconds).

**6. Display**
When data arrives, the panel calls its own `render()` or `update()` method. Earthquakes show a sorted list with magnitude colors. Markets show price tickers with green/red arrows. The loading spinner disappears.

**7. Refresh**
Every panel has a refresh interval. Earthquakes refresh every 5 minutes. Markets refresh every 60 seconds. AIS vessels refresh every 10 seconds. These are `setInterval` timers that re-fetch and re-render.

**8. Death (Destruction)**
If the user toggles a panel off, `destroy()` is called. The DOM elements are removed. The refresh timer is cleared. Memory is freed.

### Why are RSS panels auto-generated?
The variant config has a `FEEDS` object listing all RSS feed categories. For any feed category that doesn't have a hand-built panel (like `MarketPanel` or `CryptoPanel`), the app auto-creates a generic `NewsPanel` with that feed's articles. This means adding a new RSS category = automatic new panel with zero code.

---

## 47. Map Popups — The 40+ Information Cards

### What is it?
When you click on something on the map (a military base, an earthquake, a flight, a cable), a popup appears with detailed information. There are **40+ different popup types**, each showing different data for different item types.

### Why 40+ types?
Because an earthquake popup and a military flight popup need completely different information:

| Click Target | Popup Shows |
|---|---|
| 🔴 Earthquake | Magnitude, depth, location, distance to nearest city, tsunami warning |
| ✈️ Military flight | Callsign, aircraft type, operator, altitude, heading, speed, confidence |
| 🚢 Vessel | Name, MMSI, type, destination, speed, "dark ship?" flag |
| 🔥 Fire | Brightness, power (MW), confidence, satellite that detected it, date/time |
| 📍 Military base | Name, country, branch, coordinates |
| 🔌 Cable landing | Cable name, capacity, year laid, connected countries |
| 🏭 Nuclear facility | Name, type, status, power output |
| 📡 Internet outage | Country, scope, start date, event type |
| 💀 Conflict zone | Name, intensity, parties involved |
| 🌐 Hotspot | Name, escalation score (1-5), escalation trend, keywords |

`MapPopup.ts` is 2,400+ lines — one of the largest files in the project — because each popup type has its own layout, formatting, and data extraction logic.

### The popup flow:
```
User clicks map marker
  ↓
deck.gl reports: "They clicked item X at layer Y"
  ↓
MapPopup checks: "What type of item is X?"
  ↓
Renders the correct popup template
  ↓
Positions the popup near the clicked point
  ↓
User clicks elsewhere → popup dismissed
```

---

## 48. State Management — How the App Remembers Things

### What is it?
"State" is everything the app knows at any given moment. Think of it as the app's **working memory**: what news has loaded, which panels are open, what theme is active, where the map is centered.

### Why no Redux/MobX/Zustand?
Most apps use a state management library — a system that automatically notifies components when data changes. World Monitor doesn't, and here's the ELI5 reason:

Imagine a classroom of 44 kids (panels). With Redux, every time one kid gets a new piece of paper (data update), the teacher would walk to ALL 44 kids and ask "Do you need this paper?" Most kids say "No." That's wasted time.

Without Redux, the teacher walks directly to the one kid who needs the paper. No wasted questions.

With 44 panels updating at different speeds from 38 sources, the "walk to everyone" approach would generate hundreds of unnecessary checks per minute.

### Where state lives:

**In memory (App.ts properties):** Current news, market data, panel settings, map layers — everything that's "right now." Lost on page refresh.

**In localStorage (10+ keys):** Theme, variant, panel order, panel sizes, disabled feeds, monitor configs — everything the user customized. Survives refresh.

**In IndexedDB (2 stores):** Baselines (statistical norms for anomaly detection) and snapshots (dashboard state for time-travel). Survives refresh. Can hold megabytes.

**In URL (query params):** Sharable state — zoom level, map center, active panel. Highest priority (overrides localStorage).

### The priority chain:
```
URL params (highest) > localStorage > variant defaults (lowest)
```

This means if you share a URL like `worldmonitor.app?lat=35&lon=51&zoom=8`, it will override the user's saved map position and center on Tehran.

---

## 49. Refresh Intervals — The Heartbeat of the App

### What is it?
Every data source has a **refresh interval** — how often the app asks for new data. These are carefully tuned based on how fast the underlying data changes.

### Why different intervals?
AIS vessel positions change every few seconds. GDP data changes once a quarter. It would be wasteful (and rude) to check GDP every 10 seconds, and irresponsible to check ship positions only once a day.

### The complete refresh table:

| Data | Interval | Why |
|---|---|---|
| AIS vessels | 10 seconds | Ships move continuously, tracking needs to be near-real-time |
| OpenSky flights | 30 seconds | Aircraft positions need frequent updates for tracking |
| Stock prices | 60 seconds | Markets move fast but per-second is overkill for a dashboard |
| Crypto prices | 2 minutes | Crypto is volatile but cached aggressively due to CoinGecko rate limits |
| RSS news feeds | 5 minutes | News doesn't break faster than every few minutes |
| Earthquakes | 5 minutes | USGS regenerates its feed every 5 minutes; no point checking faster |
| Satellite fires | 10 minutes | NASA FIRMS satellite passes don't happen every second |
| Cyber threats | 10 minutes | Threat feeds update slowly |
| Service status | 1 minute | Outages need quick detection |
| FRED economic | 1 hour | Fed data updates on a schedule, not continuously |
| UNHCR refugees | 24 hours | Refugee data is annual; once per day is plenty |
| Climate anomalies | 6 hours | Monthly resolution data; 6h is conservative |
| WorldPop | 7 days | Population estimates barely change |

### Idle mode:
If the user hasn't interacted for 2 minutes, the app enters **idle mode**. In idle mode, all refresh intervals are paused. When the user moves the mouse or presses a key, they all resume instantly. This saves API calls when someone leaves the tab open.

---

## 50. The Search System — Finding Anything in One Box

### What is it?
Press `Ctrl+K` (or `Cmd+K` on Mac) and a search box appears. You can search for **anything** — countries, news stories, hotspots, stocks, predictions, military bases, cables, data centers, pipelines, and more.

### How does it work?

**20+ result types:**
```
country | news | hotspot | market | prediction | conflict |
base | pipeline | cable | datacenter | waterway | nuclear |
flight | earthquake | crypto | regulation | startup | ...
```

**Scoring:**
- Prefix match (search starts at the beginning of the word) = 2 points
- Substring match (search appears anywhere) = 1 point
- Results sorted by: priority tier first, then score

**Persistence:**
- Your last 10 search selections are saved in localStorage
- They appear as "recent" items next time you open search

**Example:** Type "Taiwan"
- 🏳️ Country result: Taiwan (with instability index)
- 📰 News results: Any articles mentioning Taiwan
- 📍 Hotspot result: Taiwan Strait hotspot (escalation score)
- 🏭 Datacenter results: TSMC facilities in Taiwan
- ✈️ Flight results: Military flights near Taiwan

---

## 51. The Theme System — Dark Mode Done Right

### What is it?
World Monitor supports **dark** and **light** themes. But unlike apps that just swap background colors, World Monitor's theme system goes deep.

### How it works:

**CSS Custom Properties (Variables):**
The entire color scheme is defined as CSS variables on the root element. When the theme changes, ~50 variables are rewritten:

```
Dark theme:  --bg-primary: #0a0a0a;   --text-primary: #e0e0e0;
Light theme: --bg-primary: #f8f9fa;   --text-primary: #1a1a1a;
```

Every component uses these variables instead of hardcoded colors. When the variables change, everything updates instantly.

**The theme change flow:**
```
User clicks theme toggle
  ↓
setTheme('light') called
  ↓
<html data-theme="light"> attribute set
  ↓
CSS variables swap (all components re-color instantly)
  ↓
Color cache invalidated (map colors recalculated)
  ↓
localStorage saves preference
  ↓
Browser meta[theme-color] updated (changes mobile browser bar color)
  ↓
Custom event 'theme-changed' dispatched
  ↓
Components listening for the event update (e.g., map recolors layers)
```

**Why a custom event?** The map's deck.gl layers have colors baked into their WebGL shaders. When the theme changes, the map needs to rebuild its color arrays. The `theme-changed` event tells the map: "Colors changed, please recalculate."

---

## 52. Internationalization (i18n) — Speaking Multiple Languages

### What is it?
i18n (short for "internationalization" — the "18" is the 18 letters between the "i" and the "n") is how the app supports multiple languages.

### How it works:
Translation files live in `src/locales/`:
```
en.json — English
ar.json — Arabic
zh.json — Chinese
es.json — Spanish
... etc
```

Each file maps keys to translated text:
```json
{
  "panels": {
    "earthquakes": "Earthquakes",
    "markets": "Markets"
  },
  "search": {
    "placeholder": "Search countries, news, markets..."
  }
}
```

Components never hardcode text. Instead of writing "Earthquakes", they write `t('panels.earthquakes')`, and the i18n system looks up the correct translation based on the active language.

### Why does it matter?
World Monitor tracks the entire world. Its users are from the entire world. An Arabic-speaking analyst in Dubai needs the interface in Arabic. A Chinese researcher needs it in Chinese. i18n makes one app serve everyone.

---

## 53. Hotspot Escalation Scoring — How Dangerous Is This Place?

### What is it?
World Monitor tracks ~30 geopolitical **hotspots** — places in the world where conflict might escalate. Each hotspot gets an escalation score from 1 to 5 and a trend (escalating, stable, de-escalating).

### How the score is calculated:
The `hotspot-escalation.ts` service looks at:

1. **News velocity:** Are more articles being written about this hotspot than usual?
2. **Source diversity:** Are multiple independent sources reporting (not just one outlet)?
3. **Keyword intensity:** Do the articles contain escalatory keywords ("troops deployed", "missiles fired", "border clashes")?
4. **Historical baseline:** Is this level of activity normal for this region, or is it a spike?

**Score meaning:**
| Score | Level | Example |
|---|---|---|
| 1 | Calm | Normal diplomatic chatter |
| 2 | Watching | Unusual troop movements reported |
| 3 | Elevated | Active confrontation, rising rhetoric |
| 4 | High | Military engagements, sanctions escalation |
| 5 | Critical | Active large-scale conflict or imminent threat |

### How does it help?
- Hotspots are color-coded on the map (green → yellow → red)
- The AI Insights panel prioritizes hotspots with rising scores
- Historical trend shows if a situation is getting worse or better

---

## 54. Country Instability Index — Rating Every Country

### What is it?
The CII (Country Instability Index) panel assigns a **composite instability score** to countries by combining multiple signals:

- Conflict event count (from ACLED)
- Internet outage frequency
- Protest intensity
- Military activity level
- Historical baseline deviation

### The ELI5 version:
Imagine you're a doctor doing a check-up on a country:
- **Pulse** = conflict events (more fighting = higher pulse)
- **Temperature** = protest activity (more protests = hotter)
- **Blood pressure** = military movements (more military = higher pressure)
- **Heart rate variability** = deviation from normal (sudden changes = concerning)

Each metric is a 0-10 score. The composite is a weighted average. The weights are tuned so that actual conflict events (ACLED) weigh more than protests.

### How does it help?
- At a glance: "Which countries are most unstable right now?"
- Trend arrows show if instability is rising or falling
- Feeds into the AI brief for country intelligence reports

---

## 55. Temporal Baselines — What's Normal?

### What is it?
To know if something is "unusual," you need to know what "usual" looks like. Temporal baselines are **30-day rolling averages** for each data metric.

### The ELI5 version:
Imagine counting how many cars pass your house every day for a month. You find the average is 50 cars/day. One day, 200 cars pass. That's a **spike** — something is going on (maybe a detour, an event, an emergency).

World Monitor does this for everything:
- "Usually 15 military flights over Poland per day. Today: 47. **SPIKE.**"
- "Usually 3 earthquakes M4.5+ per week. This week: 12. **ELEVATED.**"
- "Usually 2,000 articles mentioning Iran per day. Today: 8,500. **SPIKE.**"

### How it works:
```
z-score = (today's value - 30-day average) / standard deviation

z-score > 2.5  → SPIKE (very unusual, red alert)
z-score > 1.5  → ELEVATED (somewhat unusual, amber)
z-score < -2.0 → QUIET (unusually low, might also be significant)
otherwise      → NORMAL
```

### Where baselines are stored:
IndexedDB, `baselines` store. Each baseline entry has: the metric key, the rolling average, the standard deviation, and the last 30 data points.

---

## 56. The Playback System — Time Travel

### What is it?
Every few minutes, World Monitor takes a **snapshot** of the entire dashboard state — all panel data, all map positions, all scores. These snapshots are stored in IndexedDB with a timestamp.

A timeline slider at the bottom of the screen lets you **scrub back in time** and see what the dashboard looked like hours ago.

### Why does it matter?
Intelligence isn't just about "what's happening now" — it's about "how did we get here?" If you notice a high convergence score in Iran RIGHT NOW, you want to see: was it low this morning? Did it spike gradually or suddenly?

### How it works:
```
Normal mode: Dashboard shows LIVE data, updating in real-time
  ↓
User drags timeline slider to "6 hours ago"
  ↓
App enters PLAYBACK MODE
  ↓
All panels show the snapshot from 6 hours ago
  ↓
Refresh intervals are PAUSED (you're viewing historical data)
  ↓
User clicks "Live" button → back to real-time
```

### Retention:
Snapshots are kept for **7 days**, then auto-deleted to prevent IndexedDB from growing forever.

---

## 57. The Security Model — Keeping Secrets Safe

### What is it?
World Monitor handles sensitive data (API keys, intelligence data, user preferences). The security model has multiple layers:

### Layer 1: API Key Protection
**Problem:** If API keys are in the browser code, anyone can steal them.
**Solution:** Keys are stored as **environment variables** in Vercel. The Edge Functions use them but never expose them. The browser never sees an API key.

### Layer 2: CORS Allowlist
**Problem:** Someone could build a copycat site that calls our API endpoints.
**Solution:** Every Edge Function checks the `Origin` header. Only requests from `*.worldmonitor.app`, `localhost`, and Tauri origins are allowed. Everything else gets a 403 error.

### Layer 3: Rate Limiting
**Problem:** An attacker could flood our endpoints with thousands of requests per second.
**Solution:** IP-based sliding window rate limiter. Default: 60 requests per 60 seconds per IP. Exceeding the limit returns 429 (Too Many Requests) with a `Retry-After` header.

### Layer 4: OS Keychain (Desktop)
**Problem:** Desktop users need to store API keys locally, but config files are insecure.
**Solution:** Tauri stores secrets in the OS keychain (macOS Keychain, Windows Credential Manager, Linux Secret Service). These are encrypted by the OS and require user authentication to access.

### Layer 5: Content Security
**Problem:** News content from RSS feeds could contain malicious HTML/scripts.
**Solution:** All RSS content is sanitized server-side. HTML tags are stripped. Only plain text reaches the browser.

---

## 58. Deployment Pipeline — From Code to Live

### What is it?
How code goes from a developer's laptop to the live website that users see.

### The flow:
```
Developer writes code
  ↓
git push to GitHub
  ↓
Vercel detects the push automatically
  ↓
Vite builds the app (TypeScript → JavaScript, tree-shaking, minification)
  ↓
Three builds run for three variants:
  • VITE_VARIANT=full  → worldmonitor.app
  • VITE_VARIANT=tech  → tech.worldmonitor.app
  • VITE_VARIANT=finance → finance.worldmonitor.app
  ↓
Built files deployed to Vercel's CDN (300+ global locations)
  ↓
API files deployed as Edge Functions
  ↓
Users get the new version on next page load
```

### Preview deployments:
Every pull request gets its own preview URL (e.g., `my-feature-abc123.vercel.app`). This lets the developer test changes in a real cloud environment before merging to main.

### Desktop builds:
For the Tauri desktop app, the pipeline is different:
```
GitHub Actions runs on push to release branch
  ↓
Tauri builds for Windows (.msi), macOS (.dmg), Linux (.AppImage)
  ↓
Artifacts uploaded to GitHub Releases
  ↓
In-app update check compares local version to GitHub latest release
```

---

## 59. Desktop vs Web — What's Different?

### What is it?
World Monitor runs both as a website and a desktop app. They share 95% of the same code, but the desktop version has some **superpowers** and some **differences**.

### Desktop-only features:

| Feature | Web | Desktop | Why |
|---|---|---|---|
| **OS Keychain** | ❌ | ✅ | Browser can't access system secrets |
| **Local caching server** | ❌ | ✅ Sidecar on port 46123 | Offline caching without Upstash |
| **Full offline mode** | Partial | ✅ Full | Service Worker + local sidecar = everything cached |
| **File system access** | ❌ | ✅ | Export data, save reports to disk |
| **Auto-updates** | N/A (always latest) | ✅ | Checks GitHub releases for new versions |
| **System tray icon** | ❌ | ✅ | Runs in background, alerts on critical events |

### How the app detects desktop:
```typescript
function isDesktopRuntime(): boolean {
  return typeof window.__TAURI__ !== 'undefined';
}
```

If this returns `true`, the app unlocks desktop features:
- Switches caching from Upstash to the local sidecar
- Shows OS keychain integration in settings
- Enables file export buttons
- Starts the auto-update check

### The Sidecar (Node.js helper):
On desktop, a tiny Node.js server runs on `127.0.0.1:46123`. It provides the same API as the Vercel Edge Functions, but locally. When `SIDECAR=true` is set, the caching layer uses an in-memory `Map` + disk file instead of Upstash Redis.

This means: **the desktop app can function completely without internet** using locally cached data.

---

## 60. Entity Extraction — Knowing What You're Reading About

### What is it?
When a news article says "TSMC announced plans to build a new fab in Arizona," the entity extraction system identifies:
- **TSMC** → Company, Semiconductor sector
- **Arizona** → US state, geographic entity
- **fab** → Semiconductor fabrication facility

### How does it work?
The system has a registry of **600+ entities** organized into 5 indexes:

| Index | Example Lookup |
|---|---|
| `byId` | `"TSMC"` → company entity |
| `byAlias` | `"Taiwan Semiconductor"` → same TSMC entity |
| `byKeyword` | `"chip shortage"` → semiconductor sector |
| `bySector` | `"energy"` → all energy companies |
| `byType` | `"country"` → all country entities |

### Why 5 indexes?
Speed. Instead of scanning 600+ entities one by one for every article, the system does a quick `Map.get()` lookup in the relevant index. Matching 200 articles against 600 entities takes milliseconds, not seconds.

### How does it help?
- Entities are tags on every news cluster (visual pills showing "TSMC", "US", "Semiconductors")
- Enables filtering: "Show me only news about energy companies"
- Feeds into the search system: searching "TSMC" finds all clusters mentioning it
- The map can highlight countries mentioned in a news cluster

---

## 61. The Velocity System — Is This Story Growing?

### What is it?
Velocity measures **how fast a story is spreading**. If one source reports a story at 2 PM, and by 3 PM there are 47 sources reporting it — that's high velocity. It's breaking news.

### Three velocity levels:
| Level | Sources/Hour | What It Means |
|---|---|---|
| 🟢 **Normal** | < 3 | Routine story, normal coverage |
| 🟡 **Elevated** | 3-10 | Story gaining traction, worth watching |
| 🔴 **Spike** | > 10 | Breaking news — everyone is covering this simultaneously |

### The velocity object:
```
VelocityMetrics {
  sourcesPerHour: 47        ← raw speed
  level: 'spike'            ← classified level
  trend: 'rising'           ← still accelerating
  sentiment: 'negative'     ← mostly bad news
  sentimentScore: -0.7      ← how negative (-1 to +1)
}
```

### How does it help?
- Spike stories get 🔴 badges and rise to the top of panels
- The AI Insights panel uses velocity to decide what to summarize first
- Analysts can spot breaking stories within minutes of them starting

---

## 62. The Monitor System — Custom Watchers

### What is it?
Monitors are **custom alerts** that the user sets up. "Alert me when any article mentions 'Iran' AND 'nuclear'." Or "Watch for earthquakes above magnitude 6 near Japan."

### How monitors work:
```
User creates a monitor: {
  name: "Iran Nuclear Watch",
  keywords: ["iran", "nuclear"],
  sources: "all",
  severity: "high"
}
  ↓
Every time new data arrives, each monitor is checked:
  "Does this article/event match my keywords?"
  ↓
If yes → Desktop: system notification. Web: badge on monitor panel.
```

### Types of monitors:
- **Keyword monitors** — match text patterns in news
- **Geographic monitors** — events within X km of a location
- **Threshold monitors** — "alert when earthquake magnitude > 6"

### Persistence:
Monitors are saved in localStorage under `worldmonitor-monitors`. They survive page refresh and variant changes.

---

## 63. Technology Decision Tree — Why THIS and Not THAT?

### The complete "why not X?" for every major choice:

**Why TypeScript and not JavaScript?**
JavaScript doesn't have types. With 60+ data interfaces, you'd spend more time debugging type mismatches than writing features. TypeScript catches these during development, not in production.

**Why Vite and not Webpack?**
Webpack bundles everything on every change (slow). Vite uses native ES modules during development — only the changed file is reprocessed (fast). For a project with 200+ source files, this is minutes vs. seconds.

**Why no React/Vue/Angular?**
React adds 45KB + virtual DOM reconciliation overhead on 44 panels. Vue adds similar overhead. Angular adds even more. None of them solve a problem World Monitor has — the DOM updates are already targeted and explicit.

**Why Vercel Edge Functions and not AWS Lambda?**
Lambda runs in specific regions (us-east-1, eu-west-1, etc.). Edge Functions run in 300+ locations. For a global dashboard, edge = lower latency everywhere. Also: Vercel's free tier is generous, and deployment is git-push simple.

**Why Upstash Redis and not Momento/DynamoDB/regular Redis?**
Regular Redis needs a persistent TCP connection. Serverless functions don't have persistent connections — they start cold, run, and die. Upstash Redis uses HTTP requests (REST API), which works perfectly with serverless. DynamoDB would work but is more complex and expensive. Momento is newer and less proven.

**Why Tauri and not Electron?**
Electron bundles an entire Chromium browser (~150MB). Tauri uses the OS's existing webview (~5MB). For a dashboard app, Electron is absurd overkill. Tauri also provides Rust-based security features (OS keychain) that Electron requires additional packages for.

**Why MapLibre and not Google Maps/Mapbox?**
Google Maps charges per API call at scale. Mapbox is free for development but expensive in production. MapLibre is a fork of Mapbox's open-source version — forever free, same quality, no vendor lock-in.

**Why deck.gl and not Three.js/CesiumJS?**
Three.js is a general-purpose 3D engine — too low-level for data visualization. CesiumJS is great for 3D globes but very heavy (3MB+ bundle). deck.gl is specifically designed for data layers on maps with GPU acceleration. It does exactly what World Monitor needs and nothing more.

**Why D3.js as fallback and not Leaflet?**
Leaflet uses raster tiles (pre-drawn images) which look blurry at high zoom. D3.js with SVG creates crisp vector graphics at any zoom. For a fallback that still needs to look professional, D3's quality matters.

**Why Groq and not OpenAI/Anthropic/Google?**
Groq is 5-20x faster than GPU-based inference (OpenAI, Anthropic). For a real-time dashboard, waiting 5 seconds for a summary defeats the purpose. Groq returns summaries in 100-500ms. Also: free tier available.

**Why browser ML (Transformers.js) and not just cloud AI?**
Cloud AI costs money and requires internet. Browser ML is free and works offline. For the desktop app, it enables fully disconnected operation. It's also the third safety net — if both Groq AND OpenRouter are down, AI features still work.

**Why 5 cyber threat feeds and not 1?**
No single feed catches everything. Feodo tracks botnets, URLhaus tracks malicious URLs, AbuseIPDB tracks bad IPs. Each feed has blind spots. Aggregating 5 sources gives 90%+ coverage of the threat landscape.

**Why RSS and not Twitter/X API?**
Twitter's API became paid and unreliable. RSS is free, standardized, and universally supported. 150 news sources × free = better coverage than any single social media API.

---

## Summary — Part 2

Part 2 dove deeper into the **how** behind every system:

- How data flows from raw API response to rendered panel
- How each Edge Function processes and caches requests
- How panels are born, live, and die
- How the map knows what popup to show for 40+ item types
- How state is managed without any reactive library
- How refresh intervals are tuned per data source
- How search finds anything across 20+ result types
- How themes, languages, and hotspot scores work
- How baselines detect anomalies and playback enables time-travel
- How security protects API keys across web and desktop
- How code deploys from laptop to live
- How every technology choice was made (and what was rejected)

```
🧠 Part 1: "WHAT is each system?" (43 systems)
🔬 Part 2: "HOW do they work inside?" (20 deep dives)
Together: Complete understanding of World Monitor
```

> **Document stats (Total):** ~14,400 words · 63 sections · ELI5 format · Every system explained with What/Why/How · Every technology decision justified with alternatives · Complete data lifecycle · Security model · Deployment pipeline · No jargon unexplained.
