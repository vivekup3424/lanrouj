Roughly what we seek to achieve is for the code for have **high cohesion** and **low coupling**

High Cohesion can be implemented via practicing *[[Single Responsibility Principle]]* and *[[Interface Segregation Principle]]*
Low Coupling can be implemented by practicing *[[Open or Closed Principle]]* and  _[[Dependecy Inversion Principle]]_


## Some more digressed notes
### **Cohesion vs. Coupling**

Cohesion and coupling are two fundamental concepts in software design that describe the relationships between the elements of a system. While they are related, they focus on different aspects of the system’s structure and behavior. Understanding these concepts helps create modular, maintainable, and efficient systems.

---

### **Cohesion**

**Definition:**  
Cohesion refers to how closely related and focused the responsibilities of a single module, class, or component are.

- **High Cohesion:** When the components of a module work together to achieve a single, well-defined purpose.
- **Low Cohesion:** When a module performs multiple, unrelated tasks or has responsibilities that are not closely related.

**Characteristics of High Cohesion:**

1. The module/class has a clear, focused purpose.
2. Methods and properties are strongly related to the primary function of the class.
3. Easier to understand, maintain, and test.

**Example of High Cohesion:**

```python
class Order:
    def calculate_total(self, items):
        return sum(item.price for item in items)

    def add_item(self, item):
        # Logic to add item to the order
        pass

    def remove_item(self, item):
        # Logic to remove item from the order
        pass
```

**Explanation:**  
The `Order` class handles tasks related to managing an order, maintaining a single, focused responsibility.

**Example of Low Cohesion:**

```python
class Utility:
    def send_email(self, email, subject, message):
        pass

    def calculate_total(self, items):
        return sum(item.price for item in items)

    def log_error(self, message):
        pass
```

**Explanation:**  
The `Utility` class has multiple unrelated responsibilities (emailing, calculating, logging), which makes it harder to maintain.

---

### **Coupling**

**Definition:**  
Coupling refers to the degree of dependency between two modules, classes, or components.

- **Low Coupling:** When components are independent of each other or have minimal dependencies.
- **High Coupling:** When components are heavily dependent on each other, requiring changes in one to affect the other.

**Characteristics of Low Coupling:**

1. Modules can function independently.
2. Changes in one module don’t ripple through the system.
3. Easier to test and maintain.

**Example of Low Coupling:**

```python
class PaymentProcessor:
    def process_payment(self, amount):
        print(f"Processing payment of ${amount}")

class Order:
    def __init__(self, payment_processor):
        self.payment_processor = payment_processor

    def complete_order(self, total):
        self.payment_processor.process_payment(total)
```

**Explanation:**  
The `Order` class depends on the `PaymentProcessor` interface but does not tightly couple to its implementation. You can substitute `PaymentProcessor` with a different implementation (e.g., `PayPalProcessor`).

**Example of High Coupling:**

```python
class Order:
    def complete_order(self, total):
        print(f"Processing payment of ${total} using PaymentProcessor")
        # Logic tied to a specific payment implementation
```

**Explanation:**  
The `Order` class is tightly coupled to the logic of payment processing, making it harder to change or extend the payment processing behavior without modifying the `Order` class.

---

### **Key Differences**

|**Aspect**|**Cohesion**|**Coupling**|
|---|---|---|
|**Definition**|How well elements within a module work together.|How dependent a module is on other modules.|
|**Focus**|Internal consistency within a single module.|Relationships between different modules or classes.|
|**Goal**|Achieve high cohesion for modular and focused components.|Aim for low coupling to reduce dependencies and increase flexibility.|
|**Impact of Violation**|Low cohesion leads to harder-to-maintain and understand modules.|High coupling makes systems fragile and hard to change.|
|**Improvement**|Split responsibilities into smaller, focused classes.|Use interfaces, abstractions, or dependency injection.|

---

### **Ideal Design**

- **High Cohesion:** Each module/class focuses on a single, well-defined responsibility.
- **Low Coupling:** Modules/classes interact with each other through well-defined interfaces and minimize dependencies.

---

### **Analogy**

- **Cohesion:** Think of a specialized tool (e.g., a screwdriver). It has a single purpose and does its job well.
- **Coupling:** Think of a chain of gears. If one gear breaks, the entire system can fail due to its interdependencies.

By aiming for **high cohesion** and **low coupling**, you create a robust, modular system that is easier to extend, test, and maintain.