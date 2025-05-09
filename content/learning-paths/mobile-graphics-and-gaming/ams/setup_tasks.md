---
# User change
title: "Setup tasks"

weight: 3 # 1 is first, 2 is second, etc.

# Do not modify these elements
layout: "learningpathall"
---
## Installation

1. Install Arm Performance Studio by following the instructions in the [Arm Performance Studio install guide](/install-guides/ams). Details about changes since the last release can be found in the [Release Note](https://developer.arm.com/documentation/107649/latest/).
1. Ensure you have installed [Android Debug Bridge (adb)](https://developer.android.com/studio/command-line/adb). `adb` is available with the Android SDK platform tools, which are installed as part of Android Studio. Alternatively, you can download them separately as part of the Android SDK platform tools.
1. Performance Advisor uses a Python script to connect to your device. To run this script, you will need [Python](https://www.python.org/downloads/) 3.8 or later installed.

## Update your PATH environment variable (Linux and macOS)

Edit your `PATH` environment variable to add the paths to the Streamline and Mali Offline Compiler executables. This is so that you can run Streamline's `Streamline-cli -pa` command and Mali Offline Compiler's `malioc` command from any directory. This step is not necessary on Windows, as this is done automatically when Arm Performance Studio is installed.

On macOS, edit your `/etc/paths` file to add the following paths:

```
/<installation_directory>/streamline
/<installation_directory>/mali_offline_compiler
```

On Linux, edit your `PATH` environment variable to add the paths to the Performance Advisor executable. Add this command to the `.bashrc` file in your home directory, so that this environment variable is set whenever you initialize a shell session.

 ```
 PATH=$PATH:/<installation_directory>/streamline
 PATH=$PATH:/<installation_directory>/mali_offline_compiler
```

## Build your application

The application must be compiled with debug enabled, as well as additional options to facilitate call stack unwinding by Streamline.

* To set [Unity](https://unity.com/) applications to be debuggable, enable [Development Build](https://docs.unity3d.com/6000.0/Documentation/Manual/android-BuildProcess.html) in `Build settings`.
* In Android Studio, use a build variant that includes `debuggable true` (`isDebuggable = true` in Kotlin scripts) in the build configuration.
* In Unreal Engine, open `Project Settings > Project > Packaging > Project`, and ensure that the `For Distribution` checkbox is not set.
* For C++ or Java applications, refer to the [Target setup guide for Android](https://developer.arm.com/documentation/101813/latest/Target-Setup/Compile-your-application) for instructions on how to compile your application with the right options.

{{% notice Tip %}}
To assist with readability and add context, you can optionally include [annotations](https://developer.arm.com/documentation/101816/latest/Annotate-your-code/Add-annotations-to-your-code) in your code, which are then displayed in Streamline.
{{% /notice %}}

## Set up the Android device

1. On the device, ensure that [Developer Mode](https://developer.android.com/studio/debug/dev-options) is enabled.
1. Enable `USB Debugging` under `Settings > Developer options`. If your device asks you to authorize connection to your computer, confirm the connection.
1. Connect the device to the host through USB and approve the debug connection on the device when prompted.
1. To test the connection, run the `adb devices` command in a command terminal. If successful, this returns the ID of your device:

    ```command
    adb devices
    List of devices attached
    ce12345abcdf1a1234       device
    ```

    If you see that the device is listed as `unauthorized`, try disabling and re-enabling `USB Debugging` on the device, and accept the authorization prompt to enable connection to the computer.

1. Install the [debuggable](https://developer.android.com/studio/debug) application on the device.
