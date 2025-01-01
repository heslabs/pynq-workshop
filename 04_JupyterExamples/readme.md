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

---
## Logictools - WaveDrom 
* WaveDrom for real-time pattern generation and trace analysis
* The logictools overlay uses WaveJSON format to specify and generate real signals on the board.

<img src="https://github.com/user-attachments/assets/4ec7af16-91df-4017-9e50-52970d7cc87f" width=450>

* WaveDrom is a tool for rendering digital timing waveforms. 
    * The waveforms are defined in a simple textual format.
* This notebook will show how to render digital waveforms using the pynq library.
    * The logictools overlay uses the same format as WaveDrom to specify and generate real signals on the board.
* Tests
    * Step 1: Import the draw_wavedrom() method from the pynq library
    * Step 2: Specify and render a waveform
    * Step 3: Adding more signals to the waveform

---
#### Step 1: Import the draw_wavedrom() method from the pynq library
```
from pynq.lib.logictools.waveform import draw_wavedrom
clock = {'signal': [{'name': 'clock_0', 'wave': 'hlhlhlhlhlhlhlhl'}],
         'foot': {'tock': 1},
         'head': {'text': 'Clock Signal'}}

draw_wavedrom(clock)
```

<img src="https://github.com/user-attachments/assets/311c6cd9-efba-4ad5-89e5-0d669a92820f" width=550>

---
#### Step 3: Adding more signals to the waveform
```
pattern = {'signal': [{'name': 'clk', 'wave': 'hl' * 8},
                      {'name': 'clkn', 'wave': 'lh' * 8},
                      {'name': 'data0', 'wave': 'l.......h.......'},
                      {'name': 'data1', 'wave': 'h.l...h...l.....'}],
           'foot': {'tock': 1},
           'head': {'text': 'Pattern'}}

draw_wavedrom(pattern)
```
<img src="https://github.com/user-attachments/assets/017a1faf-9fbf-487e-acd0-d670784ac440" width=650>

---
## Logictools - Boolean Generator

* This notebook will show how to use the boolean generator to generate a boolean combinational function. The function that is implemented is a 2-input XOR.
    * Step 1: Download the logictools overlay
    * Step 2: Specify the boolean function of a 2-input XOR
    * Step 3: Instantiate and setup of the boolean generator object.
    * Step 4: Run the boolean generator verify operation
    * Step 5: Stop the boolean generator
    * Step 6: Re-run the entire boolean function generation in a single cell

---
#### Step 2: Specify the boolean function of a 2-input XOR
The logic is applied to the on-board pushbuttons and LED, pushbuttons PB0 and PB3 are set as inputs and LED LD2 is set as an output
```
function = ['LD2 = PB3 ^ PB0']
```
Find the On-board pushbuttons and LEDs

---
#### Step 4: Run the boolean generator verify operation 
```	
boolean_generator.run()
```
* Verify the operation of the XOR function
<img src="https://github.com/user-attachments/assets/8febdaa1-fffb-435a-a302-f67cb4640d5e" width=550>


#### Sample code
```
from pynq.overlays.logictools import LogicToolsOverlay

logictools_olay = LogicToolsOverlay('logictools.bit')
boolean_generator = logictools_olay.boolean_generator

function = {'XOR_gate': 'LD2 = PB3 ^ PB0'}

boolean_generator.setup(function)
boolean_generator.run()

boolean_generator.stop()
```

