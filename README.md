# pgs4a
NOTE: Unchanged from the version forked from startgridsrc, assume all first-person references to that user

An evolution of the deprecated Pygame Subset for Android. It's an easy way to port your Pygame to your mobile devices!
Pgs4a was made by Tom Rothamel, Patrick Dawson and others, using Kivy's *python-for-android* packager to make Pygame games run on android.
He developed pgs4a until 2013 until he moved on with his other projects.
Meanwhile, I made a couple of edits to pgs4a for it to work nicely in the constantly evolving android environment.

# Changelog

### 0.9.6 (last release by Tom)
* This release patches Python to work with .apk files distributed through the Amazon App Store, which are subtly different from standard apk files.
* This release fixes support for pre-2.3 Android devices

### 0.9.7 (my changes)
* immersive full screen mode (api 19+)
* removed all permissions (storage, wakelock)
* two-finger multitouch implementation
* target SDK of project can be configured by user
* added full keyboard and mouse (api 21+) support
* autobackup via google, for specified files (api 23+)
* resizeable activity (api 24+)
* adaptive icon (api 26+)
* additional 64-bit libraries
* can build APKs that run on devices up to API 31 (android 12), although no app bundles are created

The shared libraries in the *libs* folder are built by the [rapt](https://github.com/startgridsrc/rapt) toolchain. This toolchain actually builds an entire pgs4a distribution, like this repository, but it's not as well maintained as this one. Only the shared libraries (.so files) are simply copied into this (better maintained) repository. 

# Instructions
1. Clone this repository (using git, or download it as zip and extract it somewhere)
1. Install java JDK version 8 (it's an old version, but versions higher than 8 don't work well with this project)
1. Go into the folder where you'll find the file *android.py* and some other files and folders. Create a new folder here for your own game, with all your game files in it. From now on, this folder will be refered as *yourproject* in the instructions below.
1. Open a terminal there (right click / in Windows hold shift then right click to open a shell/prompt).
1. Run `python ./android.py installsdk`. This will download and extract the android SDK and Ant, to build an .APK of your game later. You will be prompted to agree with the terms and conditions of the SDK packages, requiring you to press *yes* or '*y*' many times. If a download fails, you may need to edit URLs manually in */buildlib/installsdk.py*. When everything is downloaded and unpacked, the script will help you creating a random key (in case you haven't a key already). A key is required to sign your APK later.
1. Run `python ./android.py configure yourproject`, where you replace *yourproject* with the name of your own project folder. A json file will be added to your game folder, containing several properties of your app, for example the name and version.
1. Connect your phone to your PC via USB. Make sure USB debugging is enabled (see developer options on your phone) as well as USB file transfer.
1. Run `python ./android.py build yourproject release`. An APK should be created and installed on your phone. It will run your app immediately, in theory!
1. If the app installs, but crashes immediately, use *adb logcat* to find out why. Navigate to *android-sdk/platform-tools* and run `./adb logcat`. Open your app, and when it crashes, press *Ctrl + C* to stop logging, and look for errors. For example, your project folder has to contain a file called *main.py*, so you may have to rename one of your files to that, and try again. Or you may want to change *java.target* to 1.7 in the file *\android-sdk\tools\ant\build.xml* to avoid javac warnings/errors.

The original instructions can be found [here](https://github.com/startgridsrc/rapt/blob/master/doc/android-packaging.rst).
These are the original instructions which are old but detailed, and most of it is probably still fine. You'll find handy info on using the android module in Python, for example to make your game handle the back button, and detect app switching (so you know when to call your savegame function).

# License
The Pygame Subset for Android is licensed under the GNU Lesser General Public License. To the best of our knowledge, Pygame, SDL, and all other dependences are licensed under compatible licenses.

The Pygame Subset for Android is by:

Tom Rothamel

Patrick Dawson

It integrates code from an number of projects, including:

* [Python-for-android](https://github.com/kivy/python-for-android)
* [Pygame](https://www.pygame.org/news)
* [SDL (including Pelya's Android port)](https://github.com/pelya/commandergenius)
* [Python](https://www.python.org/)
* [Jtar](https://github.com/kamranzafar/jtar)
* Jinja2
* Colorama
