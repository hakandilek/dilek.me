---
layout:     post
title:      Getting started with Ionic Framework
date:
summary:    Introduction to Ionic Framework
categories: ionic hybrid mobile
---

- npm ver: 1.3.10
- node ver: v0.10.25


 Install Ionic Framework via `npm`
 ---

On Linux:
```bash
sudo npm install -g ionic
```

On Windows:
```bash
npm install -g ionic
```

Install Cordova CLI
---

On Linux:
```bash
sudo npm install -g cordova
```

On Windows:
```cmd
npm install -g cordova
```
Create a seed project:
---

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
