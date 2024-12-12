> **Objects of a parents should be replaceable with objects of a childrens without affecting the correctness of the program.**

This means that if class `B` is a child of class `A`, then objects of class `A` should be replaceable with objects of class `B` without introducing errors or altering the behavior of the program.
Since all the methods and variables of *Parents* are also used or declared in the *Child*

---

### **Why is LSP Important?**

- It ensures **reliability** in inheritance hierarchies.
- It promotes **correct use of polymorphism**.
- Violating LSP leads to fragile code where subclasses break the expectations of their superclasses.

---

### **How to Adhere to LSP?**

1. Subclasses must fulfill all expectations of the superclass.
2. Subclasses must not violate any contracts (implicit or explicit) established by the superclass.
3. *Avoid overriding methods in a way that changes their original behavior inconsistently.*

---

### **Example 1: Violating LSP**

Consider a program modeling shapes:

```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

class Square(Rectangle):
    def __init__(self, side):
        super().__init__(side, side)

    def area(self):
        return self.width * self.height
```

Here, `Square` inherits from `Rectangle`, but this violates LSP. Why? Because:

- A `Square` behaves differently from a `Rectangle` in real life.
- If a function expects a `Rectangle`, substituting it with a `Square` may produce unexpected results.

#### **Problem in Practice**

```python
def print_area(rectangle):
    print(f"Area: {rectangle.area()}")

rect = Rectangle(10, 20)
sq = Square(10)

print_area(rect)  # Output: Area: 200
print_area(sq)    # Output: Area: 100 (seems fine here)

# If you later allow setting dimensions, this will fail:
rect.width = 15
print_area(rect)  # Output: Area: 300

sq.width = 15     # Violates Square's invariant
print_area(sq)    # Output: Area: 225 (wrong for a square!)
```

The `Square` class breaks the expectations of the `Rectangle` class because squares enforce additional constraints (equal width and height), which `Rectangle` does not.

---

### **Example 2: Fixing LSP**

To adhere to LSP, separate the behavior of `Rectangle` and `Square`:

```python
class Shape:
    def area(self):
        raise NotImplementedError("This method should be overridden in subclasses.")

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

class Square(Shape):
    def __init__(self, side):
        self.side = side

    def area(self):
        return self.side * self.side
```

Now, both `Rectangle` and `Square` inherit from a common base class, `Shape`, but they do not share constraints or behavior that would violate LSP.

#### **Usage**

```python
def print_area(shape):
    print(f"Area: {shape.area()}")

rect = Rectangle(10, 20)
sq = Square(10)

print_area(rect)  # Output: Area: 200
print_area(sq)    # Output: Area: 100
```

In this design:

- `Rectangle` and `Square` are independent implementations of `Shape`.
- Substituting `Rectangle` with `Square` (or vice versa) does not violate expectations.

---

### **Key Points**

- **Use abstraction wisely:** Ensure subclasses fulfill the contracts defined by their superclass.
- **Avoid oversharing behavior:** If subclasses require fundamentally different logic, use a common interface or base class instead of inheritance.
- **Design for substitution:** Think about how the base class will be used and ensure that all derived classes meet those expectations.

---

### **Example 3: Practical LSP with Python Interfaces**

You can use Python's `abc` module to define contracts explicitly:

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

class Square(Shape):
    def __init__(self, side):
        self.side = side

    def area(self):
        return self.side * self.side
```

By explicitly requiring all shapes to implement `area`, you enforce a consistent contract while avoiding the pitfalls of improper inheritance.

---

### **Conclusion**

The **Liskov Substitution Principle** ensures that derived classes can stand in for their base classes without breaking the program. Adhering to LSP involves thoughtful use of inheritance, abstraction, and design to create robust, maintainable systems.