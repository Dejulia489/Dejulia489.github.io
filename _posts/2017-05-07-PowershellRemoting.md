---
layout: post
title: Powershell Remoting
---

PowerShell Remoting is a feature in PowerShell that let's administrators run commands on remote systems. Built on Web Services for Management protocol, PowerShell Remoting offers a reliable framework for managing computers in a network.

# WinRM

Windows Remote Management (WinRM) service implements the WS-Management protocol for remote management. WS-Management is a standard web services protocol used for remote software and hardware management. The WinRM service listens on the network for WS-Management requests and processes them.

###### We can use the snippet below to enable WinRM, this must be run as an administrator

	Enable-PSRemoting

# Remoting From Windows 10 to Linux Ubuntu

Now that we have remoting working on our Linux Server let's remote from our Windows Hyper V host to our Linux Ubuntu Server.

...Coming Soon  

![WorkingOnIt](https://dejulia489.github.io/img/WorkingOnIt.gif)

# Credit  

* PowerShell Documentation: [Powershell Remoting Over SSH](https://github.com/PowerShell/PowerShell/blob/866b558771a20cca3daa47f300e830b31a24ee95/docs/new-features/remoting-over-ssh/README.md)