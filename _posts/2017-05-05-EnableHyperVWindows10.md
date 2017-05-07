---
layout: post
title: Powershell How to Enable Hyper V on Windows 10
bigimg: /img/HyperV.png
---

## Enabling Hyper V

Before we can enjoy our home movie content from anywhere we will need a server to host it. We are going to use Microsoft [Hyper V](https://www.microsoft.com/en-us/cloud-platform/server-virtualization) because it comes standard on Windows 10, it's free and its more than capable of handling the task at hand.

###### We can use the snipet below to install the Hyper V optional Windows Feature.

	Get-WindowsOptionalFeature -Online | 
		Where-Object {$PSItem.FeatureName -match 'Hyper'} | 
		Enable-WindowsOptionalFeature -Online


