# PYNQ Utilitis

---
## PYNQ-Z2 Wifi settings

```
# wifi.py
from pynq.lib import Wifi
from pynq.lib import pynqutils
#from pydantic import BaseModel
port = Wifi()
port.connect('LABS', 'arm12345')
#!ping -I wlan0 www.yahoo.com -c 10
# port.reset()
```

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
