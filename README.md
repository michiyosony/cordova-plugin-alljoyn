cordova-plugin-alljoyn
======================

iOS | Windows | Android
--- | --- | ---
[![Build Status](https://travis-ci.org/AllJoyn-Cordova/cordova-plugin-alljoyn.svg?branch=master)](https://travis-ci.org/AllJoyn-Cordova/cordova-plugin-alljoyn) | [![Build status](https://ci.appveyor.com/api/projects/status/1sb4akgk195q8ch8/branch/master?svg=true)](https://ci.appveyor.com/project/AllJoyn-Cordova/cordova-plugin-alljoyn/branch/master) | [![Circle CI](https://circleci.com/gh/AllJoyn-Cordova/cordova-plugin-alljoyn/tree/master.svg?style=svg)](https://circleci.com/gh/AllJoyn-Cordova/cordova-plugin-alljoyn/tree/master)

A Cordova plugin to expose the [AllJoyn](https://allseenalliance.org/alljoyn-framework-tutorial) Thin Client (AJTCL 14.12) to cross platform applications written in Javascript.

Purpose
-------

To provide a plugin which allows using the AllJoyn Thin Client library across all mobile platforms without requiring the user to deal with implementing and compiling the native code for each operating system.

Current Platforms:
* iOS
* Windows Modern App
* Windows Phone
* Android (in-progress)

An effort has been made to expose as many of the AJTCL features to Javascript as possible, while maintaining a clean Javascript API.  Features are prioritized based on which scenarios they unblock.  

Resources
---------

Various explanatory blog posts can be found here:
http://www.stefangordon.com/introducing-the-alljoyn-plugin-for-cordova/

For Plugin Developers / Contributors
--------------------
After cloning this repository, a plugin developer needs to get AJTCL by running these commands in the project root folder:

```
$ git clone https://github.com/AllJoyn-Cordova/ajtcl.git src/ajtcl
```

For plugin users, above is taken care of by a hook run after plugin is added with Cordova scripts.

Using The Plugin On Windows
---------------------------

```
$ cd /path/to/your/cordova/app
$ cordova add [/path/to/plugin or <url to this git repo> or org.allseen.alljoyn]
$ cordova platform add windows
```

Running With Cordova Scripts:

```
// To run on Windows Phone 8.1 emulator
$ cordova run windows --emulator --archs="x86" -- -phone
// Running on Windows Phone 8.1 device
$ cordova run windows --device --archs="arm" -- -phone
// To run on desktop (current default is Windows 8.0 build)
$ cordova run windows --device --archs="x64" -- -win
```

Alternative for running with Cordova scripts is to open the solution file generated after "cordova platform add windows"-command in Visual Studio and running the wanted app project. In this case, these is a need to manually select the correct architecture from build configuration.

Building For Android
--------------------

In addition to the Android SDK, the NDK is required. See https://developer.android.com/tools/sdk/ndk/index.html for installation instructions.

The environment variables ANDROID_HOME and ANDROID_NDK_HOME must be set to the point to the locations where the Android SDK and NDK are installed.

There are some external dependencies when building the plugin for the Android platform. When building on a Mac, one of the easiest ways to install the dependencies is via Homebrew http://brew.sh/ with following command:

```
$ brew install ant gradle swig
```

After dependencies are met, the steps to build and run are something like:

```
$ cordova platform add android
$ cordova build android
$ cordova run android
```

Running Tests
-------------

The tests can be run locally with:

```
$ npm install
$ npm test
```

An AllJoyn router must be accessible in the network in which the target device runs for the tests to pass.

The target platform will be selected automatically based on which platform the tests are run. On Mac, an iOS build is made. On Windows, the Cordova universal Windows platform is used and on Linux, the build will be targeting Android. To switch the target, one needs to edit the variable  cordovaPlatformMapping at the top of file tests/run.js.

To run tests on Windows, first ensure that fresh enough Cordova script is found from the path. You can look at appveyor.yml file from the root of this repository how this is done in the CI environment. You can use where command to check which cordova is found first from your path:

```
$ where cordova
```

If you only want to verify that the build is working via Cordova scripts, you can run:

```
$ npm run build-only
```
