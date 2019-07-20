---
template: post
title: Hass.io on Synology DSM (native package)
slug: /posts/2019/install-hassio-synalogy-dsm-native-package
draft: false
date: 2019-07-20T17:14:23.724Z
description: >-
 Some user on community.home-assistant.io has managed to make a DSM package that installs Hass.io on the Synology NAS. Here is how to install the package and get around of the issues with USB and add-ons.
category: blog
tags:
  - Home-assistant
  - hassio
  - iot
  - smarthome
---
![logo](/media/hassio/hassio_logo.png)

Some user on community.home-assistant.io has managed to make a DSM package that installs Hass.io on the Synology NAS. Here is how to install the package and get around of the issues with USB and add-ons.

__You need to install Docker on your Synalogy first, if not this addon will not start.__

It's now super easy to get Hass.IO up and running on a Synology NAS with this package, and I will show you how to install it and if you have USB devices plugged into it (Z-wave or Zigbee) and getting an error when you are trying to start an addon.

First you have to downloade the DSM package [here](https://www.dropbox.com/s/xgspzppc0j0c8ou/hassio_x64-6.1_20190709-1.spk) 

Everything is quite straightforward but make sure to create a __Shared Folder__ to use for data storage and select that in the first dialog.

![setup](/media/hassio/1.png)

![setup](/media/hassio/2.png)

And in the end, you press __Apply__. If you have a docker instance of Home-Assistant running on your NAS then you have to stop it before HASS.io can start. This is because of ports conflicts.

Now you should be able to connect to your HASS.io from http://yourip:8123

If you try to start an addon, in my case Visual Studio Code and got an error message:

```bash
ERROR (SyncWorker_3) [hassio.docker] Can’t start addon_a0d7b954_vscode: 
404 Client Error:
Not Found (“linux runtime spec devices:
error gathering device information while adding custom device “/dev/serial/by-id/
usb-RFXCOM_RFXtrx433_A1XZHX4D-if00-port0”: lstat /dev/serial/by-id/
usb-RFXCOM_RFXtrx433_A1XZHX4D-if00-port0: no such file or directory”)
```

I do have an RFXcom, ZigBee2Mqtt and Z-Wave stick to my NAS, so your output from /dev/serial will differ.

To get the addons to work you have to log in to your NAS from an ssh session and type:

```bash
ln -s /dev/ttyUSBXX /dev/serial/by-id/usb-Silicon_Labs_CP2102_USB_to_UART_Bridge_Controller_0001-if00-port0
```

Change your correct USB and by-id device from the error message that your HASS.io generates.

After the devices are added under /dev/serial/by-id you should be able to start the addons.