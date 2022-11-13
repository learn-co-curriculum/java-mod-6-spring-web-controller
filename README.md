# Controller Class

## Learning Goals

- Create a controller class.
- Accept different request parameters.

## Introduction

The **controller** is where we will define which methods a client request is
routed to and what should be sent back as a response. Spring provides several
annotations in the `org.springframework.web.bind.annotation` package to make it
easy to manage requests, responses, and client parameters.

## Add the Controller Class

In the previous lesson, we created a class called `LunchController.java`. Open up
the Java file in IntelliJ and add the following code:

```java
package com.example.springwebdemo.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class LunchController {

  @GetMapping("/")
  //localhost:8080/
  public String index() {
    return "Welcome to Spring Boot!";
  }
}
```

Now let's run this application and see what happens! Remember, to run the
application, navigate back to the default class. In this case, the default class
 is `SpringWebDemoApplication`. Click the green play button next to the `main`
method.

The console should pop up and show something that looks like this:

![spring-application-started](https://curriculum-content.s3.amazonaws.com/spring-mod-1/controller/spring-boot-application-console.png)

Notice that, unlike the last time we ran our default class, it does not just start
and then immediately finish executing. It's still running!

Open a browser and type in "http://localhost:8080/" into the URL. This is where
our Spring application should be running. "localhost" is the standard hostname
that a machine gives itself and "8080" is the default port that Tomcat started on.
We can see the default port actually in the console log when we start up our
Spring Boot application. When the browser loads the web page, we should see this:

![welcome-index](https://curriculum-content.s3.amazonaws.com/spring-mod-1/controller/welcome-to-spring-boot.PNG)

It's the same message we return in the `index()` method within the
`LunchController`! So what exactly happened?

Let's look at the annotations we used!

### @RestController

The `@RestController` combines the following annotations:

- `@Controller`: Indicates to Spring that the class represents a controller.
- `@ResponseBody`: Configures Spring to return a JSON response from the controller
  methods instead of view templates, which is the default.

### @GetMapping

The `@GetMapping` is a shorthand for the
`@RequestMapping(value="/", method=RequestMethod.GET)` annotation. Both
of these annotations define the endpoint path as `/`, or the root path.

The controller class handles the client requests and responses. So, the client
sent the request by navigating to the specified route (i.e., "localhost:8080/").
The controller class then finds the corresponding method based off of the route,
in our case, `/`, which is mapped to the method `index()`. The `index()` method
will then return "Welcome to Spring Boot!" back as a response, which then is
shown in the browser.

## Request Parameters

Now that we understand how the controller class works, let's add a couple of more
methods given the requirements:

- Greet the customer.
- Tell the customer the daily lunch special.
- Thank the customer for coming into our cafeteria.

In this lesson, we will focus on the first and last requirements. We will
address the second requirement in the next lesson.

Let's first look at how to greet the customer.

Add the following method to the `LunchController`:

```java
    @GetMapping("/greet")
    //localhost:8080/greet?name=Ted
    public String greet(@RequestParam(defaultValue = "customer") String name) {
        return String.format("Greetings %s!", name);
    }
```

In the method above, notice how we define the route to "/greet". This means, to
have the web application call this method, we'll need to navigate to
"http://localhost:8080/greet".

Also notice how our method takes a parameter this time. If we have a method that
takes in a parameter, we can use the `@RequestParam` annotation. The
`@RequestParam` annotation indicates that a method parameter should be bound to
the web request as a parameter. In this case, the parameter is called `name`. If
we want to provide a name to the request, we can use the HTTP request:
"http://localhost:8080/greet?name=Ted"; this would then return a `String` with a
value of "Greetings Ted!". If we do not specify a name, then we can provide a
default value. In the example above, we specify the `defaultValue` to "customer".

Let's try running the application again, and this time, we'll open the browser to
"http://localhost:8080/greet":

![param-with-default-value](https://curriculum-content.s3.amazonaws.com/spring-mod-1/controller/greetings-customer.png)

Notice we did not specify the parameter `name` in the URL, so it returns the
default value of "customer".

Now let's specify the parameter. With the application still running, go to:
"http://localhost:8080/greet?name=Ted":

![param-with-name](https://curriculum-content.s3.amazonaws.com/spring-mod-1/controller/greetings-ted.png)

The `@RequestParam` takes in some other optional elements as well. See the
Spring documentation
[RequestParam Annotation](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/bind/annotation/RequestParam.html)
for more information.

### Your Turn

Try to add another method on your own now using the annotations we have learned
about! Create a method called `thank()` and have it take in a `String name` as a
parameter and return a `String` that says "Thanks [name]! Have a great day!".

When you run the application and view it in the browser, it should look something
like this:

![thank-customer](https://curriculum-content.s3.amazonaws.com/spring-mod-1/controller/thanks-ted.png)

## Conclusion

We have learned how to create the controller class, map routes to methods, and
get information from client requests.

## References

- [RestController Annotation](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/bind/annotation/RestController.html)
- [GetMapping Annotation](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/bind/annotation/GetMapping.html)
- [RequestParam Annotation](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/bind/annotation/RequestParam.html)
