---
layout: post
title: Installing OpenSSH on Windows 10
---

# Installing OpenSSH

In two of my earlier posts we [created a Linux VM](https://dejulia489.github.io/2017-05-06-CreateLinuxVirtualServerHyperV/) and [installed Powershell on Linux](https://dejulia489.github.io/2017-05-06-InstallingPowershellOnLinux/), now let's install [OpenSSH](https://help.ubuntu.com/lts/serverguide/openssh-server.html) and start remoting. OpenSSH is a freely available version of the Secure Shell (SSH) protocol family of tools for remotely controlling, or transferring files between, computers. 

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

# Credit  

* PowerShell Documentation: [Powershell Remoting Over SSH](https://github.com/PowerShell/PowerShell/blob/866b558771a20cca3daa47f300e830b31a24ee95/docs/new-features/remoting-over-ssh/README.md)