# android_root_update
Update android 5.x while preserving root.

##Prerequisites

ADB, fastboot and the (RIGHT) system image to be installed.
An unlocked bootloader.
Custom recovery. ( Can also be installed after step 7)

Do it on your own risk!


``` bash
$ fastboot oem unlock
```
Unlocking will DELETE all your private data on the phone.

###Install Prerequisites
``` bash
$ sudo apt-get install android-tools-adb android-tools-fastboot android-tools-adbd android-tools-fsutils  
```

###Get image
For Nexus devices get the factory images [here](https://developers.google.com/android/nexus/images?hl=en). For others manufacturers check their website.


### Process

1. Check hashsum of the image to verify its integrity

``` bash
$ sha1sum 
```

2. Extract the image from the .tgz

``` bash
$ tar -xvf IMAGE_NAME.tgz
```

3. Move into the extracted folder 
``` bash
$ cd IMAGE_NAME
```

3. Move into the extracted folder 
``` bash
$ cd IMAGE_NAME
```

4. Prepare your phone

Push the supersu.zip to your sdcard ( you can use adb shell to find the right path on your phone). Reboot into bootloader.

``` bash
adb push supersu.zip /storage/sdcard0 
adb reboot-bootloader
```

5. Flash new bootloader and radio

``` bash
fastboot flash bootloader bootloader-IMAGE_SPECIFIC_NAME.img
fastboot reboot-bootloader
sleep 5
fastboot flash radio radio-IMAGE_SPECIFIC_NAME.img
fastboot reboot-bootloader
sleep 5
```

6. Extract the zip

``` bash
7z x image-IMAGE_SPECIFIC.zip
cd image-IMAGE_SPECIFIC
```

7. Flash the stuff we're interested in


``` bash
fastboot flash boot boot.img
fastboot flash system system.img
```

8. Boot into recovery and reinstall root
9. Reboot into new android.