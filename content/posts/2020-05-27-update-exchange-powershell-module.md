---
template: post
title: Update Exchange Powershell Module
slug: posts/2020/update-exchange-module/
draft: false
date: 2020-05-27T07:59:30.354Z
description: >-
  If you try to update the Microsoft Exchange Powershell Module an get error that your administrator has blocked
  this application because it potentially pose a security risk to your computer.
category: blog
tags:
  - Exchange
  - M365
  - O365
---

If you try to update the Microsoft Exchange Powershell Module an get error that your administrator has blocked
this application because it potentially pose a security risk to your computer.

There is a quick fix to get pass this error:

![](/media/ps-module-error/1.png)

Open regedit and navigate to HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\.NETFramework\Security\TrustManager\PromptingLevel

Change Internet to Enabled:

![](/media/ps-module-error/2.png)

Then you should be able to update the module.