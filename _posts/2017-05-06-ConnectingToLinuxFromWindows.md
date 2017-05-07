---
layout: post
title: Powershell How to Connect to Linux Ubuntu from Windows 10
---

Now that we have Powershell on our Linux Virtual Machine running in Hyper V, let’s work on connecting to it from our host machine running Windows 10. We will be referencing the Powershell team's [PowerShell Remoting Over SSH](https://github.com/PowerShell/PowerShell/blob/866b558771a20cca3daa47f300e830b31a24ee95/docs/new-features/remoting-over-ssh/README.md) article for a general overview of how Remoting currently works and what's planned for the future'

# Remoting Overview

PowerShell remoting normally uses WinRM for connection negotiation and data transport. SSH was chosen for this remoting implementation since it is now available for both Linux and Windows platforms. PowerShell SSH remoting lets you do basic PowerShell session remoting between Windows and Linux machines. This is done by creating a PowerShell hosting process on the target machine as an SSH subsystem.

# Install SSH on Windows 10

After reviewing the Powershell team's [PowerShell Remoting Over SSH](https://github.com/PowerShell/PowerShell/blob/866b558771a20cca3daa47f300e830b31a24ee95/docs/new-features/remoting-over-ssh/README.md) article we will be following their setup guide for both Linux and Windows. You will need at least Powershell 6.0.0 for this exercise, you can reference one of my previous posts [Powershell How to Install Powershell 6.0.0](https://dejulia489.github.io/2017-05-06-InstallPowershell6.0.0/).

###### We can use the snippet below to locate the Powershell Version.

	



# Plan for the Future

The use of the SSH subsystem will eventually change to a more general hosting model similar to how WinRM works in order to support endpoint configuration and JEA.

# Credit

* PowerShell Documentation: [Remoting Over SSh](https://github.com/PowerShell/PowerShell/blob/866b558771a20cca3daa47f300e830b31a24ee95/docs/new-features/remoting-over-ssh/README.md)

...to be continued

