---
layout: post
title: How to Create a Linux Virtual Server in Hyper V with Powershell
---

Now that we have [enabled Hyper V](https://dejulia489.github.io/2017-05-05-EnableHyperVWindows10/) we can utilize the built in Hyper V module. At the time of this post the Hyper V Module contains 232 commands, which is a rather robust module providing a lot of functionality. 

## Update Help

We will need to leverage the help documentation for this module to better understand the Functions we have at our disposal. I find it useful to review all the commands in a new module to get a feel for what it is capable of. You can gather a lot just from the name of the command, however sometimes the command doesn't always do what we expect it to do. This is where the help documentation comes into play. 

###### We can use the snippet below to update our help files.

	Update-Help

Now that our help files are up to date let's take a look at the first command we will want to use.

###### We can use the snippet below to get the help documentation for our command.

	Get-Help -Name New-VHD

# Creating a new VHD

Before we can create a new VM we will first need to create a virtual hard drive. 

###### We can use the snippet below to create a 20GB dynamic VHD.

	New-VHD -Dynamic -Path $VHDPath -SizeBytes 2e+10

# Creating a new VM

Now that we have our VHD ready let's create a new Virtual Machine and attach our VHD

###### We can use the snippet below to create a new VM. 

    New-VM -Name $VMName -VHDPath $VHDPath -Path $VMPath

# Reviewing VM configuration

Our new VM has been created let's check on the default configuration. 

###### We can use the snippet below to get our VM configuration.

	Get-VM -Name $VMName | Select-Object -Property *  

# Adding a Network Switch

We will eventually want our new VM to connect to the internet, so lets create and add a VMSwitch. 

###### We can use the snippet below to create a VMSwitch.

	New-VMSwitch -Name $VMSwitchName -SwitchType Internal | 
		Set-VMSwitch -NetAdapterName Ethernet  

Now that we have a Virtual Switch created we will need to configure the VM to use our switch.

###### We can use the snippet below to connect the VM to the Switch.

	Get-VM -Name $VMName | 
		Get-VMNetworkAdapter | 
		Connect-VMNetworkAdapter -SwitchName $VMSwitchName 

# Bootstrapping an Operating System

We will need to run an Operating System on our new VM, you can use your favorite but for this post I will use Ubuntu Studio. We will be using this VM for a few more exercises and we will need Ubuntu. [Click here](https://docs.microsoft.com/en-us/windows-server/virtualization/hyper-v/best-practices-for-running-linux-on-hyper-v) for Microsofts Best Practices for running Linux on Hyper-V.

###### We can use the snippet below to attach the OS .iso.

	Get-VMDvdDrive -VMName $VMName | 
		Set-VMDvdDrive -Path $OsIsoPath

###### We can use the snippet below to start our new VM.

		Start-VM -VMName $VMName

Unfortunately the process to install the Linux OS requires some manual intervention. I will revisit how I install Linux	at a later time so we can fully automate this server setup.

# Wrap Up 

We have barely scratched the surface of the Hyper-V Powershell module in this post. Microsoft has given us some very powerful tools built right into Windows 10 for free. I hope to have time to learn more when I revisit this module for later projects.