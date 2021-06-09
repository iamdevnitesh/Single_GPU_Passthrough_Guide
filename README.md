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
6. Downloaded Windows 10 ISO 64-bit

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



### Step 9: Follow the Commands given below:
    
    cd Downloads
    
    git clone https://github.com/iamcodernitesh/Single_GPU_Passthrough_Guide.git
    
    cd Single_GPU_Passthrough_Guide/
    
    chmod +x gpu_passthrough.sh
    
    sudo ./gpu_passthrough.sh
    
After running this command some tools will get install. And after than You'll get to see something like this:
It will also ask "Do you wan to edit it?". Press n     
     
     Complete!
     Creating backups
     Set Intel IOMMU On
     GRUB_CMDLINE_LINUX="rhgb quiet intel_iommu=on rd.driver.pre=vfio-pci kvm.ignore_msrs=1"

     Grub was modified to look like this: 
     GRUB_CMDLINE_LINUX="rhgb quiet intel_iommu=on rd.driver.pre=vfio-pci kvm.ignore_msrs=1"

     Do you want to edit it? y/n
     n
     Getting GPU passthrough scripts ready
     Updating grub and generating initramfs
     Generating grub configuration file ...
     Adding boot menu entry for UEFI Firmware Settings ...
     done



### Step 10: Now Follow the commands given below:
    sudo reboot
    
After reboot is complete open up terminal and type
       
      lspci -k
      
This command will give output something/similar to this:
```
[niteshkumar@fedora ~]$ lspci -k
00:00.0 Host bridge: Intel Corporation 8th Gen Core Processor Host Bridge/DRAM Registers (rev 0a)
	DeviceName: Onboard - Other
	Subsystem: Micro-Star International Co., Ltd. [MSI] Device 7b17
	Kernel driver in use: skl_uncore
	Kernel modules: ie31200_edac
00:01.0 PCI bridge: Intel Corporation 6th-10th Gen Core Processor PCIe Controller (x16) (rev 0a)
	Kernel driver in use: pcieport
00:02.0 VGA compatible controller: Intel Corporation CoffeeLake-S GT2 [UHD Graphics 630]			//THIS SHOULD BE PRESENT WHICH WILL HELP INTEL GPU RUN ON LINUX
	DeviceName: Onboard - Video
	Subsystem: Micro-Star International Co., Ltd. [MSI] Device 7b17
	Kernel driver in use: i915
	Kernel modules: i915*
00:08.0 System peripheral: Intel Corporation Xeon E3-1200 v5/v6 / E3-1500 v5 / 6th/7th/8th Gen Core Processor Gaussian Mixture Model
	DeviceName: Onboard - Other
	Subsystem: Micro-Star International Co., Ltd. [MSI] Device 7b17
00:12.0 Signal processing controller: Intel Corporation Cannon Lake PCH Thermal Controller (rev 10)
	DeviceName: Onboard - Other
	Subsystem: Micro-Star International Co., Ltd. [MSI] Device 7b17
	Kernel driver in use: intel_pch_thermal
	Kernel modules: intel_pch_thermal
00:14.0 USB controller: Intel Corporation Cannon Lake PCH USB 3.1 xHCI Host Controller (rev 10)
	DeviceName: Onboard - Other
	Subsystem: Micro-Star International Co., Ltd. [MSI] Device 7b17
	Kernel driver in use: xhci_hcd
00:14.2 RAM memory: Intel Corporation Cannon Lake PCH Shared SRAM (rev 10)
	DeviceName: Onboard - Other
	Subsystem: Intel Corporation Device 7270
00:14.3 Network controller: Intel Corporation Cannon Lake PCH CNVi WiFi (rev 10)
	DeviceName: Onboard - Ethernet
	Subsystem: Intel Corporation Device 02a4
	Kernel driver in use: iwlwifi
	Kernel modules: iwlwifi
00:16.0 Communication controller: Intel Corporation Cannon Lake PCH HECI Controller (rev 10)
	DeviceName: Onboard - Other
	Subsystem: Micro-Star International Co., Ltd. [MSI] Device 7b17
	Kernel driver in use: mei_me
	Kernel modules: mei_me
00:17.0 SATA controller: Intel Corporation Cannon Lake PCH SATA AHCI Controller (rev 10)
	DeviceName: Onboard - SATA
	Subsystem: Micro-Star International Co., Ltd. [MSI] Device 7b17
	Kernel driver in use: ahci
00:1b.0 PCI bridge: Intel Corporation Cannon Lake PCH PCI Express Root Port #17 (rev f0)
	Kernel driver in use: pcieport
00:1f.0 ISA bridge: Intel Corporation Z390 Chipset LPC/eSPI Controller (rev 10)
	DeviceName: Onboard - Other
	Subsystem: Micro-Star International Co., Ltd. [MSI] Device 7b17
00:1f.3 Audio device: Intel Corporation Cannon Lake PCH cAVS (rev 10)
	DeviceName: Onboard - Sound
	Subsystem: Micro-Star International Co., Ltd. [MSI] Device 7b17
	Kernel driver in use: snd_hda_intel
	Kernel modules: snd_hda_intel, snd_soc_skl, snd_sof_pci_intel_cnl
00:1f.4 SMBus: Intel Corporation Cannon Lake PCH SMBus Controller (rev 10)
	DeviceName: Onboard - Other
	Subsystem: Micro-Star International Co., Ltd. [MSI] Device 7b17
	Kernel driver in use: i801_smbus
	Kernel modules: i2c_i801
00:1f.5 Serial bus controller [0c80]: Intel Corporation Cannon Lake PCH SPI Controller (rev 10)
	DeviceName: Onboard - Other
	Subsystem: Micro-Star International Co., Ltd. [MSI] Device 7b17
00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection (7) I219-V (rev 10)
	DeviceName: Onboard - Ethernet
	Subsystem: Micro-Star International Co., Ltd. [MSI] Device 7b17
	Kernel driver in use: e1000e
	Kernel modules: e1000e
01:00.0 VGA compatible controller: NVIDIA Corporation TU106 [GeForce RTX 2070] (rev a1)		//THE NVIDIA CARD SHOULD BE vfio-pci in kernel driver in use
	Subsystem: Micro-Star International Co., Ltd. [MSI] Device 3733
	Kernel driver in use: vfio-pci
	Kernel modules: nouveau
01:00.1 Audio device: NVIDIA Corporation TU106 High Definition Audio Controller (rev a1)	//Same for this nvidia card
	Subsystem: Micro-Star International Co., Ltd. [MSI] Device 3733
	Kernel driver in use: vfio-pci
	Kernel modules: snd_hda_intel
01:00.2 USB controller: NVIDIA Corporation TU106 USB 3.1 Host Controller (rev a1)
	Subsystem: Micro-Star International Co., Ltd. [MSI] Device 3733
	Kernel driver in use: xhci_hcd
01:00.3 Serial bus controller [0c80]: NVIDIA Corporation TU106 USB Type-C UCSI Controller (rev a1)
	Subsystem: Micro-Star International Co., Ltd. [MSI] Device 3733
	Kernel driver in use: nvidia-gpu
	Kernel modules: i2c_nvidia_gpu
02:00.0 Non-Volatile memory controller: Micron Technology Inc Device 5405
	Subsystem: Micron Technology Inc Device 0100
	Kernel driver in use: nvme
	Kernel modules: nvme
```



