# Exploring the PYNQ-Z2 Board

<img src="https://github.com/user-attachments/assets/feade0f5-1bed-48ef-bcc9-194a6c22947b" width=600>

---
## Prerequisites
* PYNQ-Z2 board
* Computer with compatible browser (Supported Browsers)
* Ethernet cable
* Micro USB cable
* Micro-SD card with preloaded image, or blank card (Minimum 8GB recommended)

---
## PYNQ-Z2 Setup Guide
* PYNQ v2.6.1 [[pynq.readthedocs.io]](https://pynq.readthedocs.io/en/v2.6.1/getting_started/pynq_z2_setup.html)
* Set up the PYNQ-Z2 board from TUL to run PYNQ [[Youtube]](https://www.youtube.com/watch?v=RiFbRf6gaK4)

---
### Board Setup
</br>
<img src="https://github.com/user-attachments/assets/51997b54-e877-4176-8406-3b54723fa6e8" width=600>
</br>

1. Set the ** Boot** jumper to the SD position. (This sets the board to boot from the Micro-SD card)
2. To power the board from the micro USB cable, set the Power jumper to the USB position. (You can also power the board from an external 12V power regulator by setting the jumper to REG.)
3. Insert the Micro SD card loaded with the PYNQ-Z2 image into the Micro SD card slot underneath the board
4. Connect the USB cable to your PC/Laptop, and to the PROG - UART MicroUSB port on the board
5. Connect the Ethernet port by following the instructions below
Turn on the PYNQ-Z2 and check the boot sequence by following the instructions below

---
### Network connection
Once your board is setup, you need to connect to it to start using Jupyter notebook.

#### Ethernet
If available, you should connect your board to a network or router with Internet access. This will allow you to update your board and easily install new packages.

#### Connect directly to a computer (Static IP):

1. Assign your computer a static IP address
2. Connect the board to your computer’s Ethernet port
3. Browse to http://192.168.2.99

#### Connect to a Network Router
If you connect to a router, or a network with a DHCP server, your board will automatically get an IP address.

1. Connect the Ethernet port on your board to a router/switch
2. Connect your computer to Ethernet or WiFi on the router/switch
3. Browse to ```http://<board IP address>```

### Connecting to Jupyter Notebook
Once your board is setup, to connect to Jupyter Notebooks open a web browser and navigate to:
```http://192.168.2.99``` If your board is connected to a computer via a static IP address
If your board is configured correctly you will be presented with a login screen. 
* The username is xilinx and the password is also xilinx.

</br>
<img src="https://github.com/user-attachments/assets/9bbbc444-1f6a-4af0-a1ae-db2c92ce2004" width=400>

