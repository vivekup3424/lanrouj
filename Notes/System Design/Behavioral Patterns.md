Behavioral patterns focus on communication and responsibility between objects.

#### **Key Patterns:**

1. **[[Strategy Pattern]]**
    
    - Defines a family of algorithms, encapsulates each one, and makes them interchangeable.
    - **Use Case:** Sorting algorithms, payment strategies (credit card, PayPal).
2. **[[Observer Pattern]]**
    
    - Defines a one-to-many dependency so that when one object changes state, its dependents are notified.
    - **Use Case:** Event listeners, UI updates.
3. **Command**
    
    - Encapsulates a request as an object, allowing parameterization and queuing of requests.
    - **Use Case:** Undo/redo functionality.
4. **Mediator**
    
    - Centralizes communication between multiple objects.
    - **Use Case:** Chat applications where a central hub mediates messages.
5. **Chain of Responsibility**
    
    - Passes requests along a chain of handlers until one handles it.
    - **Use Case:** Logging frameworks, where each log level is handled by a specific handler.
6. **Template Method**
    
    - Defines the skeleton of an algorithm in a base class but lets subclasses override specific steps.
    - **Use Case:** Standardize algorithms while allowing customization.
7. **State**
    
    - Allows an object to change its behavior when its internal state changes.
    - **Use Case:** Workflow systems or finite state machines.
8. **Visitor**
    
    - Separates an algorithm from the object structure it operates on.
    - **Use Case:** Processing different elements in a data structure (e.g., a syntax tree).
9. **Interpreter**
    
    - Implements a specialized language for a particular problem.
    - **Use Case:** Parsing expressions or commands.

---
