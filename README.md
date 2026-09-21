# devboardnetworkinganalytics

## project outline / architecture

Python script or C sockets transmitting UDP/Ethernet over Cat5e/6 from Raspberry PI
Zynq ARM receives with Gigabit Ethernet MAC with C IwIP or PetaLinux
Zedboard PS pushes packets to programmable logic via AXI4-Stream - FPGA logic inspects stream, drops invalid packets, increments internal counters for reporting analytics

The valid packets can then be sent into a standard Xilinx AXI DMA IP which will handle the memory access.

## STAGES

### Stage 1:
  RPi
  Vivado
  Software

### Stage 2:
  RTL
  Testbench
  Analytics

### Stage 3
  RTL filter packaged as custom Vivado IP

### Stage 4
  Buffer

## Critical Points:
  1. if filter logic drops packets - tready must be asserted to overwrite the bad data without sending to the DMA
  2. keep track of tlast with considerations of the dropped packets to make sure the DMA doesn't get locked
  3. PetaLlinux will take a while so Xilinx Vitis with IwIP stack will work better
  4. Make the filtering simple - it is more about the inter-module networking and infrastructure
