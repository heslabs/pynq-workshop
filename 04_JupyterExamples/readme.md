# PYNQ-Z2 Jupyter Ecxamples

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

