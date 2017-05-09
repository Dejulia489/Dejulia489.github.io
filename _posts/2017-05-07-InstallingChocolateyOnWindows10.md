---
layout: post
title: Installing Chocolatey on Windows 10
---

[Chocolatey](https://chocolatey.org/about) is a package manager for Windows (like apt-get or yum but for Windows). It was designed to be a decentralized framework for quickly installing applications and tools that you need. It is built on the NuGet infrastructure currently using PowerShell as its focus for delivering packages from the distros to your computer.

# Installing Chocolatey

###### We can use the snippet below to install Chocolatey, this must be run as an administrator

	Invoke-Expression ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))

Now that Chocolatey is installed we can use the choco command to install all types of packages. We will dive more into Chocolatey later, when we setup our own Chocolatey feed.

	choco install $PackageName

# Upgrading Chocolatey

	choco upgrade chocolatey

# Credit  

* Chocolatey Documentation: [Install Chocolatey](https://chocolatey.org/install)
