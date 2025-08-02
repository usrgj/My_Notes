---
tags: [cpp]
title: c++语法进阶
created: '2025-07-30T03:59:14.073Z'
modified: '2025-08-01T06:58:55.850Z'
---

c++语法进阶

# [**class**](https://www.runoob.com/cplusplus/cpp-classes-objects.html)

类是 C++ 中面向对象编程（OOP）的核心概念之一。你可以把类想象成一个“蓝图”或“模板”，它定义了一类对象的属性和行为。通过类，你可以创建具体的对象（也称为实例），这些对象拥有类中定义的属性和方法。

## **1. 类的定义**

类由两部分组成：

- 数据成员（属性）：描述对象的特征。
- 成员函数（方法）：描述对象的行为。

```c++
class Dog {
public:
    // 数据成员（属性）
    std::string name;
    int age;

    // 成员函数（方法）
    void bark() {
        std::cout << name << " says: Woof! Woof!" << std::endl;
    }

    void celebrateBirthday() {
        age++;
        std::cout << name << " is now " << age << " years old!" << std::endl;
    }
};
```

## **2. 创建对象**

类是抽象的，而对象是类的具体实例。通过类，你可以创建多个对象。

```c++
int main() {
    // 创建对象
    Dog myDog;
    myDog.name = "Buddy";
    myDog.age = 3;

    // 调用成员函数
    myDog.bark();
    myDog.celebrateBirthday();
}
```

## **3. 访问控制**

C++ 提供了访问控制关键字，用于限制类成员的访问权限：

- `public`：类外可以访问。
- `private`：只有类内部的成员函数可以访问。
- `protected`：类内部和派生类可以访问。

## **4. 构造函数和析构函数**

## **5. 类的其他特性**

- 静态成员：属于类本身，而不是某个对象。
- 友元函数：允许外部函数访问类的私有成员。
- 继承：可以从一个类派生出新的类，实现代码复用。
- 多态：通过虚函数实现运行时多态。

## **6. 类的实际意义**

- 封装：将数据和方法封装在一起，隐藏实现细节。
- 复用：通过继承和组合，复用已有的代码。
- 抽象：通过类定义对象的抽象模型，简化复杂系统的设计。

# **inheritance**

类的继承（Inheritance）是 C++ 中面向对象编程（OOP）的核心概念之一。它允许一个类（派生类/子类）基于另一个类（基类/父类）来构建，继承基类的属性和行为，并可以扩展或修改这些属性和行为。继承的主要目的是实现代码复用和层次化设计。

在现代 C++ 中，继承不仅仅是简单的代码复用工具，还可以结合 多态、抽象类、接口 等特性，构建灵活且可扩展的软件系统。



------

## **继承的基本语法**

```c++
class Base {
public:
    void baseMethod() {
        std::cout << "Base method" << std::endl;
    }
};

class Derived : public Base { // Derived 继承 Base
public:
    void derivedMethod() {
        std::cout << "Derived method" << std::endl;
    }
};
```

- `Base` 是基类（父类）。
- `Derived` 是派生类（子类），通过 `: public Base` 继承 `Base`。
- `Derived` 可以访问 `Base` 的 `public` 和 `protected` 成员。

------

## **继承的访问控制**

C++ 中有三种继承方式，决定了派生类对基类成员的访问权限：

1. `public` 继承：
   - 基类的 `public` 成员在派生类中仍然是 `public`。
   - 基类的 `protected` 成员在派生类中仍然是 `protected`。
   - `基类的` `private` 成员不可访问。

```c++
class Derived : public Base {
    // Base 的 public 和 protected 成员在 Derived 中保持原有访问权限
};
```

1. `protected` 继承：
   - 基类的 `public` 和 `protected` 成员在派生类中都变为 `protected`。
   - 基类的 `private` 成员不可访问。

```c++
class Derived : protected Base {
    // Base 的 public 和 protected 成员在 Derived 中都变为 protected
};
```

1. `private` 继承：
   - 基类的 `public` 和 `protected` 成员在派生类中都变为 `private`。
   - 基类的 `private` 成员不可访问。

```c++
class Derived : private Base {
    // Base 的 public 和 protected 成员在 Derived 中都变为 private
};
```

------

## **继承中的构造函数和析构函数**

1. 构造函数调用顺序：
   - 先调用基类的构造函数，再调用派生类的构造函数。

```c++
class Base {
public:
    Base() { std::cout << "Base constructor" << std::endl; }
};

class Derived : public Base {
public:
    Derived() { std::cout << "Derived constructor" << std::endl; }
};

Derived d; // 输出: Base constructor -> Derived constructor
```

