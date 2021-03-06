---
layout: post
title: How to Enable Hyper V on Windows 10
---

## Enabling Hyper V

Server Virtualization is an everyday part of my life while at work and at home. I think it is an important technology to understand and it isn't as complicated as you may think. Take a moment to review the [Basics of Virtualization](http://www.dummies.com/programming/networking/basics-of-network-virtualization/) before we start our first exercise, enabling Hyper V. 

We don't need to have a virtualized media Server, but we can, so why not learn a thing or two while we set it up. We are going to use Microsoft [Hyper V](https://www.microsoft.com/en-us/cloud-platform/server-virtualization) because it comes standard on Windows 10, it's free and its more than capable of handling the task at hand. With the commands below we can enable Hyper V along with the built in Hyper V Powershell Module. 

###### We can use the snippet below to enable the Hyper V optional Windows Feature.

	Get-WindowsOptionalFeature -Online | 
		Where-Object {$PSItem.FeatureName -match 'Hyper'} | 
		Enable-WindowsOptionalFeature -Online


