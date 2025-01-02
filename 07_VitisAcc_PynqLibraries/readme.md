# PYNQ Libraries

https://github.com/Xilinx/PYNQ/tree/v3.0.1/docs/source/pynq_libraries

---
## Overlay
* The Overlay class is used to load PYNQ overlays to the PL, and manage and control existing overlays.
* The class is instantiated with the .bit file for an overlay.
* By default the overlay HWH file will be parsed, and the bitstream will be downloaded to the PL.
* This means that to use the overlay class, a .bit and .hwh must be provided for an overlay.

#### Examples
```
from pynq import Overlay
base = Overlay("base.bit") # bitstream implicitly downloaded to PL
```

---
## MMIO
https://github.com/Xilinx/PYNQ/blob/v3.0.1/docs/source/pynq_libraries/mmio.rst

* The MMIO class allows a Python object to access addresses in the **system memory** mapped.
* In particular, **registers and address space of peripherals in the PL** can be accessed.
* MMIO provides a simple but powerful way to access and control peripherals.
    * For simple peripherals with a small number of memory accesses, or where performance is not critical, MMIO is usually sufficient for most developers.
    * If performance is critical, or large amounts of data need to be transferred between PS and PL, using the Zynq HP interfaces with **DMA IP** and the **PYNQ DMA class** may be more appropriate.

<img src="https://github.com/user-attachments/assets/c8a34280-d769-4c09-92c5-ea39fe40a1f3" width=350>

#### Example
In this example, data is written to an IP and read back from the same address.
```
IP_BASE_ADDRESS = 0x40000000
ADDRESS_RANGE = 0x1000
ADDRESS_OFFSET = 0x10
from pynq import MMIO
mmio = MMIO(IP_BASE_ADDRESS, ADDRESS_RANGE)

data = 0xdeadbeef
mmio.write(ADDRESS_OFFSET, data)
result = mmio.read(ADDRESS_OFFSET)
```

---
## DMA
https://github.com/Xilinx/PYNQ/blob/v3.0.1/docs/source/pynq_libraries/dma.rst

* PYNQ supports the AXI central DMA IP with the PYNQ DMA class.
* DMA can be used for high performance burst transfers between PS DRAM and the PL.
* The DMA class supports simple mode only.

#### Block Diagram

<br/>
<img src="https://github.com/user-attachments/assets/5c293ec5-3207-406b-9b17-cb6742df7c14" width=450>
<br/><br/>

* The DMA has an **AXI lite** control interface, and a read and write channel which consist of a **AXI master port** to access the memory location, and a stream port to connect to an IP.
* The **read channel** will read from **PS DRAM**, and write to a stream.
* The **write channel** will read from a stream, and write back to **PS DRAM**.
  * Note that the DMA expects any streaming IP connected to the DMA (write channel) to set the AXI TLAST signal when the transaction is complete. If this is not set, the DMA will never complete the transaction.
  * This is important when using HLS to generate the IP - the TLAST signal must be set in the C code.

---
## Allocate
https://github.com/Xilinx/PYNQ/blob/v3.0.1/docs/source/pynq_libraries/allocate.rst

* The **pynq.allocate** function is used to allocate memory that will be used by IP in the programmable logic.
* IP connected to the AXI Master (HP or ACP ports) has access to PS DRAM. Before IP in the PL accesses DRAM, some memory must first be allocated (reserved) for the IP to use and the size, and address of the memory passed to the IP.
* An array in Python, or Numpy, will be allocated somewhere in virtual memory.
* The **physical memory address** of the allocated memory must be provided to IP in the PL.
* **pynq.allocate** allocates memory which is physically contiguous and returns a **pynq.Buffer** object representing the allocated buffer.
* The buffer is a **numpy array** for use with other Python libraries and also provides a **.device_address** property which contains the **physical address** for use with IP. For backwards compatibility a .physical_address property is also provided
* The allocate function uses the same signature as numpy.ndarray allowing for any **shape and data-type supported by numpy** to be used with PYNQ.

#### Buffer
The Buffer object returned is a sub-class of numpy.ndarray with additional properties and methods suited for use with the programmable logic.
* device_address is the address that should be passed to the programmable logic to access the buffer
* coherent is True if the buffer is cache-coherent between the PS and PL
* flush flushes a non-coherent or mirrored buffer ensuring that any changes by the PS are visible to the PL
* invalidate invalidates a non-coherent or mirrored buffer ensuring any changes by the PL are visible to the PS
* sync_to_device is an alias to flush
* sync_from_device is an alias to invalidate

#### Example

Create a contiguous array of 5 32-bit unsigned integers
```
from pynq import allocate
input_buffer = allocate(shape=(5,), dtype='u4')
```
device_address property of the buffer
```
input_buffer.device_address
```

Writing data to the buffer:
```
input_buffer[:] = range(5)
```

Flushing the buffer to ensure the updated data is visible to the programmable logic:
```
input_buffer.flush()
```

More information about memory allocation can be found in the :ref:`pynq-buffer` section in the library reference.
