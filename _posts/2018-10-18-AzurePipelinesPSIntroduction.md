---
layout: post
title: AzurePipelinesPS Introduction
---

Recently I have been working on my new module [AzurePipelinesPS](https://www.powershellgallery.com/packages/AzurePipelinesPS).
It is open source on [GitHub](https://github.com/Dejulia489/AzurePipelinesPS) and published to the [Powershell Gallery](https://www.powershellgallery.com/packages/AzurePipelinesPS) via Azure DevOps. If you are unfamiliar with Azure DevOps take a minute to browse through the [microsoft introduction](https://azure.microsoft.com/en-us/blog/introducing-azure-devops/).

# Why Azure DevOps Pipelines

I have been working with [Team Foundation Server](https://visualstudio.microsoft.com/team-services/) for many years as part of my day job as well as for my personal repositories. Working within the UI can be cumbersome and time-consuming. Making bulk changes and programmatically creating builds from the command line is something I knew I would use often. I also wanted to share the module with the rest of you to give back to all the GitHub users who have helped me over the years! Allow me to introduce you to some commands that make my day as a DevOps Engineer much easier.

# Installing AzurePipelinesPS

Installing the module from the Powershell Gallery is easy.

``` powershell
Install-Module AzurePipelinesPS
```

## Creating a New Build

Now that we have the module installed we can start creating builds from the command line.

```Powershell
$secureToken = ConvertTo-SecureString -String 'myToken' -AsPlainText -Force
Invoke-APBuild -Instance 'https://dev.azure.com/' -Collection 'michaeldejulia' -Project 'AzurePipelinesPS' -PersonalAccessToken $secureToken -ApiVersion '5.0-preview.4' -Name 'AzurePipelinesPS'
```

![alt text][Invoke-APBuildByPersonalAccessToken]

[Invoke-APBuildByPersonalAccessToken]: https://github.com/Dejulia489/Dejulia489.github.io/blob/master/img/Invoke-APBuildByPersonalAccessToken.png?raw=true "Invoke-APBuild By Personal Access Token"

![alt text][Invoke-APBuildByPersonalAccessTokenWebView]

[Invoke-APBuildByPersonalAccessTokenWebView]: https://github.com/Dejulia489/Dejulia489.github.io/blob/master/img/Invoke-APBuildByPersonalAccessTokenWebView.png?raw=true "Invoke-APBuild By Personal Access Token Web View"

That was pretty neat, however the idea was to make things easier. Typing out parameters like that over and over again is not what I call easy. That's why I implemented AzurePipelinesPS sessions.

## AzurePipelinesPS Sessions

AzurePipelinesPS session support saves a set of parameters in memory or persits them to disk for later use.
Personal Access Tokens are stored securely so you do not have to worry about saving them in a credential manager or converting it to a secure string in order to run a command.

### Creating a Session

```Powershell
$splat = @{
    Collection = 'myCollection'
    Project = 'myProject'
    Instance = 'https://dev.azure.com/'
    PersonalAccessToken = 'myPersonalAccessToken'
    Version = 'vNext'
    SessionName = 'mySession'
}
New-APSession @splat
```

### Saving a Session

Saved session data will persist on disk, it can be retrieved by Get-APSession.

```Powershell
$sessions = Get-APSession
$sessions | Save-APSession
```

### Removing a Session

Removing a session is easy, just pipe the session to Remove-APSession.

```Powershell
$sessions = Get-APSession
$sessions | Remove-APSession
```

## Getting a Build with a Session

Using the build Id from the build we just created and the session that we just saved, I can retrieve the builds details and see that it completed successfully.

```Powershell
$session = Get-APSession -SessionName 'MDAzure'
Get-APBuild -Session $session -BuildId 88
```

![alt text][Get-APBuildBySession]

[Get-APBuildBySession]: https://github.com/Dejulia489/Dejulia489.github.io/blob/master/img/Get-APBuildBySession.png?raw=true "Get-APBuild By Session"

## How can I Contribute

There are hundereds, possibly thousands of endpoints that do not yet have powershell functions, please feel free to contribute to the [module here](https://github.com/Dejulia489/AzurePipelinesPS) and tell your friends!