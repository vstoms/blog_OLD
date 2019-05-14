---
template: post
title: Identify users who have registered for MFA using the PowerShell
slug: >-
  posts/2018/pull-a-list-of-all-users-in-azure-ad-that-hasnt-enrolled-with-mfa-yet
draft: false
date: 2018-06-26T12:53:55.184Z
description: Identify users who have registered for MFA
category: blog
tags:
  - powershell
  - o365
  - mfa
---
Identify users who have registered for MFA:
```
Get-MsolUser -All | where {$_.StrongAuthenticationMethods -ne $null} | Select-Object -Property UserPrincipalName
```

Identify users who have not registered for MFA:
```
Get-MsolUser -All | where {$_.StrongAuthenticationMethods.Count -eq 0} | Select-Object -Property UserPrincipalName
```
