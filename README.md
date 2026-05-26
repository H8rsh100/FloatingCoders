<p align="center">
  <h1 align="center">🌿 Swachh Vayu — स्वच्छ वायु</h1>
  <h3 align="center">Rural Air Quality Intelligence & Agricultural Decision Platform</h3>
  <p align="center">
    <em>Empowering rural India with real-time, multilingual, AI-driven air quality monitoring — from farm to panchayat.</em>
  </p>
  <p align="center">
    <img src="https://img.shields.io/badge/Python-Flask-blue?style=for-the-badge&logo=flask" />
    <img src="https://img.shields.io/badge/React-Vite-purple?style=for-the-badge&logo=react" />
    <img src="https://img.shields.io/badge/IoT-ESP8266-green?style=for-the-badge&logo=espressif" />
    <img src="https://img.shields.io/badge/AI-Scikit--Learn-orange?style=for-the-badge&logo=scikit-learn" />
    <img src="https://img.shields.io/badge/Multilingual-6_Languages-red?style=for-the-badge" />
  </p>
</p>

---

## 🚀 The Problem

India has thousands of urban air monitoring stations — but **over 65% of the population lives in rural agricultural belts** where stubble burning, pesticide sprays, and biomass cooking fires silently destroy health. These villages have:

- ❌ **Zero** localized air quality data
- ❌ **No** actionable advisories in local languages
- ❌ **No** system linking air quality to farming decisions
- ❌ **No** incentive mechanism for cleaner agricultural practices

An arbitrary scientific "AQI number" means nothing to a farmer in Khedgaon or Pimpalgaon. They need **intelligence they can act on, in a language they speak.**

---

## 💡 Our Solution

**Swachh Vayu** is an end-to-end, offline-first platform that bridges the gap between IoT hardware, agricultural intelligence, and community-driven clean air governance.

