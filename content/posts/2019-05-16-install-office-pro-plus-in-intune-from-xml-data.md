---
template: post
title: Install Office pro plus in Intune from xml data
slug: /posts/2019/intune-office-xml/
draft: true
date: 2019-03-30T09:25:20.665Z
description: >-
  Microsoft has in Intune 1903 released that we now can deploy Office Pro Plus
  from xml, before we only have the choice to use the configuration designer.
  Why would you use the xml way?
category: blog
tags:
  - Intune
  - Office
  - XML
  - OneDrive
---
Microsoft has in Intune 1903 released that we now can deploy Office Pro Plus from xml, before we only have the choice to use the configuration designer. Why would you use the xml way?

This will allow greater customizability if the existing Intune UI options do not meet your needs.

> You must use Office 365 ProPlus licenses to activate Office 365 ProPlus apps deployed through Microsoft Intune. Currently, Office 365 Business edition is not supported by Intune.

- To create the XML file, you need for this go to [Office Customization Tool](https://config.office.com/deploymentsettings)

- In Architecture, choose 64-bit

![](/media/intunexml/4.png)

- Under Products, choose Office 365 ProPlus, and if you want Viso and Project select them. We are not going to enable them in this example. We are disabling Access and Publisher.

![](/media/intunexml/5.png)

- In Update channel we choose __Monthly channel__ (We then also get Teams!) and __Latest__ verison

![](/media/intunexml/6.png)

- Choose your preferred language, we are choosing __English__ and __Norwegian__.

![](/media/intunexml/7.png)

- Installation options, we are not showing the installation to the end user and turning off the logging.

![](/media/intunexml/8.png)

- Upgrade options, we can here choose to remove old Office that is installed from msi, same for Viso and Project.

![](/media/intunexml/9.png)

- Product key, choose to __Automatically accept the EULA__

![](/media/intunexml/10.png)

- General, type in your company property on office documents

![](/media/intunexml/11.png)

- Under __Application preferences__ we don't need to touch here, this settings we are doing from Intune.

- Export the settings to xml and save the file on your computer.

![](/media/intunexml/12.png)

- So go to your Intune portal and __Client apps__ -> __Apps__ -> __Add__

- In add type, choose Office 365 suite - Windows 10

![](/media/intunexml/1.png)

- Choose __Enter XML data__ in Setting information

![](/media/intunexml/2.png)

- Next open __App Suite Information__ and type in your information so user knows what they are getting.

![](/media/intunexml/3.png)

- Next paste inn your XML data that you get from the Office configurator.

![](/media/intunexml/13.png)

And the last step is to assign this to a group in Intune.
