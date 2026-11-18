# Image-Handling-and-Pixel-Transformations-Using-OpenCV 

## AIM:
Write a Python program using OpenCV that performs the following tasks:

1) Read and Display an Image.  
2) Adjust the brightness of an image.  
3) Modify the image contrast.  
4) Generate a third image using bitwise operations.

## Software Required:
- Anaconda - Python 3.7
- Jupyter Notebook (for interactive development and execution)

## Algorithm:
### Step 1:
Load an image from your local directory and display it.

### Step 2:
Create a matrix of ones (with data type float64) to adjust brightness.

### Step 3:
Create brighter and darker images by adding and subtracting the matrix from the original image.  
Display the original, brighter, and darker images.

### Step 4:
Modify the image contrast by creating two higher contrast images using scaling factors of 1.1 and 1.2 (without overflow fix).  
Display the original, lower contrast, and higher contrast images.

### Step 5:
Split the image (boy.jpg) into B, G, R components and display the channels

## Program Developed By:
- **Name:** PELLETI SINDHU SRI  
- **Register Number:** 212224240113

  ### Ex. No. 01

```python


import cv2
import numpy as np
import matplotlib.pyplot as plt

# 1. Read the image in grayscale
img = cv2.imread(r'C:\Users\admin\Eagle_in_Flight.jpg', 0)

# 2. Print width, height and channel
height, width = img.shape
print("Width:", width)
print("Height:", height)
print("Channel: 1")

# 3. Display grayscale image
plt.imshow(img, cmap='gray')
plt.title('Grayscale Image')
plt.axis('off')
plt.show()

# 4. Save image as PNG
cv2.imwrite('Eagle.png', img)

# 5. Read saved image as color image
img_color = cv2.imread(r'C:\Users\admin\Eagle_in_Flight.jpg')
img_color = cv2.cvtColor(img_color, cv2.COLOR_BGR2RGB)

# 6. Display color image and dimensions
plt.imshow(img_color)
plt.title('Colour Image')
plt.axis('off')
plt.show()

print("Width:", img_color.shape[1])
print("Height:", img_color.shape[0])
print("Channels:", img_color.shape[2])

# 7. Crop Eagle object
cropped = img_color[0:420, 150:570]
plt.imshow(cropped)
plt.title('Cropped Eagle')
plt.axis('off')
plt.show()

# 8. Resize image by 2x
resized = cv2.resize(cropped, None, fx=2, fy=2)

plt.imshow(resized)
plt.title('Resized Image')
plt.axis('off')
plt.show()

# 9. Flip image horizontally
flipped = cv2.flip(resized, 1)

plt.imshow(flipped)
plt.title('Flipped Image')
plt.axis('off')
plt.show()

# 10. Read Apollo 11 image
apollo = cv2.imread(r'C:\Users\admin\Apollo-11-launch.jpg')

# 11. Add text to image
text = 'Apollo 11 Saturn V Launch, July 16, 1969'
font_face = cv2.FONT_HERSHEY_PLAIN

h, w = apollo.shape[:2]
text_size = cv2.getTextSize(text, font_face, 1.5, 2)[0]
x = (w - text_size[0]) // 2
y = h - 20

cv2.putText(apollo, text, (x, y), font_face, 1.5,
            (255, 255, 255), 2)

# 12. Draw magenta rectangle
cv2.rectangle(apollo, (250, 50), (650, 550), (255, 0, 255), 3)

# 13. Display final annotated image
apollo_rgb = cv2.cvtColor(apollo, cv2.COLOR_BGR2RGB)

plt.imshow(apollo_rgb)
plt.title('Apollo 11 Launch')
plt.axis('off')
plt.show()

# 14. Read Boy image
img = cv2.imread(r'C:\Users\admin\boy.jpg')
img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

plt.imshow(img)
plt.title('Original Image')
plt.axis('off')
plt.show()

# 15. Create matrix of ones
matrix_ones = np.ones(img.shape, dtype=np.float64)

# 16. Create brighter and darker images
matrix = np.ones(img.shape, dtype=np.uint8) * 50

img_brighter = cv2.add(img, matrix)
img_darker = cv2.subtract(img, matrix)

# 17. Display brightness images
plt.figure(figsize=(12, 4))

plt.subplot(1, 3, 1)
plt.imshow(img)
plt.title('Original Image')
plt.axis('off')

plt.subplot(1, 3, 2)
plt.imshow(img_darker)
plt.title('Darker Image')
plt.axis('off')

plt.subplot(1, 3, 3)
plt.imshow(img_brighter)
plt.title('Brighter Image')
plt.axis('off')

plt.show()

# 18. Modify image contrast
matrix1 = np.ones(img.shape, dtype=np.float64) * 1.1
matrix2 = np.ones(img.shape, dtype=np.float64) * 1.2

img_lower = cv2.multiply(img, 0.9)
img_higher1 = cv2.multiply(img, 1.1)
img_higher2 = cv2.multiply(img, 1.2)

# 19. Display contrast images
plt.figure(figsize=(12, 4))

plt.subplot(1, 3, 1)
plt.imshow(img)
plt.title('Original Image')
plt.axis('off')

plt.subplot(1, 3, 2)
plt.imshow(img_lower)
plt.title('Lower Contrast')
plt.axis('off')

plt.subplot(1, 3, 3)
plt.imshow(img_higher1)
plt.title('Higher Contrast')
plt.axis('off')

plt.show()

# 20. Split image into B, G and R components
b, g, r = cv2.split(cv2.cvtColor(img, cv2.COLOR_RGB2BGR))

plt.figure(figsize=(12, 4))

plt.subplot(1, 3, 1)
plt.imshow(b, cmap='gray')
plt.title('Blue Channel')
plt.axis('off')

plt.subplot(1, 3, 2)
plt.imshow(g, cmap='gray')
plt.title('Green Channel')
plt.axis('off')

plt.subplot(1, 3, 3)
plt.imshow(r, cmap='gray')
plt.title('Red Channel')
plt.axis('off')

plt.show()

# 21. Merge R, G and B components
merged = cv2.merge([r, g, b])

plt.figure(figsize=(10, 4))

plt.subplot(1, 2, 1)
plt.imshow(img)
plt.title('Original Image')
plt.axis('off')

plt.subplot(1, 2, 2)
plt.imshow(merged)
plt.title('Merged RGB Image')
plt.axis('off')

plt.show()

# 22. Split image into H, S and V components
hsv = cv2.cvtColor(img, cv2.COLOR_RGB2HSV)

h, s, v = cv2.split(hsv)

plt.figure(figsize=(12, 4))

plt.subplot(1, 3, 1)
plt.imshow(h, cmap='gray')
plt.title('Hue')
plt.axis('off')

plt.subplot(1, 3, 2)
plt.imshow(s, cmap='gray')
plt.title('Saturation')
plt.axis('off')

plt.subplot(1, 3, 3)
plt.imshow(v, cmap='gray')
plt.title('Value')
plt.axis('off')

plt.show()

# 23. Merge H, S and V components
merged_hsv = cv2.merge([h, s, v])

result = cv2.cvtColor(merged_hsv, cv2.COLOR_HSV2RGB)

plt.figure(figsize=(10, 4))

plt.subplot(1, 2, 1)
plt.imshow(img)
plt.title('Original Image')
plt.axis('off')

plt.subplot(1, 2, 2)
plt.imshow(result)
plt.title('Merged HSV Image')
plt.axis('off')

plt.show()

# Additional: Bitwise operation
bitwise_and = cv2.bitwise_and(img, img)

plt.imshow(bitwise_and)
plt.title('Bitwise AND Image')
plt.axis('off')
plt.show()
# Generate third image using bitwise operations

gray = cv2.cvtColor(img, cv2.COLOR_RGB2GRAY)

ret, mask = cv2.threshold(gray, 120, 255, cv2.THRESH_BINARY)

bitwise_img = cv2.bitwise_and(img, img, mask=mask)

plt.figure(figsize=(12, 4))

plt.subplot(1, 3, 1)
plt.imshow(img)
plt.title('Original Image')
plt.axis('off')

plt.subplot(1, 3, 2)
plt.imshow(mask, cmap='gray')
plt.title('Binary Mask')
plt.axis('off')

plt.subplot(1, 3, 3)
plt.imshow(bitwise_img)
plt.title('Bitwise AND Image')
plt.axis('off')

plt.show()


```

