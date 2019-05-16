---
template: post
title: How to Enable Self-Service Password Reset
slug: /posts/2019/how-to-enable-sspr/
draft: false
date: 2019-04-08T08:18:05.642Z
description: >-
  Self-service password reset (SSPR) is a feature of Azure Active Directory that
  empowers users to easily reset their passwords and unlock their accounts
  without interacting with your helpdesk. SSPR is designed to enable enterprises
  to decrease support costs and to increase user productivity and security. The
  system includes detailed reporting that tracks when users access the system,
  along with notifications to alert administrators of misuse or abuse.
category: blog
tags:
  - AzureAD
  - O365
  - Password
  - Hybrid
---
Self-service password reset (SSPR) is a feature of Azure Active Directory that empowers users to easily reset their passwords and unlock their accounts without interacting with your helpdesk.
SSPR is designed to enable enterprises to decrease support costs and to increase user productivity and security. The system includes detailed reporting that tracks when users access the system, along with notifications to alert administrators of misuse or abuse.

#### Licensing Considerations

> You will need Azure AD Licenses for all users of SSPR. The number of objects in your directory and the features you wish to deploy will affect your licensing choices. While many features are included with Azure AD Free and Azure AD Basic, some features require Azure AD Premium P1 or P2.
>
> __Self-Service Password Reset for cloud-only users:__ BASIC, Azure AD P1 and P2
>
> __Self-Service Password Reset for hybrid users (with writeback):__ Azure AD P1 and P2

#### Planning for SSPR Enablement

When a user attempts to reset a password, they first verify their previously registered authentication method or methods to prove their identity. Then they provide a new password. For cloud-only users, the new password is stored in Azure Active Directory.

For hybrid users, the password is written back to the on-premises Active Directory via the Azure AD Connect service.
To write the new password back to the on-premises Active Directory, Azure AD Connect must be able to communicate with the primary domain controller (PDC) emulator.

If you need to enable this manually, you can connect Azure AD Connect to the PDC emulator.

#### Planning Password Authentication methods

These services enable administrators to configure the authentication methods that users can use to register and then prove their identity.

*	Administrators configure the __Azure AD SSPR Service__ with the available choices for end-users to provide their alternate credentials, and users access the service to register and to reset their passwords

*	Administrators configure the __Azure AD Connect Service__ to write back the passwords changes that occur in Azure AD back to the on-premises active directory.

#### Enable SSPR in Azure AD

- Sign in to the [Azure AD portal](https://aad.portal.azure.com) using a Global Administrator account.

- Browse on __Azure Active directory__ and select __Password reset__.

- From the __Properties page__, under the option __Self Service Password Reset Enabled__ you can choose between groups or all, groups are fine for pilotusers and testing. We are choosing all and click __Save__

![](/media/enable_SSPR/1.png)

- On the __Authentication methods__ page

Set the __Number of methods required to reset__ to __1 or 2__ we are choosing 1.

Choose which __Methods available to users__ your organization wants to allow. For this tutorial check the boxes to enable __Email__, __Mobile app code (preview)__ and __Mobile Phone__.

![](/media/enable_SSPR/2.png)

- On the __Registration__ page

Select __Yes__ for __Require users to register when signing in.__

__Set Number of days before users are asked to reconfirm their authentication information__ to __180 or to your choise__ And click __Save__

![](/media/enable_SSPR/3.png)

- On the Notifications page

Set __Notify users on password resets__ option to __Yes.__

Set __Notify all admins when other admins reset their password__ to __No or Yes.__ We are in this tutorial using no.

![](/media/enable_SSPR/4.png)

- On the __Customization__ page

Microsoft recommends that you set __Customize helpdesk link__ to __Yes__ and provide either an email address or web page URL where your users can get additional help from your organization in the __Custom helpdesk email or URL__ field.

For this tutorial we will leave Customize helpdesk link set to __No.__

![](/media/enable_SSPR/5.png)

You have now setup self-service password reset, and next time your users logon to Office 365 they will be forced to register for authentication methods. So information to the end users is important!

#### How the endusers will see the login and how to change password

- This is what the enduser see at next logon after we have enabled SSPR:

![](/media/enable_SSPR/6.png)

To english:

__Need more information__

The organization needs more information to protect your account

Skip now (14 days until this is necessary)

Use another account

Learn more

- User register for self-service password reset (Showing the new portal here.)

![](/media/enable_SSPR/7.png)

If you will use anoter method click __I want to set up a different methods__

![](/media/enable_SSPR/8.png)

I will use the app in this tutorial.

- Clik __Next__

![](/media/enable_SSPR/9.png)

- Open your Microsoft Authenticator app and create new account and scan the qr code and clikc __Next__:

![](/media/enable_SSPR/10.png)

- Next you will get an __Notification__ on your device, press OK and your account is approved.

![](/media/enable_SSPR/11.png)

- And click __Done__

![](//media/enable_SSPR/12.png)

- Now let us try to self-service password reset, navigate to [https://aka.ms/sspr](https://aka.ms/sspr) and type in the requered information.

![](/media/enable_SSPR/13.png)

- Open your Microsoft Authenticator app and type in the code from the app.

![](/media/enable_SSPR/14.png)

- Type in your new passord

![](/media/enable_SSPR/15.png)

- You should see an green checkmark that vertify that the password change was successfully.

![](/media/enable_SSPR/16.png)

- To vertify the password change, in Azure AD navigate to __Audit logs__

- In __Service__ choose __Self-service password management__ and click __Apply__

![](/media/enable_SSPR/17.png)

#### Enabling password writeback

Password writeback is used to synchronize password changes in Azure Active Directory (Azure AD) back to your on-premises Active Directory Domain Services (AD DS) environment.

Password writeback is enabled as part of Azure AD Connect to provide a secure mechanism to send password changes back to an existing on-premises directory from Azure AD

To configure and enable password writeback, sign in to your Azure AD Connect server and start the Azure AD Connect configuration wizard.

- On the Welcome page, select Configure.

- On the Additional tasks page, select Customize synchronization options, and then select Next.

- On the Connect to Azure AD page, enter a global administrator credential, and then select Next.

- On the Connect directories and Domain/OU filtering pages, select Next.

- On the Optional features page, select the box next to Password writeback and select Next.

![](/media/enable_SSPR/18.png)

- On the Ready to configure page, select Configure and wait for the process to finish.

- When you see the configuration finish, select Exit.

To see password writeback is active in your Azure AD, browse on __Azure Active directory__ and select __Password reset__. And go to __On-premises integration__

You should see something like this, we can also choose to only unlock acounts without resetting the passowrd.

![](/media/enable_SSPR/19.png)

Later I will show you how to setup password reset from the login screen on Windows 10 devices.
