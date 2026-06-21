# 🛡️ FarmGuard AI – Autonomous Livestock Health Monitoring

**FarmGuard AI** is a comprehensive, end-to-end IoT and AI-driven platform designed to monitor livestock health in real time. Using sensor telemetry collected from microcontrollers and smart analysis, the platform detects physical and environmental anomalies, calculates an overall health index, and provides actionable insights and automated alerts to help farmers protect their herds, maximize yield, and prevent disease outbreaks.

---

## 📂 Project Structure

The repository is organized into two primary folders:

```
animal/
├── website/              # Frontend Web Application (HTML, CSS, JavaScript)
│   ├── css/              # Core stylesheets (style.css, landing.css, dashboard.css, alerts.css)
│   ├── js/               # Interactive frontend logic (landing.js, dashboard.js, alerts.js)
│   ├── index.html        # Landing page outlining features and architecture
│   ├── dashboard.html    # Glassmorphic, real-time data visualization dashboard
│   └── alerts.html       # Smart alerts log and detailed veterinary recommendations
│
├── wokwi/                # Hardware IoT Simulation Setup
│   ├── diagram.json      # Virtual wiring diagram for ESP32 and sensors
│   ├── libraries.txt     # List of Arduino libraries used in the simulation
│   └── sketch.ino        # ESP32 C++ source code with Blynk Cloud integration
│
└── README.md             # Project documentation (this file)
```

---

## ⚡ Core Features

1. **Real-Time Telemetry**: Live streams and visualizes animal vital signs and barn metrics (temperature, humidity, heart rate, physical movement, and air quality).
2. **AI Health Analysis**: Evaluates raw sensor data to generate a dynamic, composite health index (0–100) and outputs natural-language diagnostic summaries.
3. **Environmental Tracking**: Tracks ambient conditions and harmful gas levels (using MQ2) to warn of hazardous barn environments.
4. **Smart Alerts & Recommendations**: Classifies events into tiered severity levels (`HEALTHY`, `WARNING`, `CRITICAL`) and links them directly to veterinary recommendation logs.
5. **Modern Glassmorphic UI**: High-fidelity dark mode dashboard with responsive grid layouts, custom charts, and modern typography.

---

## 🔌 Hardware Simulation (Wokwi IoT)

The project includes a ready-to-run hardware simulation in the `wokwi/` directory.

### Simulated Sensors & Components
- **ESP32 Microcontroller**: Serves as the central IoT gateway.
- **DHT22 Sensor**: Monitors ambient temperature and humidity.
- **MPU6050 Accelerometer & Gyroscope**: Track livestock movement intensity (activity detection).
- **Potentiometer**: Simulates a live heart rate sensor (generating values between 60 and 150 BPM).
- **MQ2 Gas Sensor**: Detects hazardous gases/smoke inside the barn.

### Blynk Cloud Virtual Pin Mapping
The ESP32 pushes sensor telemetry to the Blynk Cloud every **3 seconds** using the following virtual pin layout:

| Virtual Pin | Parameter | Simulated Source | Value Range / Output |
| :---: | :--- | :--- | :--- |
| **V0** | Temperature | DHT22 Sensor | °C |
| **V1** | Heart Rate | Potentiometer | 60 – 150 BPM |
| **V2** | Gas Level | MQ2 Gas Sensor | 0 – 4095 (Analog reading) |
| **V3** | Movement | MPU6050 (Absolute Accelerometer sum) | Acceleration index |
| **V4** | Overall Status | Logic Engine | `HEALTHY`, `WARNING`, `CRITICAL` |

---

## 🛠️ Getting Started

### 1. Launching the Web Application
The frontend is built using standard, modern Vanilla Web Technologies (HTML5, CSS3, ES6 JavaScript) and does not require complex build steps or external bundlers:
- Navigate to the `website/` directory.
- Open `index.html` in any modern web browser to view the landing page.
- Navigate to `dashboard.html` to see the live telemetry interface and `alerts.html` to view safety diagnostics.

### 2. Deploying to Vercel
The project is configured for zero-config deployment to **Vercel** using the root-level [vercel.json](file:///c:/Users/USER/OneDrive/Desktop/animal/vercel.json):
- Push the repository to GitHub, GitLab, or Bitbucket.
- Import the repository in your [Vercel Dashboard](https://vercel.com/dashboard).
- Vercel will automatically read [vercel.json](file:///c:/Users/USER/OneDrive/Desktop/animal/vercel.json) and serve the `website/` directory as the output directory.
- Clean URLs are active, meaning paths like `/dashboard.html` will automatically route and redirect to clean paths like `/dashboard`.

### 3. Running the Hardware Simulation
To run the virtual hardware node:
1. Open the [Wokwi IoT Simulator](https://wokwi.com).
2. Create or import a project, and load the wiring configuration from `wokwi/diagram.json` and code from `wokwi/sketch.ino`.
3. Configure your Blynk Auth Token inside `sketch.ino`:
   ```cpp
   #define BLYNK_TEMPLATE_ID "TMPL3RYm45DWM"
   #define BLYNK_TEMPLATE_NAME "farmGuard AI"
   #define BLYNK_AUTH_TOKEN "YOUR_BLYNK_AUTH_TOKEN_HERE"
   ```
4. Start the simulation. The ESP32 will connect to `Wokwi-GUEST` virtual WiFi and stream telemetry to your Blynk dashboard.

---

## 🎨 Technology Stack
- **Frontend**: HTML5, Vanilla CSS (Glassmorphism, Flexbox, Grid, CSS Variables), Vanilla JavaScript (DOM APIs, Custom components).
- **IoT Firmware**: C++, Arduino Framework, WiFi, Blynk IoT SDK.
- **Sensors & hardware**: DHT Sensor Library, Adafruit MPU6050 Library, Adafruit Unified Sensor.
