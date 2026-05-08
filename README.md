# 🚗 Automatic Number Plate Recognition (ANPR) System

An AI-powered Automatic Number Plate Recognition (ANPR) system built using **YOLOv8**, **OpenCV**, **EasyOCR**, and **SORT Tracking**.

This project detects vehicles in video streams, tracks them across frames, identifies license plates, extracts plate text using OCR, and generates a fully annotated output video with tracking information and a visual dashboard.

---

# ✨ Features

- 🚘 Real-time vehicle detection using YOLOv8
- 🔍 Custom license plate detection model
- 🧠 Vehicle tracking with SORT + Kalman Filters
- 🔠 OCR-based license plate recognition using EasyOCR
- 🛠️ Intelligent text correction and formatting
- 📈 Data interpolation for smoother tracking
- 🎥 Final annotated video rendering
- ⚡ Fast and lightweight pipeline

---

# 📂 Project Structure

```text
.
├── main.py                # Core execution: Detection and Tracking logic
├── util.py                # Helper functions: OCR, Formatting, and Matching
├── sort.py                # SORT tracking algorithm implementation
├── add_missing_data.py    # Interpolation script for data smoothing
├── visualize.py           # Final rendering script for video output
├── best.pt                # Custom YOLOv8 model for license plates
└── yolov8n.pt             # Pre-trained YOLOv8 model for vehicles (auto-downloaded)
```

---

# 🛠️ Installation

## 1️⃣ Clone or Download the Project

Extract all project files into a single directory.

---

## 2️⃣ Install Dependencies

It is highly recommended to use a **virtual environment** or **Conda environment**.

Install the required libraries:

```bash
pip install ultralytics opencv-python easyocr filterpy scipy pandas
```

---

# 📁 Required Files

Place the following files inside the project root directory:

| File | Description |
|------|-------------|
| `sample.mp4` | Input video file |
| `best.pt` | Custom-trained license plate detection model |

> ⚠️ Note: `yolov8n.pt` will be downloaded automatically during the first execution.

---

# ⚙️ Usage

The project follows a **3-step execution pipeline**.

You must run the scripts in the following order:

---

# 1️⃣ Step One — Video Processing

Run the main detection and tracking pipeline:

```bash
python main.py
```

## 🔍 What Happens?

- Detects vehicles frame-by-frame
- Assigns unique tracking IDs
- Detects license plates inside vehicles
- Reads plate text using OCR
- Saves raw detection results

## 📤 Output

```text
test.csv
```

Contains:
- Vehicle bounding boxes
- Plate coordinates
- OCR text
- Tracking IDs

---

# 2️⃣ Step Two — Data Smoothing & Interpolation

Run the interpolation script:

```bash
python add_missing_data.py
```

## 🧠 What Happens?

This stage improves tracking stability by:

- Filling missing detections
- Reducing flickering
- Smoothing bounding box movement
- Handling temporary detection failures caused by:
  - Motion blur
  - Fast movement
  - Poor lighting
  - Occlusion

## 📤 Output

```text
test_interpolated.csv
```

---

# 3️⃣ Step Three — Final Visualization

Generate the final annotated video:

```bash
python visualize.py
```

## 🎥 What Happens?

The visualization module:

- Draws vehicle bounding boxes
- Displays tracking IDs
- Adds detected plate text
- Creates a license plate dashboard
- Produces the final rendered video

## 📤 Output

```text
out.mp4
```

---

# 🧠 Technical Highlights

## 🚘 Two-Stage Detection Pipeline

The system improves accuracy using a **hierarchical detection approach**:

1. Detect the vehicle first
2. Search for the license plate only inside the detected vehicle region

This reduces:
- False positives
- Background noise
- Unnecessary OCR operations

---

## 📍 Vehicle Tracking with SORT

Vehicle tracking is implemented using:

- **SORT (Simple Online Realtime Tracking)**
- **Kalman Filters**
- **Hungarian Assignment Algorithm**

This allows:
- Stable vehicle IDs
- Continuous tracking across frames
- Efficient real-time performance

---

## 🔠 OCR & Smart Text Formatting

License plate text is extracted using **EasyOCR**.

The project also includes a custom formatting pipeline that:

- Corrects common OCR mistakes
- Validates plate structure
- Standardizes output formatting

### Example Corrections

| Incorrect | Correct |
|-----------|---------|
| `O` | `0` |
| `I` | `1` |
| `S` | `5` |

---

## 📈 Data Interpolation

Interpolation is implemented using **SciPy** to smooth tracking results across frames.

This ensures:
- Smooth bounding box movement
- Better visualization quality
- Reduced flickering
- Recovery from temporary missed detections

---

# 🧰 Technologies Used

| Technology | Purpose |
|------------|---------|
| Python | Core programming language |
| YOLOv8 | Object detection |
| OpenCV | Video processing |
| EasyOCR | Text recognition |
| SORT | Vehicle tracking |
| Pandas | Data handling |
| SciPy | Interpolation & smoothing |

---

# 🎯 Final Output

The generated video includes:

- ✅ Vehicle tracking
- ✅ License plate detection
- ✅ OCR text recognition
- ✅ Real-time annotations
- ✅ Smoothed visualization
- ✅ License plate dashboard

Final file:

```text
out.mp4
```

---

# 🚀 Future Improvements

Potential enhancements for the project:

- Real-time webcam support
- Speed estimation
- Multi-camera tracking
- Database integration
- Web dashboard
- Arabic license plate recognition
- Deployment with Flask/FastAPI

---

# 👨‍💻 Author

Developed as an AI-based Computer Vision project using modern deep learning and tracking techniques.

---
