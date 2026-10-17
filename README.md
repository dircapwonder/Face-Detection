# Face Detection with OpenCV

A simple face detection project built with **Python** and **OpenCV** using the Haar Cascade classifier. It comes with two scripts: one that detects faces in a single image, and one that processes every `.jpg` image in the folder.

## Features

- Face detection with OpenCV's pre-trained Haar Cascade classifier
- Detects multiple faces in one image (portraits and group photos)
- Draws a bounding box around every detected face
- Batch mode that goes through all `.jpg` files in the project folder automatically

## Project Structure

```text
Face-Detection/
├── single_face_detect.py                  # Detects faces in one image
├── multiple_face_detect.py                # Detects faces in all .jpg images in the folder
├── haarcascade_frontalface_default.xml    # Haar Cascade classifier for frontal faces
├── 1.jpg ... 7.jpg                        # Sample images
└── README.md
```

## Requirements

- Python 3.8+
- OpenCV

```bash
pip install opencv-python
```

## Usage

### Single image

```bash
python single_face_detect.py
```

The script reads `5.jpg`, detects the faces in it, draws a box around each one, and shows the result in a window. Press any key to close the window. To use another image, change the file name in this line of the script:

```python
img = cv2.imread('5.jpg')
```

### Multiple images

```bash
python multiple_face_detect.py
```

The script finds all `.jpg` files in the current folder, runs the detection on each one, and shows every result for 2 seconds. This script loads `haarcascade_frontalface_default.xml` from the project folder, so keep the file next to the script.

> **Note:** `cv2.imshow` opens a window, so both scripts need a desktop environment. They will not display anything on a headless server.

## How It Works

1. The image is read with `cv2.imread()` and converted to grayscale with `cv2.cvtColor()`, since the classifier works on grayscale images.
2. `detectMultiScale()` scans the image at several scales and returns the position and size `(x, y, w, h)` of every region that looks like a face.
3. `cv2.rectangle()` draws a box around each detected face.
4. `cv2.imshow()` displays the result.

### Detection parameters

```python
faces = face_cascade.detectMultiScale(gray, scaleFactor=1.1, minNeighbors=5)
```

| Parameter | Value | Meaning |
|---|---|---|
| `scaleFactor` | `1.1` | How much the image is shrunk at each scale. Smaller values can find more faces but are slower. |
| `minNeighbors` | `5` | How many neighboring detections are needed to accept a face. Higher values reduce false positives but may miss real faces. |

## Example Results

With the default settings, the included sample images give these results:

| Image type | Result |
|---|---|
| Portraits (`1.jpg` to `5.jpg`) | One face detected in each image |
| Group photo (`6.jpg`) | 6 of the 7 faces detected |
| Group photo (`7.jpg`) | 4 of the 5 faces detected |

## Limitations

- Haar Cascades work best on **frontal, well-lit faces**. Faces that are turned, tilted, or partly covered (for example by hair or hands) can be missed, as the group photos show.
- The classifier can sometimes mark non-face regions as faces. Adjusting `minNeighbors` helps.
- `multiple_face_detect.py` only looks for `.jpg` files. To include PNG files as well, change the search line to:

  ```python
  all_images = glob.glob("*.jpg") + glob.glob("*.png")
  ```

- In `multiple_face_detect.py`, an image with no detected faces can show the previous image's result, because the result variable is only updated when a face is found.

## Ideas for Improvement

- Save the annotated images to a folder instead of only displaying them
- Take the image path as a command-line argument
- Fix the no-face case in the multiple-image script
- Try a deep-learning detector (such as OpenCV's DNN module) for better accuracy
- Add real-time detection from a webcam

## Credits

- Face detection with [OpenCV](https://opencv.org/). The Haar Cascade file `haarcascade_frontalface_default.xml` is distributed with OpenCV and keeps its original license notice.

## Disclaimer

This project is for educational and learning purposes only. The sample images are used for demonstration and belong to their respective copyright holders. Replace them with your own images if you reuse this project.
