1. 多态的基础概念

   定义：
   多态是指通过基类指针或引用调用派生类对象的函数，运行时根据对象的实际类型（dynamic type）决定调用哪个实现。
   中文：一个接口（interface），多种实现（implementation）。

   实现方式：
   使用虚函数（virtual function）和抽象基类（abstract base class）。
   例子：
   Sorter* sorter = new SelectionSorter();
   sorter->sort(arr, n);
   调用 SelectionSorter 的 sort()。
2. 抽象基类与纯虚函数

   抽象基类：
   包含纯虚函数（virtual void func() = 0;）的类，不能实例化。
   作用：定义接口，强制派生类实现。
   例子：Sorter 类定义 virtual void sort(float* a, int n) = 0;，派生类必须实现。

   纯虚函数：
   没有实现（= 0），只定义函数签名（function signature）。
   函数签名：函数名 + 参数列表（不包括返回类型）。
   例子：display(std::ostream&) 的签名是 display(std::ostream&)，派生类必须匹配签名。

   继承与实现：
   派生类必须实现所有纯虚函数，否则也变成抽象类。
   例子：Student 继承 iPerson，必须实现 display()，否则不能实例化。

3. 虚函数与动态分派

   虚函数：
   使用 virtual 关键字标记，运行时通过 vtable（虚函数表）动态分派（dynamic dispatch）。
   例子：iPerson 的 display() 是虚函数，Student::display() 覆盖它。

   vtable 和 vptr：
   编译器为每个包含虚函数的类生成 vtable，存储虚函数地址。
   对象内存中包含 vptr（虚函数表指针），指向 vtable。
   内存布局：对象内存 = [vptr][基类成员][派生类成员]。
   例子：new Student() 创建对象，vptr 指向 Student 的 vtable，调用 display() 时查找 vtable 中的地址。

   虚性传递：
   基类的虚函数（如析构函数）是 virtual，派生类的同名函数（即使不显式声明 virtual）也参与动态分派。
   例子：Base::~Base() 是 virtual，即使 Derived1::~Derived1() 不是 virtual，析构时仍动态调用。
4. 内存管理相关知识点（重点）

   虚析构函数：
   作用：确保通过基类指针删除派生类对象时，正确调用派生类的析构函数。
   例子：Base* ptr = new Derived1_1(); delete ptr; 如果 Base::~Base() 不是 virtual，只调用 Base::~Base()，可能导致内存泄漏。
   规则：
   基类析构函数必须是 virtual，否则析构不完整。
   中文：就像拆房子（对象），要从最顶层（派生类）拆到最底层（基类）。
   析构顺序：
   析构从最派生类（most derived class）开始，逆序到基类。
   例子：Derived1_1 → Derived1 → Base。

   内存泄漏风险：
   问题：
   如果基类析构函数不是 virtual，delete ptr 只调用基类的析构函数，派生类的资源未释放。
   例子：Student 分配了动态数组（如 grade），但未析构，内存泄漏。
   解决：
   确保基类析构函数是 virtual。
   使用智能指针（如 std::unique_ptr）自动管理内存。
   智能指针改进：
   问题：手动 delete 容易忘记，引发泄漏。
   例子：Sorter* sorter = new SelectionSorter(); 如果忘记 delete sorter，内存泄漏。
   改进：使用 std::unique_ptr 或 std::shared_ptr。
   例子：auto sorter = std::make_unique<SelectionSorter>(); 自动释放。

5. 接口分离与低耦合

   接口分离：
   客户端代码只依赖抽象基类接口（如 iPerson 或 Sorter），不直接依赖具体类（如 Student 或 SelectionSorter）。
   例子：iPerson* person = new Student(); person->display(std::cout); 只依赖 iPerson 接口。

   低耦合：
   具体类的实现（.cpp 文件）对客户端是隐藏的，客户端只需知道接口（.h 文件）。
   例子：main.cpp 不直接包含 Student.cpp，通过 iPerson 访问。

   工厂模式：
   进一步隐藏具体类创建，客户端通过工厂函数（如 CreatePerson()）创建对象。
   问题：原工厂模式（如 CreatePerson()）耦合了用户输入逻辑。
   改进：将输入逻辑分离，工厂只负责创建。
   例子：createSorter(SortType type) 只创建对象，不处理输入。

6. 容易混淆的内存管理细节

   虚析构函数的必要性：
   混淆点：如果基类析构函数不是 virtual，通过基类指针删除对象时，只调用基类析构函数。
   后果：派生类的析构函数未调用，动态资源（如 new int[]）未释放。
   例子：Base* ptr = new Derived1_1(); delete ptr; 如果 Base::~Base() 非 virtual，Derived1_1::~Derived1_1() 不执行。
   解决：基类析构函数总是设为 virtual。

   手动内存管理：
   混淆点：忘记 delete 或重复 delete 导致泄漏或崩溃。
   例子：iPerson* p = new Student(); 如果不 delete p，内存泄漏。
   改进：使用智能指针。
   例子：std::vector<std::unique_ptr<iPerson>> people; 自动释放。

   动态分派与对象内存：
   混淆点：vptr 占用对象内存，可能误以为对象大小只包含数据成员。
   例子：Student 对象包含 [vptr][Person::name][Student::no][Student::grade][Student::ng]。
   细节：vptr 指向 vtable，vtable 存放在 .rodata 段，函数机器码在 .text 段。
7. 其他相关知识点

   函数签名：
   函数签名包括函数名和参数列表，不包括返回类型。
   混淆点：误以为返回类型是签名的一部分。
   例子：void run(int) 和 int run(int) 不能重载，因为签名相同。

   虚函数机器码：
   虚函数的机器码存放在 .text 段，vtable 存放在 .rodata 段，vtable 中的指针指向 .text 段的函数地址。

内存管理常见混淆点总结

   虚析构函数遗漏：
   问题：基类析构函数非 virtual，派生类析构不执行。
   解决：总是将基类析构函数设为 virtual。

   手动 delete 忘记：
   问题：new 后忘记 delete，导致内存泄漏。
   解决：使用 std::unique_ptr 或 std::shared_ptr。

   对象内存误解：
   问题：忽略 vptr 占用的内存。
   解决：了解对象包含 vptr，指向 vtable。

   析构顺序：
   问题：误以为析构顺序与构造相同。
   解决：析构逆序，从最派生类到基类。

中英对照关键点

   多态 (Polymorphism)：
   中文：通过基类接口调用派生类实现。
   英文：Calling derived class implementations through a base class interface。

   虚析构函数 (Virtual Destructor)：
   中文：确保正确析构派生类对象。
   英文：Ensures proper destruction of derived class objects。

   vtable 和 vptr：
   中文：虚函数表和指针，用于动态分派。
   英文：Virtual function table and pointer for dynamic dispatch。

   智能指针 (Smart Pointer)：
   中文：自动管理内存，避免泄漏。
   英文：Automatically manages memory to prevent leaks。