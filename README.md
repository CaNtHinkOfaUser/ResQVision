# ResQVision
#### Report: [https://docs.google.com/document/d/1l-hyJfFRXItIPHYwDCEK0mPhddvvDSbjZcy9AnIE4mM/edit?tab=t.0](url)
Autonomous Disaster Response System powered by YOLO object detection, Raspberry Pi, and Arduino integration.

## Overview

ResQVision is a computer vision system designed for autonomous disaster-response robotics. The system identifies disaster types from visual markers and assists in warehouse resource assessment through real-time medkit counting.

The project consists of two independent deep-learning pipelines using YOLO26 Nano Architecture:

### Model 1 — Disaster Classification

Detects and classifies:

* Tsunami
* Earthquake
* Fire

When a target disaster class is detected, the Raspberry Pi communicates with an Arduino through serial communication, allowing the robot to respond appropriately.

### Model 2 — Medkit Counting

Detects and counts medkits inside a warehouse environment.

To improve robustness, detections are aggregated over time and the modal count is written to a text file, reducing fluctuations caused by frame-to-frame detection noise.

---

## Features

* Real-time object detection on Raspberry Pi
* YOLO-based disaster classification
* Arduino integration through serial communication
* Temporal confirmation filtering to reduce false triggers
* Real-time medkit counting
* Robustness against lighting and viewpoint variations
* Dataset augmentation pipeline
* Approximately 10 FPS inference on Raspberry Pi hardware

---

## System Architecture

```text
Camera
   │
   ▼
YOLO Disaster Model
   │
   ▼
Temporal Confirmation Filter
   │
   ▼
Raspberry Pi
   │
   ▼
Serial Communication
   │
   ▼
Arduino
   │
   ▼
Robot Response
```

### Medkit Pipeline

```text
Camera
   │
   ▼
YOLO Medkit Model
   │
   ▼
Frame-by-Frame Counting
   │
   ▼
Mode-Based Stabilisation
   │
   ▼
Text File Output
```

---

## Dataset Development

### Disaster Classification Dataset

* 706 original images
* ~1900 images after augmentation

Augmentations used:

* Rotation
* Blur
* Brightness adjustment
* Saturation adjustment
* Grayscale conversion
* Noise injection

### Medkit Dataset

* Approximately 170 manually annotated images
* 408 total images after augmentation

##

## Performance

### Disaster Classification Model

| Metric          | Score   |
| --------------- | ------- |
| Precision       | 98.5%   |
| Recall          | 90.3%   |
| F1 Score        | 94.2%   |
| mAP@50          | 96.5%   |
| Inference Speed | ~10 FPS |

### Medkit Counting Model

| Metric    | Score |
| --------- | ----- |
| Precision | 94.7% |
| Recall    | 100%  |
| F1 Score  | 97.3% |
| mAP@50    | 99.1% |

---

## Hardware

* Raspberry Pi
* Arduino
* Raspberry Pi Camera
* USB Camera (optional)

---

## Software Stack

* Python
* OpenCV
* Ultralytics YOLO
* NumPy
* PySerial

---

## Installation

```bash
git clone https://github.com/<username>/SentinelDR.git
cd SentinelDR

pip install ultralytics
pip install opencv-python
pip install numpy
pip install pyserial
```

---

## Running Disaster Detection

```bash
python disaster_detection.py \
--model best.pt \
--source picamera0 \
--thresh 0.15
```

---

## Running Medkit Counting

```bash
python medkit_counter.py \
--model best.pt \
--source picamera0 \
--thresh 0.04
```

---

##