1. 析构函数调用顺序：
   - 先调用派生类的析构函数，再调用基类的析构函数。

```c++
class Base {
public:
    ~Base() { std::cout << "Base destructor" << std::endl; }
};

class Derived : public Base {
public:
    ~Derived() { std::cout << "Derived destructor" << std::endl; }
};

Derived d; // 输出: Derived destructor -> Base destructor
```

------

## **多态与虚函数**

多态（Polymorphism）是继承的一个重要特性，允许派生类重写基类的行为。通过 虚函数（`virtual`）和 动态绑定，可以在运行时调用正确的函数。

#### 示例：多态

```c++
class Base {
public:
    virtual void print() { // 虚函数
        std::cout << "Base print" << std::endl;
    }
};

class Derived : public Base {
public:
    void print() override { // 重写基类的虚函数
        std::cout << "Derived print" << std::endl;
    }
};

int main() {
    Base* ptr = new Derived(); // 基类指针指向派生类对象
    ptr->print(); // 输出: Derived print（动态绑定）
    delete ptr;
    return 0;
}
```

- `override` 关键字（C++11）用于显式标记重写的虚函数。https://www.runoob.com/w3cnote/c-templates-detail.html
- `virtual` 关键字用于声明虚函数，支持动态绑定。

------

## **纯虚函数与抽象类**

纯虚函数（Pure Virtual Function）是一种没有实现的虚函数，用于定义接口。包含纯虚函数的类称为 抽象类，不能实例化。

#### 示例：抽象类

```c++
class Shape { // 抽象类
public:
    virtual void draw() = 0; // 纯虚函数
};

class Circle : public Shape {
public:
    void draw() override {
        std::cout << "Drawing a circle" << std::endl;
    }
};

int main() {
    Shape* shape = new Circle();
    shape->draw(); // 输出: Drawing a circle
    delete shape;
    return 0;
}
```

------

## **多重继承**

C++ 支持多重继承，即一个类可以从多个基类继承。虽然强大，但容易引发 菱形继承问题（Diamond Problem），需要通过 虚继承 解决。

#### 示例：多重继承

```c++
class A {
public:
    void foo() { std::cout << "A::foo" << std::endl; }
};

class B {
public:
    void bar() { std::cout << "B::bar" << std::endl; }
};

class Derived : public A, public B { // 多重继承
};

int main() {
    Derived d;
    d.foo(); // 调用 A::foo
    d.bar(); // 调用 B::bar
    return 0;
}
```

------

## **总结**

类的继承是 C++ 中实现代码复用和多态的重要机制。通过继承，可以构建层次化的类结构，结合虚函数和抽象类实现多态，并通过多重继承扩展功能。现代 C++ 还引入了 `override`、`final` 等关键字，使继承更加安全和清晰。


# [模板template](https://www.runoob.com/w3cnote/c-templates-detail.html)
> 模板是创建泛型类或函数的**蓝图**或公式。

## 函数模板
### 定义
```c++
// class关键字可以使用typename,type是数据类型的占位符
// <>括号中的参数叫模板形参，模板形参和函数形参很相像，模板形参不能为空。
// 调用该模板函数时，传入的实参会初始化模板形参
template <class 形参名，class 形参名，......> 返回类型 函数名(参数列表) {//body}
```
### 使用
```cpp
template <typename T>
void  Swap(T& a, T& b){
    T temp = a;
    a = b;
    b = temp;
}
int main (){
    int i = 39, j = 20;
    Swap(i,j);
    cout << i << endl;//输出20

    double f1 = 13.5, f2 = 20.7;
    Swap(f1,f2);
    cout << f1 << endl;//20.1

    string s1 = "Hello", s2 = "World";
    Swap(s1,s2);
    cout << s1;//world

    return 0;
}
```

## 类模板
### 定义
```c++
//类似于函数模板
template <class  形参名，class 形参名，…> class 类名{};
```

### **使用**

#### **类模板对象的创建：**

比如一个模板类A，则使用类模板创建对象的方法为`A<int> m`;在类A后面跟上一个<>尖括号并在里面填上相应的类型，这样的话类A中凡是用到模板形参的地方都会被int 所代替。当类模板有两个模板形参时创建对象的方法为`A<int, double> m`;类型之间用逗号隔开。

#### 在类模板外部定义成员函数的方法为：

```c++
template<模板形参列表> 函数返回类型 类名<模板形参名>::函数名(参数列表){函数体}，
template<class T1,class T2> void A<T1,T2>::h(){}。
// 注意：当在类外面定义类的成员时template后面的模板形参应与要定义的类的模板形参一致。
```





