# Rooted-Android-Pixel-Update-Guide
A guide on updating the Android OS while rooted | Written for the Google Pixel 7 Pro | Works across Major OS Version Upgrades

**NOTE: I followed this guide to update my Pixel 7 Pro from Android 13 to Android 14 and it worked without any isues at all :)**
**UPDATE: This guide still works for the Pixel 8 series of phones**

## Let's begin

0. Assumes prerequisites are already installed: [Google's USB Drivers for PC-Phone interaction](https://developer.android.com/studio/run/win-usb), [platform-tools from Google](https://developer.android.com/tools/releases/platform-tools), [bootloader unlocked, Magisk is already up and running on phone](https://forum.xda-developers.com/t/june-20-2023-tq3a-230605-012-a1-verizon-mvnos-june-13-2023-tq3a-230605-012-global-unlock-bootloader-root-pixel-7-pro-cheetah-safetynet.4502805/), [USB-Debugging is enabled](https://www.howtogeek.com/129728/how-to-enable-developer-options-menu-and-enable-and-usb-debugging-on-android/), PC-Phone connection is set to File Transfer

1. Download the latest Google Pixel 7 Pro factory image from: <https://developers.google.com/android/images#cheetah>

2. Extract the .zip that it comes in (will look something like `"cheetah-tq2a.230305.008.c1.zip"`). 

3. Extract the `init_boot.img` file located inside `"image-cheetah-some.timestamp.build.number.zip"` which is inside the zip we extracted in step 2.

4. Copy that `init_boot.img` file to your phone. Personally, I copy it to my Downloads folder.

5. Patch that `init_boot.img` file with Magisk via [1. Install -> 2. Select and Patch a File -> 3. "Let's Go"]. The file will be patched and sent to the _Downloads_ folder on your phone.

6. Copy the **magisk patched boot image** file (`magisk_patched-version_someRandomSequenceOfChars.img`) back to your computer

7. Open the [Android Flash Tool (AFT) by Google](https://flash.android.com/) in your browser. 
**If the device shows up as "Already in use", run `adb kill-server` in your computer's commandline, and then reload the AFT page.** If you see this screen, click "More Releases": ![image](https://github.com/pritster5/Rooted-Android-Pixel-Update-Guide/assets/7132319/0f810a3d-a848-45d6-8872-7e0f96eb0e21)

8. Then click your current Android version (13 at the time of writing) and the AFT will automatically choose the latest stable build. Then choose "Default" unless you're on the Verizon version of the device (bless your soul, why would you do that to yourself :|) 

9. **De-Select** the following build flags: "Wipe Device", "Lock Bootloader", "Force Flash all partitions". **Make sure to do this, or you will lose all personal data on the device!**

10. Click "install build". **DO NOT INTERACT WITH YOUR PHONE DURING THE INSTALL PROCESS**. Let it complete fully. It will take several minutes and reboot on its own several times including into a mode called `"FastbootD"`, and finally reboot back to the lockscreen.

11. Once the phone is back to the lockscreen, unlock the phone once and then launch `platform-tools` on your connected PC. If `platform-tools` is in your `PATH` environment variable, then this is not necessary, just type `adb devices` in any command prompt/Powershell window and the command will be recognized.

12. Check that connection to your phone via `platform-tools` works via `adb devices`. You should see a device which represents your phone. If it says "unauthorized", make sure to hit "Allow" on the USB Debugging Notification on your phone.

13. Run `adb reboot bootloader` to get into Fastboot mode on your phone. 

14. Check that the connection persisted via the `fastboot devices` command. You should see a similar message to step 12.

15. Now run `fastboot flash init_boot ./path/to/magisk-patched-init_boot.img`

16. Once that is done, run `fastboot reboot` to restart the device. You should be updated + have Magisk installed now.

## Thanks for reading!
