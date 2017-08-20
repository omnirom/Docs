

<big>You '''must''' have a 64-bit environment.</big>

<big>A Linux computer '''should have 4 GB RAM''' or more, otherwise build errors may occur.</big>

Depending on your environment, it may be interesting to set-up a chroot to separate your Android build packages from the remainder of your system. However, implementation of such a setup is beyond the scope of this article. (Hint: ChromiumOS uses  something along those lines.)

== Ubuntu 13.10 ==
:''These instructions should work for other version of Ubuntu and most other Debian-based systems.)

'''Install build packages'''
Open a terminal (ctrl + alt + t). First install the necessary packages; copy paste the code below and hit enter.

<pre style="white-space: pre-wrap;
white-space: -moz-pre-wrap;
white-space: -pre-wrap;
white-space: -o-pre-wrap;
word-wrap: break-word;">
sudo apt-get update && sudo apt-get install git-core gnupg flex bison gperf libsdl1.2-dev libesd0-dev libwxgtk2.8-dev squashfs-tools build-essential zip curl libncurses5-dev zlib1g-dev openjdk-6-jre openjdk-6-jdk pngcrush schedtool libxml2 libxml2-utils xsltproc lzop libc6-dev schedtool g++-multilib lib32z1-dev lib32ncurses5-dev lib32readline-gplv2-dev gcc-multilib
</pre>

Check your java version (it must be 1.7)
  javac -version

If you're using multiple JDKs, change it using update alternatives, like so:
  update-java-alternatives -s java-1.7.0-openjdk-amd64

== Fedora 19 x64 ==
Source : http://rootzwiki.com/topic/30884-compile-aosp-on-fedora-17

First, due to some difference in the paths, installing Oracle's JDK6 is the easiest way to go:
Oracle's JDK [http://www.oracle.com/technetwork/java/javase/downloads/index.html]
Once downloaded,
<pre>sudo sh jdk-6u45-linux-x64-rpm.bin</pre>
<pre>sudo ln -s /usr/java/default/bin/javah /usr/bin/javah</pre>

