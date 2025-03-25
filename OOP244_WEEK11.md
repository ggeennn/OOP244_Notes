# 模板（Templates）

模板是C++中实现**参数化多态（Parametric Polymorphism）**的一种方式，允许编写与类型无关的代码，从而提高代码的复用性。模板可以应用于函数和类。

## 1. 函数模板（Function Template）

### 1.1 模板语法
函数模板的定义类似于全局函数，但使用尖括号`<>`来指定模板参数。模板头的基本形式如下：

```cpp
template<typename T>
void swap(T& a, T& b) {
    T c;
    c = a;
    a = b;
    b = c;
}
```

- `template<typename T>`：定义模板，`T`是类型参数。
- `T`可以是任何类型（基本类型或复合类型）。

### 1.2 调用模板函数
调用模板函数时，编译器会根据传递的参数类型自动生成相应的函数实例。例如：

```cpp
double a = 2.3, b = 4.5;
swap(a, b); // 编译器生成 swap(double, double)
```

## 2. 类模板（Class Template）

类模板的语法与函数模板类似，允许定义与类型无关的类。例如：

```cpp
template <class T, int N>  //这里class T和typename T等效
class Array {
    T a[N];
public:
    T& operator[](int i) { return a[i]; }
};
```

- `template <class T, int N>`：定义类模板，`T`是类型参数，`N`是非类型参数（如整数）。
- 使用类模板时，需要指定类型参数和非类型参数：

```cpp
Array<int, 5> a; // 生成一个包含5个int元素的数组
```

## 3. 受限类型转换（Constrained Casts）

C++提供了四种受限类型转换操作符，以提高类型安全性：

### 3.1 `static_cast<Type>(expression)`
-用于`相关类型`之间的转换，如将`int`转换为`double`。编译器会进行有限的类型检查。

```cpp
double hours = static_cast<double>(minutes) / 60;
```

### 3.2 `reinterpret_cast<Type>(expression)`
-用于不相关类型之间的转换，`rejects conversions between related types`。编译器进行最少的类型检查(`保持bit pattern一致，重新编译`)。

```cpp
int* p = reinterpret_cast<int*>(x);
```

### 3.3 `const_cast<Type>(expression)`
-用于移除`const`修饰符(类型一致)，通常用于处理非`const`参数的函数，`rejects conversions between different types`。

```cpp
int* b = const_cast<int*>(a);
```

### 3.4 `dynamic_cast<Type>(expression)`
用于类层次结构中的类型转换，如将基类指针转换为派生类指针。
-编译器会进行运行时类型检查。（`向下cast必须要包含virtual以进行类型检查，确保cast的对象（src）是派生的`）

```cpp
Derived* d = dynamic_cast<Derived*>(b);
```

## 4. 总结

- **模板**：允许编写与类型无关的代码，提高代码复用性。
- **函数模板**：用于定义与类型无关的函数。
- **类模板**：用于定义与类型无关的类。
- **受限类型转换**：提供更安全的类型转换方式，避免绕过类型系统。

## 5. 练习

- 阅读Wikipedia上关于模板的文章，进一步理解模板的应用场景和最佳实践。

---

**参考资料**：
- [C++ Templates - Wikipedia](https://en.wikipedia.org/wiki/Template_(C%2B%2B))
- [Seneca College - Introduction to Object Oriented Programming (C++)](https://intro2oop.sdds.ca/E-Polymorphism/templates)
