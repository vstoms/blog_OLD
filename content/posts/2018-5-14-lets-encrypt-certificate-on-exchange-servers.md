---
template: post
title: Let’s Encrypt certificate on Exchange servers
slug: /posts/2018/lets-encrypt-certificate-on-exchange-servers
draft: false
date: 2018-05-11T17:14:23.724Z
description: >-
  Create free certificate from Lets`s encrypt to create a Exchange Lab.
category: blog
tags:
  - Certificate
  - Exchange
  - Hybrid
---

After Let’s Encrypt accept wildcard certificate we now can use this to build labs.

Ive been using [sslforfree.com](https://www.sslforfree.com) and [zerossl.com](https://zerossl.com) if you dont want to use the ACME to get the certificate.

1. Request the certificate from sslforfree or zerossl
2. Validate the domain, DNS TXT record.
3. Download the cer and key file
4. Install OpenSSL from [indy.fuglan.com/ssl/](https://indy.fulgan.com/SSL/)
5. Run this command to "merge" the certificate and privatekey into an pfx:
   
```
openssl pkcs12 -export -in certificate.crt -inkey private.key -out yourcert.pfx
```

1. Import this into your windows server.