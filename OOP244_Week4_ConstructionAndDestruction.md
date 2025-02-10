# OOP244 Week 3.1 - Construction and Destruction 📚
https://intro2oop.sdds.ca/C-Encapsulation/construction-and-destruction

## 学习路径图 (Learning Path) 🗺️
```
Construction and Destruction
├── Class Features
│   ├── Instance of a Class
│   ├── Instance Variables
│   └── Logic
├── Class Privacy
├── Constructor
│   ├── Definition
│   ├── Example
│   ├── Default Behavior
│   └── Understanding Order
├── Safe Empty State
└── Destructor
    ├── Definition
    ├── Example
    ├── Default Behavior
    └── Understanding Order
```

## 目录 (Table of Contents) 📑
1. [Class Features](#class-features)
2. [Class Privacy](#class-privacy)
3. [Constructor](#constructor)
4. [Safe Empty State](#safe-empty-state)
5. [Destructor](#destructor)
6. [Construction and Destruction of Arrays](#construction-and-destruction-of-arrays)

## 知识点详解 (Detailed Content) 📝

### Class Features (类特性) 🟢

#### Instance of a Class (类的实例) 
- **定义 | Definition**: 每个类的对象或实例占用自己的内存区域。对象的数据存储在该内存区域中。
- **示例 | Example**:
```cpp
const int NG = 20;

class Student {
    int no;
    float grade[NG];
    int ng;
public:
    void set(int, const float*, int);
    void display() const;
};

// 创建对象
Student harry; // 创建一个 Student 类的对象
Student a, b, c, d, e; // 创建多个对象
```

#### Instance Variables (实例变量)
- **定义 | Definition**: 类定义中的数据成员称为对象的实例变量。实例变量可以是基本类型、复合类型（类类型、指针类型、引用类型）。
- **示例 | Example**:
```cpp
int no; // 基本类型
float grade[NG]; // 数组类型
```

#### Logic (逻辑)
- **定义 | Definition**: 成员函数的指令适用于所有类的对象，运行时每次调用成员函数时访问相同的代码，但使用不同的实例变量。
- **示例 | Example**:
```cpp
Student a, b, c, d, e;
a.display(); // 调用 display() 函数，显示 a 的数据
```

### Class Privacy (类的私有性) 🟡
- **定义 | Definition**: C++ 编译器在类级别应用隐私。任何成员函数可以访问其类的任何私有成员，包括任何实例的私有数据成员。
- **示例 | Example**:
```cpp
class Student {
    int no;
    float grade[NG];
    int ng;
public:
    void copyFrom(const Student& src);
};

// 在成员函数中访问私有数据
void Student::copyFrom(const Student& src) {
    no = src.no; // 从另一个对象复制数据
}
```
- **总结**: 
  - 私有成员只能在类的内部访问。
  - 通过公共成员函数，可以访问同一类的其他对象的私有成员。
  - 不同类的对象无法直接访问另一个类的私有成员。

### Constructor (构造函数) 🟢

#### 定义 | Definition
- **构造函数**是对象在创建时调用的特殊成员函数。它的名称与类相同，没有返回类型。
- **示例 | Example**:
```cpp
class Student {
public:
    Student(); // 默认构造函数声明
};

Student::Student() {
    no = 0; // 初始化数据成员
}
```

#### 初始化列表 | Initialization List
- **定义 | Definition**: 初始化列表是一种在构造函数中初始化成员变量的语法。它在构造函数体执行之前执行，通常用于初始化常量成员、引用成员或需要复杂初始化的成员。
- **语法 | Syntax**:
```cpp
ClassName::ClassName(parameters) : member1(value1), member2(value2) {
    // 构造函数体
}
```

- **示例 | Example**:
```cpp
class Student {
    int no;
    float grade;
public:
    // 使用初始化列表
    Student(int studentNo, float initialGrade) : no(studentNo), grade(initialGrade) {
        // 构造函数体，可以为空
    }
};

// 创建对象
Student harry(1234, 85.5f); // 使用初始化列表初始化成员
```

#### 默认行为 | Default Behavior
- 如果类定义中没有声明构造函数，编译器会插入一个空体的默认构造函数。
- **示例 | Example**:
```cpp
Student::Student() {
    // 空体构造函数
}
```

#### 理解顺序 | Understanding Order
- **构造顺序**:
  1. 为每个实例变量分配内存。
  2. 执行构造函数中的逻辑。

### Safe Empty State (安全空状态) 🟡
- **定义 | Definition**: 在创建时初始化对象的实例变量，确保对象在创建时具有良好的定义状态。
- **示例 | Example**:
```cpp
Student::Student() {
    no = 0; // 设置安全空状态
    ng = 0;
}
```

### Destructor (析构函数) 🟡

#### 定义 | Definition
- **析构函数**是对象在销毁时调用的特殊成员函数。它的名称与类相同，前面加上波浪号（~）。
- **示例 | Example**:
```cpp
class Student {
public:
    ~Student(); // 析构函数声明
};

Student::~Student() {
    // 终止逻辑
}
```

#### 默认行为 | Default Behavior
- 如果类定义中没有声明析构函数，编译器会插入一个空体的析构函数。
- **示例 | Example**:
```cpp
Student::~Student() {
    // 空体析构函数
}
```

#### 理解顺序 | Understanding Order
- **析构顺序**:
  1. 执行析构函数中的逻辑。
  2. 以与类定义中列出的顺序相反的顺序释放每个实例变量的内存。(opposite order)

### Construction and Destruction of Arrays (数组的构造与析构) 🟡
- **定义 | Definition**: 数组元素的构造和析构顺序遵循上述描述的顺序。
- 编译器依次创建数组中的每个元素，从第一个元素开始，直到最后一个元素。每个对象在创建时调用默认构造函数。当数组超出作用域时，最后一个元素首先调用其析构函数，第一个元素最后调用其析构函数。
- **示例 | Example**:
```cpp
// Constructors, Destructors and Arrays
// ctorsDtorsArrays.cpp

#include <iostream>
#include <cstring>
using namespace std;
const int NG = 20;

class Student {
    int no;
    float grade[NG];
    int ng;
public:
    Student();
    ~Student();
    void set(int, const float*, int);
    void display() const;
};

Student::Student() {
    cout << "In constructor" << endl;
    no = 0;
    ng = 0;
}

Student::~Student() {
cout << "In destructor for " << no
        << endl;
}

void Student::set(int sn, const float* g, int ng_) {
    bool valid = sn > 0 && g != nullptr && ng_ >= 0;
    if (valid)
        for (int i = 0; i < ng_ && valid; i++)
            valid = g[i] >= 0.0f && g[i] <= 100.0f;

    if (valid) {
        // accept the client's data
        no = sn;
        ng = ng_ < NG ? ng_ : NG;
        for (int i = 0; i < ng; i++)
            grade[i] = g[i];
    } else {
        no = 0;
        ng = 0;
    }
}

void Student::display() const {
    if (no > 0) {
        cout << no << ":\n";
        cout.setf(ios::fixed);
        cout.precision(2);
        for (int i = 0; i < ng; i++) {
            cout.width(6);
            cout << grade[i] << endl;
        }
        cout.unsetf(ios::fixed);
        cout.precision(6);
    } else {
        cout << "no data available" << endl;
    }
}

int main () {
    Student a[3];
    float g0[] = {89.4f, 67.8f, 45.5f};
    float g1[] = {83.4f, 77.8f, 55.5f};
    float g2[] = {77.8f, 83.4f, 55.5f};
    a[0].set(1234, g0, 3);
    a[1].set(1235, g1, 3);
    a[2].set(1236, g2, 3);
    for (int i = 0; i < 3; i++)
        a[i].display();
}
```

### Overloading Constructors (构造函数重载) 🟡
- **定义 | Definition**: 重载类的构造函数为客户端代码提供了更多的通信选项。客户端代码可以在创建时选择最合适的参数集。
- **示例 | Example**:
```cpp
// Overloaded Constructor
// overload.cpp

#include <iostream>
using namespace std;
const int NG = 20;

class Student {
    int no;
    float grade[NG];
    int ng;
public:
    Student();
    Student(int, const float*, int);
    ~Student();
    void set(int, const float*, int);
    void display() const;
};

Student::Student() {
    cout << "In constructor" << endl;
    no = 0;
    ng = 0;
}

Student::Student(int sn, const float* g, int ng_) {
    cout << "In 3-arg constructor" << endl;
    set(sn, g, ng_);
}

Student::~Student() {
cout << "In destructor for " << no
        << endl;
}

void Student::set(int sn, const float* g, int ng_) {
    bool valid = sn > 0 && g != nullptr && ng_ >= 0;
    if (valid)
        for (int i = 0; i < ng_ && valid; i++)
            valid = g[i] >= 0.0f && g[i] <= 100.0f;

    if (valid) {
        // accept the client's data
        no = sn;
        ng = ng_ < NG ? ng_ : NG;
        for (int i = 0; i < ng; i++)
            grade[i] = g[i];
    } else {
        no = 0;
        ng = 0;
    }
}

void Student::display() const {
    if (no > 0) {
        cout << no << ":\n";
        cout.setf(ios::fixed);
        cout.precision(2);
        for (int i = 0; i < ng; i++) {
            cout.width(6);
            cout << grade[i] << endl;
        }
        cout.unsetf(ios::fixed);
        cout.precision(6);
    } else {
        cout << "no data available" << endl;
    }
}

int main () {
    float gh[] = {89.4f, 67.8f, 45.5f};
    float gj[] = {83.4f, 77.8f, 55.5f};
    Student harry, josee(1235, gj, 3);
    harry.set(1234, gh, 3); // 使用无参数构造函数创建对象   
    harry.display();
    josee.display();
}
```

### No-argument constructor is not always implemented (无参数构造函数并不总是实现) 🟡
- **定义 | Definition**: 如果类定义包含带参数的构造函数的原型，但不包含无参数默认构造函数的原型，编译器**不会**插入一个空体的无参数默认构造函数。编译器仅在类定义中未声明**任何**构造函数时插入空体的无参数默认构造函数。
- **总结**: 如果我们定义了带参数的构造函数，通常也会定义一个无参数默认构造函数。这在创建对象数组时非常重要。数组中每个元素的创建都需要一个无参数默认构造函数。

## 版本控制 (Version Control) 🔄
```
更新日期：2024-03-19
版本号：v1.0
更新内容：
- 添加了构造函数和析构函数的详细信息
- 包含类特性和私有性相关内容
- 详细示例和代码片段
```

[End of Document] 