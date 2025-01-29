# OOP244 Week 5 - Member Operators 📚
https://intro2oop.sdds.ca/C-Encapsulation/member-operators

## 学习路径图 (Learning Path) 🗺️
```
Member Operators
├── Operations
│   ├── Operator Overloading Basics
│   ├── Candidates for Overloading
│   └── Operator Classification
├── Binary Operators
│   ├── Assignment
│   └── Arithmetic
├── Unary Operators
│   ├── Pre-fix Operations
│   └── Post-fix Operations
├── Type Conversion
│   ├── bool Operator
│   └── Cast Operations
└── Temporary Objects
    ├── Constructor Logic
    └── Design Tips
```

## 目录 (Table of Contents) 📑
1. [Operations](#operations)
2. [Binary Operators](#binary-operators)
3. [Unary Operators](#unary-operators)
4. [Type Conversion](#type-conversion)
5. [Temporary Objects](#temporary-objects)

## 知识点详解 (Detailed Content) 📝

### Operations (运算符操作) 🟢

#### 定义 | Definition
- 中文解释：运算符重载是为类类型的操作数定义运算符的过程。表达式由运算符和操作数组成，评估后得到特定类型的值。
- English: Operator overloading is the process of defining operators for operands of class type. An expression consists of an operator and operands, evaluating to a value of specific type.

#### 运算符重载语法 | Operator Overloading Syntax
```cpp
// 基本语法
return_type operator symbol (parameters);

// 示例：赋值运算符
Student& operator=(const Student&);
```

#### 可重载运算符 | Overloadable Operators 🟡
1. **二元算术运算符**:
   - `+` `-` `*` `/` `%`

2. **赋值运算符**:
   - `=` `+=` `-=` `*=` `/=` `%=`

3. **一元运算符**:
   - `++` `--` `+` `-`

4. **关系运算符**:
   - `==` `<` `>` `<=` `>=` `!=`

5. **逻辑运算符**:
   - `&&` `||` `!`

6. **输入输出运算符**:
   - `<<` `>>`

#### 不可重载运算符 | Non-overloadable Operators ⚠️
- 作用域解析运算符 `::`
- 成员选择运算符 `.`
- 成员指针选择运算符 `.*`
- 条件运算符 `?:`

### Binary Operators (二元运算符) 🟡

#### 定义 | Definition
- 中文解释：二元运算符需要两个操作数，左操作数是当前对象，右操作数作为参数传入。
- English: Binary operators require two operands, with the left operand being the current object and the right operand passed as a parameter.

#### 示例 | Example
```cpp
class Student {
public:
    // 加法赋值运算符
    Student& operator+=(float g) {
        if (no != 0 && ng < NG && g >= 0.f && g <= 100.f)
            grade[ng++] = g;
        return *this;
    }
};

// 使用示例
Student harry;
harry += 78.23f; // 添加一个成绩
```

### Unary Operators (一元运算符) 🟡

#### 前缀运算符 | Pre-fix Operators
```cpp
class Student {
public:
    // 前缀递增运算符
    Student& operator++() {
        for (int i = 0; i < ng; i++)
            if (grade[i] < 99.0f) grade[i] += 1.f;
        return *this;
    }
};
```

#### 后缀运算符 | Post-fix Operators
```cpp
class Student {
public:
    // 后缀递增运算符
    Student operator++(int) {
        Student s = *this;  // 保存原始值
        ++(*this);         // 调用前缀运算符
        return s;          // 返回原始值
    }


};
```

### Type Conversion (类型转换) 🟡

#### bool 运算符 | bool Operator
```cpp
class Student {
public:
    operator bool() const {
        return no != 0; // 如果学号非零则返回true
    }
};
```

#### 类型转换运算符 | Type Conversion Operators
```cpp
class Student {
public:
    // 单参数构造函数用于类型转换（显式）
    explicit Student(int sn) {
        float g[] = {0.0f};
        set(sn, g, 0);
    }
};
Student s1 = 123; // 错误，隐式构造函数写法
Student s2(123); // 正确，显式构造函数写法
```

### Temporary Objects (临时对象) 🟡

#### 构造函数逻辑本地化 | Localizing Constructor Logic
```cpp
Student::Student(int sn) {
    float g[] = {0.0f};
    *this = Student(sn, g, 0); // 使用临时对象
}
```

#### 设计提示 | Design Tips 💡
1. 使用临时对象避免重复逻辑
2. 确保运算符的行为符合直觉
3. 注意返回值的选择（引用vs值）
4. 谨慎使用类型转换运算符

### 参数提升与缩小 | Promotion or Narrowing of Arguments ⚠️
- 如果编译器无法找到与操作符签名的精确匹配，编译器将尝试进行复杂的选择过程，以找到最佳匹配，必要时将操作数值提升或缩小为相关类型。

## FAQ (常见问题) ❓

1. **为什么需要运算符重载？**
   - 使类对象能够使用自然的表达式语法
   - 提高代码的可读性和可维护性
   - 实现类型的自定义行为

2. **前缀和后缀运算符的区别是什么？**
   - 前缀：先增加再返回引用
   - 后缀：先返回原值，再增加
   - 后缀运算符参数列表中需要int参数

## 实践示例 (Practice Examples) 💻

### 完整示例：学生类运算符重载
```cpp
class Student {
    int no;
    float grade[NG];
    int ng;
public:
    // 赋值运算符
    Student& operator=(const Student& src) {
        if (this != &src) {
            no = src.no;
            ng = src.ng;
            for (int i = 0; i < ng; i++)
                grade[i] = src.grade[i];
        }
        return *this;
    }
    
    // 加法赋值运算符
    Student& operator+=(float g) {
        if (no != 0 && ng < NG && g >= 0.f && g <= 100.f)
            grade[ng++] = g;
        return *this;
    }
    
    // 类型转换运算符
    operator bool() const {
        return no != 0;
    }
};
```

## 学习建议 (Study Tips) 💡

1. 理解运算符重载的目的和限制
2. 注意保持运算符的自然语义
3. 合理使用临时对象优化代码
4. 谨慎使用类型转换运算符

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