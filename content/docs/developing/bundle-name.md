+++
title = "Bundle Names"
description = "Development variables."
date = 2021-05-01T08:00:00+00:00
updated = 2021-05-01T08:00:00+00:00
draft = false
weight = 10
sort_by = "weight"
template = "docs/page.html"
publish = true

[extra]
lead = "Configuring development variables."
toc = true
top = false
+++

## Networking permissions

[https://docs.flutter.dev/development/data-and-backend/networking#platform-notes](https://docs.flutter.dev/development/data-and-backend/networking#platform-notes)

## Rename app

```bash
flutter pub global activate rename
flutter pub global run rename setAppName --value "medicamina"
flutter pub global rename setBundleId --targets ios --value "us.medicamina.ios"
flutter pub global rename setBundleId --targets android --value "us.medicamina.android"
flutter clean
flutter pub get
```

## iOS

##### ios/Runner/info.plist

```xml
	<key>CFBundleDisplayName</key>
	<string>medicamina</string>
	<key>CFBundleName</key>
	<string>medicamina</string>
```

## macOS

This is broken?

##### macos/Podfile

```C
post_install do |installer|
  installer.pods_project.targets.each do |target|
    flutter_additional_macos_build_settings(target)
    target.build_configurations.each do |config|
      config.build_settings['MACOSX_DEPLOYMENT_TARGET'] = '10.15'
    end
  end
end
```

```bash
flutter clean
flutter pub get
cd ./macos && pod install
```

## android

##### android/app/src/main/AndroidManifest.xml

```xml
<manifest ...> 
  <uses-permission android:name="android.permission.INTERNET"/>
  <application ... />
</mainfest>
```