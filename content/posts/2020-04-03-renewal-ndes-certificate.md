---
template: post
title: Renewal of "Enrollment Agent" certificate used by NDES
slug: posts/2020/renewal-ndes-certificate/
draft: false
date: 2020-04-03T08:56:00.695Z
description: >-
  Network Device Enrollment Service (NDES) requests two certificates according the following two certificate templates configured with the "Intended purpose" (Enhanced Key Usages) set to "Certificate Request Agent":

* CEP Encryption.
* Exchange Enrollment Agent (Offline request).

category: blog
tags:
  - Certificate
  - Intune
  - Ndes
  - reminder
---
To renew CEP certificate do the following:
* Open MMC console and add certificates snap-in
* Browse to the CEP certificate located in Personal certificates container
* Right click and select All Task -> Advanced -> Renew
* Follow the workflow using the CEP encryption template

To renew Exchange Enrollment Agent certificate:

Create a file named Request.inf with the following contents

```
[Version]
Signature="$Windows NT$"
[NewRequest]
RenewalCert="<Certificate Hash>"
MachineKeySet=TRUE
```

You can get the Exchange Enrollment Agent (Offline request) certificate's certificate hash by copying the value of the certifiate's "thumbprint” extension retriveved from certificate's "Details tab”.

Note: MachineKeySet set to "True" so the certificate and its private key will be stored in computer certificate store.

2. Run the following 3 commands to renew that old Enrollment Agent certificate:

CertReq.exe -New Request.inf Certnew.req
CertReq.exe -Submit Certnew.req Certnew.cer
CertReq.exe -Accept Certnew.cer