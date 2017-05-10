---
layout: post
title: Installing OpenSSH on Windows 10
---

We have [Installed OpenSSH on Linux Ubuntu](https://dejulia489.github.io/2017-05-07-InstallingOpenSSHOnLinux/), now let's install OpenSSH on Windows 10.

# Installing OpenSSH

We can use the following choco command to install OpenSSH, see [Installing Chocolatey on Windows 10](https://dejulia489.github.io/2017-05-07-InstallingChocolateyOnWindows10/) for a quick Chocolatey setup. 

###### We can use the snippet below to install OpenSSH with Chocolatey

	choco install openssh

The choco command will download the OpenSSH package to 'C:\ProgramData\chocolatey\lib' by default. The Choco command will also execute it's chocolateyinstall.ps1 script which will in turn install OpenSSH to 'C:\Program Files\OpenSSH-Win64'. Here we can locate the install-sshd.ps1.

###### We can use the snippet below to execute the install.sshd.ps1 

	. "C:\Program Files\OpenSSH-Win64\install-sshd.ps1"

OpenSSH requires host keys and access to those hosts private keys.
			
###### We can use the snippet below to generate all the 'host' keys needed by sshd

	. "C:\Program Files\OpenSSH-Win64\ssh-keygen.exe" -A

###### We can use the snippet below to grant the 'NT Service\sshd' read access to the host private key files

	   Get-ChildItem -Path 'C:\Program Files\OpenSSH\ssh_host_*_key' | % {    
		   $acl = get-acl $_.FullName
		   $ar = New-Object  System.Security.AccessControl.FileSystemAccessRule("NT Service\sshd", "Read", "Allow")
		   $acl.SetAccessRule($ar)
		   Set-Acl $_.FullName $acl
		}

We will also need to open port 22 in the firewall for inbound traffic for SSH.

###### We can use the snippet below to generate all the 'host' keys needed by sshd

	New-NetFirewallRule -Protocol TCP -LocalPort 22 -Direction Inbound -Action Allow -DisplayName SSH

We will need this service running after a reboot, let's set sshd and the ssh-agent service to auto-start mode.

###### We can use the snippet below to set both services to autostart

	Set-Service sshd -StartupType Automatic
	Set-Service ssh-agent -StartupType Automatic

Now that we have OpenSSH installed let's configure the sshd_config file.

###### We can use the snippet below to modify the Password Authentication and add the Powershell Subsystem.
	
	$FilePath = "C:\Program Files\OpenSSH-Win64\sshd_config"
	$FileData = (Get-Content $FilePath).Replace('#PasswordAuthentication yes','PasswordAuthentication yes') 
	$FileData += 'Subsystem	powershell C:\Program Files\PowerShell\6.0.0-alpha.18\powershell.exe -sshs -NoLogo -NoProfile' 
	$FileData | Out-File $FilePath -Force

Finally for these configurations to take affect we need to restart the SSHD Service.

###### We can use the snippet below to restart the SSHD Service.

	Restart-Service sshd

Now that we have a OpenSSH configured let's use it to connect to our Linux Server via Powershell Remoting. 

###### We can use the snippet below to remote to our Linux Server

	Enter-PSSession -HostName $LinuxServerIP -UserName administrator

###### Results

![Windows10ToLinuxUbutuPSSession](https://dejulia489.github.io/img/Windows10ToLinuxUbutuPSSession.PNG)

# Credit  

* PowerShell Documentation: [Powershell Remoting Over SSH](https://github.com/PowerShell/PowerShell/blob/866b558771a20cca3daa47f300e830b31a24ee95/docs/new-features/remoting-over-ssh/README.md)
* PowerShell Documentation: [Install Win32 OpenSSH](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)