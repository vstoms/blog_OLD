---
template: post
title: Powershell script to change proxyaddresses in bulk
slug: /posts/2019/powershell-script-change-proxyaddresses
draft: false
date: 2019-09-04T08:14:23.724Z
description: >-
 Quick tip to change proxy-addresses in bulk from csv files, and change / adds domains if you are changing email-domain in O365 without local Exchange
category: blog
tags:
  - Powershell
  - Exchange
  - csv
  - reminder
---
<img src="/media/powershell-logo.png" alt="logo" width="300"/>

Quick tip to change proxyaddresses in Active Directory fast with csv input. This is usfull if you are running Exchange Online with dirsync. (This is an unsuported, you should have a local Exchange server for management.)

```powershell
Import-Csv .\SMTPLIST.csv | ForEach-Object {

$username = $_.samaccountname
$userproxy = $_.emailaddress -split ';'
Set-ADUser -Identity $username -Add @{proxyAddresses= $userproxy}

}
```

your header in csv should be: samaccountname,emailaddress

To change the domain you could use:

```powershell
Import-Module Servermanager
#gathering and adding aliases
$x = get-aduser -SearchBase "OU to your users" -filter * -pr * | select SAMAccountname,UserPrincipalName,proxyaddresses
foreach ($line in $x){
    foreach ($addr in $line.proxyaddresses){
                if ($addr -like "smtp:*"){
                $addr = $addr.replace("old domain","new domain")
                $addr = $addr.replace("SMTP:","")
                $addr = $addr.replace("smtp:","")
                $addr
                get-aduser -identity "$($line.samaccountname)" | set-aduser -add @{'ProxyAddresses'=@("smtp:$($addr)")}

                }
                }
               
}
#check results
$y = get-aduser -SearchBase "OU to your users" -filter * -pr * | select SAMAccountname,UserPrincipalName,proxyaddresses
foreach ($line in $y){
$line.samaccountname
    foreach ($addr in $line.proxyaddresses){
                if ($addr -like "smtp:*"){
                $addr
                }
                }
               
}
```