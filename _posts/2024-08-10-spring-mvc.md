---
layout: post
title: Introduction to Spring MVC - A Comprehensive Overview
categories: [Spring, Java]
---

- [What is Spring MVC?](#what-is-spring-mvc-)
- [Key Components of Spring MVC](#key-components-of-spring-mvc)
    * [1. DispatcherServlet](#1-dispatcherservlet)
    * [2. Controllers](#2-controllers)
    * [3. Model](#3-model)
    * [4. View](#4-view)
    * [5. ViewResolver](#5-viewresolver)
- [How Does Spring MVC Work?](#how-does-spring-mvc-work-)
- [Example Spring MVC Application](#example-spring-mvc-application)
    * [Step 1: Controller](#step-1--controller)
    * [Step 2: View (Thymeleaf)](#step-2--view--thymeleaf-)
    * [Step 3: Configuration](#step-3--configuration)
- [Conclusion](#conclusion)

**Spring MVC (Model-View-Controller)** is a web framework that is part of the **Spring Framework**. It simplifies the development of web applications by providing a robust framework for handling web requests and responses, processing data, and rendering views. This article will provide a detailed introduction to Spring MVC, its components, and how it works.

## What is Spring MVC?

Spring MVC is based on the **Model-View-Controller (MVC)** design pattern, which separates the application into three main components:

- **Model**: Represents the data or the state of the application.
- **View**: Displays the data to the user (typically as HTML pages).
- **Controller**: Handles the incoming requests, processes data, and returns a response in the form of a view or other format.

This separation of concerns makes the application easier to maintain and test by keeping the business logic separate from the presentation layer.

## Key Components of Spring MVC

### 1. DispatcherServlet

At the heart of Spring MVC is the **DispatcherServlet**. It is the front controller that receives all incoming HTTP requests and dispatches them to the appropriate handler based on the URL pattern.

- **DispatcherServlet** handles:
  - Routing of requests to controllers.
  - Resolving views (e.g., HTML pages or JSON responses).
  - Handling exceptions.
  
It acts as a centralized point for request processing, delegating tasks to other components in the framework.

### 2. Controllers

**Controllers** in Spring MVC handle the requests from users, process them, and return the appropriate response. Controllers are annotated with the `@Controller` annotation.

Example of a simple Spring MVC controller:

```java
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
@RequestMapping("/greet")
public class GreetingController {

    @GetMapping
    @ResponseBody
    public String greet() {
        return "Hello, Welcome to Spring MVC!";
    }
}
```

In this example:
- The `@Controller` annotation indicates that the class is a Spring MVC controller.
- The `@RequestMapping` annotation maps HTTP requests to handler methods.
- The `@ResponseBody` annotation ensures the returned value is written directly to the HTTP response body (in this case, as plain text).

### 3. Model

In Spring MVC, the **Model** is used to pass data from the controller to the view. It typically contains the business data that the view will display to the user.

The `Model` interface in Spring is used to encapsulate the data:

```java
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class HomeController {

    @GetMapping("/home")
    public String home(Model model) {
        model.addAttribute("message", "Welcome to the Spring MVC application!");
        return "home";
    }
}
```

In this example:
- The `model.addAttribute` method adds a key-value pair to the model that can be accessed in the view.
- The method returns the logical name of the view (`home`), which will be resolved by the view resolver.

### 4. View

The **View** in Spring MVC is responsible for rendering the response. Views can be in various formats such as HTML, JSON, XML, etc. The view name returned by the controller is resolved by the **ViewResolver** into an actual view.

Here is an example of an HTML view using Thymeleaf:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Home</title>
</head>
<body>
    <h1 th:text="${message}"></h1>
</body>
</html>
```

In this view:
- The `${message}` expression will be replaced by the value of the `message` attribute in the model, which was passed by the controller.

### 5. ViewResolver

The **ViewResolver** is responsible for mapping the view name returned by the controller to the actual view implementation. Spring MVC provides several built-in view resolvers such as **InternalResourceViewResolver** for JSP views or **ThymeleafViewResolver** for Thymeleaf views.

For example, a simple configuration of a `ViewResolver` for JSP views would look like this:

```java
@Bean
public InternalResourceViewResolver viewResolver() {
    InternalResourceViewResolver resolver = new InternalResourceViewResolver();
    resolver.setPrefix("/WEB-INF/views/");
    resolver.setSuffix(".jsp");
    return resolver;
}
```

This configuration resolves view names to JSP files located in the `/WEB-INF/views/` directory.

## How Does Spring MVC Work?

The typical flow of a Spring MVC application can be broken down into the following steps:

1. **Client Request**: A client sends an HTTP request (e.g., accessing a URL in the browser).
2. **DispatcherServlet**: The **DispatcherServlet** intercepts the request and looks for the appropriate handler (controller).
3. **Controller**: The **Controller** processes the request, performs business logic, and prepares the data (model) for the view.
4. **ViewResolver**: The **ViewResolver** resolves the logical view name returned by the controller to a physical view (e.g., an HTML page).
5. **View Rendering**: The view (e.g., JSP, Thymeleaf) is rendered and sent back to the client as an HTTP response.

## Example Spring MVC Application

Let’s build a simple example where we display a list of products using Spring MVC.

### Step 1: Controller

```java
@Controller
public class ProductController {

    @GetMapping("/products")
    public String getProducts(Model model) {
        List<String> products = Arrays.asList("Laptop", "Smartphone", "Tablet");
        model.addAttribute("products", products);
        return "productList";
    }
}
```

### Step 2: View (Thymeleaf)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Product List</title>
</head>
<body>
    <h1>Product List</h1>
    <ul>
        <li th:each="product : ${products}" th:text="${product}"></li>
    </ul>
</body>
</html>
```

### Step 3: Configuration

In a Spring Boot application, this would be automatically configured, but in traditional Spring MVC applications, you would define a `DispatcherServlet` and configure the `ViewResolver`.

For example:

```java
@Bean
public InternalResourceViewResolver viewResolver() {
    InternalResourceViewResolver resolver = new InternalResourceViewResolver();
    resolver.setPrefix("/WEB-INF/views/");
    resolver.setSuffix(".jsp");
    return resolver;
}
```

## Conclusion

Spring MVC is a powerful framework for building web applications in Java. By adopting the **Model-View-Controller (MVC)** pattern, it separates concerns, making it easier to manage, test, and maintain applications. Key components like **DispatcherServlet**, **Controllers**, **Model**, **View**, and **ViewResolver** make it a complete solution for handling web requests, processing data, and rendering responses.

If you're looking to build scalable and maintainable web applications in Java, **Spring MVC** is an excellent choice. Its robust features and integration with other Spring modules make it one of the most popular web frameworks in the Java ecosystem.
