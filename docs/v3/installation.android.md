# Android Installation v3

## Prerequisites

* Android SDK 28+
* Android Studio
* Kotlin

## Step 1. Migrating to AndroidX.

We use Kotlin and AndroidX in the native module.

Android Studio -> Refactor -> Migrate to AndroidX... -> Migrate

[Google Official Doc](https://developer.android.com/jetpack/androidx/migrate)

## Step 2. Link the library.

### Automatic

Use `react-native link` to add the library to your project:

```shell script
react-native link react-native-agora
```

### Manual

Define the `react-native-agora` project in `android/settings.gradle`:

```groovy
...
include ':react-native-agora'
project(':react-native-agora').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-agora/android')
```

Add the `react-native-agora` as a dependency of your app in `android/app/build.gradle`:

```groovy
...
dependencies {
  ...
  implementation project(':react-native-agora')
}
```

Add `import io.agora.rtc.react.RCTAgoraRtcPackage;` and `new RCTAgoraRtcPackage()` in your `MainApplication.java`:

```java
import io.agora.rtc.react.RCTAgoraRtcPackage;
...
    @Override
    protected List<ReactPackage> getPackages() {
        return Arrays.<ReactPackage>asList(
                new MainReactPackage(),
                new RCTAgoraRtcPackage()
        );
    }
```

## Step 3. Add ext Config. (**recommended**)

If you've defined *[project-wide properties](https://developer.android.com/studio/build/gradle-tips.html)* in your root `build.gradle`, this library will detect the presence of the following properties:

```groovy
buildscript {...}
allprojects {...}

/**
 * Project-wide Gradle configuration properties
 */
ext {
    compileSdkVersion = 28
    buildToolsVersion = "28.0.3"
    minSdkVersion = 16
    targetSdkVersion = 28
    kotlin_version = "1.3.72"
}
```
or do
```groovy
buildscript {
    ext {
        compileSdkVersion = 28
        buildToolsVersion = "28.0.3"
        minSdkVersion = 16
        targetSdkVersion = 28
        kotlin_version = "1.3.72"
    }
}
...
```

## Step 4. Add Network Security Config.

Add `android:networkSecurityConfig` to your manifest file (`android/app/src/main/AndroidManifest.xml`):

```xml
<application android:networkSecurityConfig="@xml/network_security_config">
...
</application>
```

[Google Official Doc](https://developer.android.com/training/articles/security-config)
