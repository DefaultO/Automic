# Not yet cleaned Automic
Automic is an Android Internal made for the Game [Growtopia](https://www.growtopiagame.com/). Autofarming in this Game can be very lucrative which why this one in particuliar got some hype, next to Exafarm and a few private Bots.

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

### **compile.bat:**

Change ``D:\android-ndk-r16b`` to where you have extracted **Android NDK** to. Everything else points to folders in the same directory the script got run. Leave them as they are.
```batch
D:\android-ndk-r16b\ndk-build
NDK_PROJECT_PATH=\
NDK_APPLICATION_MK=\jni\Application.mk
cmd /k
```

### **install.bat**


Same here. Edit all paths. Even though I don't know why it has to be included here. Optional: Remove the ``REM`` in front of ``adb uninstall com.rtsoft.growtopia``. This will uncomment that line. And will cause Growtopia to get uninstalled every build. Which is quite useful when you have builds that just won't work or you find small things that you have to edit. It won't be able to install/update the android package when you have one with the same name already installed. So choose for yourself if you want it to happen automatically, or you want to uninstall it yourself every single small update.
```batch
@ECHO OFF
SET PATH=%PATH%;C:\Program Files\7-Zip;D:\android-ndk-r16b;D:\platform-tools
ECHO Installing on default phone...
REM adb uninstall com.rtsoft.growtopia
adb install growtopia.apk

ECHO Done, spawning logcat...
adb logcat -s "INfERNAL"
```

### **PackageApk**

This is something I couldn't manage to work. It won't place the library into Growtopia's APK Lib Folder on it's own. You will probably have to replace ``libblue.so`` to ``libinfernal.so``. I don't know, they had a private version or this source is super old.

Also create a new Folder in the Source Folder (where all those batches are) called ``gt``. In this Folder you put the original ``growtopia.apk``, since it gets deleted, don't download it to this folder, but always copy-paste it into that folder. You will probably need the one for 3.59, not sure what version the sigs are there for.

```batch
@ECHO OFF

SET PATH=%PATH%;C:\Program Files\7-Zip;D:\android-ndk-r16b;D:\platform-tools
ECHO Copying library...
REM Copy the so file from libs/armeabi-v7a to gt's lib dir
COPY libs\armeabi-v7a\libinfernal.so gt\lib\armeabi-v7a\libinfernal.so

ECHO Packaging the library...
REM delete the original apk
DEL growtopia.apk

REM package the apk itself
CD gt
7Z a -tzip growtopia.apk *
CD ..
MOVE gt\growtopia.apk growtopia.apk

ECHO Signing the apk...
REM sign the apk
java -jar apksigner.jar sign  --key apkeasytool.pk8 --cert apkeasytool.pem  --v4-signing-enabled false growtopia.apk
```
