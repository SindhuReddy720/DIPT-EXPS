# Histogram Equalization Using OpenCV (Grayscale & Color Images)

---

## Aim

To write a Python program using OpenCV to perform histogram equalization on both grayscale and color images to enhance image contrast and brightness.

The program performs the following operations:

- Read and display a grayscale image  
- Plot histogram of the grayscale image  
- Apply histogram equalization on grayscale image  
- Read and display a color image  
- Plot histogram of B, G, R channels  
- Convert image to HSV color space  
- Apply histogram equalization on the Value (V) channel  
- Convert the enhanced image back to BGR format  
- Display original and enhanced images with histograms  

---

## Software Used

- Anaconda – Python 3.7  
- Jupyter Notebook / VS Code  
- OpenCV (`cv2`)  
- NumPy  
- Matplotlib  

---

## Algorithm

### Step 1:
Import the required libraries: OpenCV, NumPy, and Matplotlib.

### Step 2:
Read the image `parrot.jpg` in grayscale format.

### Step 3:
Display the grayscale image and plot its histogram.

### Step 4:
Apply histogram equalization using `cv2.equalizeHist()` to enhance contrast.

### Step 5:
Display original grayscale image, its histogram, enhanced image, and its histogram using a 2 × 2 grid.

### Step 6:
Read the same image in color format.

### Step 7:
Split the image into B, G, R channels and plot their histograms.

### Step 8:
Convert the image from BGR to HSV color space.

### Step 9:
Apply histogram equalization on the V (Value) channel.

### Step 10:
Merge the channels and convert the image back to BGR format.

### Step 11:
Display original color image, histogram, enhanced image, and enhanced histogram using a 2 × 2 grid.

---

## Program

### Developed By:
**Name:** PELLETI SINDHU SRI

**Register No:** 212224240113 
```python

import cv2
import numpy as np
import matplotlib.pyplot as plt

image_path = r"C:\Users\admin\little-cat-sitting-grass.jpg"

gray_img = cv2.imread(image_path, cv2.IMREAD_GRAYSCALE)

fig, axes = plt.subplots(1, 2, figsize=(12, 4))

axes[0].imshow(gray_img, cmap='gray')
axes[0].set_title("Original Grayscale Image")
axes[0].axis('off')

axes[1].hist(gray_img.ravel(), bins=256, range=[0, 256], color='black')
axes[1].set_title("Original Grayscale Histogram")
axes[1].set_xlim([0, 256])

plt.show()
equalized_img = cv2.equalizeHist(gray_img)
fig, axes = plt.subplots(2, 2, figsize=(10, 8))

axes[0, 0].imshow(gray_img, cmap='gray')
axes[0, 0].set_title("Original Grayscale Image")
axes[0, 0].axis('off')

axes[0, 1].hist(gray_img.ravel(), bins=256, range=[0, 256], color='black')
axes[0, 1].set_title("Original Grayscale Histogram")
axes[0, 1].set_xlim([0, 256])

axes[1, 0].imshow(equalized_img, cmap='gray')
axes[1, 0].set_title("Enhanced Grayscale Image")
axes[1, 0].axis('off')

axes[1, 1].hist(equalized_img.ravel(), bins=256, range=[0, 256], color='black')
axes[1, 1].set_title("Equalized Grayscale Histogram")
axes[1, 1].set_xlim([0, 256])

plt.tight_layout()
plt.show()
color_img = cv2.imread(image_path)

color_img_rgb = cv2.cvtColor(color_img, cv2.COLOR_BGR2RGB)

plt.imshow(color_img_rgb)
plt.title("Original Color Image")
plt.axis('off')
plt.show()
b, g, r = cv2.split(color_img)

plt.figure(figsize=(10, 5))
plt.title("RGB Channel Histograms")
plt.xlabel("Pixel Intensity Value (0 - 255)")
plt.ylabel("Pixel Count")

colors = ('b', 'g', 'r')
channel_labels = ('Blue Channel', 'Green Channel', 'Red Channel')

for i, col in enumerate(colors):
    hist = cv2.calcHist([color_img], [i], None, [256], [0, 256])
    plt.plot(hist, color=col, label=channel_labels[i])

plt.xlim([0, 256])
plt.legend()
plt.show()
hsv_img = cv2.cvtColor(color_img, cv2.COLOR_BGR2HSV)
h, s, v = cv2.split(hsv_img)

v_equalized = cv2.equalizeHist(v)
hsv_equalized = cv2.merge((h, s, v_equalized))

enhanced_color_bgr = cv2.cvtColor(hsv_equalized, cv2.COLOR_HSV2BGR)
enhanced_color_rgb = cv2.cvtColor(enhanced_color_bgr, cv2.COLOR_BGR2RGB)

fig, axes = plt.subplots(2, 2, figsize=(10, 8))

axes[0, 0].imshow(color_img_rgb)
axes[0, 0].set_title("Original Color Image")
axes[0, 0].axis('off')

axes[0, 1].hist(v.ravel(), bins=256, range=[0, 256], color='gray')
axes[0, 1].set_title("Original V-Channel Histogram")
axes[0, 1].set_xlim([0, 256])

axes[1, 0].imshow(enhanced_color_rgb)
axes[1, 0].set_title("Enhanced Color Image (HSV Equalized)")
axes[1, 0].axis('off')

axes[1, 1].hist(v_equalized.ravel(), bins=256, range=[0, 256], color='gray')
axes[1, 1].set_title("Equalized V-Channel Histogram")
axes[1, 1].set_xlim([0, 256])

plt.tight_layout()
plt.show()
```

---

##  Output

### Grayscale Histogram Equalization

- Original grayscale image is displayed
  
<img width="601" height="497" alt="image" src="https://github.com/user-attachments/assets/e3c7fb98-c0d1-482e-b781-2a54ba9006ba" />
 
- Histogram of original grayscale image is plotted

<img width="702" height="502" alt="image" src="https://github.com/user-attachments/assets/7f3f5fb0-2fbf-43c5-b98e-54ae578ef91e" />

- Enhanced image after histogram equalization is displayed

<img width="586" height="440" alt="image" src="https://github.com/user-attachments/assets/1df3957e-9c86-4a15-b6ec-103bb0cea139" />

- Histogram of enhanced grayscale image shows improved contrast

<img width="703" height="513" alt="image" src="https://github.com/user-attachments/assets/29cfb9b7-798c-4d3d-8bd0-79f100667f16" />


### Color Image Histogram Equalization

- Original color image is displayed

<img width="675" height="463" alt="image" src="https://github.com/user-attachments/assets/15aefe41-0943-4235-9274-5010842c356d" />

- Histogram of B, G, R channels is plotted

<img width="1075" height="585" alt="image" src="https://github.com/user-attachments/assets/a71eb5c7-556d-436b-87e8-1a09a9441a46" />

- Enhanced image after HSV-based equalization is displayed

<img width="596" height="478" alt="image" src="https://github.com/user-attachments/assets/92eba476-7084-4b55-94ba-718a1126b1ad" />

- Histogram of enhanced image shows better intensity distribution  

<img width="693" height="506" alt="image" src="https://github.com/user-attachments/assets/7cfe4d68-b683-4c92-aa53-295b181c1fa5" />

<img width="696" height="492" alt="image" src="https://github.com/user-attachments/assets/a920ae52-c37f-4a86-a9ad-0e1447d1e642" />


---

## Result

Thus, histogram equalization is successfully performed on both grayscale and color images using OpenCV. The contrast and brightness of the images are significantly improved, enhancing visual quality and feature visibility.
