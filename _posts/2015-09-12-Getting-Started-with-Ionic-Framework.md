---
layout:     post
title:      Getting started with Ionic Framework
date:       2015-09-12 22:00:00
summary:    Introduction to Ionic Framework
categories: ionic hybrid mobile
---

This guide aims to give a brief introduction for [Ionic Framework](http://ionicframework.com/) for starters.

I would like to thank to [Prof. Akif Eyler](http://mimoza.marmara.edu.tr/~maeyler/) for his patience and contributions in this post.

### Prerequisites

Following tools have to be installed in order to follow this guide.
- [npm](https://www.npmjs.com/) version 2.11.3
- [node](https://nodejs.org) version v0.12.7
- [Android SDK](https://developer.android.com/sdk/index.html) with API version 22

This guide aims to build a mobile app for the Android platform but will also provide instructions for iOS. iOS has another set of tools and SDK for building mobile apps which is not completely covered here.

### Install Ionic Framework via `npm`

[npm](https://www.npmjs.com/) is the pre-installed package manager for the [Node.js](https://en.wikipedia.org/wiki/Node.js) platform.

##### On Linux:
```bash
sudo npm install -g ionic
```

##### On Windows:
```bash
npm install -g ionic
```

### Install Cordova CLI

##### On Linux:
```bash
sudo npm install -g cordova
```

##### On Windows:
```
npm install -g cordova
```
### Create a seed project:

```bash
ionic start ionic-getting-started
```

Answer `n` to the following question indicating that you'll skip ionic.io cloud integration. We want to keep it simple here, right?

```
Create an ionic.io account to send Push Notifications and use the Ionic View app?
(Y/n): n
```
This will create the seed project:

![Ionic seed project]({{ site.url }}/assets/Screenshot-2015-09-09.png)


### Running your app in browser

```bash
ionic serve
```

You'll see it in browser:

![Project running in browser]({{ site.url }}/assets/Screenshot-2015-09-09-2.png)

Adding a target platform
---

##### For Android:
```
ionic platform add android
```

See the [Android Platform Guide](https://cordova.apache.org/docs/en/edge/guide_platforms_android_index.md.html) for full Android installation instructions:

Cordova requires the `ANDROID_HOME` environment variable to be set. This should point to the `[ANDROID_SDK_DIR]\android-sdk` directory. Next, create an environment variable for `JAVA_HOME` environment variable pointing to the root folder where the Java JDK was installed.

See [Ionic installation guide](http://ionicframework.com/docs/guide/installation.html) for further instructions.

##### For iOS:
```
ionic platform add ios
```
Note: iOS development requires OS X currently

Adding Android platform should generate Android source code under `platforms/android` directory, add a resource directory for images and extend existing `config.xml` and `package.json` files.

![New files after adding Android platform]({{ site.url }}/assets/Screenshot-2015-09-12-1.png)

# Running your app on a device
Run your app on a device: ionic run <PLATFORM>

##### For Android:
```
ionic run android
```

##### For iOS:
```
ionic run ios
```

App on Android device:

![Running on Android device]({{ site.url }}/assets/Screenshot-2015-09-12-2.png)

# Building your app

##### For Android:
```
ionic build android
```

This should generate an `android-debug.apk` file under `\platforms\android\build\outputs\apk\` folder.

##### For iOS:
```
ionic build ios
```

# Running your app on an emulator

Simulate your app: ionic emulate <PLATFORM>

##### For Android:
```
ionic emulate android
```

If you are using Genymotion instead of the standard Android emulator, note that Genymotion behaves like a device, so it requires `run` rather than `emulate`

##### For iOS:
```
ionic emulate ios
```

### Packaging your app

You can package your app using Cordova Command :
`cordova build <MODE> <PLATFORM>`

##### For Android debug packaging:
```
cordova build --debug android
```
This will generate the file `\platforms\android\build\outputs\apk\android-debug.apk`

##### For Android release packaging:
```
cordova build --release android
```
This will generate the file `\platforms\android\build\outputs\apk\android-release-unsigned.apk`

You will need to sign this file if you want to publish it in Google Play Store.
See [Ionic publishing instructions](http://ionicframework.com/docs/guide/publishing.html) for further information.
