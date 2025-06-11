`private` and `protected` are both access specifiers that restrict access to class members, but they work differently when it comes to inheritance:

1. `private` members:
- Only accessible within the same class
- Not accessible by derived classes
- Not accessible from outside the class

Example:
```cpp
class Base {
private:
    int privateVar;    // Only accessible within Base class
};

class Derived : public Base {
    void someFunction() {
        privateVar = 5;    // Error: Can't access private member
    }
};
```

2. `protected` members:
- Accessible within the same class
- Accessible by derived classes
- Not accessible from outside the class

Example:
```cpp
class Base {
protected:
    int protectedVar;    // Accessible in Base and derived classes
};

class Derived : public Base {
    void someFunction() {
        protectedVar = 5;    // OK: Can access protected member
    }
};
```

A quick comparison:
```cpp
class Base {
private:
    int priv;     // Only Base can access
protected:
    int prot;     // Base and derived classes can access
public:
    int pub;      // Everyone can access
};

class Derived : public Base {
    void func() {
        priv = 1;  // Error
        prot = 2;  // OK
        pub = 3;   // OK
    }
};

int main() {
    Derived d;
    d.priv = 1;    // Error
    d.prot = 2;    // Error
    d.pub = 3;     // OK
}
```

