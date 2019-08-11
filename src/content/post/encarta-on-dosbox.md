---
title: "How to install Encarta 96... on Windows 95... on DOSBox"
date: 2019-08-11T6:26:52-07:00
draft: false
---

The song *Still Alive* in the Classic Valve game **Portal** has the lyric:

> "We do what we must, because we can"

I can't think of a better way to describe what I'm about to present.

Nobody **needs** to run **Encarta 96** in a virtualized **Windows 95** environment, unless there is a very particular need to feel nostalgic for mid-1990s computing.

## So Then, Why Exactly?

It started with a Tweet by [@shanselman](https://twitter.com/shanselman) that got people taking about pre-internet **Wikipedia**, otherwise known as **Microsoft Encarta**:

{{< tweet 1158780839464849409 >}}

From there it sparked many, including myself, to remember their childhoods watching postage stamp resolution videos and playing the **Mind Maze** trivia game that came with it.

![Mind Maze](/images/encarta_1.png)

Well, good news! **Encarta 96** is available on [archive.org](https://archive.org/details/MicrosoftEncarta96Encyclopedia1996EnglishOEM).

More good news everyone! It is still (amazingly) compatible and works* on **Windows 10**. Holy backwards compatibility, Batman!

  > *Make sure you use the MPEG Edition, to avoid any codec issues
  >
  > {{< tweet 1159181177527259137 >}}

But I had to go deeper.

{{< tweet 1158797039972450305 >}}

I didn't just want **Encarta 96**, I wanted **Encarta 96** in its natural environment.

**I wanted the full Windows 95 experience.**

So I went where the classic pc gamers go: **DOSBox**.

I found a [great guide from 2014](https://dsync.blogspot.com/2014/03/a-complete-guide-to-install-windows-95.html) that got me started, but still needed some DIY.

## Step 1: Setup DOSBox

![DOSBox](/images/encarta_2.png)

**DOSBox** is a virtualization program that emulates older hardware, so that games (and other software) that is tied to processor speed or certain architecture work the way the creators originally intended.

1. If you want to journey down the same path [Download DOSBox](https://www.dosbox.com/download.php?main=1) and install it.

1. Take note of your **DOSBox install folder**. Mine was `C:\Program Files (x86)\DOSBox-0.74-3`. You will be moving a few files here.

1. Launch **DOSBox 0.74-3 Options** (this is a start menu option that launches a text file in notepad)

    Set this property under `[cpu]`:

    ```bash
    core=normal
    cputype=pentium_slow
    ```

    As noted in the original guide (and test by me), not setting this make Windows 95 go crazy graphically (the cursor becomes a black box, for instance).

1. Don't forget to save!

## Step 2: File Download and Preparation

Here is a rundown of all the files you will need to do this yourself! This will all be used later, I promise.

### FAT16 Hard Drive Image

Everything we are dealing with is 16-bit You will want a **FAT16** formatted hard drive image.

You can download a pre-made one [here](https://sites.google.com/site/dotalshoff/games/dosbox).

If you don't know what size, use the 2GB image (**hdd-2gb.7z**), plenty of room for the fun in this guide.

> Fun Fact: A Best Buy employee once told my dad 2GB of Hard Drive space is all we'd ever need.

Download and extract that bad boy (with **7zip**) and move it to your **DOSBox install folder** (see I told you that you would need that).

**Note:** The original guide said to check it was formatted properly, but I personally didn't have any problem with just using it.

### XCOPY

Something that is super useful for file movement, like what we'll do later is **XCOPY**. However, It's not in **DOSBox** by default.

¯\\_(ツ)_/¯

Let's get it from **FreeDOS**!

1. **FreeDOS**'s XCOPY command is available [Here](http://www.ibiblio.org/pub/micro/pc-stuff/freedos/files/distributions/1.2/repos/pkg-html/xcopy.html)

2. Download, extract, and move the **XCOPY.EXE** file from **/BIN/** to your **DOSBox install folder**.

### Boot Disk

You will need an MS-DOS 6.22 boot disk to install windows 95.

[Here](https://www.allbootdisks.com/download/dos.html) is one of many places you can get one.

Copy **Dos6.22.img** to your (you guessed it) **DOSBox install folder**.

### Windows 95

Version **4.00.950** of **Windows 95** works with **DOSBox** and is available on archive.org [here](https://archive.org/details/MicrosoftWindows954.00.9501995EnglishOEM).

Copy **95ARKFUL.ISO** to your **DOSBox install folder**.

Take notice of the **Certificate of Authenticity** [here](https://archive.org/download/MicrosoftWindows954.00.9501995EnglishOEM/Scans.zip/Certificate%20of%20Authenticity%201.tif) for use during install.

### Encarta 96

For an easier time, use the MPEG Edition [here](https://archive.org/details/MicrosoftEncarta96Encyclopedia1996EnglishOEM).

Copy **ENCAR96ENCY.iso** to your **DOSBox install folder**.

### Double Check

You should now have all these highlighted files in your **DOSBox install folder**

![Files you should have](/images/encarta_3.png)

## Step 3: Setup your FAT16 Hard Drive

DOSBox can have Windows 95 installed on it, and that's what I want to do.

I like to use the `[autoexec]` area at the end of this file to run a batch of commands in DOSBox. Any time I say "Change the `[autoexec]`" I mean:

1. Launch **DOSBox 0.74-3 Options**
2. Edit the lines at the end of the file (under `[autoexec]`)
3. save.

Got it? Here we go!

1. These are the command you want to run in DOSBox. Change the `[autoexec]` to be these commands. You can always clear `[autoexec]` and run them individually to troubleshoot.

    ```bash
    IMGMOUNT C hdd2gb.img
    MOUNT D .
    IMGMOUNT E 95ARKFUL.iso -t iso
    C:
    COPY D:\XCOPY.EXE
    MKDIR WIN95
    XCOPY E:\WIN95\*.* C:\WIN95 /E
    Z:
    BOOT Dos6.22.img
    ```

2. Launch DOSBox, if you put the commands above in `[autoexec]` (or ran them individually), you should be at a boot disk prompt.

    ![Startup Disk Prompt](/images/encarta_4.png)

3. You are about to see some stuff you may not have seen in a while. Use the following set of commands to launch Setup (without scanning the disk first).

    ```bash
    C:
    CD WIN95
    setup /is
    ```

4. Do all the standard options, you don't need any additional drivers or to make a startup disk. You'll need that **[Certificate of Authenticity](https://archive.org/download/MicrosoftWindows954.00.9501995EnglishOEM/Scans.zip/Certificate%20of%20Authenticity%201.tif)**.

5. At the end of installation it'll reboot and DOSBox will quit.

6. Change the `[autoexec]` to the following two commands:

    ```bash
    imgmount 2 hdd-2gb.img -size 512,63,64,520 -fs none
    boot -l c
    ```

7. Launch DOSBox again, and let Windows 95 finish doing its thing.

After all of this, you now have a Windows 95 virtual environment! There was much rejoicing.

## Step 4: Install Encarta

1. Change the `[autoexec]` to (again these can be run individually as well):

    ```bash
    IMGMOUNT C hdd-2gb.img
    IMGMOUNT D ENCAR96ENCY.iso -t iso
    C:
    MKDIR ENCARTA
    XCOPY D:\*.* C:\ENCARTA /E
    ```

1. Open DOSBox, knowing this will take a bit.

1. After everything is copied, close DOSBox

1. Change the `[autoexec]` back to the following two commands:

    ```bash
    imgmount 2 hdd-2gb.img -size 512,63,64,520 -fs none
    boot -l c
    ```

1. Start DOSBox. Now that you are in Windows 95 proper, go to **My Computer** > **C:** and open the **ENCARTA** folder.

    ![Windows 95](/images/encarta_5.png)

1. Run **Setup.exe** and do the typical install.

1. Once done, launch Encarta 96!

## ...And That's Jenga!

Hello fellow time traveller. You will now experience the joy and lag of FULL WINDOWS 95!

{{< tweet 1159117731150487553 >}}

This can also be used for any other ISO files from the 16-bit era. Just follow the same copy process in Step 4.

Maybe I'll post again with my adventures actually using Encarta 96!
