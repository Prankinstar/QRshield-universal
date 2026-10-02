# 🛡️ QRShield Universal

> **AI-Powered Continuous Cyber Risk Quantification & Investment Optimization Platform**  
> *Smart India Hackathon (SIH) | Problem Statement ID: 26105*

QRShield Universal is an asynchronous cyber-physical security architecture designed to perform real-time continuous risk quantification, physical QR tampering detection, sticker swap identification, and rogue payment routing prevention in **sub-80ms**.

---

## 📸 System Interface & Live Telemetry

<p align="center">
  <img src="./assets/scanner-hud.png" width="48%" alt="QRShield Inspector HUD" />
  <img src="./assets/soc-dashboard.png" width="48%" alt="Enterprise SOC Dashboard" />
</p>
<p align="center">
  <img src="./assets/diagnostics.png" width="48%" alt="Deep Payload Diagnostics" />
  <img src="./assets/soundbox.png" width="48%" alt="Digital Soundbox Terminal" />
</p>

| Interface | Description |
| :--- | :--- |
| **Real-Time AR Inspector HUD** | Client-side C++ WASM engine inspecting video streams for physical paper overlays and Moiré screen patterns in sub-80ms. |
| **Enterprise CISO SOC Hub** | Live geospatial telemetry map rendering physical threat markers, risk heatmaps, and global terminal status. |
| **Deep Payload Diagnostics** | Multi-vector payload inspection tool for manual stress testing, URL unwinding, and MITM vulnerability checks. |
| **Zero-Hardware Digital Soundbox** | Software terminal replacing ₹3,000–₹4,000 IoT audio boxes by streaming instant WebSocket voice alerts to existing devices. |

---

## 🏗️ Architectural Highlights

- **Multi-Vector Risk Fusion Engine (`core/fusion_engine.py`):** Evaluates parallel asynchronous risk vectors (Client-Side Computer Vision, Haversine Geofencing, Cryptographic binding, Domain WHOIS age, and VPA velocity) to produce a dynamic Continuous Risk Index ($0.0 - 100.0$).
- **Hybrid Edge Computer Vision Engine (`cv_engine/`):** Executes compiled browser-side C++ via WebAssembly (`moire_detector.cpp`, `sticker_detector.cpp`) with server-side surface analyzer fallbacks (`surface_analyzer.py`), offloading 70%+ of compute load to client browsers.
- **Profile-Based Risk Evaluators (`profile_evaluators/`):** Context-aware evaluation modules tailored for Retail Terminals, P2P Transfers, Public Ads/Billboards, and POS Digital Screens.
- **Zero-Hardware Software Soundbox (`soundbox_gateway/`):** Optimizes CapEx by eliminating physical IoT hardware, multiplexing real-time payment and threat verification alerts over WebSockets directly to existing staff web browsers.
- **4-Tier Spatial Geofencing Array (`core/spatial_engine.py`):** Overcomes satellite deadzones in indoor shopping malls by combining Device GPS, Wi-Fi BSSID matching, Corporate IP subnets, and Haversine Distance Decay.

---

## 🚦 Risk Score Decision Matrix

| Continuous Risk Index | Status Level | System Action & UI Response |
| :---: | :---: | :--- |
| **0 – 39** | `VERIFIED / SAFE` | Payload is cryptographically and physically clear. Green HUD target bounds render and WebSocket confirmation broadcasts to store staff. |
| **40 – 69** | `FLAGGED / WARN` | Domain registration is young or location delta is elevated. Yellow HUD warning prompt requires explicit user confirmation before navigation. |
| **70 – 100** | `BLOCKED / CRITICAL` | High confidence physical sticker anomaly, malicious URL redirect, or spoofed VPA handle. Immediate block with attack marker logged to SOC map. |

---

## 🌐 Active System Endpoints

| Portal / Endpoint | Local URL | Primary Function |
| :--- | :--- | :--- |
| **Scanner UI** | `http://localhost:8000/scanner` | AR camera scanning terminal with live HUD diagnostics |
| **Staff Soundbox** | `http://localhost:8000/soundbox` | Real-time WebSocket zero-hardware audio receiver |
| **SOC Dashboard** | `http://localhost:8000/soc` | Real-time geospatial threat map and attack logs |
| **API OpenDocs** | `http://localhost:8000/docs` | Interactive OpenAPI / Swagger documentation |

---

## 📂 Project Structure

```text
qrshield-universal/
├── config.py                        # System environment & threshold configurations
├── main.py                          # FastAPI server entry point, routes, & WS hub
├── qr_parser.py                     # Top-level QR payload parser
├── test_main.py                     # Pytest suite harness
├── requirements.txt                 # Dependencies (FastAPI, Uvicorn, Jinja2, Pydantic)
│
├── core/                            # Zero-Trust Cryptographic & Risk Engines
│   ├── crypto_verifier.py          # HMAC-SHA256 signature and TTL validator
│   ├── fusion_engine.py           # Sub-80ms multi-vector risk aggregator
│   ├── identity_router.py         # Merchant identity & profile routing logic
│   └── spatial_engine.py          # Haversine geofencing & IP network fallbacks
│
├── cv_engine/                       # Edge Computer Vision & WebAssembly Engine
│   ├── surface_analyzer.py        # Python fallback surface diagnostics
│   ├── profile_evaluators/         # Contextual scenario evaluators
│   │   ├── digital_screen_evaluator.py
│   │   ├── peer_transfer_evaluator.py
│   │   ├── public_ad_evaluator.py
│   │   └── retail_evaluator.py
│   └── wasm_src/                   # Native C++ WASM source files
│       ├── build_wasm.sh           # Emscripten toolchain compilation script
│       ├── moire_detector.cpp      # C++ FFT digital screen Moiré detector
│       └── sticker_detector.cpp    # C++ Canny edge physical sticker detector
│
├── soundbox_gateway/                # Zero-Hardware WebSocket Broadcast Network
│   ├── socket_hub.py               # WebSocket client connection manager
│   └── webhook_dispatcher.py       # Async alert webhook dispatcher
│
├── threat_intel/                    # Real-Time Intelligence & Analytics
│   ├── domain_inspector.py         # DoH DNS lookup & redirect unwinder
│   ├── velocity_tracker.py         # Redis transaction frequency anomaly tracker
│   └── vpa_reputation.py           # Payment handle age & syntax verifier
│
├── utils/                           # Utility Decoders
│   └── payload_decoder.py          # Deep UPI URI & scheme decoder
│
├── static/                          # Static Frontend Assets
│   ├── css/
│   │   ├── enterprise_soc.css      # SOC dashboard styling
│   │   └── scanner.css             # Scanner HUD diagnostic styling
│   ├── js/
│   │   ├── soc_leaflet_map.js      # Interactive SOC threat map logic
│   │   ├── soundbox_staff_receiver.js # Client-side TTS audio engine
│   │   └── universal_scanner.js    # Camera stream & canvas analyzer script
│   └── wasm/
│       ├── cv_engine.wasm          # Compiled C++ OpenCV WebAssembly binary
│       └── cv_wrapper.js           # JavaScript bridge for WASM module
│
└── templates/                       # Web Portals
    ├── scanner.html                # Universal AR Scanner Terminal
    ├── soc_dashboard.html         # Enterprise SOC Real-Time Threat Map
    └── staff_soundbox.html        # Software Soundbox Portal
