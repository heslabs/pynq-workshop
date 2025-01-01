# PYNQ-Z2 Jupyter Examples

---
## Buttons and LEDs Demonstration

* This demo shows how to use push-buttons (BTN0-3), LEDs (LD0-3), and RGB LEDs (LD4-5) on the board.
* You can do the following to control the LEDs or RGB LEDs:

| Action | Expected Results |
|:-|:-|
| Button 0 pressed | RGB LEDs change color |
| Button 1 pressed | LEDs shift from right to left (LD0 -> LD3) |
| Button 2 pressed | LEDs shift from left to right (LD3 -> LD0) |
| Button 3 pressed | Turns off all the LEDS and ends this demo |

### Sample code
```
from time import sleep
from pynq.overlays.base import BaseOverlay

base = BaseOverlay("base.bit")

Delay1 = 0.3
Delay2 = 0.1
color = 0
rgbled_position = [4,5]

for led in base.leds:
    led.on()    
while (base.buttons[3].read()==0):
    if (base.buttons[0].read()==1):
        color = (color+1) % 8
        for led in rgbled_position:
            base.rgbleds[led].write(color)
            base.rgbleds[led].write(color)
        sleep(Delay1)
elif (base.buttons[1].read()==1):
        for led in base.leds:
            led.off()
        sleep(Delay2)
        for led in base.leds:
            led.toggle()
            sleep(Delay2)
            
    elif (base.buttons[2].read()==1):
        for led in reversed(base.leds):
            led.off()
        sleep(Delay2)
        for led in reversed(base.leds):
            led.toggle()
            sleep(Delay2)                  
    
print('End of this demo ...')
for led in base.leds:
    led.off()
for led in rgbled_position:
    base.rgbleds[led].off()
```

---
## OpenCV Filters Webcam

### Introduction
* In this notebook, several filters will be applied to webcam images.
* Those input sources and applied filters will then be displayed either directly in the notebook or on HDMI output.
* To run all cells in this notebook a webcam and HDMI output monitor are required. 

### Tests
* Start HDMI output
* Applying OpenCV filters on Webcam input
  * Step 1: Specify webcam resolution
  * Step 2: Initialize camera from OpenCV
  * Step 3: Send webcam input to HDMI output
  * Step 4: Edge detection
  * Step 5: Canny edge detection
  * Step 6: Show results

---
### Applying OpenCV filters on Webcam input

---
#### Step 1: Specify webcam resolution
```
# camera (input) configuration
frame_in_w = 640
frame_in_h = 480
```

#### Step 2: Initialize camera from OpenCV
```
import os
os.environ["OPENCV_LOG_LEVEL"]="SILENT"
import cv2
videoIn = cv2.VideoCapture(0)
videoIn.set(cv2.CAP_PROP_FRAME_WIDTH, frame_in_w);
videoIn.set(cv2.CAP_PROP_FRAME_HEIGHT, frame_in_h);
print("capture device is open: " + str(videoIn.isOpened()))
```

#### Step 3: Send webcam input to HDMI output
```
import os
os.environ["OPENCV_LOG_LEVEL"]="SILENT"
import cv2
videoIn = cv2.VideoCapture(0)
videoIn.set(cv2.CAP_PROP_FRAME_WIDTH, frame_in_w);
videoIn.set(cv2.CAP_PROP_FRAME_HEIGHT, frame_in_h);
print("capture device is open: " + str(videoIn.isOpened()))
```

#### Step 4: Edge detection
```
import time
num_frames = 20
readError = 0
start = time.time()
for i in range (num_frames):   
    # read next image
    ret, frame_vga = videoIn.read()
    if (ret):
        outframe = hdmi_out.newframe()
        laplacian_frame = cv2.Laplacian(frame_vga, cv2.CV_8U, dst=outframe)
        hdmi_out.writeframe(outframe)
    else:
        readError += 1
end = time.time()
print("Frames per second: " + str((num_frames-readError) / (end - start)))
print("Number of read errors: " + str(readError))
```

#### Step 5: Canny edge detection
```
num_frames = 20
Mode = VideoMode(640,480,8)
hdmi_out = base.video.hdmi_out
hdmi_out.configure(Mode,PIXEL_GRAY)
hdmi_out.start()
start = time.time()
for i in range (num_frames):
    # read next image
    ret, frame_webcam = videoIn.read()
    if (ret):
        outframe = hdmi_out.newframe()
        cv2.Canny(frame_webcam, 100, 110, edges=outframe)
        hdmi_out.writeframe(outframe)
    else:
        readError += 1
end = time.time()
print("Frames per second: " + str((num_frames-readError) / (end - start)))
print("Number of read errors: " + str(readError))
```

#### Step 6: Show results
```
%matplotlib inline 
from matplotlib import pyplot as plt
import numpy as np

frame_canny = cv2.Canny(frame_webcam, 100, 110)
plt.figure(1, figsize=(10, 10))
frame_vga = np.zeros((480,640,3)).astype(np.uint8)
frame_vga[:,:,0] = frame_canny
frame_vga[:,:,1] = frame_canny
frame_vga[:,:,2] = frame_canny
plt.imshow(frame_vga)
plt.show()
```

