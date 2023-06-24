# Rooted-Android-Pixel-Update-Guide
A guide on updating the Android OS while rooted | Written for the Google Pixel 7 Pro

## Let's begin

0. Assumes prerequisites are already installed: Google USB Drivers for PC-Phone interaction, platform-tools from Google, bootloader unlocked, Magisk is already up and running on phone, USB-Debugging is enabled, PC-Phone connection is set to File Transfer

1. Download the latest Google Pixel 7 Pro factory image from: https://developers.google.com/android/images#cheetah

2. Extract the .zip that it comes in (will look something like "cheetah-tq2a.230305.008.c1.zip"). 

3. Extract the init_boot.img file located inside "image-cheetah-some.timestamp.build.number.zip" which is inside the zip we extracted in step 2.

4. Copy that init_boot.img file to your phone. Personally, I copy it to my Downloads folder.

5. Patch that init_boot.img file with Magisk via [1. Install -> 2. Select and Patch a File -> 3. "Let's Go"]. The file will be patched and sent to the location of the original init_boot.img file.

6. Copy the MAGISK PATCHED init_boot.img file back to your computer

7. Open the Android Flash Tool by Google in your browser (flash.android.com), and DESELECT the following build flags: "Wipe Device", "Lock Bootloader", "Force flash all partitions". Make sure to do this, or you will lose all personal data on the device

8. Click "install build". DO NOT INTERACT WITH YOUR PHONE DURING THE INSTALL PROCESS. Let it complete fully (it will take several minutes and reboot on its own several times including into a mode called "FastbootD", and finally reboot back to the lockscreen).

9. Once the phone is back to the lockscreen, launch platform-tools on your connected PC.

10. Check that connection to your phone via platform-tools works via "adb devices". You should see a device which represents your phone. If it says "unauthorized", make sure to hit "Allow" on the USB Debugging Notification on your phone.

11. Run "adb reboot bootloader" to get into Fastboot mode on your phone. 

12. Check that the connection persisted via "fastboot devices". You should see a similar message to step 10.

13. Now run "fastboot flash init_boot ./path/to/magisk-patched-init_boot.img"

14. Once that is done, run "fastboot reboot" to restart the device. You should be updated + have Magisk installed now.
