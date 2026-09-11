# Image & Text Recognition System (OCR)

A Python-based Optical Character Recognition (OCR) system built as part of the DecodeLabs AI Engineering Internship (Project 4). It takes a sample image, runs it through a computer vision preprocessing pipeline, and extracts readable text using a pre-trained OCR engine — with confidence-based filtering and visual bounding box output.

## Overview

This project demonstrates how raw, unstructured image data (scanned documents, receipts, signs) can be converted into structured, machine-readable text. It bridges classical image processing (OpenCV) with a pre-trained recognition model (Tesseract OCR), and applies a minimum confidence threshold so the system only reports results it's actually sure about — a core principle in production AI systems.

## Features

- Image preprocessing pipeline: grayscale conversion, Gaussian blur, adaptive thresholding
- Text recognition using Tesseract OCR (`pytesseract`)
- Per-word confidence scoring with an 80% minimum threshold
- Bounding boxes and labels drawn directly on the image for high-confidence detections
- Side-by-side visualization of every preprocessing stage
- Overall output confidence score

## Tech Stack

- Python 3
- OpenCV (`cv2`) — image preprocessing
- Tesseract OCR + `pytesseract` — text recognition
- Matplotlib — visualization

## How It Works

1. **Load Image** — reads the sample image into memory.
2. **Preprocessing:**
   - Grayscale conversion — removes color, reduces data to one channel
   - Gaussian blur — smooths noise before thresholding
   - Adaptive thresholding — converts to clean black/white text, robust to uneven lighting
3. **OCR Recognition** — Tesseract scans the processed image and extracts text with per-word confidence scores.
4. **Confidence Filtering** — only words scoring ≥80% confidence are kept and highlighted.
5. **Visual Output** — bounding boxes and labels are drawn on the original image; all pipeline stages are displayed side by side.

## Installation & Usage (Google Colab)

```python
!apt-get install -y tesseract-ocr
!pip install pytesseract opencv-python-headless
```

Upload a sample image, then run the pipeline script. The output includes:
- Full extracted text
- List of high-confidence words with their scores
- Overall output confidence
- A 4-panel visual (original → grayscale → thresholded → labeled detections)

## Example Output

```
=== RECOGNIZED TEXT (full) ===
CASH RECEIPT
Item 1 ......... $4.99
Item 2 ......... $2.50
TOTAL ........... $7.49
THANK YOU

=== HIGH-CONFIDENCE WORDS (≥80%) ===
'CASH' — 91%
'RECEIPT' — 88%
'TOTAL' — 94%

Overall Output Confidence: 91.0%
```

## Project Structure

```
image-text-recognition/
├── ocr_recognition.py
├── sample_image.jpg
└── README.md
```

## Concepts Demonstrated

- Image preprocessing (grayscale, blur, thresholding)
- Pre-trained model integration (Tesseract)
- Confidence-based filtering to reduce false positives
- Visual/bounding box output for recognition results
- Handling real-world unstructured data (photos, scans, receipts)

## Known Limitations

- Low-resolution or thermal-printed receipts can produce degraded OCR accuracy — a documented limitation of Tesseract on small, low-contrast fonts rather than a pipeline bug.
- Skewed or crumpled source images benefit from an added deskewing step.
- Handwritten text is not reliably recognized — this system is optimized for printed text.

## Future Improvements

- Add automatic deskew correction for tilted images
- Add image upscaling for low-resolution inputs
- Swap in `cv2.dnn` + MobileNet-SSD for object detection mode
- Batch processing for multiple images at once

## Author

Built by Khadija as part of the DecodeLabs AI Engineering Internship, 2026 Batch.

## License

MIT