### 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                        SWACHH VAYU PLATFORM                        │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌──────────┐    WiFi/LoRa    ┌──────────────┐    REST API         │
│  │ ESP8266  │ ──────────────► │ Raspberry Pi │ ◄──────────────┐    │
│  │ + MQ135  │    HTTP POST    │  Flask + DB  │                │    │
│  │ + LCD    │                 │  + ML Model  │    ┌───────────┴─┐  │
│  │ + LEDs   │                 └──────┬───────┘    │ React + Vite│  │
│  │ + Buzzer │                        │            │  Dashboard  │  │
│  └──────────┘                        │            │  + Leaflet  │  │
│       │                              ▼            │  + i18n     │  │
│  Local Alert               ┌─────────────────┐   └─────────────┘  │
│  (LCD + LED                │   Sarvam AI     │                     │
│   + Buzzer)                │  Translation +  │                     │
│                            │  Voice Alerts   │                     │
│                            └─────────────────┘                     │
└─────────────────────────────────────────────────────────────────────┘
```

---

## ✨ Key Features

### 🌾 Agricultural Decision Intelligence (Our USP)

This is **not** just a monitoring tool. Swachh Vayu converts raw air data into **farm-level actionable intelligence**:

| Feature | Description |
|---------|-------------|
| 🚜 **Farm Safety Index** | Dynamic index advising if it's safe for outdoor harvesting, pesticide spraying, or crop processing today |
| 🧑‍🌾 **Crop Advisory** | Automated recommendations based on atmospheric health — "Delay pesticide application by 4 hours" |
| 📊 **4-Hour Predictive Forecasting** | ML model predicts air quality 4 hours ahead so farmers can plan their day |
| ✅ **Clean Air Measures Checklist** | Interactive, gamified checklist for villages to adopt eco-friendly practices (bio-decomposers over stubble burning, organic pest control, etc.) |

### 🗣️ Multilingual & Inclusive

- Full UI translation in **6 languages**: English, Hindi, Marathi, Tamil, Kannada, Telugu
- **Sarvam AI** integration for real-time translation, text-to-speech voice alerts, and voice assistant
- Designed for **low-literacy users** — visual indicators (color-coded LEDs, simple icons) alongside text

### 🗺️ Live Interactive Map

- **Leaflet.js** powered real-time map of all deployed nodes
- Color-coded markers showing live node status (🟢 Active / 🔴 Offline)
- Village-level zoom with geographic clustering
- Currently deployed in **Nashik Rural District**: Khedgaon & Pimpalgaon

### 🏆 Village Leaderboard & Gamification

- Quarterly village rankings based on air quality improvement scores
- **Podium-style leaderboard** to create healthy inter-village competition
- Tracks: Average Air Quality, Best/Worst readings, Reduction %, Participation Score
- Incentivizes panchayats to promote cleaner agricultural and cooking practices

### 🤖 AI/ML Prediction Engine

| Parameter | Value |
|-----------|-------|
| **Model** | Random Forest Regressor (scikit-learn) |
| **Trees** | 100 estimators, max depth 12 |
| **Dataset** | CPCB Rural Air Quality dataset with agricultural burning patterns |
| **Features** | Current AQI, Previous AQI, Temperature, Humidity, Hour of Day, Day of Week, 3hr Rolling Avg, AQI Change Rate |
| **Target** | 4-hour ahead air quality forecast |
| **Use Case** | Early warning for farmers — reschedule outdoor activities before air degrades |

### 📡 IoT Hardware Nodes

| Component | Specification |
|-----------|--------------|
| **Microcontroller** | ESP8266 NodeMCU (WiFi) / ESP32 (LoRa-ready) |
| **Air Quality Sensor** | MQ135 — detects NH3, NOx, benzene, smoke, CO₂ |
| **Local Display** | 16×2 I2C LCD — shows real-time AQI + status |
| **Visual Alerts** | 3× LEDs (Green/Yellow/Red) with 220Ω resistors |
| **Audio Alert** | Active Buzzer — triggers at dangerous AQI levels |
| **Data Transmission** | HTTP POST JSON to Raspberry Pi every 5 seconds |
| **Power** | USB / Solar-ready with 3.7V battery backup |

### 🔌 Offline-First Design

- ESP nodes work **without internet** — local LCD + LED + Buzzer alerts always functional
- Raspberry Pi can create local WiFi hotspot (`AIRWATCH_LOCAL`)
- Phones access dashboard via local IP on the village network
- GSM module (SIM800L) for SMS/voice alerts when cellular is available

---

## 📂 Project Structure

```
Code2Change/
├── backend/                    # Flask REST API Server
│   ├── app.py                  # Main Flask application
│   ├── config.py               # Environment & app configuration
│   ├── database.py             # SQLite connection manager
│   ├── schema.sql              # Complete database schema (6 tables)
│   ├── swachh_vayu.db          # Pre-seeded SQLite database
│   ├── routes/                 # API route blueprints
│   ├── services/               # Business logic layer
│   │   ├── node_service.py     # Node management & status
│   │   ├── prediction_service.py  # ML prediction engine
│   │   └── sarvam_service.py   # Sarvam AI integration
│   ├── ml/                     # Machine Learning
│   │   ├── train_model.py      # Model training pipeline
│   │   └── rf_model.pkl        # Trained Random Forest model
│   ├── utils/                  # Utility functions
│   ├── deployment/             # Deployment configurations
│   └── test_*.py               # Comprehensive test suite
│
├── frontend/                   # React + Vite Dashboard
│   ├── src/
│   │   ├── App.jsx             # Main app with React Router
│   │   ├── pages/              # Page components
│   │   │   ├── LandingPage.jsx      # Hero + live stats dashboard
│   │   │   ├── VillageRankings.jsx  # Podium leaderboard
│   │   │   ├── MeasuresPage.jsx     # Clean air checklist
│   │   │   └── ContentPage.jsx      # Educational content
│   │   ├── components/         # Reusable UI components
│   │   ├── services/
│   │   │   ├── api.js          # Axios API client
│   │   │   └── i18n.js         # 6-language translation engine
│   │   ├── data/
│   │   │   └── mockData.js     # Fallback data for offline mode
│   │   └── hooks/              # Custom React hooks
│   └── package.json
│
├── hardware/                   # IoT Firmware
│   ├── esp8266_node/
│   │   └── esp8266_node.ino    # WiFi sensor node (primary)
│   └── esp32_node/
│       └── esp32_node.ino      # LoRa-ready node (secondary)
│
├── Documentation/              # 19 detailed project documents
│   ├── 01_Problem_Statement.docx
│   ├── 04_System_Architecture.docx
│   ├── 05_Hardware_Design.docx
│   ├── 11_AI_Model_Document.docx
│   ├── 12_SarvamAI_Integration.docx
│   └── ... (14 more documents)
│
└── .gitignore
```

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| **Frontend** | React 18 + Vite, Leaflet.js (maps), Chart.js (graphs) |
| **Backend** | Python Flask, SQLite, RESTful API |
| **AI/ML** | Scikit-learn (Random Forest), Joblib, Pandas, NumPy |
| **Multilingual** | Custom i18n engine + Sarvam AI (Mayura v1, Bulbul v2, Saarika v2) |
| **IoT Hardware** | ESP8266/ESP32, MQ135 sensor, I2C LCD, LEDs, Buzzer |
| **Communication** | WiFi HTTP POST (active), LoRa SX1278 (planned) |
| **Gateway** | Raspberry Pi 4 |
| **Alerts** | LCD + LED + Buzzer (local), SMS + Voice (remote via Sarvam AI / SIM800L) |

---

## ⚡ Quick Start

### Backend (Raspberry Pi / Local Machine)

```bash
# Clone the repository
git clone https://github.com/H8rsh100/FloatingCoders.git
cd FloatingCoders

