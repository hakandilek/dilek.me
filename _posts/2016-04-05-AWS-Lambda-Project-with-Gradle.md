---
layout:     post
title:      AWS Lambda Project with Gradle
date:       2016-04-05 18:00:00
summary:    Creating an AWS Lambda Project with Gradle
categories: Gradle AWS Lambda
---

In project directory initialize `build.gradle` file and gradle Wrapper:

```bash
$ gradle init
```

Edit generated `build.gradle` file

```gradle
buildscript {
  repositories { jcenter() }
  dependencies {
    //Gradle shadow plugin
    classpath 'com.github.jengelman.gradle.plugins:shadow:1.2.3'
  }
}

apply plugin: 'java'
apply plugin: 'com.github.johnrengelman.shadow'

repositories { jcenter() }
dependencies {
    //AWS Lambda core library
    compile 'com.amazonaws:aws-lambda-java-core:1.1.0'
}
```

Create a simple Java class under `project-dir/src/main/java/example/Hello.java`
```java
package example;

public class Hello {
  
}
```

Use the following gradle command to generate your standalone .jar deployment file:
```bash
./gradlew shadowJar
```
This will generate the .jar file with all dependencies under `build/libs` folder which can be uploaded to AWS Lambda.
