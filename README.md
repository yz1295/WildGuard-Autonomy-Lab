# WildGuard-Autonomy-Lab
A minimal lab to show an autonomous loop: capture video → detect objects with YOLO → apply a rule → command a drone (SITL or real Pixhawk) via MAVLink/DroneKit.


1) Features

Runs on Windows (WSL2), Linux, macOS or Raspberry Pi 4/5

YOLOv8 (Ultralytics) for detection (CPU or GPU)

DroneKit/MAVLink to send actions (e.g., RTL, LOITER)

Works with ArduPilot SITL or real Pixhawk

Simple CSV logging + debounce (trigger only if condition holds N frames)


2) Repo layout
wildguard-autonomy-lab/
├─ README.md                 ← (this file)
├─ requirements.txt
├─ detect_autonomy.py        ← YOLOv8 + DroneKit integration (main)
├─ utils/
│  └─ classes_coco80.txt     ← COCO labels (for convenience)
└─ examples/
   └─ sample.jpg             ← any test image (optional)


requirements.txt

ultralytics>=8.1.0
opencv-python
dronekit
pandas
