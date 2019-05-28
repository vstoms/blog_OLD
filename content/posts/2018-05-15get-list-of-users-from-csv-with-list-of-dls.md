---
template: post
title: Get list of users from CSV with list of DL's
slug: /posts/2018/get-list-of-users-from-csv-with-list-of-dls
draft: false
date: 2018-06-26T17:14:23.724Z
description: >-
  Powershell script export users in groups
category: blog
tags:
  - Microsoft
  - O365
  - O365
  - Self-reminder
---

Header in the csv file should be DL

```powershell
$PathToCsv = "groups.csv"

Import-Csv $PathToCsv |
    ForEach-Object {

        $group = $null

        $group = $_.DL
        Get-ADGroupMember $group |
            Select-Object samaccountname |
            ForEach-Object {

                New-Object psobject -Property @{
                    DL = $group
                    UserName = $_.samaccountname
                }
            }
    } |
    Export-Csv -NoTypeInformation "output.csv"
```