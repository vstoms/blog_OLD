---
template: post
title: Intune Autopilot Hybrid Join error - Something went wrong 80070774
slug: intune-autopilot-error-80070774
draft: true
date: 2019-05-20T17:14:23.724Z
description: >-
  Autopilot Hybrid Join error 80070774, no devices can get enrolled into
  Autopilot and Hybrid join.
category: blog
tags:
  - Intune
  - Autopilot
  - Hybrid
---
Quick blog around Intune Autopilot Hybrid Join and error message 80070774.

#####Case

This environment was working fine a week ago, but today we got an interesting error message when new clients try to get enrolled into Hybrid Join from Autopilot. Nothing was change from Intune / Network side.

Error message on the clients

```
Offline Domain Join: Could not establish connectivity after time: (0x16E39F) milliseconds. Result: (Could not find the domain controller for this domain.).
```

As well as some other warnings during the process:

```
AutoPilot policy [CloudAssignedDeviceName] not found."

AutoPilot policy [AUTOPILOT_OOBE_SETTINGS_AAD_AUTH_USING_DEVICE_TICKET] not found.
```

And where the Intune Connector for Active Directory was installed, there was no indication around offline domain join blob was created or handled to the clients.


#####Solution

The logs did not tell us much what the cause was, and different blogs-post on the internet was telling us that maybe the Computer Name Prefix was wrong, but it was correct like "Company-" 

So the solution was a Device configuration with SkipUserStatusPage was active 

So if you have this error message and can`t get clients enrolled and you have an device configuration with OMA-URI _./Vendor/MSFT/DMClient/Provider/MS DM Server/FirstSyncStatus/SkipUserStatusPage_ then disable it or delete the profile.
 
