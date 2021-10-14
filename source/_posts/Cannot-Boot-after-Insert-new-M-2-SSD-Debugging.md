---
title: Cannot Boot after Insert new M.2 SSD Debugging
date: 2021-10-14 15:54:00
tags:
---


Just record what I thought and how I debug.

## Situation

The device kept showing `Reboot and Select proper Boot device` after I added a M.2 SSD.
It was totally fine before that.

## Conclucion

Make sure M.2 slot does not conflict with SATA ports. Check it with motherboard manual.

<!-- more -->

## What happened

My Device:
+ CPU: AMD R5 3600
+ MB: ASUS TUF B550 PLUS
+ SSD(system disk): Adata XPG SX8200 Pro 512GB
+ HDD(data disk): WD HDD 2TB
+ SSD(new added): WD BLACK SN750 1TB

There are two M.2 slots on the motherboard (actually is three, two for SSD and one for wireless network card). M.2_1 has PCIe 4.0 x4 direct to cpu, M.2_2 go through B550 chipset share PCIe 3.0 x4 bandwidth with other devices.

System disk is on M.2_1, I wanted to add new ssd on M.2_2. After plug in and boot, it displayed `Reboot and Select proper Boot device`.
{% asset_img RebootAndSelectProperBootDevice.jpg Reboot and Select proper Boot device %}
But system disk can always been read in BIOS.
{% asset_img DisksBerforeAdd.jpg Disks Before Adding new M.2 SSD %}
{% asset_img DisksAfterAdd.jpg Disks After Adding new M.2 SSD %}
And I noticed that HDD disappeared.

So there was two issues:
1. Cannot boot into Windows
2. HDD undetected

I tried to solve the boot issue first. Since system disk was fine, it should be able to boot into Windows.
Fisrt thing I did was to check boot priority. It seems nothing abnormal, system disk was still the first boot device.
{% asset_img BootOptionPriorities.jpg Boot Option Priorities %}

Therefore I reset BIOS to default and cleared CMOS.
{% asset_img BiosResetDefault.jpg BIOS Reset Default %}

Then... **all disks disappeared... WTF?**

I figured out CSM mode (legacy BIOS) is default disabled and both my disks are MBR partition. Disks can be detected after i turned it on. But still `Reboot and Select proper Boot device`.
So I removed the new SSD and try if it can boot properly. It could works just fine. So I am sure that there is somthing wrong with the new SSD.

Then I thought if new SSD is GPT partition, could it cause the system unbootable?
The answer is no, computer with three disks mixed with both MBR and GPT is still bootable and work properly without problems.

I had kind of gived up and moved on to HDD undetected issue.

I looked into my motherboard manual on ASUS website, found out if M.2_2 slot is ocuppied, SATA port 5 and 6 are disabled. The HDD was connected on SATA port 5, this might be the reason. But it still cannot explain why the computer was unbootable. 

After i plugged HDD to SATA port 2 instead of 5, **BOOM! All problems solved!**

M.2_2 and SATA port 5, 6 confliction shall only cause disks undetectable but not unbootable.
ASUS you should make better side effect control......

Good news after torture, I recieve new RTX 3070 from EVGA with initial price the day after.

{% asset_img EvgaRtx3070.jpg EVGA RTX 3070 %}

*Thank you EVGA ~*