# PYNQ Utilitis

---
## PYNQ-Z2 Wifi settings

```
# wifi.py
from pynq.lib import Wifi
port = Wifi()
port.connect('LABS', 'arm12345')
#!ping -I wlan0 www.yahoo.com -c 10
# port.reset()
```

---
### nmcli
```
$ sudo apt-get install network-manager
$ sudo nmcli dev wifi connect <SSID> password <PASSWD>
$ sudo nmcli dev wifi connect SOCLABS password Call6576886
$ sudo nmcli dev wifi connect LABS password arm12345
```

---
### wifi settings
```
auto wlan0
allow-hotplug wlan0
iface wlan0 inet dhcp
wpa-ssid LABS
wpa-psk 1899ea07044c0cb7dd5b9917f9ccc03bc9023bf785d01aba390bd5021c1347b9
wpa-scan-ssid 1
```

---
### Troubleshouting 

```
## /etc/network/interfaces.d/eth0
auto eth0
iface eth0 inet dhcp
auto eth0:1
iface eth0:1 inet static
address 192.168.2.99
netmask 255.255.255.0
```


```
ipython
/etc/network/if-up.d/resolved: 12: mystatedir: not found
```

---

```
sudo apt-cache search pydantic
sudo apt install python3-pydantic
```

---
#### ModuleNotFoundError: No module named 'pynqutils'
``` 
ModuleNotFoundError: No module named 'pynqutils'
pip3 install pynq
```

Please use pip3 install pynq to upgrade to pynq v2.6.2
``` 
sudo pip3 install pynq==2.6.2
```

Expected log message
```
Successfully built pynq
Successfully uninstalled pynq-2.6.0
Successfully installed pynq-2.6.2
```
