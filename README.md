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



### Step 4: Boot into your BIOS and go to advance settings and change Intel Graphics Configuration to IGD instead of PEG.
Now, boot into your BIOS and enable Intel VT-d/VT-x or if you have AMD CPU enable AMD-v/AMD-svm

#### For MSI Motherboards: 
Please enter BIOS setup and go to OC => CPU Features  => Intel Virtualization Tech => Enable
                                                      => Intel VT-d Tech => Enable
(Note: You can find all these settings for all motherboard vendors on the internet,forums or official site motherboard guide)

#### Here are the images for my Motherboard configuration

###### This is the default BIOS Page
   <p align="center">
       <img src=https://user-images.githubusercontent.com/73643989/121306114-16940a00-c91c-11eb-91d9-6beddc2ad11c.jpeg>
   </p>
   
###### Click on OC
   <p align="center">
       <img src=https://user-images.githubusercontent.com/73643989/121306198-2b709d80-c91c-11eb-8a1e-6c4d3c53849a.jpeg>
   </p>
   
###### Scroll down till you see CPU features
   <p align="center">
       <img src=https://user-images.githubusercontent.com/73643989/121306247-388d8c80-c91c-11eb-8c04-0407151d2ba6.jpeg>
   </p>
   
###### Click on CPU features and enable Intel Virtualization Tech
   <p align="center">
       <img src=https://user-images.githubusercontent.com/73643989/121306300-4b07c600-c91c-11eb-977f-401a26226072.jpeg>
   </p>
   
###### Enable Intel VT-D Tech
   <p align="center">
       <img src=https://user-images.githubusercontent.com/73643989/121306353-59ee7880-c91c-11eb-8b46-8515389b8ed0.jpeg>
   </p>
   
   

### Step 5: Changing the Intel Graphics Configuration on BIOS
For this part as well you will find solutions on forums or official website.

#### Here are the images for my Motherboard configuration

###### This is the default BIOS Page
   <p align="center">
       <img src=https://user-images.githubusercontent.com/73643989/121306114-16940a00-c91c-11eb-91d9-6beddc2ad11c.jpeg>
   </p>
   
###### Click on Settings
   <p align="center">
       <img src=https://user-images.githubusercontent.com/73643989/121307154-57405300-c91d-11eb-81ee-29a911ff394b.jpeg>
   </p>
   
###### Click on Advanced
   <p align="center">
       <img src=https://user-images.githubusercontent.com/73643989/121307251-6d4e1380-c91d-11eb-9b7c-9d77236efa7b.jpeg>
   </p>
   
###### Click on Integrated Graphics Configuration
   <p align="center">
       <img src=https://user-images.githubusercontent.com/73643989/121307380-8eaeff80-c91d-11eb-82c7-16d43ac4f0fb.jpeg>
   </p>

###### Change Initiate Graphics Adapter to IGD
   <p align="center">
       <img src=https://user-images.githubusercontent.com/73643989/121307467-a71f1a00-c91d-11eb-9bfe-de95a2260415.jpeg>
   </p>



### Step 6: Save and Exit BIOS



### Step 7: Remove the cable connected to GPU HDMI/DP port and connect it to the motherboard. So, that intel iGPU will be used as a display adapter for linux.
   <p align="center">
       <img src=https://user-images.githubusercontent.com/73643989/121302366-34ab3b80-c917-11eb-8b48-518436328315.png>
   </p>
 


### Step 8: After logging in to Fedora/OS. Open terminal and update once again using the command given below:
    sudo dnf update -y
Most probably there won't be any update if there are complete it.



### Step 9: Clone my github to Downloads folder.
