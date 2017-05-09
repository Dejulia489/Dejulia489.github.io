---
layout: post
title: How to Install Powershell on Linux Ubuntu
---

Now that we have our new Linux Virtual Machine running in Hyper V lets work on installing Powershell. Powershell in now an [open source](https://github.com/PowerShell/PowerShell) project on GitHub and is available for both Linux and Mac. We will first need to logon to our Virtual Server we created in a previous post titled [How to Create a Virtual Machine in Hyper V]https://dejulia489.github.io/2017-05-06-CreateLinuxVirtualServerHyperV/) and open the Terminal.

# Installing Powershell  

First we will need to setup a public repository. 

###### We can use the snippet below to Import the public repository GPG keys.

	curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add

###### We can use the snippet below to Register the Microsoft Ubuntu repository.

	curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | sudo tee /etc/apt/sources.list.d/microsoft.list

Powershell requires the latest apt-get. 

###### We can use the snippet below to Update apt-get.

	sudo apt-get update

Now that our apt-get is up to date and we have a registered repository lets install PowerShell.  

###### We can use the snippet below to Install PowerShell.

	sudo apt-get install -y powershell

Simply type powershell into the Terminal and [voila](https://www.merriam-webster.com/dictionary/voil%C3%A0), We now have 350 Powershell commands at our disposal on Linux, the possibilities are endless.

###### We can use the snippet below to Start PowerShell.

	powershell

###### We can use the snippet below to show the PowerShell version.

	$PSversionTable

# Uninstalling Powershell

If you need to uninstall for any reason it is as simple as running the code below. 

###### We can use the snippet below to uninstall PowerShell.

	sudo apt-get remove powershell

# Credit  
* PowerShell Documentation: [Install Powershell on Linux](https://github.com/PowerShell/PowerShell/blob/master/docs/installation/linux.md)