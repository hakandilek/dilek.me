---
layout:     post
title:      Hello World with GraalVM Native Image
date:       2019-05-23 23:00:00
summary:    An introduction to GraalVM Native Image
categories: Java GraalVM native-image benchmark
---

## Prerequisites

* [GraalVM is installed](https://github.com/oracle/graal/releases) and <GraalVM>/bin directory is in the `$PATH`
* [Native Image](https://www.graalvm.org/docs/reference-manual/aot-compilation/) is installed using the command `gu install native-image`
* Clone the [graalvm-playground repository](https://github.com/hakandilek/graalvm-playground)

## Run in the VM

* For convenience first run the example in the local JVM:

   ```shell
    $ cd graalvm-playground/01hello-world 
    $ ./gradlew clean jar && \
      time java -jar build/libs/01hello-world.jar

    BUILD SUCCESSFUL in 0s
    3 actionable tasks: 3 executed
    Hello World!
    java -jar build/libs/01hello-world.jar  0,08s user 0,03s system 139% cpu 0,083 total
    $
    ```

## Build Native Image

* Make sure that you have the right JVM version (Currently most recent supported version is JDK8-u212):

  ```shell
  $ javac -version
  javac 1.8.0_212
  ```

* Build and run native image

  ```shell
    $ ./gradlew clean jar && \
      native-image -jar build/libs/01hello-world.jar && \
      time ./01hello-world

    BUILD SUCCESSFUL in 0s
    3 actionable tasks: 3 executed
    Build on Server(pid: 4674, port: 34081)
    [01hello-world:4674]    classlist:     172.74 ms
    [01hello-world:4674]        (cap):     955.19 ms
    [01hello-world:4674]        setup:   1,690.68 ms
    [01hello-world:4674]   (typeflow):   2,260.10 ms
    [01hello-world:4674]    (objects):     770.75 ms
    [01hello-world:4674]   (features):     147.15 ms
    [01hello-world:4674]     analysis:   3,250.30 ms
    [01hello-world:4674]     (clinit):      78.32 ms
    [01hello-world:4674]     universe:     262.43 ms
    [01hello-world:4674]      (parse):     313.86 ms
    [01hello-world:4674]     (inline):     913.91 ms
    [01hello-world:4674]    (compile):   2,593.18 ms
    [01hello-world:4674]      compile:   4,097.51 ms
    [01hello-world:4674]        image:     390.85 ms
    [01hello-world:4674]        write:      89.51 ms
    [01hello-world:4674]      [total]:  10,045.79 ms
    Hello World!
    ./01hello-world  0,00s user 0,00s system 87% cpu 0,002 total
  ```

## Benchmark results

JVM Call **(0,083s)** vs Native Image **(0,002)**: quiet an improvement!

