---
layout: post
title: Powershell How to Install Powershell on Linux Ubuntu
---

Now that we have our new Linux Virtual Machine running in Hyper V lets work on installing Powershell. Powershell in now an [open source](https://github.com/PowerShell/PowerShell) project on GitHub and is available for both Linux and Mac. We will first need to logon to our Media Server and open the Terminal.
# Install

###### We can use the snipet below to Import the public repository GPG keys.

	curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add

###### We can use the snipet below to Register the Microsoft Ubuntu repository.

	curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | sudo tee /etc/apt/sources.list.d/microsoft.list

###### We can use the snipet below to Update apt-get.

	sudo apt-get update

Now that our apt-get is up to date and we have a registered repository lets install PowerShell.  

###### We can use the snipet below to Install PowerShell.

	sudo apt-get install -y powershell

###### We can use the snipet below to Start PowerShell.

	powershell

###### We can use the snipet below to show the PowerShell version.

	$PSversionTable

We now have 350 Powershell commands at our disposal on Linux, the possibilities are endless.

# Uninstall

###### We can use the snipet below to Uninstall PowerShell.

	sudo apt-get remove powershell

## Credit
* [Powershell Installation Documents](https://github.com/PowerShell/PowerShell/blob/master/docs/installation/linux.md)  

...to be continued