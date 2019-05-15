---
template: post
title: Block Download via Conditional Access and MCAS
slug: /posts/2019/block-downloade-conditional-access/
draft: false
date: 2019-03-17T10:13:38.438Z
description: >-
  More and more customers today want control over data located in Office 365,
  such that the device must be reported in Azure AD and compliant so my home
  devices cant download content from home.


  Luckily for us, this is very easy to set up and I will show you how fast and
  easy this is.
category: blog
tags:
  - Intune
  - AzureAD
  - Conditional Access
---
Hi, today I want to talk about Conditional Access and Conditional Access App Control (MCAS for short) but why?

More and more customers today want control over data located in Office 365, such that the device must be reported in Azure AD and compliant so my home devices cant download content from home.

Luckily for us, this is very easy to set up and I will show you how fast and easy this is.

#### How it works

Conditional Access App Control uses a reverse proxy architecture and is uniquely integrated with Azure AD conditional access. Azure AD conditional access allows you to enforce access controls on your organization’s apps based on certain conditions. The conditions define who (user or group of users) and what (which cloud apps) and where (which locations and networks) a conditional access policy is applied to. After you’ve determined the conditions, you can route users to Microsoft Cloud App Security where you can protect data with Conditional Access App Control by applying access and session controls.

Conditional Access App Control enables user app access and sessions to be monitored and controlled in real time based on access and session policies. Access and session policies are used within the Cloud App Security portal to further refine filters and set actions to be taken on a user. With the access and session policies, you can:

* __Block on download:__ You can block the download of sensitive documents. For example, on unmanaged devices.
* __Protect on download:__ Instead of blocking the download of sensitive documents, you can require documents to be protected via encryption on download. This encryption makes sure the document is protected and user access is authenticated if the data is downloaded to an untrusted device.
* __Monitor low-trust user sessions:__ Risky users are monitored when they sign into apps and their actions are logged from within the session. You can investigate and analyze user behavior to understand where, and under what conditions, session policies should be applied in the future.
* __Block access:__ You can completely block access to specific apps for users coming from unmanaged devices or from non-corporate networks.
* __Create read-only mode:__ By monitoring and blocking custom in-app activities, you can create a read-only mode to specific apps for specific users.
* __Restrict user sessions from non-corporate networks:__ Users accessing a protected app from a location that isn't part of your corporate network are allowed restricted access. The download of sensitive materials is blocked or protected.

> To use Cloud App Security Conditional Access App Control, you need an Azure Active Directory P1 license and an active Microsoft Cloud App Security subscription. Or be a part of EMS E5 SKU.

#### Setup the Conditional Access rules

- Go to [Azure AD Portal](https://aad.portal.azure.com) and find [Conditional Access](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies)
- Create new policy and give it a name
- Under Users and groups, choose all users or groups, I will just choose all. (You could also exclude user/groups if you have any. I do exclude Global Administrators.)

![](/media/camcas/1.png)

- Next open Cloud Apps, I will just choose "All cloud apps." but Office 365 SharePoint Online should be enough.

![](/media/camcas/2.png)

- Next we go to Conditions and Device state, to select which devices we will force this rule on. And we will exclude devices that are Hybrid joined and marked as compliant.

![](/media/camcas/3.png)

Here we will exclude devices that are hybrid joined and marked as compliant (Intune).

![](/media/camcas/4.png)

- Next we go to Access controls and __Grant__ and mark Grant Access, Require device to be marked as compliant and Require Hybrid Azure AD joined device

![](/media/camcas/5.png)

- Next go to Sessions, and pick Use Conditional Access App Control (Block downloads)

![](/media/camcas/6.png)

- Last enable the policy

![](/media/camcas/7.png)

#### End-user experience

Lets see how the end-user will see the changes.

When the user try to open OneDrive on an devices that is not compliant or hybrid joined the user will see this: (Sorry for the Norwegian text)

![](/media/camcas/8.png)

Quick google translate:
You can't go from here
The program contains sensitive information and can only be accessed from:
Stoms Corp domain-affiliated entities. Access from personal devices is not permitted.
However, if you do not plan to do so now, you may be able to visit other Stoms Corp sites. If not, sign out to protect your account.

We have now block all users who is trying to access OneDrive from any diveces that not match our requirements. But if we want our user to login to OneDrive but not able to download contents?

Lets remove all Conditions and Grants so only Users and Groups, Cloud apps and Sessions is one.

This is what the end user will see:

![](/media/camcas/9.png)
We now are proxies from eu2.cas.ms to our OneDrive, and we now can open docs from OneDrive.

But what happens if we wants to download a file from OneDrive?

![](/media/camcas/10.png)
We are being blocking to download the contents!

![](/media/camcas/11.png)
There is also no way to edit this file in word!

#### Logging

How is the logging when we are using this?

From Azure AD:
![](/media/camcas/12.png)


[Read more on Cloud App](https://docs.microsoft.com/en-us/cloud-app-security/proxy-intro-aad)
