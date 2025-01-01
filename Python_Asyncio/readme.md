# PYNQ and Asyncio

* PYNQ v2.0 [[pynq.readthedocs]](https://pynq.readthedocs.io/en/v2.0/overlay_design_methodology/pynq_and_asyncio.html)

---
## Numpy Data Movement
* Simple data movement code snippet that can be used to share data with programmable logic. 
* Leverage the **Python numpy package** to manipulate the buffer on the Arm processors and can then send a buffer pointer to programmable logic for sharing data.
* Asyncio Integration: PYNQ also leverages the **Python asyncio module** for communicating with programmable logic devices through events (namely interrupts).


---
## Example

<img src="https://github.com/user-attachments/assets/33e55b10-cad5-4c8e-a44d-98857abb5e0a" width=650>

* To send the buffer pointer to programmable logic, we use its physical address which is what programmable logic would need to communicate using this shared buffer.

<img src="https://github.com/user-attachments/assets/fce76486-98db-4254-bfb7-4fbb4471506f" width=450>

* In this short example, we showed a simple allocation of a numpy array that is now ready to be shared with programmable logic devices. With numpy arrays that are accessible to programmable logic, we can quickly manipulate and move data across software and hardware.

---
## Asyncio Integration
PYNQ also leverages the Python asyncio module for communicating with programmable logic devices through events (namely interrupts).

* A Python program running on PYNQ can use the asyncio library to manage multiple IO-bound tasks asynchronously, thereby avoiding any blocking caused by waiting for responses from slower IO subsystems. 
* Instead, the program can continue to execute other tasks that are ready to run. 
* When the previously-busy tasks are ready to resume, they will be executed in turn, and the cycle is repeated.

---
## Asyncio Example

* A function that will yield to asyncio.sleep() for a few seconds and then resume, having preserved its state while suspended

<img src="https://github.com/user-attachments/assets/624f4990-e34b-4a1e-9765-886d30af80ba" width=450>

* Show here a software-only asyncio example that uses asyncio's sleep method.
* With the wake_up function defined, we then can add a new task to the event loop

<img src="https://github.com/user-attachments/assets/d8c6dcdd-6b23-4cad-aa7f-7b632a59d618" width=450>



