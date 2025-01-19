# OOP244 Week 3 - Member Functions and Privacy 📚

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
struct Student {
    int no;
    float grade[NG];
    int ng; // 成员变量定义
    
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

// 修改函数定义示例 | Modifier Example
void Student::set(int id, const float* grades, int count) {
    studentId_ = id; // 修改学生ID
    numGrades_ = count; // 设置成绩数量
    for (int i = 0; i < count; i++) {
        grades_[i] = grades[i]; // 存储成绩
    }
}

// 特殊函数定义示例 | Special Example
void Student::initialize() {
    studentId_ = 0; // 初始化学生ID
    numGrades_ = 0; // 初始化成绩数量
    for (int i = 0; i < 20; i++) {
        grades_[i] = 0.0f; // 初始化成绩为0
    }
}
```

💡 实践提示 | Practice Tips
- 声明在类定义内部
- 定义在类定义外部
- 定义时需要使用作用域解析运算符 `::`
- `const` 成员函数不能修改对象的数据

### Privacy (私有性) 🟡

#### 定义 | Definition
- 中文解释：数据私有性是封装的核心概念，用于限制对类成员的访问权限。
- English: Data privacy is central to encapsulation. It controls access to class members and helps hide implementation details.

#### 访问标签 | Access Labels 🟢
1. **private:**
   - 默认情况下 class 的成员是私有的
   - 只能被类的成员函数访问
   
2. **public:**
   - 可以被任何代码访问
   - 通常用于接口函数

```cpp
class Student {
private:
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
1. **基本输入** 🟢
```cpp
cin >> variable;  // 基本输入操作
```

2. **特殊成员函数** 🟡
- `ignore()`: 忽略输入缓冲区的字符
- `get()`: 获取字符
- `getline()`: 获取一行

#### cout 操作 | cout Operations
1. **格式化输出** 🟢
```cpp
cout.width(10);    // 设置字段宽度
cout.fill('*');    // 设置填充字符
cout.precision(2); // 设置精度
```

2. **格式标志** 🟡
```cpp
cout.setf(ios::fixed);      // 固定格式
cout.setf(ios::scientific); // 科学计数法
cout.setf(ios::left);      // 左对齐
```

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