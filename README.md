# Not yet cleaned Automic
The original project was made by [iProgramInCpp](https://github.com/iProgramMC) & [Playingo](https://github.com/playingoDEERUX). Which of course turned out to be an Account Stealer for relaunching Growalts. Keep that in mind and don't praise them for that.

This project makes use of letting the game load their own library. I have never seen Dear Imgui getting used for Android Mod Menus before, which why I was interested in stuff like Exafarm and Automic the whole time. Guess, because of them, we will see menus like this pop up for not only Growtopia pretty soon, but also other mobile phone games. Credits to that.

## Prerequisites
Since both original Devs use Windows. Other Operating Systems might not be supported.
- [Java Runtime](https://java.com/en/download/)
- [Android NDK](https://dl.google.com/android/repository/android-ndk-r16b-windows-x86_64.zip)
- [Android SDK Platform-Tools](https://developer.android.com/studio/releases/platform-tools)
- [7-Zip](https://www.7-zip.org/)

After having all of that installed. Restart your PC for the better. Now you will need to edit the batch files from the Automic Project Folder, since your Paths might not be the same.

### **buildall.bat:**

Change ``C:\Program Files\7-Zip`` to where you have installed **7-Zip**. This is the default path. If you haven't changed the directory in the Setup, you can leave it like that. Change ``D:\android-ndk-r16b`` to where you have extracted **Android NDK** to.
```batch
@ECHO OFF
SET PATH=%PATH%;C:\Program Files\7-Zip;D:\android-ndk-r16b;
CALL COMPILE.BAT
CALL PACKAGEAPK.BAT
CALL INSTALL.BAT
```
