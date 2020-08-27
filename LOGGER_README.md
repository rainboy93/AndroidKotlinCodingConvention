# Module Logger - ViettelPay App

This guide shows how to user Module Logger in ViettelPay App

## Table of content
- [Setup logger module](#setup-logger-module)
- [Usage](#usage)
## Setup logger module
- Add this line of code at ```onCreate()``` in ```BankPlusApp.java```
```java
Logger.init(this);
```
With this setup, Logger only allow log with logcat
- In order to customize Logger, use this method:
```java
Logger.init(new LoggerConfig.Builder(this)
            .dir(new File(getExternalFilesDir(null), "ViettelPay"))
            .minLevel(LoggerConst.Level.V)
            .defaultTag("ViettelPay")
            .logOnScreen(true)
            .logToServer(true)
            .logToFile(true)
            .build());
```
- ```dir()``` specified file directory, default directory: ```File(context.getExternalFilesDir(null), "logger").absolutePath```
This default directory is inside package of our app in device and cant be read by other app and will be deleted when app is uninstall
- ```minLevel()``` specified min level of log, default value is: ```LoggerConst.Level.V``` all level includes:
```java
	LoggerConst.Level.V //0
	LoggerConst.Level.D //1
	LoggerConst.Level.I //2
	LoggerConst.Level.W //3
	LoggerConst.Level.E //4
```
- ```defaultTag()``` specified default tag of all logs, default value is appname; 
- ```logToFile()``` is flag to enable/disable log to file.
 This feature requires WRITE_EXTERNAL_STORAGE permission so make sure this permission is granted
- ```logOnScreen()``` is flag to ennable/disable log on screen.
This feature does not work without 2 things
 1. App permission allows draw overlay, if not use this code to request:
 ```kotlin
 if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M && !Settings.canDrawOverlays(this)) {
            val intent = Intent(
                Settings.ACTION_MANAGE_OVERLAY_PERMISSION,
                Uri.parse("package:$packageName")
            )
            startActivityForResult(intent, 1200)
        }
 ```
 2. If permission is granted, use this code to trigger OnScreen Log feature:
 ```kotlin
 if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M && Settings.canDrawOverlays(this)) {
                val intent = Intent(this, LogHeadService::class.java)
                startService(intent)
            } 
 ```
 OnScreenDialog will showup to display log of ViettelPay App and all App on device still can navigate normallly
- ```logToServer()``` is not developed yet

## Usage
- When all setup is done, the Usage is extremely easy
```java
Logger.v("This is log verbose");
Logger.v("Tag", "This is log verbose with tag");
Logger.d("This is log debug");
Logger.d("Tag", "This is log debug with tag");
Logger.i("This is log info");
Logger.i("Tag", "This is log info with tag");
Logger.w("This is log warning");
Logger.w("Tag", "This is log warning with tag");
Logger.e("This is log error");
Logger.e("Tag", "This is log error with tag");
```
- Module also supports log error with specified exception:
```java
Logger.e(new RuntimeException("this is dummy exception"));
Logger.e("This is log error with exception", new RuntimeException("this is dummy exception"));
```
- By default, all log with Logger will be showup at Logcat of Android Studio. 
To be stored in file or displayed on screen or send to server(not available yet), please just follow the setup guide and it'll be fine!
- To capture screen, image will be save at sub folder named ```captures``` of ```logger``` folder :
```kotlin
Logger.capture(activity)
```
- In order to enable/disable logger for release
```kotlin
Logger.setEnable(isEnable) //if isEnable = true it means turn on and vice versa 
```
