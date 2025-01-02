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
### Troubleshouting 
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
