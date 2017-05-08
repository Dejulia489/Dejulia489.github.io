---
layout: post
title: How to Install Powershell on Windows 10
---

Now that we have our new Linux Virtual Machine running Powershell let's update our Hyper V host.

# Install Powershell

To install PowerShell on Windows [download](https://github.com/PowerShell/PowerShell/releases/download/v6.0.0-alpha.18/PowerShell-6.0.0-alpha.18-win10-win2016-x64.msi) a released package from their GitHub [releases page](https://github.com/PowerShell/PowerShell/releases). Once downloaded, double-click the installer and follow the install wizard.

There is a shortcut placed in the Start Menu upon installation.

By default the package is installed to $env:ProgramFiles\PowerShell\

You can launch PowerShell via the Start Menu or $env:ProgramFiles\PowerShell\powershell.exe

# Credit  

* PowerShell Documentation: [Install Powershell on Windows](https://github.com/PowerShell/PowerShell/blob/master/docs/installation/windows.md#msi)