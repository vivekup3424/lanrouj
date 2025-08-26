# Introduction To Object Oriented Programming Paradigm

> Object Oriented Programming (OOP) is a programming paradigm that uses the concept of objects as a way to structure and organize code.

## What is Object Oriented Programming (OOP) 🤔

Object Oriented Programming (OOP) is a programming paradigm that uses the concept of objects as a way to structure and organize code. It is based on the principles of abstraction, encapsulation, inheritance, and polymorphism, which enable developers to build more flexible, reusable, and maintainable software.

Here is a graph illustrating OOP and its four main concepts as branches. Each branch has a brief explanation of the corresponding concept to help visualize their relationships and their importance within the OOP paradigm.
![[Pasted image 20250227130545.png]]

### Abstraction

This principle allows programmers to represent real-world entities as objects in code, hiding their complexity and focusing on the essential features relevant to the problem being solved. By using abstraction, developers can create simplified models of complex systems.

### Encapsulation

Encapsulation is the mechanism of bundling data (attributes) and operations (methods) together within a single unit, called a class. This principle helps to achieve separation of concerns, allowing each object to manage its own state and behavior, and restrict access to its internal data.

Encapsulation means keeping data safe inside the class and controlling access using getters and setters.

```java
class BankAccount {
    private double balance;  // hidden (private)

    // public methods to control access
    public void deposit(double amount) {
        balance += amount;
    }

    public double getBalance() {
        return balance;
    }
}

```

### Inheritance
Inheritance enables the creation of new classes that inherit attributes and methods from existing classes. The new classes, called subclasses, can extend or override the behavior of the parent class (also known as the base or superclass). This promotes code reusability and modularity, as common functionalities can be shared among related classes.

### Polymorphism

Polymorphism allows a single interface to represent different types of objects. This enables objects of different classes to be treated as objects of a common superclass, allowing the same code to work with different data types. Polymorphism simplifies code maintenance and enables developers to create more flexible and extensible systems.