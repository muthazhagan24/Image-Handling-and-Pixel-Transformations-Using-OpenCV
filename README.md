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
- **Name:** Rahul M R
- **Register Number:** 2305003005

  ### Ex. No. 01

#### 1. Read the image ('Eagle_in_Flight.jpg') using OpenCV imread() as a grayscale image.
```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

img = cv2.imread(r"WhatsApp Image 2026-04-28 at 14.38.24.jpeg", cv2.IMREAD_COLOR)
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
```

#### 2. Print the image width, height & Channel.
```python
img.shape
```

#### 3. Display the image using matplotlib imshow().
```python
plt.imshow(img_rgb)
plt.show()
```

#### 4. Save the image as a PNG file using OpenCV imwrite().
```python
cv2.imwrite("Eagle.png", img)
```

#### 5. Read the saved image above as a color image using cv2.cvtColor().
```python
img = cv2.imread("Eagle.png")
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
```

#### 6. Display the Colour image using matplotlib imshow() & Print the image width, height & channel.
```python
plt.imshow(img_rgb)
plt.show()
img.shape
```

#### 7. Crop the image to extract any specific (Eagle alone) object from the image.
```python
crop = img_rgb[100:600, 200:900]

plt.imshow(crop)
plt.title("Cropped Region")
plt.axis("off")
plt.show()

crop.shape
```

#### 8. Resize the image up by a factor of 2x.
```python
res = cv2.resize(crop, (400, 400))
```

#### 9. Flip the cropped/resized image horizontally.
```python
flip = cv2.flip(res, 1)

plt.imshow(flip)
plt.title("Flipped Horizontally")
plt.axis("off")
```

#### 10. Read in the image ('Apollo-11-launch.jpg').
```python
img = cv2.imread(r"C:\Users\admin\OneDrive\Desktop\DIP1\WhatsApp Image 2026-04-28 at 14.38.24.jpeg", cv2.IMREAD_COLOR)
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
img_rgb.shape
```

#### 11. Add the following text to the dark area at the bottom of the image (centered on the image):
```python
text = cv2.putText(img_rgb, "Eagle Image", (200, 700),
                   cv2.FONT_HERSHEY_SIMPLEX, 1,
                   (255, 255, 255), 2)

plt.imshow(text)
plt.title("New Image")
plt.show()
```

#### 12. Draw a magenta rectangle that encompasses the launch tower and the rocket.
```python
# Reload original image to remove old rectangles
img = cv2.imread(r"WhatsApp Image 2026-04-28 at 14.38.24.jpeg", cv2.IMREAD_COLOR)
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

rcol = (255, 0, 255)

# Correct rectangle around eagle
cv2.rectangle(img_rgb, (200, 50), (530, 415), rcol, 4)
```

#### 13. Display the final annotated image.
```python

plt.figure(figsize=(8,6))
plt.imshow(img_rgb)
plt.title("Annotated Image")
plt.axis("on")
plt.show()
```

#### 14. Read the image ('Boy.jpg').
```python
img = cv2.imread(r"WhatsApp Image 2026-04-28 at 14.38.24.jpeg", cv2.IMREAD_COLOR)
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
```

#### 15. Adjust the brightness of the image.
```python
m = np.ones(img_rgb.shape, dtype="uint8") * 50
```

#### 16. Create brighter and darker images.
```python
img_brighter = cv2.add(img_rgb, m)
img_darker = cv2.subtract(img_rgb, m)
```

#### 17. Display the images (Original Image, Darker Image, Brighter Image).
```python
plt.figure(figsize=(10,5))

plt.subplot(1,3,1)
plt.imshow(img_rgb)
plt.title("Original Image")
plt.axis("off")

plt.subplot(1,3,2)
plt.imshow(img_darker)
plt.title("Darker Image")
plt.axis("off")

plt.subplot(1,3,3)
plt.imshow(img_brighter)
plt.title("Brighter Image")
plt.axis("off")

plt.show()
```

#### 18. Modify the image contrast.
```python
# Create matrices
matrix1 = np.ones(img_rgb.shape, dtype="float32") * 1.1
matrix2 = np.ones(img_rgb.shape, dtype="float32") * 1.2

# Apply contrast
img_higher1 = cv2.multiply(img_rgb.astype("float32"), matrix1)
img_higher2 = cv2.multiply(img_rgb.astype("float32"), matrix2)

# Convert back to uint8
img_higher1 = np.clip(img_higher1, 0, 255).astype("uint8")
img_higher2 = np.clip(img_higher2, 0, 255).astype("uint8")
```

#### 19. Display the images (Original, Lower Contrast, Higher Contrast).
```python
plt.figure(figsize=(10,5))

plt.subplot(1,3,1)
plt.imshow(img_rgb)
plt.title("Original Image")
plt.axis("off")

plt.subplot(1,3,2)
plt.imshow(img_higher1)
plt.title("Higher Contrast (1.1x)")
plt.axis("off")

plt.subplot(1,3,3)
plt.imshow(img_higher2)
plt.title("Higher Contrast (1.2x)")
plt.axis("off")

plt.show()
```

