---
template: post
title: Quick tip to get GUID Code for Apps
slug: /post/create-a-certificate-for-package-signing-msix/
draft: false
date: 2019-03-03T09:56:02.649Z
description: Fast way to get the GUID code from applications.
category: blog
tags:
  - Intune
  - Powershell
  - ''
---
```
get-wmiobject Win32_Product | Format-Table IdentifyingNumber, Name, LocalPackage -AutoSize
```
