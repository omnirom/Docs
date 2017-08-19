![LOGO](images/omnirom_logo-big_layout_transparent-250px-150x150.png)
# OmniROM Documents
## Porting Omni to your device
=====
### Introduction
Omni is designed to use a basic AOSP device tree, with a few small modifications. This page will detail the necessary changes.

### Setup the base
To begin, fork an already working device repo and delete their makefiles and stuff like `omni_[device].mk` and `omni.dependencies`.

**Tip #1 - Never blindly edit anything that says full. If you do so, chances are your device won't boot.**

### Create the Omni make files
1. First you need to add a new make file for Omni. See the one below for an example:
  - https://github.com/omnirom/android_device_oneplus_oneplus3/blob/android-7.1/omni_oneplus3.mk
2. Add the makefile you created into `AndroidProducts.mk`. See the one below for an example:
  - https://github.com/omnirom/android_device_oneplus_oneplus3/blob/android-7.1/AndroidProducts.mk
3. Create a new file named `vendorsetup.sh`. See the one below for an example:
  - https://github.com/omnirom/android_device_oneplus_oneplus3/blob/android-7.1/vendorsetup.sh
4. Create a json file named `omni.dependencies` which will pull all of the necessary repos to build. See the one below for an example:
  - https://github.com/omnirom/android_device_oneplus_oneplus3/blob/android-7.1/omni.dependencies

**Tip #2 - JSON files can be really annoying. Go to http://jsonlint.com/, paste in your json file and let it check for errors.**

5. You now need to setup your device tree for **Team Win Recovery Protocol, aka TWRP**. This usually consists of the following (visit this [link](http://forum.xda-developers.com/showthread.php?t=1943625) for more information):
  - adding TWRP specific build flags in `BoardConfig.mk`
  - creating `twrp.fstab` file
  - adding `twrp.fstab` to the **PRODUCT_COPY_FILES** make variable.

That's it. If you did everything correctly, then you should have a working build.

### CAF Devices
#### Android 7.0
**Basic QCOM Support**
To enable basic QCOM hardware support, the following must be added to your device's `BoardConfig.mk`:
```
BOARD_USES_QCOM_HARDWARE := true
```
Furthermore, QCOM_BSP support should be included in your device's `BoardConfig.mk` as follows:

```
TARGET_USES_QCOM_BSP := true
```

**Audio/Display/Media HAL**
*hardware/qcom/[audio/display/media]* are separated on a per-platform basis. You must declare the HAL variant for your platform in your device's `BoardConfig.mk` via:

```
TARGET_QCOM_[AUDIO/DISPLAY/MEDIA]_VARIANT := caf-msm89**
```

**Enabling QCOM Audio/Video Enhancements**
Include the following in your `BoardConfig.mk`:

```
TARGET_ENABLE_QC_AV_ENHANCEMENTS := true
```
