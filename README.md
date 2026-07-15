# Document Scanner

A Python-based document scanner that transforms photos of documents into clean, scanned-like images with perspective correction and image enhancement.

## Features

- **Automatic Document Detection**: Uses edge detection and contour analysis to locate documents in images
- **Perspective Correction**: Applies 4-point perspective transformation to get a top-down view
- **Image Enhancement**: 
  - Converts to grayscale
  - Applies CLAHE (Contrast Limited Adaptive Histogram Equalization) for better contrast
  - Uses local thresholding to create a "black and white" paper effect
- **Fallback Mode**: Handles edge cases where document detection fails by using the full image
- **Flexible Output**: Saves processed images with "scanned_" prefix

## Requirements

- Python 3.6+
- OpenCV (`cv2`)
- NumPy
- scikit-image
- imutils

## Installation

1. Clone or download this repository:
```bash
cd document_scanner
```

2. Install dependencies:
```bash
pip install opencv-python numpy scikit-image imutils
```

## Usage

Run the scanner with an image file:

```bash
python scan.py -i /path/to/image.jpg
```

### Arguments

- `-i`, `--image` (required): Path to the image file to be scanned

### Example

```bash
python scan.py -i photos/document.jpg
```

The script will:
1. Display edge detection results
2. Show the detected document outline
3. Display the original and scanned images side-by-side
4. Save the final result as `scanned_document.jpg` in the current directory

## How It Works

### Step 1: Edge Detection
- Resizes the image to 500px height for processing
- Converts to grayscale and applies Gaussian blur
- Uses Canny edge detection to find edges in the image

### Step 2: Contour Detection
- Finds contours in the edge-detected image
- Keeps the 5 largest contours and looks for a 4-point polygon
- This polygon represents the document corners

### Step 3: Perspective Transformation
- Uses the detected corners to apply a perspective transform
- Applies the transform to the original (full resolution) image
- This creates a top-down view of the document

### Step 4: Image Enhancement
- Converts to grayscale
- Applies CLAHE to improve local contrast
- Uses local thresholding to create a clear black-and-white effect

## Output

The processed image is saved with the filename pattern: `scanned_<original_filename>`

Example: If input is `photo.jpg`, output will be `scanned_photo.jpg`

## Project Structure

```
document_scanner/
├── scan.py                 # Main script
├── transform_opencv.py     # Perspective transformation utilities
├── images/                 # Sample images directory
└── README.md              # This file
```

## Troubleshooting

### Image not found error
- Check that the file path is correct
- Use absolute paths or ensure the file is in the correct location

### No 4-point contour found warning
- This is normal for complex backgrounds
- The script will fall back to using the entire image as the document
- Try with a simpler background or higher contrast

### Poor results
- Ensure good lighting in the original photo
- Try to capture the document at a more perpendicular angle
- Avoid busy backgrounds that may interfere with edge detection

## License

This project is provided as-is for educational purposes.

## Dependencies Details

- **OpenCV**: Computer vision library for image processing
- **NumPy**: Numerical computing library
- **scikit-image**: Image processing algorithms
- **imutils**: OpenCV utilities and convenience functions
