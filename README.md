# Single_GPU_Passthrough_Guide

Hello everyone, this guide will help you passthrought your nVidia/AMD GPU on to a Virtual Machine.
You can follow this Github guide or if you are a linux noob you can follow this video guide.

## Who is this for ?
This guide is for all the people who wants to use linux and windows/other OS at same time.

## Requirements:
1. Discrete GPU (nVidia/AMD).
2. Integrated GPU [(intel based GPUs)](https://www.intel.com/content/www/us/en/support/articles/000057924/processors/intel-core-processors.html).
3. Monitor - A single monitor is enough but if you have 2 monitors it will be more efficient.
4. Make sure you have enough RAM to make both host and virtual OS work.
5. Any Linux Distribution.

## My Setup:
1. CPU - [Intel® Core™ i5-9600K Processor](https://ark.intel.com/content/www/us/en/ark/products/134896/intel-core-i5-9600k-processor-9m-cache-up-to-4-60-ghz.html)
2. Motherboard - [MSI Z390 Gaming Edge AC](https://www.msi.com/Motherboard/mpg-z390-gaming-edge-ac)
3. GPU - [MSI RTX 2080 Gaming X Trio](https://www.msi.com/Graphics-Card/GeForce-RTX-2080-GAMING-X-TRIO)
4. RAM - [Corsair Vegeance LPX 16GB 3000Mhz](https://www.corsair.com/ww/en/Categories/Products/Memory/VENGEANCE%C2%AE-LPX-16GB-%281-x-16GB%29-DDR4-DRAM-3000MHz-C16-Memory-Kit---Black/p/CMK16GX4M1D3000C16) x2
5. OS - [Fedora 34](https://getfedora.org/en/workstation/download/)

## :warning:Warning !:warning:
1. Make sure you have enough CPU/RAM resources to distribute on both the resources.
2. Laptops are not recommended as we'll be changing the display ports between Motherboard and GPU back and forth.
3. Trying to passthrough nvidia GPU on a macOS virtual machine is not recommended as macOS dropped nvidia support after High Sierra.

## STEPS

### Step 1: Install fedora 34 using this [guide].
### Step 2: After installing open up the terminal and type
    sudo dnf update -y
and press enter.
   <p align="center">
       <img src=https://user-images.githubusercontent.com/73643989/121302116-d2523b00-c916-11eb-8896-aac80b7811c7.png>
   </p>
   
### Step 3: After the update is complete type
    sudo shutdown
in the terminal and press Enter.
### Step 4: Remove your HDMI/DP from the GPU slot and connect it to the Motherboard slot.
   <p align="center">
       <img width="460" height="300" src="![port_switch](https://user-images.githubusercontent.com/73643989/121296648-039f1c80-c8bf-11eb-86d2-d1411506c5d8.jpg)">
   </p>
### Step 5: Boot into your BIOS and go to advance settings and change Intel Graphics Configuration to IGD instead of PEG.
