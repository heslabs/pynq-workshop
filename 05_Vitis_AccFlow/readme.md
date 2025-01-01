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
## Vitis™ Application Acceleration Development Flow

AMD Vitis Tutorials [[Github]](https://github.com/Xilinx/Vitis-Tutorials/tree/2023.2/Getting_Started/Vitis)

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
<br/><br/>
<img src="https://github.com/user-attachments/assets/6a38b76f-8dff-46ee-b99c-191ae8dcb4db" width=550>
<br/><br/>
* The software program, or host application, is written in C/C++ and runs on a conventional CPU. 
* The software program uses the XRT native API implemented by the AMD Runtime library (XRT) to interact with * the acceleration kernel in the AMD device.
* The hardware accelerated kernels can be written in C/C++ or RTL (Verilog or VHDL) and run within the programmable logic part of the AMD device. 

---
### Interaction between Software and Hardware

There are multiple ways by which the software program can interact with the hardware kernels. The simplest method can be decomposed into the following steps:

1. The host application writes the data needed by a kernel into the global memory of the FPGA device.
2. The host program sets up the input parameters of the kernel.
3. The host program triggers the execution of the kernel.
4. The kernel performs the required computation, accessing global memory to read or write data, as necessary. Kernels can also use streaming connections to communicate with other kernels, passing data from one kernel to the next.
5. The kernel notifies the host that it has completed its task.
6. The host program transfers data from global memory back into host memory, or can give ownership of the data to another kernel.

---
### Vitis Build Process
The Vitis build process follows a standard compilation and linking process for both the host program and the kernel code:

* The host program is built using the GNU C++ compiler (g++) for Data Center applications or the GNU C++ Arm cross-compiler for Embedded Processor devices.
* The FPGA binary is built using the Vitis compiler (v++). First the kernels are compiled into a AMD object (.xo) file. Then, the .xo files are linked with the hardware platform to generate the AMD device binary (.xclbin) file. 
* As described in V++ Command, the Vitis compiler and linker accepts a wide range of options to tailor and optimize the results.

<br/><br/>
<img src="https://github.com/user-attachments/assets/12dcf42e-d712-41aa-85ac-47f9dc72cb8e" width=550>
<br/><br/>

* The Vitis build process follows a standard compilation and linking process for both the host program and the kernel code

---
### Vitis Build Targets

The Vitis compiler provides three different build targets

* Software Emulation
  * The kernel code is compiled to run on the host processor. This allows iterative algorithm refinement through fast build-and-run loops.
  * This target is useful for identifying syntax errors, performing source-level debugging of the kernel code running together with application, and verifying the behavior of the system.
* Hardware Emulation
  * The kernel code is compiled into a hardware model (RTL), which is run in a dedicated simulator. This build-and-run loop takes longer but provides a detailed, cycle-accurate view of kernel activity.
  * This target is useful for testing the functionality of the logic that will go in the FPGA and getting initial performance estimates.
* Hardware
  * The kernel code is compiled into a hardware description language (RTL), and then synthesized and implemented for a target AMD device, resulting in a binary (xclbin) file that will run on the actual FPGA.
