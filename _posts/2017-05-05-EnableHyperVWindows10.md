---
layout: post
title: Powershell How to: Install Hyper V on Windows 10
subtitle: Part 1 - Home Media Server
bigimg: /img/path.jpg
---


Before we can enjoy our home movie content from anywhere we will need a server to host it. We are going to use Microsoft [Hyper](https://www.microsoft.com/en-us/cloud-platform/server-virtualization) V because it comes standard on Windows 10, it's free and its more than capable of handling the task at hand.

We can use the snipet below to install the Hyper V optional Windows Feature.
{% highlight Powershell linenos %}
Get-WindowsOptionalFeature -Online | 
    Where-Object {$PSItem.FeatureName -match 'Hyper'} | 
    Enable-WindowsOptionalFeature -Online
{% endhighlight %}

