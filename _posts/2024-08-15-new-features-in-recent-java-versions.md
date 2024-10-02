---
layout: post
title: New Features in Recent Java Versions
categories: [Java]
---

Java has gone through many changes since its inception, with regular updates introducing new features, performance improvements, and enhancements for developers. In this article, we’ll look at the most significant new features from Java 8 to the latest version, Java 21, highlighting how these features improve the language and make it more efficient and developer-friendly.

## 1. Java 8 (March 2014)

Java 8 was a major release, introducing several groundbreaking features that shaped modern Java development.

### Key Features:

### 1.1 Lambdas and Functional Programming

Java 8 introduced **lambda expressions**, which allow for more concise code when working with functional interfaces (interfaces with a single abstract method).

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
names.forEach(name -> System.out.println(name));
```

### 1.2 Streams API

The **Streams API** allows for functional-style operations on collections of data, such as filtering, mapping, and reducing.

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
names.stream()
    .filter(name -> name.startsWith("A"))
    .forEach(System.out::println);
```

### 1.3 Default Methods in Interfaces

Interfaces can now include **default methods**, which provide implementations for methods directly in the interface.

```java
public interface Vehicle {
    default void start() {
        System.out.println("Vehicle is starting.");
    }
}
```

### 1.4 Optional Class

The **Optional** class was introduced to handle null values more gracefully, avoiding `NullPointerExceptions`.

```java
Optional<String> name = Optional.ofNullable(null);
name.ifPresent(System.out::println);  // Will not print anything
```

### 1.5 Date and Time API

Java 8 introduced a new **Date and Time API** (java.time package) to replace the outdated `Date` and `Calendar` classes.

```java
LocalDate date = LocalDate.now();
System.out.println(date);
```

---

## 2. Java 9 (September 2017)

Java 9 introduced a series of significant changes, including modularity and improvements to the JDK.

### Key Features:

### 2.1 Project Jigsaw (Module System)

The **Java Platform Module System** (JPMS) allows developers to modularize their applications, improving security, maintainability, and performance.

```java
module com.example.myapp {
    requires java.base;
}
```

### 2.2 JShell (Interactive REPL)

Java 9 introduced **JShell**, an interactive Read-Eval-Print Loop (REPL) that allows developers to run Java code snippets without needing to write an entire class or method.

```shell
jshell> System.out.println("Hello, JShell!");
Hello, JShell!
```

### 2.3 Factory Methods for Collections

Java 9 added **factory methods** for creating immutable collections in a simpler way.

```java
List<String> names = List.of("Alice", "Bob", "Charlie");
```

---

## 3. Java 10 (March 2018)

Java 10 brought small but useful improvements to the language, focusing on developer productivity.

### Key Features:

### 3.1 Local Variable Type Inference (`var`)

The `var` keyword introduced **type inference** for local variables, allowing the compiler to infer the type based on the context.

```java
var names = List.of("Alice", "Bob", "Charlie");
```

This feature reduces boilerplate code and improves readability while maintaining type safety.

---

## 4. Java 11 (September 2018)

Java 11 is a Long-Term Support (LTS) release that brought several important improvements, especially for cloud-native and microservice development.

### Key Features:

### 4.1 HTTP Client API

The **new HTTP Client API** replaces the legacy `HttpURLConnection` class, providing a more modern and flexible way to send HTTP requests.

```java
HttpClient client = HttpClient.newHttpClient();
HttpRequest request = HttpRequest.newBuilder()
    .uri(URI.create("https://example.com"))
    .build();
client.sendAsync(request, HttpResponse.BodyHandlers.ofString())
      .thenApply(HttpResponse::body)
      .thenAccept(System.out::println);
```

### 4.2 New String Methods

Java 11 introduced helpful new methods for working with strings, such as `strip()`, `isBlank()`, and `lines()`.

```java
String text = " Hello World ";
System.out.println(text.strip());  // "Hello World"
System.out.println(text.isBlank());  // false
```

### 4.3 Running Java Files without `javac`

You can now run Java source files directly without compiling them manually with `javac`.

```bash
java HelloWorld.java
```

---

## 5. Java 12 (March 2019)

Java 12 continued to introduce smaller enhancements focused on improving language usability and performance.

### Key Features:

### 5.1 Switch Expressions (Preview)

