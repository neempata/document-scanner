# OpenCV Document Scanner

A computer vision application that automatically detects documents within an image, corrects perspective distortion, and produces a clean, high-contrast scanned version suitable for reading, printing, or archiving.

Built with OpenCV and Python, this project demonstrates a complete document scanning pipeline using edge detection, contour analysis, perspective transformation, and adaptive image thresholding.

## Project Overview

Flatbed scanners produce high-quality document scans but aren't always available. This project recreates much of that functionality using only a photograph taken with a camera or smartphone.

The scanner automatically identifies the document in an image, detects its boundaries, corrects perspective distortion, enhances local contrast, and generates a black-and-white scanned output that resembles a traditional document scan.

The application also includes a fallback mechanism that scans the entire image when a document boundary cannot be reliably detected, making it more robust when working with difficult images or cluttered backgrounds.

## Features

- Automatic document detection
- Edge detection using Canny
- Contour detection and polygon approximation
- Perspective correction
- Adaptive thresholding
- Local contrast enhancement using CLAHE
- Automatic output image generation
- Graceful fallback when no document contour is detected

## Technologies Used

- Python
- OpenCV
- NumPy
- Scikit-image
- imutils

## Image Processing Pipeline

### 1. Image Loading

The application loads the input image and resizes it while preserving its aspect ratio. Working on a resized image improves processing speed while maintaining the original image for the final transformation.

### 2. Edge Detection

The image is converted to grayscale before applying Gaussian Blur to reduce noise.

Canny Edge Detection is then used to identify strong edges, followed by a dilation step that strengthens document boundaries and improves contour detection.

### 3. Document Detection

The largest contours in the image are analyzed and approximated as polygons.

If a contour containing four vertices is found, it is assumed to represent the document.

If no suitable contour is detected, the application automatically falls back to treating the entire image as the document instead of terminating with an error.

### 4. Perspective Transformation

Once the document corners have been identified, a perspective transformation is applied to generate a top-down view of the page.

The transformation matrix is calculated using OpenCV before warping the original high-resolution image.

### 5. Image Enhancement

The warped image is converted to grayscale before applying:

- CLAHE (Contrast Limited Adaptive Histogram Equalization)
- Adaptive Gaussian Thresholding

These techniques improve readability by increasing local contrast while producing the appearance of a scanned document.

### 6. Output Generation

The processed image is displayed alongside the original photograph and is automatically saved to disk with the filename:

```
scanned_<original_filename>
```

## Repository Structure

```
OpenCV-Document-Scanner/
│
├── scan.py
├── transform_opencv.py
├── README.md
├── requirements.txt
└── sample_images/
```

## Installation

Clone the repository:

```bash
git clone https://github.com/neempata/opencv-document-scanner.git
```

Install the required packages:

```bash
pip install -r requirements.txt
```

Run the application:

```bash
python scan.py --image path/to/document.jpg
```

Example:

```bash
python scan.py --image images/receipt.jpg
```

## Example Processing Pipeline

```
Original Image
       │
       ▼
Grayscale Conversion
       │
       ▼
Gaussian Blur
       │
       ▼
Canny Edge Detection
       │
       ▼
Contour Detection
       │
       ▼
Perspective Transformation
       │
       ▼
CLAHE Contrast Enhancement
       │
       ▼
Adaptive Thresholding
       │
       ▼
Final Scanned Document
```

## Results

The application successfully transforms photographs of documents into clean, high-contrast scanned images.

The final output includes:

- Corrected document perspective
- Improved readability
- Enhanced local contrast
- Automatic black-and-white scan
- Saved output image for future use

The fallback detection mechanism also allows the scanner to continue processing images where document boundaries cannot be confidently identified, making the application more robust across a wider variety of inputs.

## What I Learned

This project gave me practical experience with the fundamental concepts behind computer vision and digital image processing. I learned how multiple image processing techniques can be combined into a complete pipeline, where each stage contributes to improving the final result.

Building the scanner also strengthened my understanding of perspective transformations, contour detection, image enhancement, and the importance of designing software that can handle unexpected inputs gracefully. Rather than stopping when ideal conditions are not met, the application was designed to continue producing useful output whenever possible.

## Future Improvements

Some improvements I'd like to explore include:

- Automatic rotation correction
- Support for multiple documents in a single image
- Color document enhancement
- Shadow removal
- OCR integration using Tesseract
- Batch processing of multiple images
- Desktop GUI using PyQt or Tkinter
- Mobile-friendly interface

## License

This project is intended for educational and portfolio purposes.
