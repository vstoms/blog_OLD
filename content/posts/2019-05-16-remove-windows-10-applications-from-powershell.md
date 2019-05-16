---
template: post
title: Remove Windows 10 applications from powershell
slug: /posts/2018/remove-windows-10-applications-from-powershell/
draft: false
date: 2018-07-08T09:32:33.047Z
description: >-
  You can remove application as Get Office, Calender and Mail from powershell,
  if you are using Intune. Create an script to remove the built-in applications
  from Windows 10.
category: blog
tags:
  - Intune
  - Powershell
---
You can remove application as Get Office, Calender and Mail from powershell, if you are using Intune. Create an script to remove the built-in applications from Windows 10.

##### Calendar and Mail:
```
Get-AppxPackage *windowscommunicationsapps* | Remove-AppxPackage
```
##### Get Office:
```
Get-AppxPackage *officehub* | Remove-AppxPackage
```

##### Xbox:
```
Get-AppxPackage *xboxapp* | Remove-AppxPackage
```

##### Movies & TV:
```
Get-AppxPackage *zunevideo* | Remove-AppxPackage
```
