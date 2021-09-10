# AppCenter-SDK-UE4

This is a fork of the [origin project](https://github.com/PushkinStudio/AppCenter-SDK-UE4).

Development repository for the App Center SDK for Unreal Engine 4 platforms

Only selected features are implemented.

- Analytics (basic integration and events traking)
- Crashes
- Distribute

Platforms: both iOS and Android.

> Force ANSI allocator for iOS build! Just add `GlobalDefinitions.Add("FORCE_ANSI_ALLOCATOR=1");` to `YourProject.Target.cs`
> 
## Quick way to compile breakpad for Android

[Breakpad](https://github.com/google/breakpad) library is required by **appcenter** for native crash reporting.

Pre-requirements

- Android NDK installed and `$NDKROOT` environment variable set.
- Google depot-tools installed and added to `$PATH`

```bash
# fetch source code
mkdir breakpad && cd breakpad
fetch breakpad
# navigate to the sample application
cd src/android/sample_app
# comment out APP_STL that breaks compilation on recent NDKs
sed -ie '/^[^#]/ s/\(^.*APP_STL.*$\)/#\1/' jni/Application.mk
# build
$NDKROOT/ndk-build APP_PLATFORM=android-23
```

The compiled libraries will be available at `breakpad/src/android/sample_app/obj/local/arm64-v8a/libbreakpad_client.a` and `breakpad/src/android/sample_app/obj/local/armeabi-v7a/libbreakpad_client.a`
