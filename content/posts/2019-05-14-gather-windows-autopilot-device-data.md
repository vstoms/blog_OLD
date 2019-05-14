---
template: post
title: Gather Windows Autopilot Device Data
slug: Gather Windows Autopilot Device Data
draft: false
date: 2019-05-14T06:39:49.545Z
description: Gather Windows Autopilot Device Data
category: blog
tags:
  - Powershell
  - Autopilot
---
[Link to powershell script ](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo)

##### Export Computer AutoPilot Data
```
.\Get-WindowsAutoPilotInfo.ps1 -ComputerName MYCOMPUTER -OutputFile .\MyComputer.csv
```

##### Append Computer AutoPilot Data
```
.\Get-WindowsAutoPilotInfo.ps1 -ComputerName MYCOMPUTER -OutputFile .\MyComputer.csv -Append
```

##### Export AutoPilot Data from a SCCM Collection
```
Get-CMCollectionMember -CollectionName "All Systems" | .\GetWindowsAutoPilotInfo.ps1 -OutputFile .\MyComputers.csv
```

##### Export AutoPilot Data from a Active Directory
```
Get-ADComputer -Filter * | .\GetWindowsAutoPilotInfo.ps1 -OutputFile .\MyComputers.csv
