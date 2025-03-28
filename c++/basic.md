# C++ Basics Cheat Sheet

This is a quick reference for modern C++ essentials. It includes syntax, data types, functions, classes, and other core concepts. Ideal for those who need a refresher or are transitioning from another language.

---

## 🧱 Hello World

```cpp
#include <iostream>

int main() {
    std::cout << "Hello, World!" << std::endl;
    return 0;
}
```

---

## 🔤 Variables and Types

```cpp
int x = 10;
double pi = 3.14;
char c = 'A';
bool flag = true;
std::string name = "Alice";
```

### Type Modifiers
```cpp
short, long, unsigned, signed
```

---

## 🧮 Operators

```cpp
+  -  *  /  %     // Arithmetic
== != > < >= <=  // Comparison
&& || !          // Logical
= += -= *= /=    // Assignment
++ --            // Increment / Decrement
```

---

## 🧾 Control Flow

### If / Else

```cpp
if (x > 0) {
    std::cout << "Positive";
} else {
    std::cout << "Non-positive";
}
```

### Switch

```cpp
switch (x) {
    case 1: std::cout << "One"; break;
    case 2: std::cout << "Two"; break;
    default: std::cout << "Other";
}
```

### Loops

```cpp
for (int i = 0; i < 5; ++i) {
    std::cout << i;
}

int i = 0;
while (i < 5) {
    std::cout << i;
    ++i;
}

do {
    std::cout << i;
    ++i;
} while (i < 5);
```

---

## 🔧 Functions

```cpp
int add(int a, int b) {
    return a + b;
}

void greet(std::string name) {
    std::cout << "Hello " << name;
}
```

---

## 🗃️ Arrays and Vectors

```cpp
int arr[5] = {1, 2, 3, 4, 5};

#include <vector>
std::vector<int> nums = {1, 2, 3};
nums.push_back(4);
```

---

## 🧱 Structs and Classes

### Struct (default: public)

```cpp
struct Point {
    int x, y;
};

Point p = {10, 20};
```

### Class (default: private)

```cpp
class Animal {
public:
    std::string name;
    void speak() {
        std::cout << name << " makes a sound";
    }
};
```

---

## 🚪 Constructors and Destructors

```cpp
class Dog {
public:
    Dog() { std::cout << "Constructor"; }
    ~Dog() { std::cout << "Destructor"; }
};
```

---

## 🪝 Pointers and References

```cpp
int a = 5;
int* p = &a;       // Pointer
int& ref = a;      // Reference

std::cout << *p;   // Dereference pointer
```

---

## 📦 Namespaces

```cpp
namespace MyApp {
    void run() {
        std::cout << "Running MyApp";
    }
}

MyApp::run();
```

---

## 🧵 Input and Output

```cpp
int age;
std::cout << "Enter age: ";
std::cin >> age;
```

---

## 📄 Header Files

Separate declarations and implementations:

**math_utils.h**
```cpp
int add(int a, int b);
```

**math_utils.cpp**
```cpp
#include "math_utils.h"
int add(int a, int b) {
    return a + b;
}
```

---

## ✅ Modern C++ Features (C++11+)

- `auto` keyword for type inference
- `nullptr` replaces `NULL`
- `range-based for` loops
```cpp
for (int x : nums) {
    std::cout << x;
}
```
- `std::unique_ptr`, `std::shared_ptr` for smart memory management
- Lambda functions:
```cpp
auto sum = [](int a, int b) { return a + b; };
```

---

## 🧠 Final Tips

- Always `#include` only what you need.
- Use `const` wherever you can.
- Prefer `std::vector` over raw arrays.
- Compile with `-Wall -Wextra` to catch issues early.
- Avoid raw pointers unless necessary—prefer smart pointers.

---

**Happy C++ coding!**
