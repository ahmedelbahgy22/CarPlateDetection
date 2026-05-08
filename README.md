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

