---
title: Rooting Deivce with Magisk
date: 2021-12-20 22:55:41
tags:
---


{% asset_img Magisk_Logo.png Magisk %}

Magisk is a systemless rooting system.
Which was developed by Topjohnwu and launched in the year 2016, and since then has been widening its horizons with each passing year.
Magisk Root is a boon especially when it comes to running the financial applications.

<!-- more -->

## Preparation

+ SDK Platform Tools (or any adb/fastboot tool you prefer):
https://developer.android.com/studio/releases/platform-tools

## Install Magisk App

Download the latest Magisk app from {% link https://github.com/topjohnwu/Magisk/releases Topjohnwu's Github releases %} and install it.
Open Magisk app and check if value of `Ramdisk` is `Yes`. If not, you will need advanced tutorial from my reference links below.

## Patch Boot Image

You need a copy of `boot.img` which is exracted from official firmware packages or custom ROM that your device is currently using.
If your device utilizes the A/B partition scheme, you will need a Payload Dumper to extract `payload.bin` in `ROM.zip` (see my previous article).
{% asset_img partitionsUnderPayloadDumper.png Partitions under Payload Dumper %}

Once you reach the boot image, copy it to your device.
In Magisk App, press the `Install` button and choose method `Select and Patch a File`, and select the stock boot image that you just copied.

## Flash Patched Boot Image

Magisk App will patched the image to `Download` file in your device, the path shall be `{Internal Storage}/Download/magisk_patched_{random_strings}.img`. Copy it to your PC.

Flash the patched boot image to your device:
```
fastboot flash boot magisk_patched_{random_strings}.img
```

Reboot the device:
```
fastboot reboot
```

## Enjoy Magisk

Open App and check if Magisk in installed properly:
{% asset_img Magisk-Installed.png Magisk after installed %}


# TroubleShooting

## Cannot Boot after Flashing Boot Image

If you stuck at booting logo screen, you may have patched wrong boot image.
Download exact same version of ROM of your device current system. Re-patch `boot.img` and re-flash the new patched boot image to device shall fix it.

# Reference

> https://topjohnwu.github.io/Magisk/install.html
> https://magiskmanager.com/
> https://www.xda-developers.com/how-to-install-magisk/