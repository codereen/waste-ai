# WasteAI 🗑️

A real-time waste classification app that uses computer vision to identify objects through your camera and tell you how to dispose of them — running entirely in the browser with no backend, no server, and no data ever leaving your device.

**[Live Demo →](https://codereen.github.io/waste-ai)**

---

## What it does

Point your camera at any object, then hover over it (desktop) or tap it (mobile) to classify it as:

- ♻️ **Recyclable** — bottles, glass, metal utensils, paper, cardboard
- 🌱 **Organic** — food scraps, fruit, garden waste
- 🗑️ **General waste** — e-waste, mixed materials

A confidence score is shown for each detection, and a session counter tracks how many items of each type you've classified.

---

## How it works

The app uses two browser-based machine learning libraries — no API calls, no cloud processing:

- **[TensorFlow.js](https://www.tensorflow.org/js)** — runs ML model inference directly in the browser
- **[COCO-SSD](https://github.com/tensorflow/tfjs-models/tree/master/coco-ssd)** (MobileNet v2 backbone) — a pre-trained object detection model that identifies 80 object classes in real time

On each animation frame, COCO-SSD scans the full video feed and returns bounding boxes with class labels and confidence scores. A lookup table then maps detected classes (e.g. `"bottle"`, `"banana"`, `"laptop"`) to waste categories. Only the object your cursor or finger is on gets highlighted and counted — everything else is dimmed.

```
Camera feed → TensorFlow.js → COCO-SSD detection → waste category mapping → canvas overlay
```

---

## Features

- 🎥 Live webcam feed with real-time bounding boxes
- 🖱️ Hover to select on desktop / tap to select on mobile
- 📊 Session stats (total detected, recyclable, organic)
- 🔒 100% client-side — no data sent anywhere
- 📱 Responsive — works on desktop and mobile browsers
- ⚡ No install, no build step — single HTML file

---

## Tech stack

| Technology | Purpose |
|---|---|
| HTML / CSS / JavaScript | UI and app logic |
| TensorFlow.js 4.17 | In-browser ML inference |
| COCO-SSD 2.2 (MobileNet v2) | Object detection model |
| Canvas API | Bounding box rendering |
| MediaDevices API | Webcam access |

---

## Run locally

No install needed. Just clone and open:

```bash
git clone https://github.com/codereen/waste-ai.git
cd waste-ai
open index.html   # or just drag the file into your browser
```

> **Note:** camera access requires a secure context. If opening the file directly doesn't work, serve it locally:
> ```bash
> python3 -m http.server 8000
> # then visit http://localhost:8000
> ```

---

## Limitations

- COCO-SSD was trained on 80 general object classes, not specifically on waste — so detection accuracy varies. A custom-trained model on waste datasets (e.g. TrashNet, TACO) would significantly improve results.
- Hover/tap interaction means the stats reflect intentional classifications, not passive scanning.
- Works best in good lighting with objects held clearly in frame.

---

## Background

Built as a portfolio project alongside a research report on *AI for Sustainable Waste Management* for AAI202 Applications of Artificial Intelligence at Torrens University Australia. The report examines how computer vision, machine learning, and robotics (AMP Robotics, Greyparrot, ZenRobotics) are being applied to real-world waste collection and recycling challenges.

---

## License

MIT — free to use, modify, and build on.
