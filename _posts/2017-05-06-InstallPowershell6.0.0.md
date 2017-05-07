---
layout: post
title: Powershell How to Install Powershell 6.0.0
---

We will need Powershell 6.0.0 in order to remote to our new linux server, so let's get that out of the way so we can continue onto the fun part. Better yet let's make this a fun exercise by installing Powershell 6.0.0 on Nano Server.

# Installing Nano server

We want to stay focused on Powershell 6.0.0 in the post, but feel free to review one of my previous post on [How to Install Nano Server](https://dejulia489.github.io/2017-05-06-InstallNanoServer/)


# Installing Powershel 6.0.0 on Nano Server


###### We can use the snippet below to Import the public repository GPG keys.

	curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add



# Planning for the Future

The use of the SSH subsystem will eventually change to a more general hosting model similar to how WinRM works in order to support endpoint configuration and JEA.

# Credit

* PowerShell Documentation: [Remoting Over SSh](https://github.com/PowerShell/PowerShell/blob/866b558771a20cca3daa47f300e830b31a24ee95/docs/new-features/remoting-over-ssh/README.md)

...to be continued