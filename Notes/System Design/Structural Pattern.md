Structural patterns focus on organizing classes and objects into larger structures, ensuring proper relationships between them.

#### **Key Patterns:**

1. [[Adapter Patterm]]
    
    - Converts an interface of a class into another interface the client expects.
    - **Use Case:** Making incompatible classes work together.
    - **Example (Python):**
        
        ```python
        class EuropeanSocket:
            def voltage(self):
                return 220
        
        class USASocketAdapter:
            def __init__(self, european_socket):
                self.european_socket = european_socket
            
            def voltage(self):
                return self.european_socket.voltage() / 2
        ```
        
2. **Bridge**
    
    - Decouples an abstraction from its implementation so both can evolve independently.
    - **Use Case:** Separating GUI controls from platform-specific rendering.
3. **Composite**
    
    - Treats individual objects and groups of objects uniformly.
    - **Use Case:** Represent hierarchical data like file systems or UI components.
4. **Decorator**
    
    - Adds responsibilities to an object dynamically without altering its structure.
    - **Use Case:** Adding features to objects (e.g., logging, validation).
5. **Facade**
    
    - Provides a simplified interface to a complex subsystem.
    - **Use Case:** Simplify access to libraries or frameworks.
6. **Proxy**
    
    - Acts as a placeholder or intermediary for another object.
    - **Use Case:** Lazy initialization, access control, or logging.
7. **Flyweight**
    
    - Reduces memory usage by sharing common parts of objects.
    - **Use Case:** Large numbers of similar objects (e.g., rendering characters in text editors).

---
