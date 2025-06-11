Hexagonal Architecture, also known as **Ports and Adapters Architecture**, is a design pattern created by Alistair Cockburn. It focuses on building maintainable, flexible, and testable software by separating the **core business logic** from the **external systems** it interacts with (e.g., databases, APIs, or user interfaces).

Let’s break it down step by step.

---

### **Core Idea**

The main idea is to put your application’s **business logic** in the center (the hexagon) and make it independent of external systems. The application interacts with the outside world through well-defined **ports** and **adapters**.

#### **Key Terms:**

1. **Core (Hexagon):**  
    This is the heart of your application. It contains:
    
    - The **business logic** (rules and processes).
    - The application’s use cases (what it does).
    - It doesn’t care about _how_ data is stored, _how_ users interact, or _how_ external APIs work.
2. **Ports (Interfaces):**
    
    - These are the **entry points** and **exit points** to the core logic.
    - They define **what** needs to be done but not **how**.
    - Example: An interface like `saveData(data)` doesn’t care if the data is saved to a database, a file, or sent to an API.
3. **Adapters (Implementations):**
    
    - Adapters are responsible for **bridging the gap** between the core and the outside world.
    - They implement the ports and handle specific external interactions.
    - Example: A `DatabaseAdapter` might implement the `saveData()` port to save data to a database.

---

### **Structure**

Here’s how the hexagonal architecture is typically structured:

```
            +-------------------+
            |     Adapter       |  (e.g., Web Controller)
            +-------------------+
                    ^
                    |
        +---------------------------+
        |         INPUT PORT        |  (Interface for entering the system)
        +---------------------------+
                    ^
                    |
        +---------------------------+
        |         CORE LOGIC        |  (Business rules and use cases)
        +---------------------------+
                    |
                    v
        +---------------------------+
        |        OUTPUT PORT        |  (Interface for leaving the system)
        +---------------------------+
                    |
                    v
            +-------------------+
            |     Adapter       |  (e.g., Database/External API)
            +-------------------+
```

---

### **Why Use Hexagonal Architecture?**

1. **Independence:**
    
    - The core logic doesn’t depend on frameworks, databases, or APIs. This makes it easier to replace or test these external dependencies.
2. **Flexibility:**
    
    - You can swap out adapters (e.g., change databases or APIs) without modifying the core logic.
3. **Testability:**
    
    - Since the core logic is isolated, you can test it independently from the external systems.
4. **Maintainability:**
    
    - Clear separation of concerns means less tangled code and easier debugging.

---

### **Example in Python**

Let’s build an example of a **Task Management System** using Hexagonal Architecture.

#### **1. Core Logic (The Hexagon)**

This contains the application’s **use case** and **business logic**:

```python
# INPUT PORT (Interface)
class TaskManager:
    def add_task(self, task):
        pass
    def list_tasks(self):
        pass

# OUTPUT PORT (Interface)
class TaskRepository:
    def save(self, task):
        pass
    def get_all(self):
        pass

# CORE LOGIC
class TaskManagerImpl(TaskManager):
    def __init__(self, repository: TaskRepository):
        self.repository = repository

    def add_task(self, task):
        self.repository.save(task)

    def list_tasks(self):
        return self.repository.get_all()
```

---

#### **2. Adapters (Bridging External Systems)**

**Adapter 1: Database Adapter (Output Port Implementation):**

```python
class DatabaseTaskRepository(TaskRepository):
    def __init__(self):
        self.db = []  # Simulating a database

    def save(self, task):
        self.db.append(task)

    def get_all(self):
        return self.db
```

**Adapter 2: CLI Adapter (Input Port Implementation):**

```python
class CLIAdapter:
    def __init__(self, task_manager: TaskManager):
        self.task_manager = task_manager

    def run(self):
        print("Welcome to the Task Manager!")
        while True:
            choice = input("1. Add Task, 2. List Tasks, 3. Exit: ")
            if choice == "1":
                task = input("Enter task: ")
                self.task_manager.add_task(task)
            elif choice == "2":
                tasks = self.task_manager.list_tasks()
                print("Tasks:", tasks)
            elif choice == "3":
                break
```

---

#### **3. Putting It All Together**

```python
if __name__ == "__main__":
    # Use database adapter for storing tasks
    repository = DatabaseTaskRepository()

    # Create the core with the repository
    task_manager = TaskManagerImpl(repository)

    # Use CLI adapter for user interaction
    cli = CLIAdapter(task_manager)
    cli.run()
```

---

### **Flow in Action**

1. The **CLIAdapter** sends a user request (e.g., adding a task) to the core logic (`TaskManager`).
2. The core logic performs the task and delegates data persistence to the **DatabaseTaskRepository**.
3. The **DatabaseTaskRepository** handles the specifics of saving the data.

---

### **Advantages of Hexagonal Architecture in This Example:**

1. You could replace `DatabaseTaskRepository` with a `FileTaskRepository` or an `APITaskRepository` without touching the core logic.
2. You could swap the `CLIAdapter` with a `WebControllerAdapter` if you wanted a web-based interface.
3. The `TaskManagerImpl` can be unit-tested independently of adapters.

---

### **When to Use Hexagonal Architecture?**

- You’re building a **long-term project** where flexibility and testability are critical.
- The system interacts with multiple external systems (e.g., databases, APIs, message queues).
- You want to **future-proof** your design to easily adapt to changes.

---

### **Summary**

- Hexagonal Architecture is about isolating your **business logic** from **external systems**.
- **Ports** define the entry/exit points for the core logic.
- **Adapters** implement these ports to handle specific external interactions.
- It makes your application **flexible, maintainable, and testable**.
