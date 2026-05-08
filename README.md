# Automatic Number Plate Recognition (ANPR) System

A robust, multi-stage pipeline for detecting and recognizing vehicle license plates in video streams using YOLOv8, SORT tracking, and EasyOCR.

## 🚀 Overview
This project implements a complete computer vision pipeline that:
1.  **Detects Vehicles:** Identifies cars, trucks, and buses using a pre-trained YOLOv8 model.
2.  **Tracks Vehicles:** Assigns a unique ID to each vehicle using the SORT (Simple Online and Realtime Tracking) algorithm to maintain consistency across frames.
3.  **Detects License Plates:** Locates the license plate area within the detected vehicle using a custom-trained YOLOv8 model (`best.pt`).
4.  **Recognizes Text:** Extracts alphanumeric characters from the plate using EasyOCR with custom formatting and error-correction logic.
5.  **Refines Data:** Uses linear interpolation to fill in gaps where the model might have missed a plate in a few frames.
6.  **Visualizes Results:** Generates a final video with professional overlays showing the tracked vehicle and its recognized license plate.

## 📁 Project Structure
```text
.
├── main.py                # Core execution: Detection and Tracking logic
├── util.py                # Helper functions: OCR, Formatting, and Matching
├── sort.py                # SORT tracking algorithm implementation
├── add_missing_data.py    # Interpolation script for data smoothing
├── visualize.py           # Final rendering script for video output
├── best.pt                # Custom YOLOv8 model for license plates
└── yolov8n.pt             # Pre-trained YOLOv8 model for vehicles (auto-downloaded)

##🛠️ Installation
Clone or Download the project:
Extract all files into a single directory.

## Install dependencies:
It is recommended to use a virtual environment or Conda.
pip install ultralytics opencv-python easyocr filterpy scipy pandas

##⚙️ Usage
The project follows a 3-step execution pipeline. You must run these scripts in the following order:

Step 1: Processing the Video
Run the main detection and tracking script. This will process the video frame-by-frame and generate a raw test.csv file.
python main.py

step 2: Smoothing the Data
Run the interpolation script to fill missing frames and fix "flickering" detections. This generates test_interpolated.csv.
python add_missing_data.py

Step 3: Generating Final Output
Run the visualization script to produce the final video (out.mp4) with all graphical overlays and the cropped plate dashboard.
python visualize.py

##🧠 Technical Highlights
Two-Stage Detection: Improves accuracy by first finding the vehicle and then looking for the plate within that specific region.

Custom OCR Logic: Includes a mapping dictionary (e.g., 'O' to '0', 'I' to '1') and strict format validation to handle common OCR misidentifications.

Data Interpolation: Uses Scipy to ensure bounding boxes follow the car smoothly even if the detector fails for a few frames due to lighting or motion blur.

