---
title: Install Arrow OS on Redmi K40
tags:
---

# INSTALLATION PROCEDURE:

## Preparation

SDK Platform Tools (adb/fastboot tools):
https://developer.android.com/studio/releases/platform-tools

Unlock Xiaomi Device:
1. Enable Developer Options
2. Settings> Additional Settings> Developer Options> My Unlock Status
3. Login Xiaomi account under 4G LTE connection
4. Wait 168 hours (or bypass waiting time using modified Mi unlock tool)
5. Unlock device from Mi Unlock Tool

## First installation (Clean flash):

You need adb/fastboot tools.
Download boot, vendor_boot and rom zip:
https://drive.google.com/file/d/1o-4T4hfEtxECIss-DVSSYAM1Kvy2iDN9/view?usp=sharing
https://drive.google.com/file/d/1PgtI8bOV1yjmTZJ7euP6xDFzMszY6AXb/view?usp=sharing
https://arrowos.net/download/alioth

Reboot in fastboot. Flash arrowos recovery (boot.img and vendor_boot.img):

```
fastboot flash boot_ab boot_alioth.img
fastboot flash vendor_boot_ab vendor_boot_alioth.img
```

Reboot in ArrowOS Recovery:

```
fastboot reboot recovery
```

Make format data (Factory reset -> Format data).

Flash ROM (Apply update -> Apply from ADB):

```
adb sideload name.zip
```

Follow what show on device, should be ... Step 1/2 -> 2/2, then flashing ended, can reboot device in system. (In cmdline: If the process succeeds the output will stop at 47% and report `adb: failed to read command: Success`. In some cases it will report `adb: failed to read command: No error` which is also fine!")

If you want install separate gapps on vanilla buildtype, after flash ROM:

Advanced -> Reboot to recovery

Flash gapps (Apply update -> Apply from ADB):

```
adb sideload name.zip
```
__________________________________________________

## Install Update (dirty flash):

Go in Settings -> System -> Updater

Download new build -> Install

Device will automatically download, reboot into recovery and install a new build.



> Reference
> https://forum.xda-developers.com/t/rom-11-0-0-alioth-aliothin-arrowos-11-0-official-monthly.4279481/#post-85045261
> https://blog.jhangy.us/post/unlock-and-flash-xiaomi-redmi-phones/