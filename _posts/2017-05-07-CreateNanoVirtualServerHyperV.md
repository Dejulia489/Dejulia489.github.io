---
layout: post
title: How to Create a Nano Server in Hyper V
---

Nano Server is a stripped-down version of Windows Server developed by Microsoft specifically for running cloud applications and containers. There is no local logon or Remote Desktop. Instead, management of the OS is performed remotely via WMI and PowerShell cmdlets.

# Spinning Up Nano server

You can [download](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016) a preconfigured Nano Server VHD(.exe) from microsoft, you will need to sign in and register if you haven't already. The download is quick and the installation wizard is simple. Next > Next > Next and we have ourselves a Nano Server Data Center VHD. This VHD was built using the public TP4 media, and will expire on the same date as TP4 (July 15th, 2016).

Let's use some commands we learned in an earlier post to create a [New Linux VM in Hyper V](https://dejulia489.github.io/2017-05-06-CreateLinuxVirtualServerHyperV/).

###### We can use the snippet below to create a new VM. 

	New-VM -Name $VMName -VHDPath 'C:\Windows Server 2016 DataCenter Nano VHD\NanoServerDataCenter.vhd' -Path $VMPath 

###### We can use the snippet below to configure the network adapter. 

	Get-VM -VMName $VMName | 
		Get-VMNetworkAdapter | 
		Connect-VMNetworkAdapter -SwitchName $VMSwitchName 

###### We can use the snippet below to start our VM

	Start-VM -VMName $VMName

# Remoting into Nano Server

We now have a Nano VM up and running in Hyper V, let's try remoting into it. 

First we will need to trust our new Nano Server's IP
	
###### We can use the snippet below to add our VM to our Trusted Hosts

	Set-Item WSMan:\localhost\Client\TrustedHosts $NanoServerIP

Now we can remote in by using the Enter-PSSession command.

###### We can use the snippet below to remote into our Nano Server

	Enter-PSSession -ComputerName $NanoServerIP -Credential Administrator

##### Results

	[$NanoServerIP]: PS C:\Users\Administrator\Documents> 

We can exit our remoting session by using the following commands.

##### We can use the snippet below to exit our remote session

	Exit-PSSession

# Wrap Up 

Using a preconfigured VHD seems like the easy way out but we will revisit configuring Nano Server Images at a later time.

# Credit

* Microsoft Documentation: [Nano Server Quick Start](https://docs.microsoft.com/en-us/windows-server/get-started/nano-server-quick-start)