Switch expressions simplify switch-case statements by returning values and eliminating fall-through behavior.

```java
String day = "MONDAY";
String result = switch (day) {
    case "MONDAY", "TUESDAY", "WEDNESDAY" -> "Weekday";
    case "THURSDAY", "FRIDAY" -> "Almost weekend";
    case "SATURDAY", "SUNDAY" -> "Weekend";
    default -> "Unknown";
};
```

---

## 6. Java 13 (September 2019)

Java 13 focused on refining existing features and providing new productivity tools.

### Key Features:

### 6.1 Text Blocks (Preview)

Text blocks allow you to write multi-line strings in a more readable and concise way.

```java
String json = """
    {
      "name": "Alice",
      "age": 25
    }
    """;
```

---

## 7. Java 14 (March 2020)

Java 14 continued to refine features introduced in earlier versions, with some exciting new additions.

### Key Features:

### 7.1 Pattern Matching for `instanceof` (Preview)

This feature simplifies type checks by eliminating the need for explicit casting after an `instanceof` check.

```java
if (obj instanceof String s) {
    System.out.println(s.length());
}
```

### 7.2 Records (Preview)

**Records** provide a simple way to declare classes that are primarily used to hold data.

```java
public record Person(String name, int age) {}
```

---

## 8. Java 15 (September 2020)

Java 15 introduced several refinements and made some preview features permanent.

### Key Features:

### 8.1 Sealed Classes (Preview)

**Sealed classes** restrict which classes can extend or implement them, providing better control over inheritance hierarchies.

```java
public abstract sealed class Shape
    permits Circle, Square, Rectangle {}
```

---

## 9. Java 16 (March 2021)

Java 16 added final touches to many features introduced earlier and enhanced the development experience.

### Key Features:

### 9.1 Records (Permanent)

Records became a permanent feature, offering concise data carriers without the boilerplate code.

### 9.2 Pattern Matching for `instanceof` (Permanent)

The pattern matching feature for `instanceof` is now officially part of the language.

---

## 10. Java 17 (September 2021)

Java 17 is another Long-Term Support (LTS) release, with several major enhancements.

### Key Features:

### 10.1 Sealed Classes (Permanent)

Sealed classes became a permanent feature, providing better control over class hierarchies.

### 10.2 Pattern Matching for Switch (Preview)

Switch expressions now support pattern matching, further simplifying code involving conditional logic.

```java
Object obj = "Hello";
switch (obj) {
    case String s -> System.out.println(s.length());
    case Integer i -> System.out.println(i + 10);
    default -> System.out.println("Unknown type");
}
```

---

## 11. Java 21 (September 2023)

Java 21 is the latest Long-Term Support (LTS) release, introducing exciting new features aimed at enhancing developer experience and performance.

### Key Features:

### 11.1 Record Patterns (Preview)

Record patterns allow you to destructure records directly in patterns, making it easier to access fields without manual extraction.

```java
record Person(String name, int age) {}

void printPerson(Person person) {
    switch (person) {
        case Person(String name, int age) -> 
            System.out.println("Name: " + name + ", Age: " + age);
    }
}
```

### 11.2 Virtual Threads (Preview)

Virtual threads simplify multithreading in Java, allowing you to create lightweight threads that are managed by the Java Virtual Machine (JVM) rather than the operating system.

```java
Thread.ofVirtual().start(() -> {
    // Your task here
});
```

### 11.3 Scoped Values (Preview)

Scoped values provide a way to store data that is automatically scoped to a specific context, allowing for better control over data visibility.

```java
ScopedValue<String> value = ScopedValue.newValue();
```

### 11.4 Enhanced Switch Patterns (Preview)

This feature extends switch statements to include the ability to match on types and destructure complex data structures, making code more concise and readable.

```java
switch (object) {
    case String s -> System.out.println("It's a string: " + s);
    case Integer i -> System.out.println("It's an integer: " + i

);
    // Other cases...
}
```

---

## Conclusion

The evolution of Java has been marked by significant improvements in syntax, performance, and developer productivity. With each version, Java continues to adapt to modern programming needs, making it a powerful choice for building robust applications. Whether you're starting a new project or maintaining an existing one, familiarizing yourself with these new features will help you leverage the full potential of the Java programming language.