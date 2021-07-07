# Real_time_face_detection_using_Python_and_OpenCV

# Face detection
is a type of artificial intelligence (AI) based computer technology used to find and identify human faces in digital images. It can be applied to various fields including security, biometrics, law enforcement, entertainment and personal safety.
</br>
</br>
<p align="center"><img src="https://user-images.githubusercontent.com/85819577/124750716-7935f100-df2e-11eb-94df-42e614b71f84.png" width="300" height="300" /></p>
We are still working on the second robot project which is: reception robot. And we will use face detection process to make the robot detect peoples' faces to welcoming them. For that we need a camera to capture peoples' faces, and RaspberryPi to put our program in.
</br>
</br>
what we means by <b>RaspberryPi</b>?
RaspberryPi is a small, low-cost computer that can be connected to a computer monitor or TV screen, and can also be connected to a mouse and keyboard to make it easier to control, and do many tasks such as surfing the Internet, playing video, creating spreadsheets, word processing and even playing games.
So we will need to use RaspberryPi instead of a regular computer, so that the robot can move around without any obstacles.
<p align="center"><img src="https://upload.wikimedia.org/wikipedia/commons/f/f1/Raspberry_Pi_4_Model_B_-_Side.jpg" width="200" height="200" /></p>

______________________________________________

Instead of writing the program on Raspberry Pi, I wrote it directly in Windows.
I wrote the code in the editor **Jupyter Notebook (Anaconda3)**, which is an open source web application that allows writing code in Python (and other languages), widely used for learning Python language and machine learning algorithms, easy to use and has a simple user interface.
<p align="center"><img src="https://upload.wikimedia.org/wikipedia/commons/3/38/Jupyter_logo.svg" width="100" height="100" /></p>

______________________________________________

# Let's move to the code


1. we need to install OpenCV package
``` 
pip install opencv-python==3.4.8.29
```
2. import cv2 
```
import cv2
```
3. Load the file haarcascade_frontalface_default.xml and assign it to the faceCascade variable. 
**Note:** The path of this file must be written completely, depending on your device.
```
faceCascade = cv2.CascadeClassifier('C:\\Users\\iiber\\anaconda3\\Lib\\site-packages\\cv2\\data\\haarcascade_frontalface_default.xml')
```

4. Write this code to capture video from webcam
```
video_capture = cv2.VideoCapture(0)
```

5. The face detection process will be as a loop, exiting this loop when the condition is met.

```
while True: 
    # Capture frame-by-frame
    ret, frame = video_capture.read()
```

6. Here the image is converted to gray
```
    gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
    
    faces = faceCascade.detectMultiScale(
        gray,
        scaleFactor=1.1,
        minNeighbors=5,
    )
```
7. Draw a rectangle around the faces
```    
for (x, y, w, h) in faces:
        cv2.rectangle(frame, (x, y), (x+w, y+h), (0, 255, 0), 2)
```
8. Display the resulting frame
```
    cv2.imshow('Video', frame)
```
9. Camera recording is stopped when the 'q' key is pressed
```
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break
```

10. When everything is done, release the capture
```
video_capture.release()
cv2.destroyAllWindows()
```



# This is the full code:

```
pip install opencv-python==3.4.8.29

import cv2

faceCascade = cv2.CascadeClassifier('C:\\Users\\iiber\\anaconda3\\Lib\\site-packages\\cv2\\data\\haarcascade_frontalface_default.xml')


video_capture = cv2.VideoCapture(0)

while True: 
    # Capture frame-by-frame
    ret, frame = video_capture.read()

    gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)

    faces = faceCascade.detectMultiScale(
        gray,
        scaleFactor=1.1,
        minNeighbors=5,
    )

    # Draw a rectangle around the faces
    for (x, y, w, h) in faces:
        cv2.rectangle(frame, (x, y), (x+w, y+h), (0, 255, 0), 2)

    # Display the resulting frame
    cv2.imshow('Video', frame)

    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

# When everything is done, release the capture
video_capture.release()
cv2.destroyAllWindows()
```
