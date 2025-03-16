**Visitor** is a behavioral design pattern that lets you separate algorithms from the objects on which they operate.

The **Visitor Design Pattern** is a **behavioral pattern** that allows you to add new operations to a set of objects **without changing their structure or classes**. It achieves this by separating the operation (visitor) from the object structure it operates on.

---
## **Key Concepts**

1. **Visitor**:
    
    - Defines an interface with a `visit` method for each type of element in the structure.
    - Encapsulates operations to perform on elements of the structure.
2. **Element**:
    
    - Represents an object in the structure that can accept a visitor.
    - Implements the `accept` method, allowing a visitor to operate on it.
3. **Object Structure**:
    
    - A collection of elements (e.g., a list, tree, or graph).
    - The visitor traverses these elements to perform operations.

---

## **When to Use the Visitor Pattern**

- When you need to perform multiple unrelated operations on an object structure.
- When the object structure rarely changes, but new operations are frequently added.
- Example: Abstract syntax trees in compilers, file systems, or UI components.

---

## **Implementation in Python**

Here’s an example of a simple **Visitor Design Pattern** for a **shapes drawing program**.

### **Code Example**

```python
from abc import ABC, abstractmethod

# Visitor Interface
class Visitor(ABC):
    @abstractmethod
    def visit_circle(self, circle):
        pass

    @abstractmethod
    def visit_rectangle(self, rectangle):
        pass


# Concrete Visitor
class AreaCalculator(Visitor):
    def visit_circle(self, circle):
        area = 3.14159 * (circle.radius ** 2)
        print(f"Circle Area: {area}")

    def visit_rectangle(self, rectangle):
        area = rectangle.width * rectangle.height
        print(f"Rectangle Area: {area}")


class PerimeterCalculator(Visitor):
    def visit_circle(self, circle):
        perimeter = 2 * 3.14159 * circle.radius
        print(f"Circle Perimeter: {perimeter}")

    def visit_rectangle(self, rectangle):
        perimeter = 2 * (rectangle.width + rectangle.height)
        print(f"Rectangle Perimeter: {perimeter}")


# Element Interface
class Shape(ABC):
    @abstractmethod
    def accept(self, visitor):
        pass


# Concrete Elements
class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def accept(self, visitor):
        visitor.visit_circle(self)


class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def accept(self, visitor):
        visitor.visit_rectangle(self)


# Object Structure
shapes = [
    Circle(5),
    Rectangle(4, 7)
]

# Using Visitors
area_calculator = AreaCalculator()
perimeter_calculator = PerimeterCalculator()

print("Calculating Areas:")
for shape in shapes:
    shape.accept(area_calculator)

print("\nCalculating Perimeters:")
for shape in shapes:
    shape.accept(perimeter_calculator)
```

---

### **Output**

```
Calculating Areas:
Circle Area: 78.53975
Rectangle Area: 28

Calculating Perimeters:
Circle Perimeter: 31.4159
Rectangle Perimeter: 22
```

---

## **How It Works**

1. **Element Classes** (`Circle`, `Rectangle`) implement the `accept` method, which allows a visitor to process them.
2. **Concrete Visitor Classes** (`AreaCalculator`, `PerimeterCalculator`) implement specific operations for each element type.
3. The `shapes` list acts as the **object structure**, containing elements for the visitor to traverse.

---


| Pros                                                                                                                                                                                                                                                     | Cons                                                                                                                           |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| _Open/Closed Principle_. You can introduce a new behavior that can work with objects of different classes without changing these classes.                                                                                                                | You need to update all visitors each time a class gets added to or removed from the element hierarchy.                         |
| _Single Responsibility Principle_. You can move multiple versions of the same behavior into the same class.                                                                                                                                              | Visitors might lack the necessary access to the private fields and methods of the elements that they’re supposed to work with. |
| A visitor object can accumulate some useful information while working with various objects. This might be handy when you want to traverse some complex object structure, such as an object tree, and apply the visitor to each object of this structure. |                                                                                                                                |

---

## Relations with Other Patterns

- You can treat [[Visitor Pattern]] as a powerful version of the [[Command Pattern]] Its objects can execute operations over various objects of different classes.
    
- You can use [[Visitor Pattern]] to execute an operation over an entire [[Composite Pattern]] tree.
    
- You can use [[Visitor Pattern]] along with [[Iterator Pattern]] to traverse a complex data structure and execute some operation over its elements, even if they all have different classes.