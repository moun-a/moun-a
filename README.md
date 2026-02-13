<div align="center">

```ascii
╔═══════════════════════════════════════════════════════════════╗
║                                                               ║
║   ███████╗███╗   ███╗██████╗ ███████╗██████╗ ██████╗ ███████╗║
║   ██╔════╝████╗ ████║██╔══██╗██╔════╝██╔══██╗██╔══██╗██╔════╝║
║   █████╗  ██╔████╔██║██████╔╝█████╗  ██║  ██║██║  ██║█████╗  ║
║   ██╔══╝  ██║╚██╔╝██║██╔══██╗██╔══╝  ██║  ██║██║  ██║██╔══╝  ║
║   ███████╗██║ ╚═╝ ██║██████╔╝███████╗██████╔╝██████╔╝███████╗║
║   ╚══════╝╚═╝     ╚═╝╚═════╝ ╚══════╝╚═════╝ ╚═════╝ ╚══════╝║
║                                                               ║
║              → Architecting Intelligence at the Edge ←       ║
║                                                               ║
╚═══════════════════════════════════════════════════════════════╝
```

**`$ whoami`** → Embedded Systems Engineer | Real-Time Architect | Edge AI Developer

[![Typing SVG](https://readme-typing-svg.demolab.com?font=JetBrains+Mono&size=16&duration=3000&pause=1000&color=39FF14&center=true&vCenter=true&width=600&lines=Building+production+systems+that+ship;From+silicon+to+cloud+and+everything+between;Real-time+%E2%89%A0+fast+enough;Hardware+constraints+breed+software+creativity)](https://git.io/typing-svg)

</div>

---

## `> cat status.txt`

```diff
+ Currently: Building distributed sensor networks with LoRaWAN mesh topology
+ Learning: Rust for embedded (because C is great, but memory safety is greater)
+ Reading: "The Art of Designing Embedded Systems" - Jack Ganssle
- Not doing: Blocking operations in ISRs (we've all been there)
! Warning: May talk excessively about RTOS task priorities
```

---

## `> ls -la ~/projects`

```bash
drwxr-xr-x  12 engineer  staff   384B  Feb 14 2026  .
drwxr-xr-x   8 engineer  staff   256B  Jan 15 2026  ..
-rw-r--r--   1 engineer  staff   64KB  Feb 10 2026  ecocold/
-rw-r--r--   1 engineer  staff   48KB  Jan 28 2026  secure-entry/
-rw-r--r--   1 engineer  staff   92KB  Dec 15 2025  vision-guard/
-rw-r--r--   1 engineer  staff   36KB  Nov 20 2025  mesh-network/
```

### **`./ecocold` — Industrial Cold Chain Monitoring**
<sup>ESP32 • LoRaWAN • FreeRTOS • MQTT • InfluxDB</sup>

Multi-node sensor network for temperature-critical logistics. Battery life: 6+ months on 2500mAh.

**The Problem:** Traditional cold chain monitoring relies on centralized systems—single point of failure, expensive infrastructure, limited range.

**The Solution:** Decentralized mesh where each node acts as a relay. Self-healing topology with automatic route discovery.

```c
// Power consumption optimization: deep sleep between readings
void sensor_task(void *pvParameters) {
    while(1) {
        read_sensors();
        transmit_data();
        esp_deep_sleep(30 * 60 * 1000000); // 30 min sleep
        // Actual avg consumption: 0.15mA in deep sleep
    }
}
```

**Key Metrics:** 
- 📡 15km range in rural areas (LoRa SF12)
- ⚡ 0.15mA deep sleep current
- 📊 <100ms latency for critical alerts
- 🔋 Projected 8-month battery life in production

[→ View Repository](#) · [→ Technical Writeup](#)

---

### **`./secure-entry` — RFID Access Control System**
<sup>ESP8266 • MFRC522 • MySQL • AES-256 • WebSockets</sup>

Built this to solve the "campus access card vs forgotten phone" problem. Decentralized auth with offline fallback.

**Architecture:**
```
┌─────────────┐      HTTPS/TLS      ┌──────────────┐
│ RFID Reader │ ←─────────────────→ │ Auth Server  │
│  (ESP8266)  │                     │  (Flask API) │
└─────────────┘                     └──────────────┘
       │                                    │
       │ Offline Mode:                     │
       │ Local whitelist                   │
       │ AES-encrypted                     │
       └────────────────────────────────────┘
```

**Why It's Different:**
- Works offline with cached credentials (30-day TTL)
- Real-time WebSocket notifications (door events stream to dashboard)
- Zero-trust model: every swipe requires fresh token validation
- Tamper detection with immediate lockdown

**Performance:**
- Average swipe-to-unlock: 280ms
- 99.97% uptime over 6 months
- Handled 12K+ authentications

[→ View Repository](#) · [→ System Diagram](#)

---

### **`./vision-guard` — Edge AI Surveillance**
<sup>Raspberry Pi 4 • Coral TPU • YOLOv8 • OpenCV • TensorFlow Lite</sup>

Privacy-first surveillance that never sends video to the cloud. All inference happens on-device.

**The Challenge:** Traditional IP cameras send everything to the cloud. Privacy nightmare, bandwidth hog, latency issues.

**The Approach:**
```python
# Optimized inference pipeline
def process_frame(frame):
    # Preprocessing on CPU
    preprocessed = cv2.resize(frame, (416, 416))
    
    # Inference on Coral TPU (15ms avg)
    detections = model.detect(preprocessed)
    
    # Only transmit alerts, never raw video
    if is_anomaly(detections):
        send_alert(metadata_only=True)  # No images, just bbox coords
```

**Benchmarks:**
| Model | Hardware | FPS | Latency | Power |
|-------|----------|-----|---------|-------|
| YOLOv8n | RPi 4 CPU | 12 | 83ms | 6W |
| YOLOv8n | Coral TPU | 85 | 12ms | 8W |
| YOLOv5s | Coral TPU | 62 | 16ms | 8W |

**Privacy Features:**
- ✅ 100% local processing
- ✅ No cloud uploads (ever)
- ✅ Encrypted storage with automatic 7-day purge
- ✅ Face detection without identification

[→ View Repository](#) · [→ Performance Analysis](#)

---

## `> cat ~/tech_stack.json`

```json
{
  "languages": {
    "expert": ["C", "Python"],
    "proficient": ["C++", "JavaScript"],
    "learning": ["Rust"]
  },
  "embedded": {
    "microcontrollers": ["STM32F4/H7", "ESP32-S3", "nRF52840", "RP2040"],
    "rtos": ["FreeRTOS", "Zephyr", "ThreadX"],
    "protocols": ["I2C", "SPI", "UART", "CAN", "Modbus RTU"],
    "tools": ["STM32CubeIDE", "PlatformIO", "Segger J-Link", "Logic Analyzer"]
  },
  "iot": {
    "wireless": ["LoRaWAN", "BLE 5.0", "WiFi 6", "Zigbee", "Thread"],
    "application": ["MQTT", "CoAP", "HTTP/2", "WebSockets"],
    "edge_computing": ["Edge Impulse", "TensorFlow Lite Micro", "ONNX Runtime"]
  },
  "ai_ml": {
    "frameworks": ["TensorFlow", "PyTorch", "ONNX"],
    "computer_vision": ["OpenCV", "YOLOv8", "MediaPipe"],
    "optimization": ["Quantization", "Pruning", "Knowledge Distillation"]
  },
  "backend": {
    "databases": ["PostgreSQL", "InfluxDB", "TimescaleDB", "Redis"],
    "message_brokers": ["Mosquitto", "RabbitMQ", "Apache Kafka"],
    "containers": ["Docker", "Docker Compose"]
  }
}
```

---

## `> git log --all --graph --oneline`

```
* b4e8f92 (HEAD -> main) Optimized LoRa packet structure: 51B → 23B (55% reduction)
* a7d3c14 Implemented Kalman filter for sensor fusion (DHT22 + DS18B20)
* 9f2e8a1 Added OTA firmware updates with rollback capability
* 7c5b3f0 Migrated from Arduino framework to ESP-IDF for better control
* 6a4d2e8 Reduced power consumption: 45mA → 0.15mA in deep sleep
* 5b1c7f3 Implemented AES-CTR encryption for LoRa payloads
* 4a0e6d2 Built custom PCB with auto-routing and impedance matching
* 3d9f5e1 Added hardware watchdog timer for fault recovery
* 2c8e4f0 Implemented priority-based task scheduler for FreeRTOS
* 1b7d3e9 Initial commit: bare-metal UART driver for STM32
```

---

## `> cat ~/philosophy.md`

**On Real-Time Systems:**
> "Real-time doesn't mean fast. It means deterministic. I'd rather have guaranteed 10ms than unpredictable 5ms."

**On Optimization:**
> "Premature optimization is the root of all evil. But we're past premature—we're in production."

**On Embedded Constraints:**
> "64KB of RAM teaches you more about efficient algorithms than any textbook ever will."

**On Documentation:**
```c
// Code should be self-documenting, they said.
// Then I had to debug my 6-month-old interrupt handler.
// Now I comment like I'm writing a novel.
```

---

## `> top` — Active Processes

```
PID    PROCESS                        STATUS    PRIORITY
────────────────────────────────────────────────────────
1001   learning_rust_embedded         RUNNING   HIGH
1002   optimizing_power_consumption   RUNNING   HIGH  
1003   designing_pcb_v2               RUNNING   MEDIUM
1004   writing_technical_blog         RUNNING   LOW
1005   contributing_to_zephyr_rtos    WAITING   MEDIUM
1006   reading_arm_cortex_m7_manual   RUNNING   LOW
```

---

## `> netstat -an` — Connect With Me

```bash
Protocol  Local Address           Status      
────────────────────────────────────────────
TCP       linkedin.com:443        LISTENING   # https://linkedin.com/in/YOUR_PROFILE
TCP       github.com:443          ESTABLISHED # https://github.com/YOUR_USERNAME  
TCP       email:587               LISTENING   # your.email@example.com
TCP       portfolio:443           LISTENING   # https://your-portfolio.com
```

---

## `> df -h` — GitHub Stats

<div align="center">

<img src="https://github-readme-stats.vercel.app/api?username=YOUR_USERNAME&show_icons=true&theme=dark&bg_color=0d1117&title_color=39ff14&text_color=c9d1d9&icon_color=39ff14&border_color=30363d&hide_border=false&include_all_commits=true&count_private=true" width="48%" />
<img src="https://github-readme-streak-stats.herokuapp.com?user=YOUR_USERNAME&theme=dark&background=0d1117&ring=39ff14&fire=39ff14&currStreakLabel=39ff14&border=30363d" width="48%" />

</div>

<div align="center">
<img src="https://github-readme-stats.vercel.app/api/top-langs/?username=YOUR_USERNAME&layout=compact&theme=dark&bg_color=0d1117&title_color=39ff14&text_color=c9d1d9&border_color=30363d&hide_border=false&langs_count=8" width="48%" />
</div>

---

## `> cat /proc/contributions`

```
█████████░░░░░░░░░░░░░░░░░░░ 35% ESP-IDF
████████░░░░░░░░░░░░░░░░░░░░ 28% Zephyr RTOS  
██████░░░░░░░░░░░░░░░░░░░░░░ 18% TensorFlow Lite Micro
████░░░░░░░░░░░░░░░░░░░░░░░░ 12% PlatformIO Core
██░░░░░░░░░░░░░░░░░░░░░░░░░░  7% Open-Source PCB Libraries
```

---

## `> crontab -l` — Automated Habits

```bash
0  9  * * *  /usr/local/bin/read_datasheets.sh
0  14 * * *  /usr/local/bin/code_review.sh
0  20 * * *  /usr/local/bin/optimize_something.sh
0  23 * * *  /usr/local/bin/git_commit.sh "daily progress"
*/30 * * * *  /usr/local/bin/check_running_systems.sh
```

---

## `> tail -f /var/log/interests.log`

```log
[2026-02-14 09:23:15] INFO: Exploring RISC-V for embedded applications
[2026-02-14 10:47:32] INFO: Experimenting with ESP32-C6 (WiFi 6 + Zigbee)
[2026-02-14 14:15:08] INFO: Reading about LVGL for embedded GUIs
[2026-02-14 16:39:44] INFO: Optimizing TinyML models for microcontrollers
[2026-02-14 18:22:11] INFO: Designing custom LoRa antenna for 868MHz
[2026-02-14 20:51:37] INFO: Contributing to Rust embedded WG discussions
```

---

<div align="center">

```
┌─────────────────────────────────────────────────────────┐
│                                                         │
│  "The best code is the code that ships—on time,        │
│   on budget, and on a microcontroller with 32KB RAM."  │
│                                                         │
│                               — Unknown Embedded Dev    │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

![Visitor Count](https://komarev.com/ghpvc/?username=YOUR_USERNAME&color=39ff14&style=flat-square&label=VISITORS)

**`> exit`**

</div>
