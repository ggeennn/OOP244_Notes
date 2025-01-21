# OOP244 Week 3 - Member Functions and Privacy 📚
https://intro2oop.sdds.ca/C-Encapsulation/member-functions-and-privacy
## 学习路径图 (Learning Path) 🗺️
```
Member Functions & Privacy
├── Member Functions Basics
│   ├── Declaration & Definition
│   └── Function Scope & Access
├── Privacy Concepts
│   ├── Accessibility Control
│   └── Class vs Struct
└── Input/Output Operations
    ├── cin Operations
    └── cout Operations
```

## 目录 (Table of Contents) 📑
1. [Member Functions](#member-functions)
2. [Privacy](#privacy)
3. [Empty State](#empty-state)
4. [Input and Output Examples](#input-and-output-examples)

## 知识点详解 (Detailed Content) 📝

### Member Functions (成员函数) 🟢

#### 定义 | Definition
- 中文解释：成员函数是类中定义的函数，用于提供类与客户端代码之间的通信链接。
- English: Member functions provide communication links between client code and objects of the class. They are functions defined within a class that can access and operate on class data.

#### 成员函数分类 | Member Function Categories 
1. **Queries (查询函数)** 🟢
   - 也称为访问器方法 (accessor methods)
   - 用于报告对象的状态
   - 不修改对象的数据
   - 通常使用 `const` 限定符

2. **Modifiers (修改函数)** 🟢
   - 也称为修改器方法 (mutator methods)
   - 改变对象的状态
   - 可以修改对象的数据

3. **Special (特殊函数)** 🟡
   - 也称为管理方法 (manager methods)
   - 负责对象的创建、赋值和销毁

#### 成员函数声明与定义 | Declaration & Definition 🟢

```cpp
// 声明示例 | Declaration Example
class Student {
private:
    int no;
    float grade[NG];
    int ng; // 成员变量定义
public:
    void display() const; // The const qualifier identifies the member function as a query.
    void set(int id, const float* grades, int count); // 修改函数声明
    void initialize(); // 特殊函数声明
};

// 定义示例 | Definition Example
void Student::display() const {
    cout << no << ": \n";
    for (int i = 0; i < ng; i++)
        cout << grade[i] << endl;
}
void Student::set(int id, const float* grades, int ng_) {
    no = id;
    ng = ng_<NG?ng_:NG;
    for (int i = 0; i < ng; i++)
        grade[i] = grades[i];
}

// 定义成员函数     特殊函数定义示例 | Special Example
void Student::initialize(int id, int count) {
    studentId_ = id; // 访问成员变量
    numGrades_ = count; // 访问成员变量
    // 可以在这里调用 display() 函数
    ::display(); // calls the global function(display:another function defined globally)
    display(); // 直接调用同一类中的另一个成员函数
}



// 在主函数中, Client code calls a member function in the same way that an instance of a struct refers to one of its data members.
Student harry; // 创建结构体对象
harry.studentId_ = 123; // 访问并设置成员变量
harry.display(); // 调用成员函数
```

💡 实践提示 | Practice Tips
- 声明在类定义内部
- 定义在类定义外部
- 定义时需要使用作用域解析运算符（Scope Resolution Operator） `::`
- `const` 成员函数不能修改对象的数据
- The Student:: prefix on the function name identifies it as a member of our Student type
- 在类外部定义成员函数时，需要使用类名和作用域解析运算符 `::` 来标识该函数是类的成员函数。

### Privacy (私有性) 🟡

#### 定义 | Definition
- 中文解释：数据私有性是封装的核心概念，用于限制对类成员的访问权限。
- English: Data privacy is central to encapsulation. It controls access to class members and helps hide implementation details.

#### 访问标签 | Access Labels 🟢
1. **private:**
   - 默认情况下 class 的成员是私有的
   - 只能被类的成员函数访问
   
2. **public:**
   -  struct 的成员默认公有
   - 可以被任何代码访问
   - 通常用于接口函数

```cpp
class Student {
//class成员默认 private:
    int no;
    float grade[NG];
    int ng;
public:
    void set(int, const float*, int);
    void display() const;
};
```

### Empty State (空状态) 🟡

#### 定义 | Definition
- 中文解释：空状态是对象的一种特殊状态，表示对象不包含有效数据。
- English: Empty state is a special state that identifies the absence of valid data in an object.

#### 设计建议 | Design Tips 💡
1. 选择一个数据成员来标识空状态
2. 在验证失败时将对象置于空状态
3. 所有成员函数都应该考虑空状态的处理

```cpp
void Student::set(int sn, const float* g, int ng_) {
    if (sn < 1) {
        no = 0; // 设置空状态
    } else {
        // 存储有效数据
        no = sn;
        // ...
    }
}
```

### Input and Output Examples (输入输出示例) 🟢

#### cin 操作 | cin Operations
1. **基本输入语法** 🟢
```cpp
// 基本语法
cin >> variable;  // 基本输入操作

// 多变量输入示例
int i;
char c;
double x;
char s[8];
cin >> i >> c >> x >> s;  // 可以连续读取多个值
```

2. **输入特性** 🟢
- 自动跳过前导空白字符（空格、制表符、换行符）
- 对数值类型、字符串类型和字符类型都会跳过空白
- 类似于 C 语言中的 `scanf("%d")`, `scanf("%lf")`, `scanf("%s")`, `scanf(" %c")`

3. **特殊成员函数** 🟡
```cpp
// ignore() 示例
cin.ignore();           // 忽略一个字符
cin.ignore(2000, '\n'); // 忽略最多2000个字符或直到遇到换行符

// get() 和 getline() 示例
char ch;
cin.get(ch);           // 读取单个字符，包括空白字符
char str[100];
cin.getline(str, 100); // 读取一行，直到遇到换行符
```

#### cout 操作 | cout Operations

1. **字段宽度控制** 🟢
```cpp
int attendance = 27;
cout << "1234567890" << endl;    // 用于对齐参考
cout.width(10);                  // 设置下一个输出字段宽度为10
cout << attendance << endl;      // 输出: "        27"
cout << attendance << endl;      // 输出: "27" (width设置仅对下一个字段有效)
```

2. **填充字符设置** 🟢
```cpp
cout.fill('*');                  // 设置填充字符为 '*'
cout.width(10);
cout << attendance << endl;      // 输出: "********27"
// 填充字符设置会持续有效，直到被重新设置
```

3. **格式化控制** 🟡
```cpp
double pi = 3.141592653;

// 固定格式
cout.setf(ios::fixed);          // 设置固定格式
cout.precision(2);              // 设置精度为小数点后2位
cout << pi << endl;             // 输出: "3.14"

// 科学计数法
cout.unsetf(ios::fixed);        // 取消固定格式
cout.setf(ios::scientific);     // 设置科学计数法
cout << pi << endl;             // 输出: "3.141593e+00"

// 对齐控制
cout.setf(ios::left);           // 左对齐
cout.width(10);
cout << pi << endl;             // 输出: "3.14      "
cout.unsetf(ios::left);         // 取消左对齐
```

4. **格式标志持续性** ⚠️
```cpp
// 重要注意事项：
// 1. width() 设置仅对下一个输出字段有效，字段宽度包含小数点
// 2. fill() 设置持续有效直到被重置
// 3. precision() 设置持续有效直到被重置，默认6位
// 4. setf() 设置的格式标志持续有效直到被 unsetf()
```

5. **精度控制** 🟡
```cpp
double value = 123.456789;

// 一般格式（默认）
cout.precision(6);              // 设置精度为6
cout << value << endl;          // 输出: "123.457"

// 固定格式
cout.setf(ios::fixed);
cout.precision(2);
cout << value << endl;          // 输出: "123.46"

// 科学计数法
cout.setf(ios::scientific);
cout << value << endl;          // 输出: "1.23e+02"
```

### 格式化输出的注意事项 ⚠️

1. **字段宽度 (width)**
   - 只影响下一个输出操作
   - 如果数据长度超过设定宽度，则完整显示数据
   - 默认右对齐

2. **填充字符 (fill)**
   - 持续有效直到被重新设置
   - 默认使用空格字符
   - 在设定的字段宽度内填充未被数据占用的空间

3. **格式标志 (setf/unsetf)**
   - 多个格式标志可以同时使用
   - 某些标志之间可能相互冲突
   - 使用 unsetf() 可以取消之前的设置

4. **精度设置 (precision)**
   - 在不同格式下有不同的含义
   - 一般格式：控制有效数字
   - 固定格式：控制小数位数
   - 科学计数法：控制小数位数
   - 一直控制输出直到改变精度（默认6位）

## FAQ (常见问题) ❓

1. **为什么需要成员函数？**
   - 提供类与外部的接口
   - 保护数据的安全性
   - 实现封装的概念

2. **class 和 struct 的区别是什么？**
   - class 默认成员为 private
   - struct 默认成员为 public
   - 在面向对象编程中推荐使用 class

## 实践示例 (Practice Examples) 💻

### 基础示例：学生类实现
```cpp
class Student {
private:
    int studentId_;
    float grades_[20];
    int numGrades_;

public:
    // 设置学生信息
    void set(int id, const float* grades, int count);
    // 显示学生信息
    void display() const;
};
```

## 学习建议 (Study Tips) 💡

1. 先理解封装的概念，再学习具体实现
2. 多练习成员函数的声明和定义
3. 注意 const 成员函数的使用
4. 理解并实践数据隐藏的重要性

## 版本控制 (Version Control) 🔄
```
更新日期：2024-03-19
版本号：v1.0
更新内容：
- 初始化文档
- 添加所有基础概念
- 添加示例代码
```

[End of Document] 