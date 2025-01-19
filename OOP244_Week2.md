# OOP244 Week 2 - Types, Function Overloading and Memory Management 📚
> C++类型、函数重载与内存管理 | C++ Types, Function Overloading and Memory Management

## 文档信息 (Document Information) 📋
更新日期 | Update Date：2024-03-19
版本号 | Version：v1.0
更新内容 | Update Content：
- 初始化文档 | Initialize document
- 添加类型系统内容 | Added type system content
- 添加函数重载内容 | Added function overloading content
- 添加内存管理内容 | Added memory management content

## 目录 (Table of Contents) 📑
1. [概述 (Overview)](#1-概述-overview-)
2. [学习路径图 (Learning Path)](#2-学习路径图-learning-path-)
3. [知识点详解 (Detailed Content)](#3-知识点详解-detailed-content-)
   - [3.1 C++类型系统 (C++ Type System)](#31-c类型系统-c-type-system-)
   - [3.2 声明和定义 (Declarations and Definitions)](#32-声明和定义-declarations-and-definitions-)
   - [3.3 函数重载 (Function Overloading)](#33-函数重载-function-overloading-)
   - [3.4 引用与指针 (References and Pointers)](#34-引用与指针-references-and-pointers-)
   - [3.5 作用域 (Scope)](#35-作用域-scope-)
   - [3.6 指针数组 (Array of Pointers)](#36-指针数组-array-of-pointers-)
   - [3.7 C++关键字 (C++ Keywords)](#37-c关键字-c-keywords-)
   - [3.8 动态内存管理 (Dynamic Memory Management)](#38-动态内存管理-dynamic-memory-management-)
4. [实践示例 (Practice Examples)](#4-实践示例-practice-examples-)
5. [重要概念框架 (Key Concepts Framework)](#5-重要概念框架-key-concepts-framework-)
6. [学习建议 (Study Tips)](#6-学习建议-study-tips-)
7. [FAQ (常见问题)](#7-faq-常见问题-)
8. [快速复习指南 (Quick Review Guide)](#8-快速复习指南-quick-review-guide-)
9. [相关概念链接 (Related Concepts)](#9-相关概念链接-related-concepts-)

## 1. 概述 (Overview) 📑
### 本章要点 | Chapter Points
- 理解C++类型系统 | Understanding C++ type system
- 掌握函数重载机制 | Mastering function overloading
- 学习引用和指针 | Learning references and pointers
- 理解作用域规则 | Understanding scope rules
- 掌握动态内存管理 | Mastering dynamic memory management

### 前置知识 | Prerequisites
- C语言基础 | C Language Basics
  - 基本数据类型 | Basic data types
  - 指针概念 | Pointer concepts
  - 函数定义 | Function definition

## 2. 学习路径图 (Learning Path) 🗺️
1. 掌握C++类型系统 | Master C++ type system
2. 理解函数重载机制 | Understand function overloading
3. 学习引用和指针 | Learn references and pointers
4. 掌握作用域规则 | Master scope rules
5. 学习指针数组 | Learn array of pointers
6. 掌握动态内存管理 | Master dynamic memory management

## 3. 知识点详解 (Detailed Content) 📝

### 3.1 C++类型系统 (C++ Type System) 🟢

> 原文：C++ provides basic types for precise data storage and compound types built from other types.

💡 解析步骤 | Analysis Steps:
1. 关键词提取 | Key Terms:
   - basic types (基本类型)
   - compound types (复合类型)
   - type storage (类型存储)
   - auto keyword (auto关键字)

2. 核心概念 | Core Concepts:
   - C++提供多种数据类型
   - 类型分为基本类型和复合类型
   - 支持类型推导

3. 简化解释 | Simplified Explanation:
   - 基本类型就像积木的基础块
   - 复合类型是由基础块组合而成
   - auto关键字让编译器自动推断类型

4. 具体示例：

#### 3.1.1 基本类型 (Basic Types)
```cpp
// 整型 | Integer types
bool flag = true;       // 布尔型 | Boolean
char ch = 'A';         // 字符型 | Character
int number = 42;       // 整数 | Integer
short small = 123;     // 短整型 | Short integer
long big = 123456L;    // 长整型 | Long integer

// 浮点型 | Floating-point types
float f = 3.14f;       // 单精度 | Single precision
double d = 3.14159;    // 双精度 | Double precision
```

#### 3.1.2 复合类型 (Compound Types)
```cpp
// 结构体 | Structure
struct Student {
    int id;
    char name[50];
    double grade;
};

// C++风格的结构体使用 | C++ style structure usage
Student s1;            // 不需要struct关键字 | No struct keyword needed
s1.id = 12345;

// C风格的结构体使用 | C style structure usage
struct Student s2;     // C语言中需要struct关键字 | struct keyword needed in C
```

#### 3.1.3 Auto关键字 (Auto Keyword)
```cpp
// 自动类型推导 | Automatic type deduction
auto i = 42;          // int
auto d = 3.14;        // double
auto s = "Hello";     // const char*

// 必须初始化 | Must initialize
auto x;               // 错误：需要初始化器 | Error: initializer needed
```

### 3.2 声明和定义 (Declarations and Definitions) 🟡

> 原文：Modular programming can result in multiple definitions. To avoid conflicts or duplication, we need to design our header and implementation files accordingly.

#### 3.2.1 循环依赖与前向声明 (Circular Dependency & Forward Declaration)
```cpp
// 循环依赖问题 | Circular dependency problem
// file1.h
#include "file2.h"  // 需要 B
class A {
    B* b;  // 使用B
};

// file2.h
#include "file1.h"  // 需要 A
class B {
    A* a;  // 使用A
};
```

```cpp
// 使用前向声明解决 | Solution using forward declaration
// file1.h
class B;  // 前向声明 | Forward declaration
class A {
    B* b;
};

// file2.h
class A;  // 前向声明 | Forward declaration
class B {
    A* a;
};
```

#### 3.2.2 一次定义规则 (One Definition Rule)
```cpp
// header.h
struct MyStruct {  // 在头文件中定义
    int x;
};

// file1.cpp
#include "header.h"

// file2.cpp
#include "header.h"  // 没问题：头文件包含防重复包含宏
```

### 3.3 函数重载 (Function Overloading) 🟡

> 原文：C++ supports function overloading, which allows defining multiple functions with the same name but different parameter lists. Function signature uniquely identifies an overloaded function.

💡 解析步骤 | Analysis Steps:
1. 关键词提取 | Key Terms:
   - function overloading (函数重载)
   - function signature (函数签名)
   - parameter list (参数列表)
   - name mangling (名称修饰)

2. 核心概念 | Core Concepts:
   - 同名函数可以有不同参数列表
   - 函数签名用于区分重载函数
   - 返回类型不是函数签名的一部分

3. 简化解释 | Simplified Explanation:
   - 函数重载就像同一个工具的不同版本
   - 根据使用的材料（参数）选择合适的工具版本
   - 编译器根据参数类型自动选择正确的版本

4. 具体示例：

```cpp
// 函数重载示例 | Function overloading example
class Calculator {
public:
    // 整数加法 | Integer addition
    int add(int a, int b) { 
        return a + b; 
    }
    
    // 浮点数加法 | Floating-point addition
    double add(double a, double b) { 
        return a + b; 
    }
    
    // 字符串连接 | String concatenation
    string add(string a, string b) { 
        return a + b; 
    }
};

int main() {
    Calculator calc;
    cout << calc.add(5, 3);        // 调用整数版本 | Calls integer version
    cout << calc.add(3.14, 2.0);   // 调用浮点数版本 | Calls floating-point version
    cout << calc.add("Hello", "!"); // 调用字符串版本 | Calls string version
}
```

#### 3.3.1 函数签名 (Function Signature)
- 组成部分 | Components
  - 函数名 | Function name
  - 参数类型 | Parameter types
  - 参数顺序 | Parameter order
- 不包含 | Not included
  - 返回类型 | Return type
  - 参数名称 | Parameter names

#### 3.3.2 默认参数值 (Default Parameter Values)
```cpp
// 带默认参数的函数 | Function with default parameters
void display(string msg, int times = 1, bool newline = true) {
    for(int i = 0; i < times; i++) {
        cout << msg;
        if(newline) cout << endl;
    }
}

// 调用方式 | Calling methods
display("Hello");           // 使用所有默认值 | Uses all defaults
display("Hi", 3);          // 覆盖times参数 | Overrides times
display("Test", 2, false); // 覆盖所有默认值 | Overrides all defaults
```

### 3.4 引用与指针 (References and Pointers) 🟡

> 原文：References are aliases for variables or objects. C++ relies heavily on references. Function calls using references pass the variable or object itself, not a copy.

💡 解析步骤 | Analysis Steps:
1. 关键词提取 | Key Terms:
   - references (引用)
   - pointers (指针)
   - pass by reference (引用传递)
   - memory address (内存地址)

2. 核心概念 | Core Concepts:
   - 引用是变量的别名
   - 指针存储内存地址
   - 引用传递避免复制
   - 指针可以修改指向

3. 简化解释 | Simplified Explanation:
   - 引用像是变量的昵称
   - 指针像是变量的地址
   - 引用必须初始化且不能改变指向
   - 指针可以改变指向，也可以为空

4. 具体示例：

```cpp
// 引用与指针的比较 | Comparison of references and pointers
void demoReferencesAndPointers() {
    int x = 10;
    
    // 引用 | Reference
    int& ref = x;     // ref是x的别名 | ref is an alias for x
    ref = 20;         // 修改x的值 | Modifies x
    
    // 指针 | Pointer
    int* ptr = &x;    // ptr存储x的地址 | ptr stores x's address
    *ptr = 30;        // 通过指针修改x | Modifies x through pointer
    
    cout << "x = " << x << endl;     // 输出: 30
    cout << "ref = " << ref << endl;  // 输出: 30
    cout << "*ptr = " << *ptr << endl;// 输出: 30
}

// 引用传递示例 | Pass by reference example
void swapByReference(int& a, int& b) {
    int temp = a;
    a = b;
    b = temp;
}

// 指针传递示例 | Pass by pointer example
void swapByPointer(int* a, int* b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}
```

### 3.5 作用域 (Scope) 🟡

> 原文：The scope of a declaration is the part of the program where the declaration is visible. Once a declaration goes out of scope, the program can no longer access the declared variable or object.

💡 解析步骤 | Analysis Steps:
1. 关键词提取 | Key Terms:
   - scope (作用域)
   - declaration (声明)
   - visibility (可见性)
   - shadowing (遮蔽)

2. 核心概念 | Core Concepts:
   - 作用域定义了声明的可见范围
   - 不同作用域可以有同名变量
   - 内部作用域可以遮蔽外部作用域

3. 简化解释 | Simplified Explanation:
   - 作用域像是变量的"生存范围"
   - 每个大括号对创建新的作用域
   - 内层作用域可以"遮盖"外层同名变量

4. 具体示例：

```cpp
// 作用域示例 | Scope example
int globalVar = 100;  // 全局作用域 | Global scope

void scopeDemo() {
    int localVar = 200;  // 函数作用域 | Function scope
    
    {  // 新的块作用域开始 | New block scope starts
        int blockVar = 300;  // 块作用域 | Block scope
        int globalVar = 400; // 遮蔽全局变量 | Shadows global variable
        
        cout << globalVar;   // 输出400（局部变量）| Prints 400 (local variable)
        cout << ::globalVar; // 输出100（全局变量）| Prints 100 (global variable)
    }  // blockVar在这里结束生命周期 | blockVar ends its lifecycle here
    
    // cout << blockVar;  // 错误：blockVar超出作用域 | Error: blockVar out of scope
}  // localVar在这里结束生命周期 | localVar ends its lifecycle here
```

#### 3.5.1 作用域类型 (Scope Types)
1. 全局作用域 | Global Scope
   - 在所有函数外部声明
   - 整个程序都可访问
   - 程序结束时销毁

2. 文件作用域 | File Scope
   - 使用static声明的全局变量
   - 仅在当前文件可见
   - 文件作用域结束时销毁

3. 函数作用域 | Function Scope
   - 函数参数和局部变量
   - 仅在函数内部可见
   - 函数返回时销毁

4. 块作用域 | Block Scope
   - 在代码块中声明的变量
   - 仅在块内部可见
   - 离开块时销毁

### 3.6 指针数组 (Array of Pointers) 🟡

> 原文：A pointer array is a data structure that contains addresses rather than values. Objects stored at those addresses are referenced by dereferencing the specific address.

💡 解析步骤 | Analysis Steps:
1. 关键词提取 | Key Terms:
   - pointer array (指针数组)
   - address (地址)
   - dereferencing (解引用)
   - memory management (内存管理)

2. 核心概念 | Core Concepts:
   - 数组元素是指针
   - 每个指针存储一个地址
   - 通过解引用访问数据
   - 支持动态内存管理

3. 简化解释 | Simplified Explanation:
   - 指针数组像是地址簿
   - 每个元素存储一个地址
   - 通过地址找到实际数据
   - 可以动态管理内存空间

4. 具体示例：

```cpp
// 指针数组示例 | Pointer array example
const int N_CHARS = 31;

struct Student {
    int no;
    double grade;
    char name[N_CHARS];
};

int main() {
    const int NO_STUDENTS = 3;
    
    // 创建学生对象 | Create student objects
    Student john = {1234, 67.8, "john"};
    Student jane = {1235, 89.5, "jane"};
    Student dave = {1236, 78.4, "dave"};

    // 创建并初始化指针数组 | Create and initialize pointer array
    Student* pStudent[NO_STUDENTS];
    pStudent[0] = &john;
    pStudent[1] = &jane;
    pStudent[2] = &dave;

    // 通过指针数组访问数据 | Access data through pointer array
    for (int i = 0; i < NO_STUDENTS; i++) {
        cout << pStudent[i]->no << endl;     // 使用->访问成员
        cout << pStudent[i]->grade << endl;   // Access members using ->
        cout << pStudent[i]->name << endl;
        cout << endl;
    }
}
```

#### 3.6.1 指针数组与数组指针的区别
```cpp
// 指针数组：每个元素是指针 | Array of pointers: each element is a pointer
int* arr1[5];  // 5个指向int的指针 | 5 pointers to int

// 数组指针：指向数组的指针 | Pointer to array: points to an array
int (*arr2)[5];  // 指向包含5个int的数组的指针 | Pointer to array of 5 ints
```

### 3.7 C++关键字 (C++ Keywords) 🟢

> C++11标准包含84个关键字，不能用作标识符。加粗的也是C语言的关键字。

常用关键字分类：
1. 类型关键字 | Type Keywords
   - **int**, **char**, **float**, **double**, **void**
   - bool, wchar_t, auto

2. 控制流关键字 | Control Flow Keywords
   - **if**, **else**, **for**, **while**, **do**
   - **switch**, **case**, **break**, **continue**

3. 面向对象关键字 | OOP Keywords
   - class, private, public, protected
   - virtual, friend, this, new, delete

### 3.8 动态内存管理 (Dynamic Memory Management) 🟡

> 原文：C++ programs can use either static memory or dynamic memory during execution. Static memory is allocated at compile time, while dynamic memory is allocated at runtime.

#### 3.8.1 静态内存与动态内存 (Static vs Dynamic Memory)
```cpp
// 静态内存示例 | Static memory example
const int size = 5;
int arr[size];  // 编译时分配内存 | 数组的大小必须是常量，以便编译器在编译时能够确定所需的内存

// 动态内存示例 | Dynamic memory example
int n;
cout << "Enter array size: ";
cin >> n;
int* dynamicArr = new int[n];  // 运行时分配内存 | Memory allocated at runtime
```

#### 3.8.2 内存分配过程 (Memory Allocation Process)
1. 编译阶段 | Compilation Phase
   - 预处理：处理预处理指令 | Preprocessing: Handle preprocessor directives
   - 编译：转换为汇编语言 | Compilation: Convert to assembly
   - 汇编：生成目标文件 | Assembly: Generate object files
   - 确定静态内存需求 | Determine static memory requirements
   - 生成内存分配描述 | Generate memory allocation descriptions

2. 链接阶段 | Linking Phase
   - 合并目标文件 | Merge object files
   - 解决符号引用 | Resolve symbol references
   - 计算总内存需求 | Calculate total memory requirements
   - 生成可执行文件 | Generate executable file

3. 运行阶段 | Runtime Phase
   - 加载程序 | Load program
   - 分配内存 | Allocate memory
     - 代码段：程序指令 | Code segment: Program instructions
     - 数据段：全局和静态变量 | Data segment: Global and static variables
     - 堆：动态内存 | Heap: Dynamic memory
     - 栈：局部变量 | Stack: Local variables
   - 执行代码 | Execute code

#### 3.8.3 动态内存生命周期 (Dynamic Memory Lifecycle)
```cpp
void dynamicMemoryExample() {
    // 动态分配内存 | Dynamic memory allocation
    int* p = new int[5];
    
    // 使用内存 | Use memory
    p[0] = 10;
    
    // 释放内存 | Free memory
    delete[] p;
    p = nullptr;  // 防止悬空指针 | Prevent dangling pointer
}  // p的作用域结束，但如果没有delete，内存会泄漏 
    // p goes out of scope, but memory leaks if not deleted
```

#### 3.8.4 内存问题 (Memory Issues)
1. 内存泄漏 | Memory Leaks
```cpp
void memoryLeakExample() {
    int* p = new int[5];  // 分配内存 | Allocate memory
    p = new int[10];      // 原来的内存丢失 | Original memory lost
    // 内存泄漏：无法访问或释放第一次分配的内存
    // Memory leak: Can't access or free first allocation
}
```

2. 内存不足 | Out of Memory
```cpp
try {
    int* p = new int[1000000000];  // 尝试分配大量内存
} catch (std::bad_alloc& e) {
    cout << "内存分配失败 | Memory allocation failed" << endl;
}
```

#### 3.8.5 最佳实践 (Best Practices)
1. 总是配对使用 new 和 delete | Always pair new with delete
2. 释放后将指针设为 nullptr | Set pointers to nullptr after deletion
3. 使用智能指针管理内存 | Use smart pointers to manage memory
4. 避免内存泄漏 | Avoid memory leaks

#### 3.8.6 单个实例的动态内存 (Single Instance Dynamic Memory)
```cpp
// 单个实例的动态分配 | Single instance allocation
Student* harry = nullptr;   // 静态内存中的指针 | Pointer in static memory
harry = new Student;        // 动态内存中的Student对象 | Student in dynamic memory

// 使用对象 | Use the object
harry->no = 1234;
harry->grade = 85.5;

// 释放单个实例 | Deallocate single instance
delete harry;        // 不需要[] | No [] needed
harry = nullptr;     // 良好的编程习惯 | Good programming practice
```

#### 3.8.7 动态内存释放详解 (Dynamic Memory Deallocation Details)
```cpp
// 数组释放 | Array deallocation
int* arr = new int[5];
delete[] arr;    // 必须使用[]释放数组 | Must use [] for arrays

// 单个实例释放 | Single instance deallocation
int* p = new int;
delete p;        // 不使用[]释放单个实例 | No [] for single instances

// 错误示例 | Error examples
int* arr2 = new int[5];
delete arr2;     // 错误：只释放第一个元素 | Error: only frees first element

int* p2 = new int;
delete[] p2;     // 错误：对单个实例使用[] | Error: using [] for single instance
```

#### 3.8.8 完整示例程序 (Complete Example)
```cpp
// 动态内存分配示例 | Dynamic memory allocation example
#include <iostream>
using namespace std;

struct Student {
    int no;
    float grade[2];
};

int main() {
    int n;
    Student* student = nullptr;

    cout << "Enter the number of students: ";
    cin >> n;
    student = new Student[n];  // 动态分配内存 | Allocate memory

    // 输入数据 | Input data
    for (int i = 0; i < n; i++) {
        cout << "Student Number: ";
        cin >> student[i].no;
        cout << "Grade 1: ";
        cin >> student[i].grade[0];
        cout << "Grade 2: ";
        cin >> student[i].grade[1];
    }

    // 显示数据 | Display data
    for (int i = 0; i < n; i++) {
        cout << student[i].no << ": "
             << student[i].grade[0] << ", "
             << student[i].grade[1] << endl;
    }

    delete[] student;  // 释放内存 | Free memory
    student = nullptr;

    return 0;
}
```

## 4. 实践示例 (Practice Examples) 💻

### 4.1 类型和函数重载示例
```cpp
#include <iostream>
using namespace std;

class NumberProcessor {
public:
    // 函数重载示例 | Function overloading example
    void process(int x) {
        cout << "Processing integer: " << x << endl;
    }
    
    void process(double x) {
        cout << "Processing double: " << x << endl;
    }
    
    void process(string x) {
        cout << "Processing string: " << x << endl;
    }
};

int main() {
    NumberProcessor proc;
    proc.process(42);      // 调用int版本
    proc.process(3.14);    // 调用double版本
    proc.process("Hello"); // 调用string版本
    return 0;
}
```

## 5. 重要概念框架 (Key Concepts Framework) 🔍
```
C++类型和函数 | C++ Types and Functions
├── 类型系统 | Type System
│   ├── 基本类型 | Basic Types
│   │   ├── 整型 | Integer Types
│   │   └── 浮点型 | Floating Types
│   └── 复合类型 | Compound Types
│       └── 结构体 | Structures
├── 函数特性 | Function Features
│   ├── 重载 | Overloading
│   ├── 默认参数 | Default Parameters
│   └── 引用参数 | Reference Parameters
├── 内存管理 | Memory Management
│   ├── 静态内存 | Static Memory
│   ├── 动态内存 | Dynamic Memory
│   └── 内存释放 | Memory Deallocation
└── 作用域规则 | Scope Rules
    ├── 全局作用域 | Global Scope
    ├── 文件作用域 | File Scope
    └── 块作用域 | Block Scope
```

## 6. 学习建议 (Study Tips) 💡
1. 理解类型系统的基础 | Understand type system basics
2. 多练习函数重载 | Practice function overloading
3. 注意作用域规则 | Pay attention to scope rules
4. 掌握引用和指针的区别 | Master differences between references and pointers

## 7. FAQ (常见问题) ❓
1. 为什么需要函数重载？| Why need function overloading?
   - 提供统一的接口 | Provide unified interface
   - 增加代码可读性 | Improve code readability

2. 引用和指针有什么区别？| What's the difference between references and pointers?
   - 引用必须初始化 | References must be initialized
   - 引用不能改变指向 | References can't be reseated
   - 引用没有空值 | References can't be null

3. 什么时候使用动态内存？| When to use dynamic memory?
   - 运行时确定大小 | Size determined at runtime
   - 需要长期存储 | Need long-term storage
   - 内存使用灵活 | Flexible memory usage

4. 如何避免内存泄漏？| How to prevent memory leaks?
   - 配对使用new/delete | Pair new with delete
   - 使用智能指针 | Use smart pointers
   - 及时释放内存 | Free memory timely

5. 指针数组和数组指针有什么区别？| What's the difference between array of pointers and pointer to array?
   ```cpp
   Student* pStudent[NO_STUDENTS];     // 指针数组：每个元素是指针
   Student (*pStudent)[NO_STUDENTS];   // 数组指针：指向整个数组的指针
   
   // 访问方式不同 | Different access methods
   pStudent[i]->no;      // 指针数组访问
   (*pStudent)[i].no;    // 数组指针访问
   ```

6. 编译时分配的内存和运行时分配的内存有什么区别？| What's the difference between compile-time and runtime memory allocation?
   - 编译时分配 | Compile-time allocation:
     - 在编译阶段确定大小 | Size determined at compile time
     - 包括全局变量、静态变量 | Includes global and static variables
     - 在可执行文件中有描述 | Described in executable file
   - 运行时分配 | Runtime allocation:
     - 在程序运行时动态确定大小 | Size determined during execution
     - 使用new/delete管理 | Managed with new/delete
     - 更灵活但需要手动管理 | More flexible but requires manual management

7. 为什么编译时的内存分配描述在运行时才实际分配？| Why is compile-time memory allocation actually performed at runtime?
   - 编译时：生成内存分配的指令 | Compilation: Generates memory allocation instructions
   - 链接时：合并目标文件，解决符号引用 | Linking: Merges object files, resolves references
   - 运行时：操作系统根据可执行文件中的描述实际分配内存 | Runtime: OS allocates memory based on executable's description

8. 动态内存的生命周期是怎样的？| What is the lifecycle of dynamic memory?
   - 分配：使用new分配内存 | Allocation: Using new
   - 使用：通过指针访问内存 | Usage: Access through pointer
   - 释放：使用delete释放内存 | Deallocation: Using delete
   - 注意：指针超出作用域不会自动释放内存 | Note: Memory not automatically freed when pointer goes out of scope

## 8. 快速复习指南 (Quick Review Guide) 📝
- Day 1: 类型系统和函数重载
- Day 2: 引用和指针
- Day 3: 作用域和内存管理

## 9. 相关概念链接 (Related Concepts) 🔗
- [动态内存管理](./Dynamic_Memory.md)
- [类和对象](./Classes_and_Objects.md)
- [运算符重载](./Operator_Overloading.md)
