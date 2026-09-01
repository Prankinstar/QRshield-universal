# QRShield Universal: Multi-Vector Zero-Trust Protection Framework

QRShield Universal is an asynchronous security architecture designed to prevent physical QR tampering, sticker swap attacks, digital display spoofing, and rogue payment routing in **sub-80ms**.

---

## 🏗️ Architectural Highlights

* **Multi-Vector Risk Fusion Engine (`core/fusion_engine.py`):** Runs parallel asynchronous evaluations across Client-Side Computer Vision, Haversine Geofencing, Cryptographic binding, Domain WHOIS age, and VPA velocity vectors.
* **Hybrid Computer Vision Engine (`cv_engine/`):** Runs compiled browser-side C++ OpenCV via WebAssembly (`moire_detector.cpp`, `sticker_detector.cpp`) with server-side surface analyzer fallbacks (`surface_analyzer.py`).
* **Profile-Based Risk Evaluators (`profile_evaluators/`):** Context-aware evaluation modules tailored for Retail, P2P Transfers, Public Ads/Billboards, and POS Digital Screens.
* **Zero-Hardware Software Soundbox (`soundbox_gateway/`):** Eliminates physical $40 audio hardware by multiplexing real-time payment and threat verification alerts over WebSockets directly to existing staff devices.
* **4-Tier Spatial Geofencing Array (`core/spatial_engine.py`):** Overcomes mall satellite deadzones by combining Device GPS, Wi-Fi BSSID matching, Corporate IP subnets, and Haversine Distance Decay.

---

## 📂 Project Structure

```text
qrshield-universal/
├── config.py                       # System environment & threshold configurations
├── main.py                         # FastAPI server entry point, routes, & WS hub
├── qr_parser.py                    # Top-level QR payload parser
├── test_main.py                    # Pytest suite harness
├── requirements.txt                # Dependencies (FastAPI, Uvicorn, Jinja2, Pydantic)
│
├── core/                           # Zero-Trust Cryptographic & Risk Engines
│   ├── crypto_verifier.py          # HMAC-SHA256 signature and TTL validator
│   ├── fusion_engine.py           # Sub-80ms multi-vector risk aggregator
│   ├── identity_router.py         # Merchant identity & profile routing logic
│   └── spatial_engine.py          # Haversine geofencing & IP network fallbacks
│
├── cv_engine/                      # Edge Computer Vision & WebAssembly Engine
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
├── soundbox_gateway/               # Zero-Hardware WebSocket Broadcast Network
│   ├── socket_hub.py               # WebSocket client connection manager
│   └── webhook_dispatcher.py       # Async alert webhook dispatcher
│
├── threat_intel/                   # Real-Time Intelligence & Analytics
│   ├── domain_inspector.py         # DoH DNS lookup & redirect unwinder
│   ├── velocity_tracker.py         # Redis transaction frequency anomaly tracker
│   └── vpa_reputation.py           # Payment handle age & syntax verifier
│
├── utils/                          # Utility Decoders
│   └── payload_decoder.py          # Deep UPI URI & scheme decoder
│
├── static/                         # Static Frontend Assets
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
└── templates/                      # Web Portals
    ├── scanner.html                # Universal AR Scanner Terminal
    ├── soc_dashboard.html         # Enterprise SOC Real-Time Threat Map
    └── staff_soundbox.html        # Software Soundbox Portal
🚀 Quickstart Guide1. Environment SetupBash# Clone repository
git clone [https://github.com/YOUR-USERNAME/qrshield-universal.git](https://github.com/YOUR-USERNAME/qrshield-universal.git)
cd qrshield-universal

# Create and activate virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
2. Launch Development ServerRun directly via Python:Bashpython main.py
Or execute via Uvicorn:Bashuvicorn main:app --reload --host 0.0.0.0 --port 8000
🌐 Active System EndpointsEndpointLocal URLFunctionScanner UIhttp://localhost:8000/scannerCamera scanning terminal with live HUD diagnostic boundsStaff Soundboxhttp://localhost:8000/soundboxReal-time WebSocket audio receiver for store staffSOC Dashboardhttp://localhost:8000/socReal-time threat location map and attack logsAPI Swaggerhttp://localhost:8000/docsInteractive OpenAPI documentation🚦 Risk Score Decision Matrix0 – 39 (VERIFIED / SAFE): Target payload is cryptographically and physically clear. Green HUD target bounds render and a WebSockets payment alert broadcasts to staff.40 – 69 (FLAGGED / WARN): Domain registration is young or location delta is elevated. Yellow HUD warning prompt requires user confirmation before navigation.70 – 100 (BLOCKED / CRITICAL): High confidence physical sticker anomaly, malicious URL redirect, or spoofed VPA. Immediate block with attack marker logged to SOC Map.
