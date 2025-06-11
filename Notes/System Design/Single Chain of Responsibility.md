---
tags:
  - behavioral-pattern
---
#### **Definition**

The Chain of Responsibility (CoR) is a behavioral design pattern that allows a request to be passed through a sequence (chain) of potential handlers. Each handler in the chain decides whether to process the request or pass it to the next handler.

---

#### **Key Components**

1. **Handler Interface**:
    
    - Declares a method for handling requests.
        
    - Optionally includes a method to set the next handler in the chain.
        
2. **Concrete Handlers**:
    
    - Implement the handler interface.
        
    - Decide whether to process the request or forward it to the next handler.
        
3. **Client**:
    
    - Initiates the request by sending it to the first handler in the chain.
        

---

#### **Flow**

1. A client sends a request to the first handler in the chain.
    
2. Each handler:
    
    - Processes the request if it can.
        
    - Forwards the request to the next handler if it cannot.
        
3. If no handler can process the request, it remains unhandled.
    

---

#### **Single Chain Characteristics**

- In a **single chain**, handlers are linked in a straight line, where each handler has a reference to the next one.
    
- Requests propagate linearly through the chain until one handler processes it or the chain ends.
    

---

#### **Advantages**

1. **Decouples Sender and Receiver**:
    
    - The client doesn’t need to know which handler will process the request.
        
2. **Flexible Chain Composition**:
    
    - Handlers can be easily added, removed, or reordered without affecting the client.
        
3. **Responsibility Delegation**:
    
    - Each handler focuses on processing a specific type of request.
        

---

#### **Disadvantages**

1. **Uncertain Handling**:
    
    - If no handler processes the request, it might remain unhandled.
        
2. **Complex Debugging**:
    
    - Tracing the path of a request through the chain can be challenging.
        

---

#### **Example in Python**

```
from abc import ABC, abstractmethod

# Handler Interface
class Handler(ABC):
    def __init__(self, next_handler=None):
        self.next_handler = next_handler

    @abstractmethod
    def handle(self, request):
        pass

# Concrete Handlers
class Level1Support(Handler):
    def handle(self, request):
        if request == "general inquiry":
            print("Level 1 Support: Handling general inquiry.")
        elif self.next_handler:
            self.next_handler.handle(request)
        else:
            print("Request could not be handled.")

class Level2Support(Handler):
    def handle(self, request):
        if request == "technical issue":
            print("Level 2 Support: Handling technical issue.")
        elif self.next_handler:
            self.next_handler.handle(request)
        else:
            print("Request could not be handled.")

class Manager(Handler):
    def handle(self, request):
        if request == "escalation":
            print("Manager: Handling escalation.")
        elif self.next_handler:
            self.next_handler.handle(request)
        else:
            print("Request could not be handled.")

# Client Code
def process_request(request):
    # Build the chain
    chain = Level1Support(Level2Support(Manager()))

    # Send the request
    chain.handle(request)

# Example Usage
process_request("general inquiry")  # Handled by Level 1
process_request("technical issue")  # Handled by Level 2
process_request("escalation")       # Handled by Manager
process_request("billing issue")    # No handler can process this
```

---

#### **Output of Example**

```
Level 1 Support: Handling general inquiry.
Level 2 Support: Handling technical issue.
Manager: Handling escalation.
Request could not be handled.
```

---

#### **Real-World Use Cases**

1. **Middleware in Web Applications**:
    
    - Authentication, logging, and request validation handlers form a chain.
        
2. **Logging Systems**:
    
    - Different loggers handle messages of varying severity (e.g., debug, info, error).
        
3. **Customer Support Systems**:
    
    - Requests are escalated through support levels based on complexity.
        
4. **Event Handling**:
    
    - GUI frameworks propagate user events (e.g., mouse clicks) through a chain of components.
        

---

#### **Summary**

The Chain of Responsibility pattern enables flexible request handling by decoupling request senders and receivers. It’s ideal when multiple handlers can process a request, and the specific handler needs to be determined at runtime.