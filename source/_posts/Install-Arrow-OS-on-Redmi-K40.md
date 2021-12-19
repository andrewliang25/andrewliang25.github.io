---
title: Install-Arrow-OS-on-Redmi-K40
date: 2021-12-19 20:34:27
tags:
---


This tutorial is mainly for Xiaomi Poco F3 / Xiaomi Mi 11X / Redmi K40.
If your phone is not the model above, you will need the ROM that fit the device.
But main steps still remain same.

**⚠ This may wipe out all personal data in the device, so backup! ⚠**

<!-- more -->

## Preparation

+ SDK Platform Tools (or any adb/fastboot tool you prefer):
https://developer.android.com/studio/releases/platform-tools

+ FastbootEnhance (or any Payload Dumper you prefer):
https://github.com/libxzr/FastbootEnhance/releases

+ Unlock Xiaomi Device:
1. Enable Developer Options
2. Settings> Additional Settings> Developer Options> My Unlock Status
3. Login Xiaomi account under 4G LTE connection
4. Wait 168 hours (or bypass waiting time using modified Mi Unlock Tool)
5. Unlock device from Mi Unlock Tool (you can try unlock to check if the device is under waiting time)

## First installation (Clean flash):

**⚠ Make sure you have unlocked the phone, or may brick it. ⚠**

Download ArrowOS ROM zip for Xiaomi Poco F3 / Xiaomi Mi 11X / Redmi K40:
https://arrowos.net/download/alioth
Vanilla Build presents the cleanest OS and GApps Build pre-installed Google apps and services.

Extract image `boot` and `vendor_boot` from ROM zip with Payload Dumper.
{% asset_img partitionsUnderPayloadDumper.png Partitions under Payload Dumper %}

Reboot in fastboot (press and hold volumn down and power button at same time when power off).
{% asset_img Xiaomi-MIUI-Fastboot-Screen-Mi-Bunny-Mitu.jpg Fastboot Screen Mi Bunny %}

Flash arrowos recovery (boot.img and vendor_boot.img):
```
fastboot flash boot_ab boot.img
fastboot flash vendor_boot_ab vendor_boot.img
```

Reboot in ArrowOS Recovery:
```
fastboot reboot recovery
```

Make format data:
Factory reset -> Format data

Flash ROM:
Apply update -> Apply from ADB
```
adb sideload Arrow-alioth.zip
```

Follow what show on device, should be ... Step 1/2 -> 2/2, then flashing ended, can reboot device in system.
In cmdline:
If the process succeeds the output will stop at 47% and report `adb: failed to read command: Success`.
In some cases it will report `adb: failed to read command: No error` which is also fine!

If you want to install separate GApps on vanilla buildtype, after flash ROM:
Advanced -> Reboot to recovery
Flash gapps:
Apply update -> Apply from ADB
```
adb sideload GApps.zip
```

## Install Update (dirty flash):

Go in Settings -> System -> Updater

Download new build -> Install

Device will automatically download, reboot into recovery and install a new build.


> Reference
> https://forum.xda-developers.com/t/rom-11-0-0-alioth-aliothin-arrowos-11-0-official-monthly.4279481/#post-85045261
> https://blog.jhangy.us/post/unlock-and-flash-xiaomi-redmi-phones/