#### 20. Split the image (boy.jpg) into the B,G,R components & Display the channels.
```python
b, g, r = cv2.split(img)

plt.figure(figsize=(10,5))

plt.subplot(1,3,1)
plt.imshow(b, cmap='gray')
plt.title("Blue Channel")
plt.axis("off")

plt.subplot(1,3,2)
plt.imshow(g, cmap='gray')
plt.title("Green Channel")
plt.axis("off")

plt.subplot(1,3,3)
plt.imshow(r, cmap='gray')
plt.title("Red Channel")
plt.axis("off")

plt.show()
```

#### 21. Merged the R, G, B , displays along with the original image
```python
merged_rgb = cv2.merge([r, g, b])

plt.figure(figsize=(10,5))

plt.subplot(1,2,1)
plt.imshow(img_rgb)
plt.title("Original Image")
plt.axis("off")

plt.subplot(1,2,2)
plt.imshow(merged_rgb)
plt.title("Merged RGB Image")
plt.axis("off")

plt.show()
```

#### 22. Split the image into the H, S, V components & Display the channels.
```python
hsv_img = cv2.cvtColor(img_rgb, cv2.COLOR_RGB2HSV)
h, s, v = cv2.split(hsv_img)

plt.figure(figsize=(10,5))

plt.subplot(1,3,1)
plt.imshow(h, cmap='gray')
plt.title("Hue Channel")
plt.axis("off")

plt.subplot(1,3,2)
plt.imshow(s, cmap='gray')
plt.title("Saturation Channel")
plt.axis("off")

plt.subplot(1,3,3)
plt.imshow(v, cmap='gray')
plt.title("Value Channel")
plt.axis("off")

plt.show()
```
#### 23. Merged the H, S, V, displays along with original image.
```python
merged_hsv = cv2.merge([h, s, v])
merged_rgb_from_hsv = cv2.cvtColor(merged_hsv, cv2.COLOR_HSV2RGB)

plt.figure(figsize=(10,5))

plt.subplot(1,2,1)
plt.imshow(img_rgb)
plt.title("Original Image")
plt.axis("off")

plt.subplot(1,2,2)
plt.imshow(merged_rgb_from_hsv)
plt.title("Merged HSV Image")
plt.axis("off")

plt.show()
```

## Output:
- **1)** Print Image Width, Height & Channels
<img width="639" height="43" alt="image" src="https://github.com/user-attachments/assets/8f1d7d04-aa06-4654-a40b-5105012c68a7" />
 
- **2)**  Display the Image
<img width="557" height="434" alt="image" src="https://github.com/user-attachments/assets/1fe020f0-b679-4e9a-a8ee-3bffb7eb315f" />

- **3)** Save the Image as PNG
<img width="642" height="45" alt="image" src="https://github.com/user-attachments/assets/afde9e9f-e7e3-43e5-88ee-b9fb1ef59e30" />

- **4)** Display the Colour Image & Shape
<img width="551" height="456" alt="image" src="https://github.com/user-attachments/assets/e20587cc-dccd-4c71-89cf-7755e8f6c724" />
- **5)** Crop the Image
<img width="525" height="455" alt="image" src="https://github.com/user-attachments/assets/bfae82e4-63f3-4807-a811-5b6c59e0b26b" />

- **6)** Flip the Image Horizontally
<img width="445" height="445" alt="image" src="https://github.com/user-attachments/assets/a923512a-e45e-4f26-9fe0-a2c891f87be9" />

- **7)** Add Text to Image
<img width="541" height="340" alt="image" src="https://github.com/user-attachments/assets/bdd0060f-2c37-43d8-ab1b-e16679849d28" />

- **8)**  Draw Rectangle
<img width="510" height="492" alt="image" src="https://github.com/user-attachments/assets/24b71a1c-95cd-491c-839e-49070e65f9d5" />

- **9)** Display the final annotated image
<img width="539" height="339" alt="image" src="https://github.com/user-attachments/assets/fd3f051f-f2f1-4b89-953c-680b6177071b" />

- **10)** Display the images (Original, Darker, Brighter)
<img width="562" height="166" alt="image" src="https://github.com/user-attachments/assets/c217a3aa-110a-431e-9cf7-3aa96e11bf42" />

- **11)** Display the images (Original, Lower Contrast, Higher Contrast)
<img width="556" height="165" alt="image" src="https://github.com/user-attachments/assets/3dfd8bb4-6cb3-401c-8c46-c6383b3c1c62" />

- **12)** Split the image into B, G, R channels
<img width="556" height="166" alt="image" src="https://github.com/user-attachments/assets/4c1ea308-239c-4f50-bf43-f6826f9904eb" />
- **12)** Merge R, G, B and display with original
<img width="556" height="227" alt="image" src="https://github.com/user-attachments/assets/cd004da6-8419-460c-b6c1-df308a6de52f" />

- **12)** Split into H, S, V c
<img width="558" height="164" alt="image" src="https://github.com/user-attachments/assets/6569c37b-da53-440b-b8c5-c525b547ddbc" />

- **12)** Merge H, S, V and display with original
<img width="559" height="231" alt="image" src="https://github.com/user-attachments/assets/8fc004f0-7b00-4b53-8854-5e1e61968e6d" />

## Result:
Thus, the images were read, displayed, brightness and contrast adjustments were made, and bitwise operations were performed successfully using the Python program.