## Output:
- **i)** Read and Display an Image.

<img width="627" height="515" alt="image" src="https://github.com/user-attachments/assets/b8ef67f3-fb98-46bb-a3ec-1f65e46703e3" />

<img width="633" height="586" alt="image" src="https://github.com/user-attachments/assets/c68565dc-af47-4674-be0c-0333d8467906" />

<img width="531" height="512" alt="image" src="https://github.com/user-attachments/assets/2efa881d-0bbb-486b-a806-ed7469805efa" />

<img width="557" height="513" alt="image" src="https://github.com/user-attachments/assets/07532d69-bbda-43b3-95ed-50d80e1d5bb4" />

<img width="512" height="516" alt="image" src="https://github.com/user-attachments/assets/9a870116-e750-4760-9a22-22f54e01fde7" />

<img width="647" height="412" alt="image" src="https://github.com/user-attachments/assets/b27a26e8-1662-45a5-872e-4fa58c7e073b" />

  
- **ii)** Adjust Image Brightness.

<img width="1190" height="320" alt="image" src="https://github.com/user-attachments/assets/390450c0-d834-4033-9493-d76a501de892" />

- **iii)** Modify Image Contrast.

<img width="1203" height="312" alt="image" src="https://github.com/user-attachments/assets/ef3abd3b-64f7-46ba-9d8e-b07e7b9e674d" />

<img width="1207" height="696" alt="image" src="https://github.com/user-attachments/assets/4d24e744-b224-41e3-9114-d73b5fb6a1ac" />

<img width="1242" height="700" alt="image" src="https://github.com/user-attachments/assets/9124a52f-3cc0-4716-ac88-e8270f6d3531" />

- **iv)** Generate Third Image Using Bitwise Operations.

<img width="1268" height="843" alt="image" src="https://github.com/user-attachments/assets/f05ac240-8f46-4570-808c-6b63e7869e04" />

## Result:
Thus, the images were read, displayed, brightness and contrast adjustments were made, and bitwise operations were performed successfully using the Python program.

