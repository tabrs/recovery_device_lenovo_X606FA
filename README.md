# TWRP device tree for Lenovo Smart Tab M10 FHD Plus (TB-X606FA/FX)

## Release info
This is an unofficial build.  Install at your own risk.

Build with minimal AOSP TWRP for Android 11.0.

### About Device

![Lenovo Smart Tab M10 HD](https://download.lenovo.com/images/ProdImageSmart/amazon_alexa.jpg "Lenovo Smart Tab M10 FHD Plus (TB-X606FA)")

Recovery Device Tree for Lenovo Smart Tab M10 FHD Plus wifi (TB-X606FA)
=======================================================================
Component   | Specs
-------:|:-------------------------
Chipset| MediaTek Helio P22T
CPU | ARM Cortex-A53, Octo-Core, 2.3 GHz
GPU     | IMG PowerVR GE8320, 650 MHz
Memory  | 2GB or 4GB (soldered)
Shipped Android Version | 9.0 (Pie), upgrade to 10.0
Storage | 32GB or 64GB eMMC
MicroSD | Up to 256 GB
Battery | 5000 mAh, Li-Po (non-removable)
Display | 1920x1200 pixels, 10.3"
Front Camera | 5.0 MP
Rear Camera  | 8.0 MP
Wifi | dual band, 802.11a/b/g/n/ac
WLAN | 4G LTE   (TB-X606X only)
Bluetooth | v5
USB | USB-C (micro USB)
Release Date | August 2020


## To build
If building for the TB-X606F, change BOARD_KERNEL_IMAGE_NAME in BoardConfig.mk before building.
```
. build/envsetup.sh
lunch twrp_X606FA-eng
mka recoveryimage
```

## Android 12: patch for FDE decryption
There was a change in the data structure for Keymaster in Android 12.  It is incompatible with vendor blobs prior to A12.

To make FDE decryption work, you will need to cherrypick this commit: [https://github.com/Yahoo-Mike/android_bootable_recovery/commit/b520ff41c5a0e7d35d8b8de426602975cf642ac0](https://github.com/Yahoo-Mike/android_bootable_recovery/commit/b520ff41c5a0e7d35d8b8de426602975cf642ac0)

Once this is available in TeamWin/android_bootable_recovery, I will delete this commit.

Make sure the following flags are set in BoardConfig.mk.  If not, Keymaster will fail with an INVALID_ARGS error:
```
PLATFORM_VERSION := 127
PLATFORM_VERSION_LAST_STABLE := $(PLATFORM_VERSION)
```
