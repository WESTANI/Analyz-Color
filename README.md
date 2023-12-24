# Analyz-Color
Analyz Color
# Code for Color Recognition using OpenCV
import cv2
import numpy as np

def recognize_colors(image_path):
    # Read the input image
    image = cv2.imread(image_path)

    # Convert the image from BGR to HSV color space
    hsv_image = cv2.cvtColor(image, cv2.COLOR_BGR2HSV)

    # Define color ranges for recognition (example: green)
    lower_green = np.array([40, 40, 40])
    upper_green = np.array([80, 255, 255])

    # Create a mask for the specified color range
    mask = cv2.inRange(hsv_image, lower_green, upper_green)

    # Find contours in the mask
    contours, _ = cv2.findContours(mask, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)

    # Draw rectangles around the detected colored objects
    for contour in contours:
        x, y, w, h = cv2.boundingRect(contour)
        cv2.rectangle(image, (x, y), (x+w, y+h), (0, 255, 0), 2)

    # Display the result
    cv2.imshow('Color Recognition', image)
    cv2.waitKey(0)
    cv2.destroyAllWindows()

# Example usage
image_path = "path/to/your/image.jpg"
recognize_colors(image_path)