**Now lets us learn something with reference to the above output.
So, now what we did is we made our nvidia card passthrough vfio-pci which we will be using in our virtual machine
Now, we'll ensure that if IOMMU Groups are valid, In short we'll see what are all the devices we can use in our virtual machine**

### Step 11: Copy the command given below and paste it in terminal
	#!/bin/bash
	shopt -s nullglob
	for g in `find /sys/kernel/iommu_groups/* -maxdepth 0 -type d | sort -V`; do
    		echo "IOMMU Group ${g##*/}:"
    		for d in $g/devices/*; do
        		echo -e "\t$(lspci -nns ${d##*/})"
    		done;
	done;
	
	
My output:
```
IOMMU Group 0:
	00:00.0 Host bridge [0600]: Intel Corporation 8th Gen Core Processor Host Bridge/DRAM Registers [8086:3ec2] (rev 0a)
IOMMU Group 1:
	00:01.0 PCI bridge [0604]: Intel Corporation 6th-10th Gen Core Processor PCIe Controller (x16) [8086:1901] (rev 0a)
	01:00.0 VGA compatible controller [0300]: NVIDIA Corporation TU106 [GeForce RTX 2070] [10de:1f02] (rev a1)
	01:00.1 Audio device [0403]: NVIDIA Corporation TU106 High Definition Audio Controller [10de:10f9] (rev a1)
	01:00.2 USB controller [0c03]: NVIDIA Corporation TU106 USB 3.1 Host Controller [10de:1ada] (rev a1)
	01:00.3 Serial bus controller [0c80]: NVIDIA Corporation TU106 USB Type-C UCSI Controller [10de:1adb] (rev a1)
IOMMU Group 2:
	00:02.0 VGA compatible controller [0300]: Intel Corporation CoffeeLake-S GT2 [UHD Graphics 630] [8086:3e98]
IOMMU Group 3:
	00:08.0 System peripheral [0880]: Intel Corporation Xeon E3-1200 v5/v6 / E3-1500 v5 / 6th/7th/8th Gen Core Processor Gaussian Mixture Model [8086:1911]
IOMMU Group 4:
	00:12.0 Signal processing controller [1180]: Intel Corporation Cannon Lake PCH Thermal Controller [8086:a379] (rev 10)
IOMMU Group 5:
	00:14.0 USB controller [0c03]: Intel Corporation Cannon Lake PCH USB 3.1 xHCI Host Controller [8086:a36d] (rev 10)
	00:14.2 RAM memory [0500]: Intel Corporation Cannon Lake PCH Shared SRAM [8086:a36f] (rev 10)
IOMMU Group 6:
	00:14.3 Network controller [0280]: Intel Corporation Cannon Lake PCH CNVi WiFi [8086:a370] (rev 10)
IOMMU Group 7:
	00:16.0 Communication controller [0780]: Intel Corporation Cannon Lake PCH HECI Controller [8086:a360] (rev 10)
IOMMU Group 8:
	00:17.0 SATA controller [0106]: Intel Corporation Cannon Lake PCH SATA AHCI Controller [8086:a352] (rev 10)
IOMMU Group 9:
	00:1b.0 PCI bridge [0604]: Intel Corporation Cannon Lake PCH PCI Express Root Port #17 [8086:a340] (rev f0)
IOMMU Group 10:
	00:1f.0 ISA bridge [0601]: Intel Corporation Z390 Chipset LPC/eSPI Controller [8086:a305] (rev 10)
	00:1f.3 Audio device [0403]: Intel Corporation Cannon Lake PCH cAVS [8086:a348] (rev 10)
	00:1f.4 SMBus [0c05]: Intel Corporation Cannon Lake PCH SMBus Controller [8086:a323] (rev 10)
	00:1f.5 Serial bus controller [0c80]: Intel Corporation Cannon Lake PCH SPI Controller [8086:a324] (rev 10)
	00:1f.6 Ethernet controller [0200]: Intel Corporation Ethernet Connection (7) I219-V [8086:15bc] (rev 10)
IOMMU Group 11:
	02:00.0 Non-Volatile memory controller [0108]: Micron Technology Inc Device [1344:5405]
```

