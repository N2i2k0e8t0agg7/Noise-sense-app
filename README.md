# 🎙️ NoiseSense — Urban Noise Intelligence
 
> **HackCity 2025 · Smart Cities Track**  
> Real-time acoustic monitoring across city zones, powered by IoT sensors and AI anomaly detection.
 
---
 
## 🏆 Hackathon Submission
 
| Field | Detail |
|---|---|
| Event | HackCity 2025 |
| Track | Smart Cities |
| Team Size | 4 members |
| Built In | 36 hours |
| License | MIT |
 
---
 
## 📌 What is NoiseSense?
 
NoiseSense is a full-stack urban noise pollution monitoring platform. It ingests acoustic data from IoT edge sensors deployed across city zones, classifies noise events using a fine-tuned AI model, detects anomalies in real time, and presents everything through a live operational dashboard.
 
The goal: give city authorities the tools to **monitor, respond to, and plan around** noise pollution — a WHO-recognised environmental health hazard affecting over 100 million people in Europe alone.
 
---
 
## ✨ Features
 
- **Live Dashboard** — per-zone dB readings, metrics, and AI anomaly alerts refreshing every 5 seconds
- **24h Trend Chart** — canvas-drawn line chart showing noise levels across the top 3 zones over the day
- **Event Breakdown** — doughnut chart classifying noise by type (traffic, construction, crowd, music, HVAC, other)
- **Hour × Zone Heatmap** — visual grid of noise intensity across 6 zones × 24 hours with hover tooltips
- **Sensor Table** — live table with dB bars, status badges (Safe / Warning / Critical), event type, and timestamps
- **AI Alert Banner** — real-time anomaly detection messages with classifier confidence scores
- **Multi-page SPA** — Home, Dashboard, How It Works, and Team pages with client-side routing
- **Zero dependencies** — pure HTML, CSS, and JavaScript; no frameworks, no CDN, works fully offline
---
 
## 🖥️ Demo
 
Open `noisesense.html` in any modern browser. No server, no install, no build step required.
 
```
# Just double-click the file, or:
open noisesense.html        # macOS
start noisesense.html       # Windows
xdg-open noisesense.html    # Linux
```
 
---
 
## 📁 Project Structure
 
```
noisesense/
├── noisesense.html     # Complete self-contained application
└── README.md           # This file
```
 
Everything — HTML, CSS, and JavaScript — lives in a single file. The Canvas 2D API handles all charts natively, eliminating any external library dependencies.
 
---
 
## 🏗️ Architecture (Conceptual Pipeline)
 
```
[MEMS Mic + RPi 4]  →  MQTT/LoRaWAN  →  [Cloud Broker]
                                               ↓
                                      [YAMNet CNN Classifier]
                                               ↓
                                    [Anomaly Detection Engine]
                                    (Z-score + Isolation Forest)
                                               ↓
                                      [TimescaleDB Storage]
                                               ↓
                                    [WebSocket → Dashboard]
```
 
### Pipeline Steps
 
1. **Edge Capture** — Raspberry Pi 4 nodes with calibrated MEMS microphones sample audio at 44.1 kHz. Only acoustic features are transmitted, never raw audio, preserving privacy.
2. **MQTT Streaming** — Feature packets are published to a cloud broker every 500 ms. LoRaWAN provides fallback connectivity in poor-signal urban canyons.
3. **AI Classification** — A lightweight CNN based on YAMNet, fine-tuned on urban soundscapes, classifies events (traffic, construction, crowds, music, alarms) in under 80 ms per inference.
4. **Anomaly Detection** — Z-score and Isolation Forest models flag readings that deviate significantly from historical zone baselines. City ops are alerted within 30 seconds of onset.
5. **Live Dashboard** — WebSocket-powered interface delivers per-zone dB, heatmaps, trend lines, and AI-generated incident summaries to operators on any device.
6. **Open Data API** — REST + GraphQL endpoints serve historical data to urban planners and researchers under an open data licence for public zones.
---
 
## 🛠️ Tech Stack
 
### Frontend (this repo)
| Technology | Role |
|---|---|
| HTML5 / CSS3 | Structure and styling |
| Vanilla JavaScript (ES5+) | Interactivity, routing, live updates |
| Canvas 2D API | Charts (trend line, doughnut, heatmap) |
 
### Backend (conceptual / production system)
| Technology | Role |
|---|---|
| Python 3.12 | Core backend language |
| FastAPI | REST + WebSocket API server |
| PyTorch + YAMNet | Audio event classification CNN |
| scikit-learn | Anomaly detection (Isolation Forest, Z-score) |
| MQTT / Mosquitto | Edge-to-cloud messaging |
| LoRaWAN | Low-power wide-area sensor connectivity |
| TimescaleDB | Time-series storage for sensor readings |
| Redis Streams | Real-time event buffering |
| Docker + Kubernetes | Containerisation and orchestration |
| OpenAPI 3.1 | API specification |
 
---
 
## 📊 Dashboard Metrics
 
| Metric | Description |
|---|---|
| Avg. City dB | Mean decibel level across all active sensors |
| Zones in Warning | Count of zones exceeding 55 dB (warning) or 70 dB (critical) |
| Quietest Zone | Zone with the lowest current reading |
| Events Classified | Cumulative AI classifications since midnight |
 
### dB Thresholds
 
| Level | Range | Status |
|---|---|---|
| Safe | < 55 dB | Green |
| Warning | 55–69 dB | Amber |
| Critical | ≥ 70 dB | Red |
 
Thresholds are aligned with WHO Environmental Noise Guidelines for the European Region (2018).
 
---
 
## 👥 Team
 
| Name | Role | Focus |
|---|---|---|
| Aisha Karimi | ML Engineer | Signal processing, YAMNet fine-tuning |
| Leo Nakamura | Embedded / IoT | Raspberry Pi, LoRaWAN, MQTT |
| Sofia Reyes | Backend / DevOps | FastAPI, TimescaleDB, Kubernetes |
| Marcus Bell | Frontend / UX | Dashboard, charts, design system |
 
---
 
## 🌍 Problem Statement
 
Environmental noise is the second-largest environmental health risk in Europe after air pollution (WHO, 2018). Chronic exposure above 53 dB at night is linked to cardiovascular disease, sleep disruption, and cognitive impairment in children.
 
Most cities lack real-time, granular noise data. NoiseSense fills that gap with an affordable, scalable, privacy-preserving sensor network and an AI layer that moves beyond raw dB readings to explain *why* noise is happening and *when* it requires intervention.
 
---
 
## 🔮 Future Roadmap
 
- [ ] Native map view with per-sensor geolocation pins
- [ ] Push notifications and SMS alerts for city operators
- [ ] Resident-facing mobile app with neighbourhood noise scores
- [ ] Predictive model — forecast noise levels 2h ahead using historical patterns
- [ ] Integration with city permitting systems (flag unlicensed construction noise automatically)
- [ ] Hardware BOM and deployment guide for low-cost sensor build
---
 
## 📄 License
 
MIT License — free to use, modify, and distribute. See `LICENSE` for details.
 
---
 
*Built with ❤️ in 36 hours at HackCity 2025.*
 
