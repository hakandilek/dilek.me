---
layout:     post
title:      Spring boot with GraalVM Native Image
date:       2019-06-30 21:00:00
summary:    Building a Spring Boot project with GraalVM Native Images
categories: GraalVM spring boot
---

## Prerequisites

* [GraalVM is installed](https://github.com/oracle/graal/releases) and `<GraalVM>/bin` directory is in the `$PATH`
* [Native Image](https://www.graalvm.org/docs/reference-manual/aot-compilation/) is installed using the command `gu install native-image`
* Clone the [graalvm-playground repository](https://github.com/hakandilek/graalvm-playground)

## Run in the VM

* For convenience first run the example in the local JVM:

   ```shell
    $ cd graalvm-playground/spring-web
    $./gradlew clean bootJar && \
      time java -jar build/libs/spring-web-0.0.1-SNAPSHOT.jar

    BUILD SUCCESSFUL in 1s
    4 actionable tasks: 4 executed

      .   ____          _            __ _ _
    /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
    ( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
    \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
      '  |____| .__|_| |_|_| |_\__, | / / / /
    =========|_|==============|___/=/_/_/_/
    :: Spring Boot ::        (v2.1.5.RELEASE)

    2019-05-23 23:19:27.344  INFO 27401 --- [           main] me.dilek.graalvm.demo.DemoApplication    : Starting DemoApplication on l380 with PID 27401 (/home/XXX/graalvm-playground/spring-web/build/libs/spring-web-0.0.1-SNAPSHOT.jar started by XXX in /home/XXX/graalvm-playground/spring-web)
    2019-05-23 23:19:27.347  INFO 27401 --- [           main] me.dilek.graalvm.demo.DemoApplication    : No active profile set, falling back to default profiles: default
    2019-05-23 23:19:28.456  INFO 27401 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8081 (http)
    2019-05-23 23:19:28.493  INFO 27401 --- [           main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
    2019-05-23 23:19:28.493  INFO 27401 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet engine: [Apache Tomcat/9.0.19]
    2019-05-23 23:19:28.592  INFO 27401 --- [           main] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
    2019-05-23 23:19:28.593  INFO 27401 --- [           main] o.s.web.context.ContextLoader            : Root WebApplicationContext: initialization completed in 1197 ms
    2019-05-23 23:19:28.925  INFO 27401 --- [           main] o.s.s.concurrent.ThreadPoolTaskExecutor  : Initializing ExecutorService 'applicationTaskExecutor'
    2019-05-23 23:19:29.169  INFO 27401 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8081 (http) with context path ''
    2019-05-23 23:19:29.171  INFO 27401 --- [           main] me.dilek.graalvm.demo.DemoApplication    : Started DemoApplication in 2.194 seconds (JVM running for 2.633)

    ```

## Build Native Image

* Make sure that you have the right JVM version (Currently most recent supported version is JDK8-u212):

  ```shell
  $ javac -version
  javac 1.8.0_212
  ```

* Try to build the native image

  ```shell
    $ ./gradlew clean bootJar && \
      native-image -jar build/libs/spring-web-0.0.1-SNAPSHOT.jar

    BUILD SUCCESSFUL in 0s
    4 actionable tasks: 4 executed
    Build on Server(pid: 4674, port: 34081)
    [spring-web-0.0.1-SNAPSHOT:4674]    classlist:     265.01 ms
    [spring-web-0.0.1-SNAPSHOT:4674]        (cap):     919.46 ms
    [spring-web-0.0.1-SNAPSHOT:4674]        setup:   1,221.87 ms
    [spring-web-0.0.1-SNAPSHOT:4674]     analysis:   4,072.66 ms
    Warning: Aborting stand-alone image build. com.oracle.svm.hosted.substitute.DeletedElementException: Unsupported field java.net.URL.handlers is reachable
    To diagnose the issue, you can add the option --report-unsupported-elements-at-runtime. The unsupported element is then reported at run time when it is accessed the first time.
    Detailed message:
    Trace: 
      at parsing java.net.URL.setURLStreamHandlerFactory(URL.java:1118)
    Call path from entry point to java.net.URL.setURLStreamHandlerFactory(URLStreamHandlerFactory): 
      at java.net.URL.setURLStreamHandlerFactory(URL.java:1110)
      at org.springframework.boot.loader.jar.JarFile.resetCachedUrlHandlers(JarFile.java:401)
      at org.springframework.boot.loader.jar.JarFile.registerUrlProtocolHandler(JarFile.java:391)
      at org.springframework.boot.loader.Launcher.launch(Launcher.java:48)
      at org.springframework.boot.loader.JarLauncher.main(JarLauncher.java:51)
      at com.oracle.svm.core.JavaMainWrapper.run(JavaMainWrapper.java:153)
      at com.oracle.svm.core.code.IsolateEnterStub.JavaMainWrapper_run_5087f5482cc9a6abc971913ece43acb471d2631b(generated:0)

    Warning: Use -H:+ReportExceptionStackTraces to print stacktrace of underlying exception
    Build on Server(pid: 4674, port: 34081)
    [spring-web-0.0.1-SNAPSHOT:4674]    classlist:     114.69 ms
    [spring-web-0.0.1-SNAPSHOT:4674]        (cap):     642.22 ms
    [spring-web-0.0.1-SNAPSHOT:4674]        setup:     896.36 ms
    [spring-web-0.0.1-SNAPSHOT:4674]   (typeflow):   1,503.32 ms
    [spring-web-0.0.1-SNAPSHOT:4674]    (objects):     705.94 ms
    [spring-web-0.0.1-SNAPSHOT:4674]   (features):      98.03 ms
    [spring-web-0.0.1-SNAPSHOT:4674]     analysis:   2,358.07 ms
    [spring-web-0.0.1-SNAPSHOT:4674]     (clinit):      64.41 ms
    [spring-web-0.0.1-SNAPSHOT:4674]     universe:     202.79 ms
    [spring-web-0.0.1-SNAPSHOT:4674]      (parse):     205.68 ms
    [spring-web-0.0.1-SNAPSHOT:4674]     (inline):     586.94 ms
    [spring-web-0.0.1-SNAPSHOT:4674]    (compile):   1,422.75 ms
    [spring-web-0.0.1-SNAPSHOT:4674]      compile:   2,394.41 ms
    [spring-web-0.0.1-SNAPSHOT:4674]        image:     245.09 ms
    [spring-web-0.0.1-SNAPSHOT:4674]        write:      56.23 ms
    [spring-web-0.0.1-SNAPSHOT:4674]      [total]:   6,324.13 ms
    Warning: Image 'spring-web-0.0.1-SNAPSHOT' is a fallback image that requires a JDK for execution (use --no-fallback to suppress fallback image generation).
  ```

* Check the resulting image:

  ```shell
    $ ls -ahl
    ...
    -rwxr-xr-x 1 XXX XXX 2,6M Mai 23 23:22 spring-web-0.0.1-SNAPSHOT
    ...
  ```

  The resulting image requires a Java for execution!

* Run the native image

  ```shell
  $ ./spring-web-0.0.1-SNAPSHOT& ps -ef | grep java
    [1] 28883
    XXX    28883  5089  0 23:31 pts/1    00:00:00 /home/XXX/tools/graalvm-ce-19.0.0/jre/bin/java -Dorg.graalvm.nativeimage.kind=fallback-executable -cp /home/XXX/mutfak/graalvm-playground/spring-web/build/libs/spring-web-0.0.1-SNAPSHOT.jar org.springframework.boot.loader.JarLauncher
  ```

## Conclusion

  The resulting image is not a real native image and needs a JRE to run. This is already indicated ruting native image build phase with the message ```Warning: Aborting stand-alone image build. com.oracle.svm.hosted.substitute.DeletedElementException: Unsupported field java.net.URL.handlers is reachable```.

  The reason is, current version of Spring 5.1 does not support GraalVM native images but the upcoming versions with 5.2 and 5.3 will mainly focus on supporting native images as mentioned [here](https://github.com/spring-projects/spring-framework/wiki/GraalVM-native-image-support#support-of-native-images-at-spring-framework-level) and [here](https://github.com/spring-projects/spring-framework/issues/21529#issuecomment-453474115)