# Create virtual environment
python -m venv .venv
source .venv/bin/activate        # Linux/Mac
# .venv\Scripts\activate         # Windows

# Install dependencies
pip install -r backend/requirements.txt

# Run the Flask server
python backend/app.py
# Server starts at http://localhost:5000
```

### Frontend (Dashboard)

```bash
cd frontend

# Install dependencies
npm install

# Start development server
npm run dev
# Dashboard at http://localhost:5173
```

### Hardware (ESP8266 Node)

1. Open `hardware/esp8266_node/esp8266_node.ino` in Arduino IDE
2. Install libraries: `ESP8266WiFi`, `LiquidCrystal_I2C`, `ESP8266HTTPClient`
3. Update WiFi credentials and Raspberry Pi IP in the code
4. Flash to ESP8266 NodeMCU
5. Connect MQ135 to A0, LEDs to D5/D6/D7, Buzzer to D4, LCD to I2C (D1/D2)

### Train the ML Model (Optional)

```bash
cd backend/ml
python train_model.py
# Generates rf_model.pkl — 100-tree Random Forest trained on rural CPCB data
```

---

## 📊 Database Schema

```sql
languages     →  10 supported languages (en, hi, mr, kn, ta, te, bn, gu, pa, ml)
users         →  Registered villagers with language preference & alert mode
nodes         →  IoT sensor nodes with GPS coordinates & battery status
aqi_readings  →  Time-series air quality data from each node
alerts        →  SMS/voice alert delivery tracking
rankings      →  Quarterly village leaderboard scores
```

---

## 🌍 Current Deployment

| Node | Village | District | Coordinates | Status |
|------|---------|----------|-------------|--------|
| NODE_01 | Khedgaon | Nashik Rural | 20.2115°N, 73.9632°E | 🟢 Active |
| NODE_02 | Pimpalgaon | Nashik Rural | 20.1585°N, 73.9850°E | 🟢 Active |

---

## 🏅 Village Rankings (Current Quarter)

| Rank | Village | Air Quality Score | Status |
|------|---------|-------------------|--------|
| 🥇 #1 | Pimpalgaon | 90 | ⭐ Leading |
| 🥈 #2 | Khedgaon | 60 | 📈 Improving |

---

## 🔮 Future Roadmap

- [ ] **LoRa Mesh Network** — Long-range, low-power communication for remote villages without WiFi
- [ ] **PMS5003 PM2.5 Sensor** — Calibrated particulate matter sensing for medical-grade accuracy
- [ ] **GSM Alert System** — SIM800L integration for SMS/voice alerts in regional languages
- [ ] **Solar Power** — Fully solar-powered nodes for zero-maintenance deployment
- [ ] **Panchayat Dashboard** — Dedicated admin panel for village leaders
- [ ] **Government API Integration** — CPCB/SAFAR data correlation for validation
- [ ] **Mobile App** — React Native companion app with push notifications

---

## 👥 Team FloatingCoders

Built with ❤️ for **Code2Change Hackathon** — solving real problems for rural India.

---

## 📜 License

This project is built for educational and social impact purposes.

---

<p align="center">
  <strong>🌱 Because every village deserves to breathe clean air and make informed farming decisions.</strong>
</p>
