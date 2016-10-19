# High DPI External Manifest Files

I use a 4k screen and a lot of the time I will launch a program that doesn't know how to scale properly. Most programs use set pixel ratios and don't know what to do when you have an extremely high pixel density.

Luckily there is an easy fix. At least most of the time it's easy. All it requires is to change one registry value to force Windows to use an external manifest file, and then create that file in the same directory as the exe you want to launch.

The only problems I've ever had were when exe's come packaged with a manifest file. Some programs have dependencies and settings inside their manifest file that you may want to keep. I'll go over all that here.

## Telling Windows to use an external manifest file

Before ever making any changes to the registry it's a good idea to make a backup. This is change is easy to fix, however, if you run into some kind of problem.  

1. Press  Windows Button + R, type “regedit”, and then click OK.
2. Navigate to the following registry subkey:
..* HKEY_LOCAL_MACHINE > SOFTWARE > Microsoft > Windows > CurrentVersion > SideBySide
3. Right-click, select NEW > DWORD (32 bit) Value
4. Type PreferExternalManifest, and then press ENTER.
5. Right-click PreferExternalManifest, and then click Modify.
6. Enter Value Data 1 and select Decimal.
7. Click OK. Exit Registry Editor.

[Credit](http://www.danantonielli.com/adobe-app-scaling-on-high-dpi-displays-fix/)

I also attached a .reg file in the repository. You can just run this on a Windows machine and it will do the above steps for you.

## Creating an external manifest file

Creating an external manifest file is easy. All you have to do is take the "default.exe.manifest" file located in this repository and change the "default" in the name to the actual name of your exe. For example if you're trying to launch photoshop which has an associated executable of "photoshop.exe" then you would cange the manifest file name to "photoshop.exe.manifest". Then you have to place this file in the same directory as your executable (in the same directory as photoshop).

Unfortunatley, this doesn't work for all programs. This is because some programs come packaged with a manifest file that could have listed dependencies needed for the program. To fix this all I had to do was open up the exe in a program like 7-zip and find the manifest file. For ANSYS Electronics Desktop it was located in the 'MANIFEST' fold after opening it in 7-zip. I copied this file out and added all the dependencies listed in ANSYS's manifest file into the "default.exe.manifest" file. Then it worked.

The ANSYS Electronics Desktop manifest file is also located in htis repository.
