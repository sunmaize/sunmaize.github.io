---
layout: post
title: Understanding Pass by Value and Pass by Reference - Why Java is Pass by Value
categories: [Java]
---

In programming, one of the most common points of confusion is the difference between **pass by value** and **pass by reference**. Understanding these concepts is important for mastering how variables are passed to methods. Java, in particular, is often mistakenly thought to pass objects by reference, but this is incorrect—**Java is pass by value**.

In this article, we'll explore the differences between the two, explain why Java is pass by value, and illustrate the concepts with code examples.

## What is Pass by Value?

In **pass by value**, the actual value of the variable is copied and passed into the method. This means that any changes made to the variable within the method do not affect the original variable outside the method.

### Example of Pass by Value

Here is a simple example in Java:

```java
public class PassByValueExample {
    public static void main(String[] args) {
        int x = 5;
        changeValue(x);
        System.out.println("Value of x after method call: " + x); // Output: 5
    }

    public static void changeValue(int num) {
        num = 10;
    }
}
```

In this example, we pass `x` to the `changeValue` method, where `num` becomes a copy of `x`. Even though we change `num` to 10 inside the method, it has no effect on the original value of `x` in the `main()` method. The output is still `5` because **Java passes a copy of the variable's value, not the variable itself**.

## What is Pass by Reference?

In **pass by reference**, a reference to the actual variable is passed to the method. This means any changes made to the variable inside the method will reflect on the original variable outside the method, because both refer to the same memory location.

However, **Java does not use pass by reference** for either primitive types or objects. This is where confusion often arises.

## How Java Handles Object Passing: Pass by Value for Object References

In Java, objects are not passed by reference. Instead, **the reference to the object** is passed by value. This means that while you can modify the object that the reference points to, you cannot change the reference itself to point to a different object.

Let’s take a look at an example:

```java
public class ObjectPassByValueExample {
    public static void main(String[] args) {
        Person person = new Person("Alice");
        changePerson(person);
        System.out.println("Person's name after method call: " + person.getName()); // Output: Bob
    }

    public static void changePerson(Person p) {
        p.setName("Bob");
    }
}

class Person {
    private String name;

    public Person(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

In this example, we create a `Person` object with the name "Alice" and pass it to the `changePerson` method. The method changes the name to "Bob". Since the **object's reference** was passed by value, the method can modify the contents of the object, but it cannot change the reference to point to a new object.

Here’s a modified version of the previous example to demonstrate that the reference itself cannot be changed:

```java
public class ObjectPassByValueExample {
    public static void main(String[] args) {
        Person person = new Person("Alice");
        changeReference(person);
        System.out.println("Person's name after method call: " + person.getName()); // Output: Alice
    }

    public static void changeReference(Person p) {
        p = new Person("Charlie");  // This creates a new object but does not affect the original reference
    }
}
```

In this case, we attempt to reassign `p` to a new `Person` object with the name "Charlie" inside the `changeReference` method. However, the original `person` object outside the method remains unchanged, with its name still set to "Alice". This proves that Java does not pass objects by reference, but instead passes the **reference by value**.

## Why Java is Pass by Value

In Java, **everything is pass by value**, including object references. The key point to understand is:

- For **primitive types** (like `int`, `float`, `boolean`), the actual value is copied and passed to the method. Therefore, changes made to the parameter inside the method have no effect on the original variable.
- For **objects**, the reference (memory address) of the object is passed by value. This means that the method gets a copy of the reference. The object itself can be modified, but reassigning the reference in the method does not affect the original reference outside the method.

### Analogy: Copying an Address

Think of it this way: if you write someone's home address on a piece of paper and give a copy of the paper to someone else, they can visit the house (modify the object), but they cannot change the original piece of paper to point to a different address (reassign the reference). This is essentially how Java handles object references.

## Key Takeaways

- **Primitive types**: Java passes the actual value. Changes inside the method do not affect the original variable.
- **Objects**: Java passes a copy of the object’s reference. The object can be modified inside the method, but the reference itself cannot be reassigned.
- **Java is always pass by value**, even for object references.

Understanding this concept is essential for debugging and reasoning about how data is manipulated inside methods in Java. By keeping in mind that Java uses pass by value, you can avoid common pitfalls when working with methods and objects.

## Conclusion

Java’s behavior of passing everything by value is sometimes a source of confusion, especially for those coming from languages that support pass by reference. However, once you understand that object references are passed by value, and that reassigning references inside methods does not affect the original objects, it becomes easier to predict how Java will behave in various situations.

Mastering this distinction can help you write clearer, more predictable code and better manage data manipulation inside your Java programs.