> **A client should not be forced to depend on methods it does not use.**

This means that large, general-purpose interfaces should be divided into smaller, more specific ones. Clients should only need to know about the methods that are relevant to them.

---

### **Why is ISP Important?**

1. **Improves Flexibility:** Small, focused interfaces make the system easier to modify or extend.
2. **Reduces Coupling:** Classes aren’t forced to implement methods they don’t need.
3. **Enhances Readability:** Each interface describes a clear, specific behavior.

---

### **How to Adhere to ISP?**

- **Avoid "fat" interfaces:** Don’t create interfaces or base classes with too many methods.
- **Split responsibilities:** Use multiple, smaller interfaces instead of a single large one.
- **Use composition over inheritance:** When appropriate, combine small interfaces to build more complex behaviors.

---

### **Example 1: Violating ISP**

Consider an interface for animals:

```python
class Animal:
    def fly(self):
        pass

    def swim(self):
        pass

    def run(self):
        pass
```

#### **Problem**

- **Violation of ISP:** Animals like fish don’t need `fly` or `run`, and birds don’t need `swim`. Classes that implement `Animal` are forced to define methods they don't use, leading to irrelevant or dummy implementations.

#### **Concrete Example**

```python
class Fish(Animal):
    def fly(self):
        raise NotImplementedError("Fish can't fly")

    def swim(self):
        print("Fish is swimming")

    def run(self):
        raise NotImplementedError("Fish can't run")
```

---

### **Example 2: Adhering to ISP**

We can refactor the design by splitting the `Animal` interface into smaller, more specific interfaces:

```python
from abc import ABC, abstractmethod

class Swimmable(ABC):
    @abstractmethod
    def swim(self):
        pass

class Flyable(ABC):
    @abstractmethod
    def fly(self):
        pass

class Runnable(ABC):
    @abstractmethod
    def run(self):
        pass
```

Now, each class only implements the behaviors it needs:

```python
class Fish(Swimmable):
    def swim(self):
        print("Fish is swimming")

class Bird(Swimmable, Flyable):
    def swim(self):
        print("Bird is swimming")

    def fly(self):
        print("Bird is flying")

class Dog(Runnable, Swimmable):
    def run(self):
        print("Dog is running")

    def swim(self):
        print("Dog is swimming")
```

---

### **Benefits of Refactoring**

1. **Relevance:** Each class implements only the methods it needs.
2. **Readability:** Interfaces are smaller and more meaningful.
3. **Flexibility:** Adding a new behavior (e.g., climbing) only requires creating a new interface and implementing it for the relevant classes.

---

### **Example 3: Practical ISP in Python**

#### **Without ISP (Single Fat Interface)**

Imagine a system for managing different types of machines in a factory:

```python
class Machine:
    def start(self):
        pass

    def stop(self):
        pass

    def print_document(self):
        pass

    def scan_document(self):
        pass

    def fax_document(self):
        pass
```

#### **Problems:**

- Machines like a scanner don’t need `fax_document` or `print_document`.
- Dummy or redundant implementations are required in classes.

#### **With ISP (Multiple Specific Interfaces)**

Refactor by creating smaller interfaces:

```python
class Startable(ABC):
    @abstractmethod
    def start(self):
        pass

    @abstractmethod
    def stop(self):
        pass

class Printable(ABC):
    @abstractmethod
    def print_document(self, document):
        pass

class Scannable(ABC):
    @abstractmethod
    def scan_document(self):
        pass

class Faxable(ABC):
    @abstractmethod
    def fax_document(self):
        pass
```

Now, only implement relevant behaviors for each machine:

```python
class Printer(Startable, Printable):
    def start(self):
        print("Printer is starting")

    def stop(self):
        print("Printer is stopping")

    def print_document(self, document):
        print(f"Printing: {document}")

class Scanner(Startable, Scannable):
    def start(self):
        print("Scanner is starting")

    def stop(self):
        print("Scanner is stopping")

    def scan_document(self):
        print("Scanning document")

class FaxMachine(Startable, Faxable):
    def start(self):
        print("Fax Machine is starting")

    def stop(self):
        print("Fax Machine is stopping")

    def fax_document(self):
        print("Faxing document")
```

---

### **Advantages of ISP**

1. **Reduces Overhead:** Clients only need to know the methods they care about.
2. **Easier to Maintain:** Smaller interfaces and behaviors are easier to understand and test.
3. **Encourages Composition:** Combine small interfaces to create specific implementations.

---

### **Key Takeaways**

- The **Interface Segregation Principle (ISP)** promotes the creation of focused, small interfaces or base classes.
- Avoid "fat" interfaces that force classes to implement irrelevant methods.
- By adhering to ISP, you create systems that are more modular, maintainable, and extensible.

[[Similarity between ISP and SRP]] - Similarity between Interface Segregation Principle and Single Responsibility Principle
