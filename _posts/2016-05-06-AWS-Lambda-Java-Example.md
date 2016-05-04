---
layout:     post
title:      AWS Lambda Java Example
date:       2016-05-05 18:00:00
summary:    A simple Java Example for AWS Lambda
categories: Java AWS Lambda
---

Please checkout the [Previous post for the gradle setup]({{ site.url }}/gradle/aws/lambda/2016/05/04/AWS-Lambda-Project-with-Gradle/)

Define Java classes under `project-dir/src/main/java/example/`

## Hello.java

```java

package example;

import com.amazonaws.services.lambda.runtime.Context;
import com.amazonaws.services.lambda.runtime.RequestHandler;

public class Hello implements RequestHandler<HelloRequest, HelloResponse> {

	@Override
	public HelloResponse handleRequest(HelloRequest input, Context context) {
		return new HelloResponse(input.getInput());
	}
	
}


```

## HelloRequest.java

```java

package example;

public class HelloRequest {

	private String input;

	public HelloRequest(String input) {
		this.input = input;
	}

	public HelloRequest() {
	}

	public String getInput() {
		return input;
	}

	public void setInput(String input) {
		this.input = input;
	}
}

```

## HelloResponse.java

```java

package example;

public class HelloResponse {

	private String hello;

	public HelloResponse(String hello) {
		this.hello = hello;
	}

	public HelloResponse() {
	}

	public String getHello() {
		return hello;
	}

	public void setHello(String hello) {
		this.hello = hello;
	}
	
}

```

Use the following gradle command to generate your standalone .jar deployment file:

```bash
./gradlew shadowJar
```

This will generate the .jar file with all dependencies under `build/libs`.
Let's say this has generated the file `build/libs/hello-sample-all.jar`.


Create an IAM Role using [AWS IAM Console](https://console.aws.amazon.com/iam/home?region=eu-central-1#roles)

 * Role Name : `hello-sample`
 * AWS Service Roles : `AWS Lambda` [Select]
 * Policy: `AdministratorAccess` [Select]
 Copy `Role ARN` 
 
 Use AWS-CLI to upload your function
 
 ```bash
 aws lambda create-function \
   --region eu-central-1 \
   --function-name hello-world-in-java \
   --zip-file fileb://build/libs/hello-sample-all.jar --role ROLE-ARN-HERE \
   --handler example.Hello \
   --runtime java8 \
   --timeout 15 \
   --memory-size 512
 ```
 
 Test your Function in [AWS Lambda Console](https://eu-central-1.console.aws.amazon.com/lambda/home?region=eu-central-1#/functions/hello-world-in-java?tab=code)
 
 Click *Test* button and change the JSON content with the following:
 
 ```
 
{
  "input": "World!"
}

 ```
 
 Click *Save and Test* button. You'll see the execution result:
 
 ![Successful Result]({{ site.url }}/assets/Screenshot-2016-05-04.png)