Then, the needed packages:
<pre style="white-space: pre-wrap;
white-space: -moz-pre-wrap;
white-space: -pre-wrap;
white-space: -o-pre-wrap;
word-wrap: break-word;">sudo yum install -y zip curl gcc gcc-c++ flex bison gperf glibc-devel.{x86_64,i686} zlib-devel.{x86_64,i686} ncurses-devel.i686 libX11-devel.i686 libstdc++.i686 readline-devel.i686 libXrender.i686 libXrandr.i686 perl-Digest-MD5-File python-markdown mesa-libGL-devel.i686 git schedtool pngcrush</pre>
From here, the [[#Get the Omni code|next step will be the same as for Ubuntu]].

== Arch Linux ==

If you are using an x64 install, you should enable the multilib repository in /etc/pacman.conf, to permit 32 bit software to be installed.

Install the following packages on an x64 system: base-devel gcc-multilib git gnupg flex bison gperf sdl wxgtk squashfs-tools curl ncurses zlib schedtool perl-switch zip unzip libxslt libxml2 lzo lzop python2 lib32-zlib lib32-ncurses lib32-readline

Install the following packages on an x86 systems: base-devel gcc git gnupg flex bison gperf sdl wxgtk squashfs-tools curl ncurses zlib schedtool perl-switch zip unzip libxslt libxml2 lzo lzop python2

The android source code expects "python" to link to "python2". Create a symlink to /usr/bin/python2 and add that to $PATH. Or you can use virtualenv. Install the python-virtualenvwrapper [https://wiki.archlinux.org/index.php/Python_VirtualEnv] and configure it.
<pre>sudo pacman -S python-virtualenvwrapper
source /usr/bin/virtualenvwrapper.h
mkvirtualenv -p `which python2` python2
workon python2</pre>

You will also need jdk7.

To install jdk7, you can use the package "jdk7-openjdk"

To install repo, you can use the package "repo" from the AUR: https://aur.archlinux.org/packages/repo/

== Mac OS X 10.9(10) Mavericks(Yosemite) ==

http://forum.xda-developers.com/showthread.php?t=2510898

'''XCode'''

XCode is roughly a 4 GB download from the AppStore. Once it is downloaded, it will start an installation process, where it will download more software and install XCode on your system. Depending on your hardware, and your internet speeds, this could take a long time.

Apple XCode 5 for OS X 10.9 Mavericks
https://developer.apple.com/xcode/

Or just search for "XCode" in the App Store

Once XCode is downloaded and installed, you can pretty much forget about it. Just don't uninstall it.


'''Java'''

Java for OS X 2013-005
http://support.apple.com/kb/DL1572?viewlocale=en_US



'''Android SDK'''

Android SDK
https://developer.android.com/sdk/index.html?hl=sk#mac-bundle

Extract the contents of the Android SDK download archive to a new folder and name it android-sdk
Create a new folder in your HOME directory ( ~/ ) named android [your home directory can be found by opening Finder, and clicking on your username in the column to the left]
Move the android-sdk folder INTO the android folder you just made in your Home directory ( it will be ~/android/android-sdk )
Using Finder, navigate to the android/android-sdk/tools folder.
Double-click the "android" file and go through the installer for Android SDK


'''Homebrew'''

Code:
ruby -e "$(curl -fsSL https://raw.github.com/mxcl/homebrew/go/install)"
This will begin the download and installation of Brew.

Depending on your hardware and internet connection, this could take a bit.

Now, we need to run a few commands through Brew, just to make sure everything is installed correctly. Enter the following into the Terminal:
Code:
brew outdated && brew update && brew upgrade && brew doctor
After running brew doctor, you should receive a message saying the follow: Your system is ready to brew.

Now, we can install the packages required to build Android.


'''Required Packages For Compiling Android'''

Enter the following command into the Terminal:
Code:
brew install git coreutils findutils gnu-sed gnupg pngcrush python
This WILL take a while.


'''Repo'''

Open Terminal and enter the following code:

mkdir -p ~/bin

PATH=~/bin:$PATH

curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo

chmod a+x ~/bin/repo


'''Creating A Case-Sensitive Volume'''

We need to create a CASE-SENSITIVE image for our development. Android cannot be build on case-insensitive images, so we need to make one.

Enter the following into the Terminal.
Code:
hdiutil create -type SPARSE -fs "Case-sensitive Journaled HFS+" -size 60g -volname "android" -attach ~/Desktop/Android
I have it set to be 60 GB here, but you can increase or decrease the size to whatever you choose, simply change the "60" to any number of GB you want it to be. I generally use 100 GB.

Once the command is done, you will see a new .img on your desktop, called android.sparseimage. This is the volume you just created that will store your source. To mount it, you just simply double-click it.


'''Setting Up bash_profile'''

Enter the following into Terminal:
Code:
~/.bash_profile
Now copy / paste this into the terminal, so it's in the bash_profile you're creating:
Code:
export PATH=~/bin:$PATH
export PATH=~/android/android-sdk/sdk/platform-tools:$PATH
export PATH=/usr/local/bin:$PATH
export BUILD_MAC_SDK_EXPERIMENTAL=1
export LC_CTYPE=C
export LANG=C
Save it by pressing Ctrl + X , then Ctrl + Y

Once back at the command line in Terminal, enter the following:
Code:
source ~/.bash_profile


'''Necessary cherry-picks for OS X compatibility'''

Here is a list of commits, organized alphabetically by repository, that you will need to cherry-pick in order to ensure the best compatibility for building on OS X:

If you come across other commits related to building on OS X that I have not listed, PLEASE respond to the thread and mention me. I'll get them added!

build
https://github.com/CyanogenMod/android_build/commit/e04d4ddad4790a5f67d96873890cdc8230f0e18a

openssl / sha1sum errors?
https://github.com/CyanogenMod/android_build/commit/18c1d6d96df97b975b87a2736446c9dfd3ab4169

readink -f errors?
https://github.com/omnirom/android_build/commit/27e819cd6b6c44cbb86a0dc2bd3d735ad5dc09e7

sed/gsed errors that is NOT "sed: RE error: illegal byte sequence"?
https://github.com/omnirom/android_build/commit/24b9c1bfe07d24f7e2a425d9d5aae52fd30f3819

errors with the zip creation?
https://github.com/omnirom/android_build/commit/08c61654feff40eeec04eef40f4970408de1e229

JNI errors in /external/chromium_org ?
external_chromium_org
https://github.com/CyanogenMod/android_external_chromium_org/commit/5130af630390487b37d99941887883647c67f37a

That's it. Refer to your individual ROM source for how to sync the manifests and get builds going. Happy building!

==Get the Omni code==

~/android/omni will be our build directory.

  mkdir -p ~/bin
  mkdir -p ~/android/omni

  <nowiki>curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo</nowiki>
  chmod a+x ~/bin/repo

Add bin to PATH

  echo "export PATH=~/bin:$PATH" >> ~/.bashrc

Configure git, if you haven't already:

  git config --global user.email "your@email.address"
  git config --global user.name "Your Name"

Move to build directory and initialize the repo manifest:

  cd ~/android/omni
  <nowiki>repo init -u https://github.com/omnirom/android.git -b android-6.0</nowiki>

(If the repo command is still not available, exit the terminal and start a new one so that your new PATH is registered. Or use source ~./bashrc)

Before you sync the source code, consider customizing which git repositories will download by using local manifests. See the [[#Reducing Download Size|Reducing Download Size]] section for more.

Sync the source code:
  repo sync -j4 -f --no-clone-bundle

Let's configure ccache too. It will reduce the build time to 40% after first build

  echo "export USE_CCACHE=1" >> ~/.bashrc
  ~/android/omni/prebuilts/misc/linux-x86/ccache/ccache -M 25G

25G means it will use upto 25 gb of disk space for ccaching. At least 10 gb is recommended. But if you want to compile for more devices, use more space for ccache.

=== Reducing Download Size ===
 <nowiki>/*TODO: Change this into more of a "Customizing which repos get downloaded section".
Add instructions and information concerning roomservice.xml.
See: http://jira.omnirom.org/browse/OMNI-1263</nowiki>

If you go through the manifest, you may notice that numerous repos may not be required for your specific needs. For eg. qcom repos for non-qcom devices and darwin repos on linux.
To reduce download size, we can tell repo tool to not download them for us.

Learn to add repos to local manifest - http://forum.xda-developers.com/showthread.php?t=2329228

It has a detailed guide on how to reduce in the first post. Many probably useless repos are listed in 2nd post. (Tip 1)

Here's what a typical cleanup manifest might look like:

 <nowiki><?xml version="1.0" encoding="UTF-8"?>
<manifest>

  <remove-project name="device/generic/mips"/>
  <remove-project name="device/generic/mini-emulator-mips"/>
  <remove-project name="device/generic/mini-emulator-arm64"/>

  <remove-project name="device/google/accessory/arduino"/>
  <remove-project name="device/google/accessory/demokit"/>

  <remove-project name="platform/prebuilts/eclipse"/>

  <remove-project name="platform/prebuilts/clang/darwin-x86/host/3.6"/>

  <remove-project name="platform/prebuilts/gcc/darwin-x86/host/headers"/>
  <remove-project name="platform/prebuilts/gcc/darwin-x86/host/i686-apple-darwin-4.2.1"/>
  <remove-project name="platform/prebuilts/gcc/darwin-x86/mips/mips64el-linux-android-4.9"/>
  <remove-project name="platform/prebuilts/gcc/darwin-x86/x86/x86_64-linux-android-4.9"/>

  <remove-project name="platform/prebuilts/python/darwin-x86/2.7.5"/>
  <remove-project name="platform/prebuilts/python/linux-x86/2.7.5"/>

</manifest></nowiki>
