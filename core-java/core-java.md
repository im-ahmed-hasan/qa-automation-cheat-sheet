# Core Java for QA Automation Engineers

PURPOSE: Solid foundation in Java concepts every QA automation engineer must know to write reliable, maintainable automation code.

---

## 1. Basic Java Syntax & Structure

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

- `class` keyword defines a class  
- `main` method is the program entry point  
- Statements end with a semicolon `;`

---

## 2. Object-Oriented Programming (OOP)

### Classes and Objects

```java
public class User {
    private String name;
    private int age;

    public User(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public void greet() {
        System.out.println("Hello, " + name);
    }
}

User user = new User("Ahmed", 30);
user.greet();
```

### Inheritance

```java
class Animal {
    void sound() {
        System.out.println("Some sound");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Bark");
    }
}
```

### Polymorphism

- Method overloading (same method name, different parameters)  
- Method overriding (subclass changes behavior of superclass method)

### Encapsulation

- Use `private` fields with public getters/setters  
- Controls access and improves maintainability

---

## 3. Exception Handling

```java
try {
    int a = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println("Cannot divide by zero");
} finally {
    System.out.println("This always runs");
}
```

- Checked exceptions (require explicit handling)  
- Unchecked exceptions (runtime exceptions)  
- Use specific catch blocks for better debugging

---

## 4. Collections Framework

### List (Ordered, allows duplicates)

```java
List<String> names = new ArrayList<>();
names.add("Ahmed");
names.add("John");
System.out.println(names.get(0)); // Ahmed
```

### Set (Unique elements, unordered)

```java
Set<String> uniqueNames = new HashSet<>();
uniqueNames.add("Ahmed");
uniqueNames.add("Ahmed"); // duplicate ignored
```

### Map (Key-value pairs)

```java
Map<String, Integer> ages = new HashMap<>();
ages.put("Ahmed", 30);
ages.put("John", 25);
System.out.println(ages.get("Ahmed")); // 30
```

---

## 5. Java Streams (Java 8+)

```java
List<String> names = Arrays.asList("Ahmed", "John", "Sara");

names.stream()
    .filter(name -> name.startsWith("A"))
    .forEach(System.out::println); // Ahmed
```

- Stream API enables functional-style operations on collections  
- Common operations: filter, map, reduce, collect

---

## 6. Multithreading Basics

```java
Thread thread = new Thread(() -> System.out.println("Running in separate thread"));
thread.start();
```

- Use `synchronized` to control access to shared resources  
- Use thread pools (`ExecutorService`) to manage multiple threads

---

## 7. Useful Java Utilities for Automation

- `String` methods: `contains()`, `split()`, `replace()`, `trim()`, `equalsIgnoreCase()`  
- `Math` class: `Math.max()`, `Math.min()`, `Math.random()`  
- Date and time API (`java.time` package): `LocalDate`, `LocalDateTime`  
- Wrapper classes: `Integer.parseInt()`, `Boolean.parseBoolean()`

---

## 8. Tips for QA Automation

- Follow Java naming conventions (camelCase for methods/variables, PascalCase for classes)  
- Keep code modular and reusable  
- Avoid hardcoding test data — use constants or external files  
- Handle exceptions gracefully and log useful info  
- Use comments sparingly but clearly  
- Write unit tests for utility methods  
- Learn to debug using IDE features (breakpoints, step execution)

---

Master these Java basics to build strong automation frameworks and solve real-world test challenges efficiently.
