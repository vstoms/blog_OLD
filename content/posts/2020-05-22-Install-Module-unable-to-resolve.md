---
template: post
title: Install-Module - unable to resolve package source 'https //www.powershellgallery.com/api/v2/'
slug: posts/2020/Install-Module-unable-to-resolve/
draft: false
date: 2020-05-20T08:56:00.695Z
description: >-
  If you try to install but get the error message unable to resolve package source 'https://www.powershellgallery.com/api/v2/'
category: blog
tags:
  - Powershell
  - reminder
---
If you try to install but get the error message unable to resolve package source 'https://www.powershellgallery.com/api/v2/' then try:

```powershell
[Net.ServicePointManager]::SecurityProtocol = "tls12"
```