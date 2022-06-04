# Ubuntu 22.04 proot-distro with XFCE4, VSCode, box86/box64, wine and optional GPU acceleration

I have been experiencing with the possibilities and limits of Termux + PRoot-Distro in the past few days/weeks, and I tried to set up a Ubuntu system inside proot that can be used for many different things like development, running non-ARM Linux and Windows software, maybe even some light gaming. I thought it would be nice to share my "finished" proot-distro(s) with you, so here they are:

**Normal image (recommended for most devices):**
[https://mega.nz/file/82oRQQaI#S8pnq2ZnjwWcX11p5-x688YcuXx5TOQZTJAgFjrTksw](https://mega.nz/file/82oRQQaI#S8pnq2ZnjwWcX11p5-x688YcuXx5TOQZTJAgFjrTksw)

What does it contain:

-   Ubuntu 22.04 installed from original rootfs provided by PRoot Distro.
    
-   Pre-installed XFCE4 with TigerVNC Server installed (Default VNC password: ubuntu)
    
-   Pre-installed Firefox ESR browser
    
-   Pre-installed Visual Studio Code for development-on-the-go (and I also installed OpenJDK 17 & Python 3.10 with pip support, so you can start coding right away by installing the right extensions in VSCode)
    
-   Box86 and Box64 pre-compiled and pre-installed, you can run x86 apps with "box86 path/to/app" and x64 apps with "box64 path/to/app" commands.
    
-   Wine 32-bit (6.18) & 64-bit (6.0.1) version pre-installed, you can open them by clicking on the desktop icons, and then you can use the explorer window to launch Windows apps.
    

**GPU-accelerated version (Mesa patched with Turnip&Zink support) for newer Adreno GPUs:**  [https://mega.nz/file/UqoVmCqZ#NU0QmJjU4UX7_4ZKolpjQwRDLuroKXzhlJ-NrczkB7k](https://mega.nz/file/UqoVmCqZ#NU0QmJjU4UX7_4ZKolpjQwRDLuroKXzhlJ-NrczkB7k)

-   Contains everything from the normal version, plus:
    
-   Mesa is patched to have support for Adreno GPUs included in newer Snapdragon-based phones.
    
-   Only Adreno GPUs are supported, and only those that have Vulkan and KGSL support in Android. For example, Adreno 650 (found in Snapdragon 865) should be fine, Adreno 620 (in Snapdragon 765G is NOT working)
    
-   GPU acceleration is OPTIONAL, which means you have to manually turn it on using a .sh file that I placed in the root directory (I also added a message on terminal startup to warn about that). The setting only applies for the current terminal session, so you have to start the applications from there if you want GPU accelerated graphics.
    
-   I also added a GPU acceleration-enabled shortcut for Wine x86 & x64, that you can launch from the desktop.
    
-   OpenGL is supported up to 3.3 version. This means that some software (like newer versions of Blender) will not work.
    

**How to install:**

-   You need an Android phone with 64-bit CPU, 64-bit Android kernel and 64-bit (or universal) Termux installed. Don't use the Play Store version of Termux, it is deprecated! Also, Android 12 will probably not work due to the new process killing "improvements".
    
-   Copy the downloaded file to your device, I'll use the Downloads folder in this guide.
    
-   Make sure your packages are up to date with "pkg update" and "pkg upgrade"
    
-   Install proot-distro on Termux with "pkg install proot-distro"
    
-   Install the base version of Ubuntu proot.distro with "proot-distro install ubuntu"
    
-   Use "termux-setup-storage" command to access your phone's internal memory (you also have to give permission in Android).
    
-   Use the "proot-distro restore ~/storage/downloads/filename.gz" (obviously replace filename with the name of the downloaded file) to install the downloaded version of Ubuntu proot-distro.(WARNING: this will delete your previous Ubuntu installation if you have one!)
    

**How to use (you have to do this everytime you want to use Ubuntu on your phone):**

-   Open Termux
    
-   Use "proot-distro login ubuntu" command to access your Ubuntu proot-distro.
    
-   Use "vncserver :1" command to launch a VNC server on localhost:5901.
    
-   Minimize Termux (make sure to setup Android so it won't kill Termux in the background) and open your preferred VNC Viewer app (I use RealVNC).
    
-   Connect to "localhost:5901" (you can also try  [127.0.0.1:5901](https://127.0.0.1:5901/)  if the former does not work), the default password of the VNC server is "ubuntu".
    
-   You should be connected to the desktop.
    

To "properly" exit from Ubuntu, use the command "vncserver -kill :1" which will close the GUI interface and the VNC server, and then use "exit" command to go back to Termux from proot-distro. After that, you can close Termux without any worries.

Also, you may get some "uid not found" messages on proot-distro startup. That's because using the restore function is not the "proper" way to install a proot-distro image, but I did not find any real-world problems (so far) with transferring the backup image to another device.
