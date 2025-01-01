

---
## Asyncio Integration
PYNQ also leverages the Python asyncio module for communicating with programmable logic devices through events (namely interrupts).

* A Python program running on PYNQ can use the asyncio library to manage multiple IO-bound tasks asynchronously, thereby avoiding any blocking caused by waiting for responses from slower IO subsystems. 
* Instead, the program can continue to execute other tasks that are ready to run. 
* When the previously-busy tasks are ready to resume, they will be executed in turn, and the cycle is repeated.
