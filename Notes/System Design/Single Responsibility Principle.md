### **Single Responsibility Principle (SRP)**

> **A class should have only one reason to change.**

In simpler terms, a class (or module) should focus on doing one thing, and doing it well. 

If a class has multiple responsibilities, changes in one responsibility might unintentionally affect others, making the code harder to maintain and test.

---

### **Why is SRP Important?**

1. **Improves maintainability:** If a class has one responsibility, it is easier to modify or extend.
2. **Reduces coupling:** Changes in one part of the system don’t affect unrelated parts.
3. **Enhances readability:** Code with focused responsibilities is easier to understand.

---

### **SRP Example in Python**

#### **Without SRP**

Imagine we’re building a system to manage books in a library. Here’s a class that violates SRP:

```python
class LibraryManager:
    def add_book(self, book):
        # Logic to add a book
        print(f"Adding book: {book}")

    def remove_book(self, book):
        # Logic to remove a book
        print(f"Removing book: {book}")

    def generate_report(self):
        # Logic to generate a report of all books
        print("Generating report of all books.")
```

**What's wrong here?**

- The `LibraryManager` class has multiple responsibilities:
    1. Managing books (adding and removing).
    2. Generating reports.

Changes to the reporting system might affect book management logic, which violates SRP.

---

#### **With SRP**

We can refactor the code to split responsibilities into separate classes:

```python
class BookManager:
    def add_book(self, book):
        # Logic to add a book
        print(f"Adding book: {book}")

    def remove_book(self, book):
        # Logic to remove a book
        print(f"Removing book: {book}")

class ReportGenerator:
    def generate_report(self):
        # Logic to generate a report of all books
        print("Generating report of all books.")
```

Now, each class has a single responsibility:

1. **`BookManager`**: Handles adding and removing books.
2. **`ReportGenerator`**: Handles generating reports.

If we need to change how reports are generated, it won’t affect the book management logic.

---

### **Benefits of Refactoring with SRP**

1. **Easier Testing:**
    - Each class can be tested independently.
2. **Reduced Risk:**
    - Changes in one class don’t accidentally break unrelated functionality.
3. **Better Collaboration:**
    - Different developers can work on different classes without interference.

---

### **Extending the Example**

Suppose we add a new requirement to send email notifications when a report is generated. With SRP, we can introduce a new class for this functionality:

```python
class NotificationService:
    def send_email(self, message):
        # Logic to send an email
        print(f"Sending email: {message}")
```

Now, `ReportGenerator` can use this service without violating SRP:

```python
class ReportGenerator:
    def __init__(self, notification_service):
        self.notification_service = notification_service

    def generate_report(self):
        # Logic to generate a report
        print("Generating report of all books.")
        self.notification_service.send_email("Report has been generated.")
```

---

### **Conclusion**

By adhering to SRP:

- **Classes become modular**, focusing on a single task.
- **Code becomes more flexible and easier to maintain.**

This is a key step towards writing clean, robust, and professional code.