In the above output we can see different IOMMU Groups.

**Group 1: nvidia Drivers**

**Group 10: audio drivers, ethernet drivers**

### STEP 11: CREATING VIRTUAL MACHINE
Here its Just a GUI thing. Just Follow me.

##### i) Open the Virtual Machine from menu ->
   
   <p align="center">
       <img src=https://user-images.githubusercontent.com/73643989/121346534-dea0bd00-c943-11eb-8949-365d4803ac17.png | width=900>
   </p>
   
   It will ask for password. Enter it.
   
##### ii) Create a new Virtual machine 
On the Top left Click File -> New Virtual Machine.

   <p align="center">
       <img src=https://user-images.githubusercontent.com/73643989/121352696-bbc5d700-c94a-11eb-86fa-de65367b71d4.png | width=900>
   </p>
   
##### iii) Select the locally installed ISO file
You'll get a window like shown below. Select **Local Install** & Click **Forward**.

   <p align="center">
       <img src=https://user-images.githubusercontent.com/73643989/121353091-1c551400-c94b-11eb-9d0e-a469b759676c.png | width=900>
   </p>
   
You will reach a window as shown below. Click **Browse**.

   <p align="center">
       <img src=https://user-images.githubusercontent.com/73643989/121353414-7655d980-c94b-11eb-9b47-df2f450537fc.png | width=900>
   </p>
   
Again a new window will pop up as shown below. Select **Browser Local** located at bottom right of window.

   <p align="center">
       <img src=https://user-images.githubusercontent.com/73643989/121353907-fd0ab680-c94b-11eb-94ff-152b23689324.png | width=900>
   </p>

Another window will pop up opening the file manager. Browser your Windows_10.iso file through the file manager and Click Open.
Mine is located at Download as you can see in the image below.

   <p align="center">
       <img src=https://user-images.githubusercontent.com/73643989/121354103-33483600-c94c-11eb-93cf-f3be46409b0d.png | width=900>
   </p>
   
Now, You'll see a window where the virtual machine will be detecting OS. If somehow Windows 10 is not detected. Enter manually as shown below

   <p align="center">
       <img src=https://user-images.githubusercontent.com/73643989/121354364-70142d00-c94c-11eb-9d3b-3a5ad99040ac.png | width=900>
   </p>
   
Click on **Forward**.
A pop up will appear as shown below. Click on **Yes**.

   <p align="center">
       <img src= | width=900>
   </p>
