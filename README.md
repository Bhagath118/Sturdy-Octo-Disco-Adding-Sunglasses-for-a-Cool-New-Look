# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look

Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:
- Detects the face in an image.
- Places a stylish sunglass overlay perfectly on the face.
- Works seamlessly with individual passport-size photos.
- Customizable for different sunglasses styles or photo types.

## Technologies Used:
- Python
- OpenCV for image processing
- Numpy for array manipulations

## How to Use:
1. Clone this repository.
2. Add your passport-sized photo to the `images` folder.
3. Run the script to see your "cool" transformation!

## Applications:
- Learning basic image processing techniques.
- Adding flair to your photos for fun.
- Practicing computer vision workflows.

## PROGRAM & OUTPUT:

```
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
```
faceImage = cv2.imread('bkk.jpg')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
```

![image](https://github.com/user-attachments/assets/99648c92-bcf4-4d4b-97e9-469eb6a6c52a)


```
faceImage.shape
```

(704, 540, 3)

```
glassPNG = cv2.imread('sunglass.png',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
```

![image](https://github.com/user-attachments/assets/a09c20c2-4ca2-48ed-a4ed-50f83c555700)



```
glassPNG = cv2.resize(glassPNG,(200,85))
print("image Dimension ={}".format(glassPNG.shape))
```

image Dimension =(85, 200, 4)



```
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]
```
```
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
```

![image](https://github.com/user-attachments/assets/c29c57be-129b-4d57-b06b-c2ec6c550d5d)


```
faceWithGlassesNaive = faceImage.copy()

faceWithGlassesNaive[150:230, 125:295]=glassBGR

plt.imshow(faceWithGlassesNaive[...,::-1])
```

![image](https://github.com/user-attachments/assets/09ea1fca-047b-4ce1-b9fa-eb9aaaf6be08)


```
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))

glassMask = np.uint8(glassMask/255)

faceWithGlassesArithmetic = faceImage.copy()

eyeROI= faceWithGlassesArithmetic[185:270, 175:375]

maskedEye = cv2.multiply(eyeROI,(1-  glassMask ))

maskedGlass = cv2.multiply(glassBGR,glassMask)

eyeRoiFinal = cv2.add(maskedEye, maskedGlass)

plt.figure(figsize=[20,20])
plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")
```


![image](https://github.com/user-attachments/assets/7e416d19-f548-4dea-b84f-e3d2aedeb6b2)




```
faceWithGlassesArithmetic[150:230, 125:295]=eyeRoiFinal

plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");
```

![image](https://github.com/user-attachments/assets/4f508de5-587b-4165-bc80-22287517cd00)


