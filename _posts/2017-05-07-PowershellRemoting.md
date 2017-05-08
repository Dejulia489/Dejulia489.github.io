---
layout: post
title: Powershell Remoting To Linux and Back 
---

PowerShell Remoting is a feature in PowerShell that let's administrators run commands on remote systems. Built on Web Services for Management protocol, PowerShell Remoting offers a reliable framework for managing computers in a network.

# WinRM

Windows Remote Management (WinRM) service implements the WS-Management protocol for remote management. WS-Management is a standard web services protocol used for remote software and hardware management. The WinRM service listens on the network for WS-Management requests and processes them.

###### We can use the snippet below to enable WinRM, this must be run as an administrator

	Enable-PSRemoting

# Remoting From Linux Ubuntu to Linux Ubuntu

In two of my earlier posts we [created a Linux VM](https://dejulia489.github.io/2017-05-06-CreateHyperVVM/) and [installed Powershell on Linux](https://dejulia489.github.io/2017-05-06-InstallingPowershellOnLinux/), now let's install [OpenSSH](https://help.ubuntu.com/lts/serverguide/openssh-server.html) and start remoting. OpenSSH is a freely available version of the Secure Shell (SSH) protocol family of tools for remotely controlling, or transferring files between, computers. 

###### We can use the snippet below to install OpenSSH in the terminal

	sudo apt install openssh-client
	sudo apt install openssh-server

We will need to edit the sshd_config file to enable password authentication and add a PowerShell subsystem enrty.

###### We can use the snippet below to edit the sshd_config file in the terminal

	sudo nano /etc/ssh/sshd_config

We will need to uncomment the following in the sshd_config file.
	
	PasswordAuthentication yes

We will also need to add the following:

	Subsystem powershell powershell -sshs -NoLogo -NoProfile

Exit nano.
	
	CTRL+X

Save the sshd_config file and restart SSH. 

###### We can use the following command to restart the sshd service in the terminal

	sudo systemctl restart sshd.service

Now we should be able to create a remote session from our Linux server to itself

###### We can use the following command to start Powershell

	Powershell

###### We can use the following command to remote to our Linux server

	Enter-PSSession -HostName MediaServer -UserName administrator

# Remoting From Windows 10 to Linux Ubuntu

Now that we have remoting working on our Linux Server let's remote from our Windows Hyper V host to our Linux Ubuntu Server.

...Coming Soon  

![WorkingOnIt](https://dejulia489.github.io/img/WorkingOnIt.gif)

# Credit  

* PowerShell Documentation: [Powershell Remoting Over SSH](https://github.com/PowerShell/PowerShell/blob/866b558771a20cca3daa47f300e830b31a24ee95/docs/new-features/remoting-over-ssh/README.md)