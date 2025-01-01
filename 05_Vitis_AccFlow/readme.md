# Vitis™ Application Acceleration Development Flow

AMD Vitis Tutorials [[Github]](https://github.com/Xilinx/Vitis-Tutorials/tree/2023.2/Getting_Started 
)
 
An overview of the Vitis workflow including kernel development, host software creation, emulation, implementation, and analysis. This tutorial is divided into separate flows:
* Data Center
* Embedded Processor
* Vitis Unified IDE

---
### AMD Vitis™ Vitis Unified IDE

* Vitis HLS
  * In-Depth how to optimize, implement, and unit test individual hardware accelerators from within the Vitis High-Level Synthesis environment.
* Vitis Libraries
  * Learn how to leverage a L1 Vitis library element to build your own design. The FFT example is selected for explanation, and you may follow similar flow to use other library elements.
* Vitis Platform
  * Create and validate a Vitis embedded acceleration platform on Versal by using the Versal Extensible Platform from Vivado Customizable Example Design and pre-built Linux common images.
* Vitis Unified IDE for Embedded Design
  * Basic steps of the Vitis Embedded design flow and uses the Vitis Unified IDE.  
  * The steps include creating the platform, adding hello world application, setting up the target connection and deploying to the target board.

---
### Vitis™ Application Acceleration Development Flow

* The Vitis tool provides a unified flow for developing FPGA accelerated application targeted to either Data Center accelerator cards or Embedded Processor platforms.  
* Get started with FPGA acceleration

<img src="https://github.com/user-attachments/assets/8fe3fea5-e672-4079-8494-fea2b0818a4b" width=650>

---
### Vitis Essential Concepts

* The Vitis unified software platform provides a framework for developing and delivering Adaptive SoC and FPGA accelerated applications using standard programming languages like C and C++. 
* The Vitis flow offers all of the features of a standard software development environment, including:
  * Compiler or cross-compiler for host applications running on x86 or Arm® processors
  * Cross-compilers for building the FPGA binary
  * Debugging environment to help identify and resolve issues in the code
  * Performance profilers to identify bottlenecks and help you optimize the application

---
### Vitis Programming and Execution Model

* A Vitis accelerated application consists of two distinct components: 
  * A software program running on a standard processor such as an X86 processor or ARM embedded processor.
  * And a AMD device binary (xclbin) containing hardware accelerated functions, or kernels.
* Vitis accelerated applications can execute on either Data Center or Embedded Processor acceleration platforms:
  * On Data Center accelerator cards, the software program runs on an x86 server and the kernels run in the FPGA on a PCIe®-attached acceleration card.
  * On Embedded Processor platforms, the software program runs on an Arm processor of an AMD MPSoC device and the kernels run within the same device.

<img src="https://github.com/user-attachments/assets/6a38b76f-8dff-46ee-b99c-191ae8dcb4db" width=550>

* The software program, or host application, is written in C/C++ and runs on a conventional CPU. 
* The software program uses the XRT native API implemented by the AMD Runtime library (XRT) to interact with * the acceleration kernel in the AMD device.
* The hardware accelerated kernels can be written in C/C++ or RTL (Verilog or VHDL) and run within the programmable logic part of the AMD device. 
