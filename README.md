# WildGuard-Autonomy Lab 🛰️🦋

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![YOLO](https://img.shields.io/badge/YOLOv8-Ultralytics-orange)](https://github.com/ultralytics/ultralytics)
[![DroneKit](https://img.shields.io/badge/MAVLink-DroneKit-green)](https://github.com/dronekit/dronekit-python)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

> **YOLO detection → rule → MAVLink action.**  
> Minimal lab for conservation robotics: capture video → detect objects with YOLO → apply a rule (e.g., “if person seen for 5 frames”) → send a command (RTL/LOITER) to an autopilot (SITL or real Pixhawk) via MAVLink/DroneKit.

![Architecture](diagrams/arch.svg)

---

## ✨ Features
- Runs on **PC (Linux/macOS/Windows WSL2)** or **Raspberry Pi 4/5**  
- **YOLOv8 (Ultralytics)** for real-time detection (CPU or GPU)  
- **DroneKit/MAVLink** for autonomy commands  
- Works with **ArduPilot SITL** or a **real Pixhawk**  
- Simple CSV logging + debounce rules  

---

## 📂 Repo Layout
```

wildguard-autonomy-lab/
├─ README.md
├─ requirements.txt
├─ detect\_autonomy.py         # main script: YOLO + DroneKit
├─ diagrams/
│  └─ arch.svg                # architecture diagram
├─ scripts/
│  ├─ start\_sitl.sh
│  ├─ run\_detector.sh
│  ├─ start\_all.sh
│  └─ run\_detector.ps1
└─ utils/
└─ classes\_coco80.txt

````

---

## 🚀 Quick Start

### A) PC (Linux/macOS or Windows via WSL2)
```bash
# clone repo
git clone https://github.com/yz1295/WildGuard-Autonomy-Lab.git
cd WildGuard-Autonomy-Lab

# create virtual env + deps
make all

# start SITL (new terminal) + detector
./scripts/start_all.sh
````

### B) Raspberry Pi 4/5

```bash
sudo apt update
sudo apt install -y python3-pip python3-venv python3-opencv libatlas-base-dev

git clone https://github.com/yz1295/WildGuard-Autonomy-Lab.git
cd WildGuard-Autonomy-Lab

python3 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt

# Connect to Pixhawk via USB
python detect_autonomy.py --source 0 --connect /dev/ttyACM0 --baud 57600 --trigger-class person --action LOITER
```

---

## 🎛️ Options

Main script (`detect_autonomy.py`) supports:

```
--source        0 | path | rtsp        # webcam=0, file path, or RTSP stream
--model         yolov8n.pt             # YOLO model
--conf          0.35                   # detection threshold
--trigger-class person                 # class to watch for
--trigger-conf  0.60                   # min conf to trigger
--hold-frames   5                      # debounce (frames before trigger)
--connect       127.0.0.1:14550        # MAVLink endpoint or serial port
--baud          57600                  # baud if using serial
--action        RTL | LOITER | NONE    # autopilot mode to set
```

---

## 🧪 Demo Flow

1. Start SITL (ArduCopter) or connect to Pixhawk.
2. Run `detect_autonomy.py`.
3. Show webcam → when a **person** enters frame:

   * YOLO detects with conf >0.6 for 5 frames.
   * Script logs detection + sends `RTL` (or LOITER).
   * SITL console / Mission Planner shows autopilot mode switch.

Output logs in:

```
runs/wildguard/detections.csv
```

---

## ⚠️ Troubleshooting

* **No GPU?** Use `yolov8n.pt` (nano model).
* **Torch install fails on Pi:** use Raspberry Pi OS 64-bit, or export YOLOv5n to ONNX and run with OpenCV DNN.
* **Serial not found:** on Linux, Pixhawk is usually `/dev/ttyACM0` or `/dev/ttyUSB0`; on Windows use `COM7`.
* **SITL only on Linux/WSL2:** Windows users should run SITL inside WSL2 Ubuntu.

---

## 👤 Author

**Yiran Zhang**

* 🎓 Graduate Student, Electrical & Computer Engineering, McMaster University
* 🔧 Embedded Systems & Cybersecurity Projects: STM32, FreeRTOS, ESP32, IoT, AI/ML...
* 🌐 GitHub: [yz1295](https://github.com/yz1295)
* 💼 Focus: Autonomous systems, embedded software, AI for edge devices

---

## 📜 License

* Code: MIT
* Models: [Ultralytics YOLO](https://github.com/ultralytics/ultralytics) license applies
* Uses ArduPilot (GPLv3) & DroneKit (Apache 2.0)

---

## 🙌 Acknowledgments

* [Ultralytics](https://github.com/ultralytics) for YOLOv8
* [ArduPilot](https://github.com/ArduPilot/ardupilot) for SITL + flight stack
* [DroneKit](https://github.com/dronekit/dronekit-python)

---

**WildGuard-Autonomy Lab** 🛰️ — a simple but powerful demo showing how AI can make drones smarter for conservation.

```

---

✨ This version now includes:
- Badges (Python, YOLOv8, DroneKit, License).  
- Clear repo URL (`yz1295/WildGuard-Autonomy-Lab`).  
- **Author section with your name + GitHub.**  
- A polished structure that looks professional on GitHub.  


