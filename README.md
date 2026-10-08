# OpenCV Face Detection with Haar Cascade

A simple face detection project built with **Python** and **OpenCV** using the Haar Cascade Classifier.

This project contains two examples:

- Detecting faces in a single image
- Detecting faces in multiple **.jpg** images automatically

## Features
- Face detection using OpenCV
- Haar Cascade Classifier
- Grayscale image processing
- Detection of multiple faces
- Drawing bounding boxes around detected faces
- Automatic processing of multiple images

## Requirements

Make sure you have **Python 3.x** installed.

Install OpenCV with:
```
pip install opencv-python
```
## Project Structure
face-detection/

│

├── 1.jpg

├── haarcascade_frontalface_default.xml

├── single_face_detect.py

└── README.md

The first example uses the Haar Cascade file included with OpenCV. The second example expects haarcascade_frontalface_default.xml to be located in the project directory.

# 1. Face Detection in a Single Image

The first example reads an image named 1.jpg and detects faces using the Haar Cascade Classifier.
```
import cv2
```
### Load the cascade classifier for face detection
```
face_cascade = cv2.CascadeClassifier(
    cv2.data.haarcascades + 'haarcascade_frontalface_default.xml'
)
```
### Read the input image
```
img = cv2.imread('1.jpg')
```
### Convert the image to grayscale
```
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
```
### Detect faces of different sizes in the input image
```
faces = face_cascade.detectMultiScale(
    gray,
    scaleFactor=1.1,
    minNeighbors=5
)
```
### Draw a rectangle around each detected face
```
for (x, y, w, h) in faces:
    cv2.rectangle(
        img,
        (x, y),
        (x + w, y + h),
        (255, 255, 0),
        2
    )
```
### Display the result
```
cv2.imshow('img', img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
### Run the Example

Save the code as `single_face_detect`.py and run:

`python single_face_detect.py`

The program will detect faces in 1.jpg and draw a rectangle around each detected face.

# 2. Face Detection in Multiple Images

The second example automatically finds all .jpg images in the current directory and detects faces in each image.
```
import cv2
import glob
```
## Find all JPG images in the current directory
```
all_images = glob.glob("*.jpg")
```
## Load the Haar Cascade classifier
```
detect = cv2.CascadeClassifier(
    "haarcascade_frontalface_default.xml"
)

for image in all_images:

    # Read the image
    img = cv2.imread(image)

    # Convert the image to grayscale
    gray_img = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

    # Detect faces
    faces = detect.detectMultiScale(
        gray_img,
        1.1,
        5
    )

    # Draw rectangles around detected faces
    for (x, y, w, h) in faces:
        final_img = cv2.rectangle(
            img,
            (x, y),
            (x + w, y + h),
            (255, 255, 0),
            2
        )

    # Display the result
    cv2.imshow("Detected Faces", final_img)
    cv2.waitKey(2000)
    cv2.destroyAllWindows()
```
## Example Directory

Your project directory can look like this:

face-detection/

│

├── image1.jpg

├── image2.jpg

├── image3.jpg

├── haarcascade_frontalface_default.xml

├── multiple_face_detect.py

└── README.md


Run the program with:
```
python multiple_face_detect.py
```

Each image will be displayed for **2 seconds** with detected faces highlighted by rectangles.

## How Does It Work?

The project uses OpenCV's **Haar Cascade Classifier** for face detection.

The classifier analyzes the image at different scales and searches for patterns that resemble human faces.

The following classifier is used:

`haarcascade_frontalface_default.xml`


It is designed primarily for detecting **frontal human faces.**

# Key Functions
### cv2.imread()

Reads an image from a file.
```
img = cv2.imread("1.jpg")
```
### cv2.cvtColor()

Converts an image from one color space to another.

In this project, images are converted to grayscale:

```
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
```
### detectMultiScale()

Detects objects, such as faces, at multiple scales.
```
faces = face_cascade.detectMultiScale(
    gray,
    scaleFactor=1.1,
    minNeighbors=5
)
```
### cv2.rectangle()

Draws a rectangle around a detected face.
```
cv2.rectangle(
    img,
    (x, y),
    (x + w, y + h),
    (255, 255, 0),
    2
)
```
### cv2.imshow()

Displays an image in a window.
```
cv2.imshow("Detected Faces", img)
```
### glob.glob()

Finds files matching a specific pattern.
```
all_images = glob.glob("*.jpg")
```
### Understanding detectMultiScale()
The following code:
```
detectMultiScale(gray, 1.1, 5)
```
is equivalent to:
```
detectMultiScale(
    gray,
    scaleFactor=1.1,
    minNeighbors=5
)
```
### scaleFactor

Controls how much the image size is reduced at each scale.
```
1.1
```
A smaller value can improve detection accuracy but may increase processing time.

### minNeighbors

Determines how many neighboring detections are required for a region to be considered a face.
```
5
```

Increasing this value can reduce false positives, but it may also cause some real faces to be missed.

### Supported Image Formats

The multiple-image example currently searches for .jpg files:
```
glob.glob("*.jpg")
```
You can add support for other formats such as PNG:
```
all_images = glob.glob("*.jpg") + glob.glob("*.png")
```

## Technologies Used
- Python
- OpenCV
- Haar Cascade Classifier

## License
This project was created for educational and learning purposes.

***Python • OpenCV • Computer Vision • Face Detection • Haar Cascade***
