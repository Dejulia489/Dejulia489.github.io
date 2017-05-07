---
layout: post
title: Powershell How to Create a Virtual Machine in Hyper V
---

Now that we have enabled Hyper V we can utilize the built in Hyper V module. At the time of this post the Hyper V Module contains 232 commands, which is a rather robust module providing a lot of functionality. We will need to leverage the help documentation for this module to better understand the Functions we have at our disposal. 

###### We can use the snippet below to update our help files.

	Update-Help


## Creating a new VHD
Before we can create a new VM we will first need to create a virtual hard drive. 

###### We can use the snippet below to create a 20GB dynamic VHD.

	New-VHD -Dynamic -Path 'C:\Virtual HardDrives\MediaServer.vhdx'-SizeBytes 2e+10


## Creating a new VM
Before we can create a new VM we will first need to create a virtual hard drive. 

###### We can use the snippet below to create a 20GB dynamic VHD.

	New-VM -Name MediaServer -VHDPath 'C:\Virtual HardDrives\MediaServer.vhdx' -Path 'C:\VirtualMachines' 


## Reviewing VM configuration
Now that we have a new VM to work with let's check on the default configuration. 

###### We can use the snippet below to get our VM configuration.

	Get-VM -Name MediaServer | Select-Object -Property *  


## Adding a Network Switch
We will eventually want our new VM to connect to the internet, so lets create and add a VMSwitch. 

###### We can use the snippet below to create a VMSwitch.

	New-VMSwitch -Name VirtualSwitch1 -SwitchType Internal | 
		Set-VMSwitch -NetAdapterName Ethernet  


###### We can use the snippet below to locate the NetAdapterName.

	Get-NetAdapter  


###### We can use the snippet below to connect the switch to the VM.

	Get-VM -Name MediaServer | 
		Get-VMNetworkAdapter | 
		Connect-VMNetworkAdapter -SwitchName 'VirtualSwitch1'  


## Bootstrapping an Operating System

We will need to run an Operating System on our new VM, you can use your favorite but for this post I will use Ubuntu Studio. [Click here](https://docs.microsoft.com/en-us/windows-server/virtualization/hyper-v/best-practices-for-running-linux-on-hyper-v) for Microsofts Best Practices for running Linux on Hyper-V.

###### We can use the snippet below to attach the OS .iso the VM.

	Get-VMDvdDrive -VMName MediaServer | 
		Set-VMDvdDrive -Path 'C:\Operating Systems\ubuntustudio-16.04.1-dvd-amd64.iso' |
		Start-VM -VMName MediaServer


Unfortunately the process to install the Linux OS requires some manual intervention. I will revisit this process at a later time to resolve this issue.

...to be continued