特殊成员函数 | 默认行为 | 调用基类行为 | 非默认行为（需要干预） | 注意事项
--- | --- | --- | --- | ---
析构函数 (Destructor) | 自动调用基类析构函数，但基类析构函数不是 virtual 时只调用基类部分。 | 基类析构函数（~Base()）在派生类析构后自动调用。 | 基类析构函数必须设为 virtual，否则派生类资源不释放，导致内存泄漏。 | 总是将基类析构函数设为 virtual，确保逐层释放资源（Derived → Base）。
拷贝构造函数 (Copy Constructor) | 逐一复制基类和派生类成员（浅拷贝），自动调用基类的拷贝构造函数（如果可访问）。 | 基类拷贝构造函数（Base(const Base&)）在初始化列表中自动调用。 | 如果有动态资源，需显式定义深拷贝，调用基类拷贝构造函数并为派生类资源分配新内存。 | 基类拷贝构造函数必须可访问（public 或 protected）。
拷贝赋值运算符 (Copy Assignment Operator) | 逐一赋值基类和派生类成员（浅拷贝），自动调用基类的赋值运算符（如果可访问）。 | 基类赋值运算符（Base::operator=()）在函数体中自动调用。 | 如果有动态资源，需显式定义深拷贝，调用基类赋值运算符并为派生类资源重新分配内存，注意自赋值检查。 | 基类赋值运算符必须可访问，避免资源泄漏（释放旧资源前检查）。
移动构造函数 (Move Constructor) | 逐一移动基类和派生类成员（C++11 默认生成），自动调用基类的移动构造函数。 | 基类移动构造函数（Base(Base&&)）在初始化列表中自动调用。 | 如果有动态资源，需显式定义，调用基类移动构造函数并转移派生类资源，避免不必要的深拷贝。 | 默认行为可能不安全，显式定义更可靠。
移动赋值运算符 (Move Assignment Operator) | 逐一移动基类和派生类成员（C++11 默认生成），自动调用基类的移动赋值运算符。 | 基类移动赋值运算符（Base::operator=(Base&&)）在函数体中自动调用。 | 如果有动态资源，需显式定义，调用基类移动赋值运算符并转移派生类资源，注意自赋值检查。 | 默认行为可能不安全，显式定义更可靠。

表格解释与代码示例

#自定义派生类的
1.拷贝构造函数：
如果忘记显式调用基类的拷贝构造函数，编译器会默认调用基类的无参数构造函数
2.赋值运算符：
如果忘记显式调用基类的拷贝赋值运算符，基类部分不会被赋值（保持原值）
*非自定义则会默认调用基类相应函数/运算符

1. 析构函数 (Destructor)
默认行为：
编译器为派生类生成默认析构函数，自动调用基类析构函数，但如果基类析构函数不是 virtual，通过基类指针删除时只调用基类析构。
需要干预：
基类析构函数必须是 virtual，否则派生类资源未释放。
代码：
```cpp
class Base {
public:
    int* basePtr = new int(10);
    ~Base() { delete basePtr; } // 非 virtual
};

class Derived : public Base {
public:
    int* derivedPtr = new int(20);
    ~Derived() { delete derivedPtr; }
};

int main() {
    Base* ptr = new Derived();
    delete ptr; // 只调用 Base::~Base()
}
```
问题：derivedPtr 未释放。
修正：virtual ~Base() { delete basePtr; }

2. 拷贝构造函数 (Copy Constructor)
默认行为：
自动调用基类拷贝构造函数，逐一复制派生类成员。
需要干预：
如果有动态资源，需定义深拷贝。

//当您在派生类中显式定义拷贝构造函数时，编译器不会自动调用基类的拷贝构造函数。
因此，您需要显式地在派生类的拷贝构造函数的初始化列表中调用基类的拷贝构造函数，以确保基类的数据成员也被正确地复制。
```cpp
class Derived : public Base {
    int* derivedPtr;
public:
    Derived(const Derived& other) : Base(other) { // 显式调用基类
        derivedPtr = new int(*other.derivedPtr); // 深拷贝
    }
};
```
3. 拷贝赋值运算符 (Copy Assignment Operator)
默认行为：
自动调用基类赋值运算符，逐一赋值派生类成员。
需要干预：
定义深拷贝，显式调用基类赋值。

```cpp
Derived& operator=(const Derived& other) {
    if (this != &other) {
        Base::operator=(other); // 调用基类赋值
        delete derivedPtr;
        derivedPtr = new int(*other.derivedPtr); // 深拷贝
    }
    return *this;
}
```

4. 移动构造函数和移动赋值运算符
默认行为：
C++11 自动生成，调用基类的移动函数。
需要干预：
显式定义以转移资源，避免深拷贝。

```cpp
Derived(Derived&& other) noexcept : Base(std::move(other)) {
    derivedPtr = other.derivedPtr;
    other.derivedPtr = nullptr;
}
```

教学重点（网页背景）
网页主题：
讨论多层继承中资源管理问题，强调默认行为可能导致资源泄漏或重复释放。
需要干预的原因：
基类和派生类都有资源时，默认行为（浅拷贝、非虚析构）不安全。
程序员必须显式定义特殊成员函数，确保资源正确管理。
调用基类的关系：
派生类的特殊成员函数需要显式调用基类的对应函数（比如 Base(other) 或 Base::operator=(other)）。
中英对照关键点
特殊成员函数 (Special Member Functions)：
中文：析构、拷贝、移动等函数。
英文：Destructor, copy, move functions.
虚析构函数 (Virtual Destructor)：
中文：确保派生类资源释放。
英文：Ensures derived class resource cleanup.
深拷贝 (Deep Copy)：
中文：复制指针指向的内存。
英文：Copies memory pointed to by pointers.


