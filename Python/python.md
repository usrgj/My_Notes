# 工厂模式

## 简单工厂模式 (Simple Factory Pattern)

简单工厂模式不是GoF（Gang of Four）定义的23种设计模式之一，但它经常被用作理解更复杂的工厂方法模式的起点。简单工厂模式的核心思想是将对象的创建集中在一个单独的工厂类中，客户端只需要知道传入什么参数就可以获取相应的产品对象，而不需要关心具体实现。

```python
# 定义产品接口或基类
class Shape:
    def draw(self):
        pass

# 具体产品类
class Circle(Shape):
    def draw(self):
        print("Drawing Circle")

class Rectangle(Shape):
    def draw(self):
        print("Drawing Rectangle")

class Square(Shape):
    def draw(self):
        print("Drawing Square")

# 工厂类
class ShapeFactory:
    @staticmethod
    def get_shape(shape_type: str) -> Shape:
        if shape_type == "circle":
            return Circle()
        elif shape_type == "rectangle":
            return Rectangle()
        elif shape_type == "square":
            return Square()
        else:
            raise ValueError(f"Unknown shape type: {shape_type}")

# 使用工厂
if __name__ == "__main__":
    # 获取 Circle 的对象
    shape1 = ShapeFactory.get_shape("circle")
    shape1.draw()

    # 获取 Rectangle 的对象
    shape2 = ShapeFactory.get_shape("rectangle")
    shape2.draw()

    # 获取 Square 的对象
    shape3 = ShapeFactory.get_shape("square")
    shape3.draw()
```

## 工厂方法模式 (Factory Method Pattern)

工厂方法模式是定义了一个创建对象的接口，但由子类决定要实例化的类是哪一个。工厂方法让类的实例化推迟到子类。

### abc模块

abc 是 Python 的标准库中的一个模块，代表 "Abstract Base Classes"（抽象基类）。它提供了用于定义抽象基类的机制。抽象基类不能被实例化，它们通常用于为其他类提供通用接口或实现一部分功能，让子类继承并实现剩余的功能。

### 抽象基类

抽象基类的特性

    抽象方法：一个没有实现的方法，它要求任何非抽象子类都必须提供自己的实现。Python 中可以通过 abc 模块的 @abstractmethod 装饰器来定义。

    抽象属性：类似于抽象方法，但用于属性。可以用 @property 和 @abstractmethod 一起装饰来定义。

    不能实例化：你不能直接创建一个抽象基类的对象；它们只能被继承。

```python
from abc import ABC, abstractmethod

# 定义抽象基类
class AbstractClassExample(ABC):

    def __init__(self, value):
        self.value = value
        super().__init__()

    @abstractmethod
    def do_something(self):
        """这是一个抽象方法，子类必须实现"""
        pass

# 尝试实例化会失败，因为这是个抽象类
# instance = AbstractClassExample()  # TypeError: Can't instantiate abstract class AbstractClassExample with abstract method do_something

# 创建具体的子类，并实现抽象方法
class ConcreteClass(AbstractClassExample):

    def do_something(self):
        return f"Doing something with value {self.value}."

# 现在可以实例化具体子类
instance = ConcreteClass(10)
print(instance.do_something())  # 输出：Doing something with value 10.
```

### 接口

在面向对象编程（OOP）中，接口 是一种抽象类型，它定义了一组操作（方法），但不提供这些操作的具体实现。接口的作用是规定一个类必须实现哪些方法和属性，而不关心具体的实现细节。通过接口，可以确保不同类之间有一致的行为，即使它们的内部逻辑可能完全不同。

在Python中，虽然没有专门的接口关键字，但是可以通过定义全是抽象方法的类来模拟接口。

## 类

### what's class

在面向对象编程（OOP）中，类（Class） 是一种用户自定义的数据类型，它封装了数据和操作这些数据的方法。类是创建对象的蓝图或模板，通过类可以创建多个具有相同属性和行为的对象（实例）。类不仅定义了对象的结构（即它包含哪些属性），还定义了对象的行为（即它可以执行哪些操作）。

以下是关于类的一些关键概念：

    属性（Attributes）：类中的变量，用于描述对象的状态。它们可以是实例变量（每个对象都有自己的副本）或类变量（所有实例共享）。

    方法（Methods）：类中定义的函数，用于定义对象的行为。方法可以访问和修改对象的状态。

    构造函数（Constructor）：一种特殊的方法，通常用于初始化新创建的对象状态。在 Python 中，    构造函数是名为    `__init__` 的方法。

    继承（Inheritance）：新类可以从现有的类派生，从而复用代码、扩展功能或修改现有行为。

    多态性（Polymorphism）：允许子类以不同的方式实现从父类继承来的方法，即同一个方法名可以在不同类中有不同的实现。

    封装（Encapsulation）：将数据和操作数据的方法绑定在一起，并隐藏对象的内部表示，仅暴露必要的接口给外部使用。

### usage

在 Python 中，\`class\` 是面向对象编程（OOP）的核心概念之一。通过 \`class\` 可以创建自定义数据类型，这些类型不仅包含数据（属性），还可以包含操作这些数据的方法。下面我们将详细介绍如何基础使用 \`class\`，包括定义类、创建实例、定义方法和属性等。

### 1. 定义一个类

使用 \`class\` 关键字来定义一个新的类。类名通常采用 PascalCase 命名法（每个单词的首字母大写）。

\`\`\`python

class MyClass:

    # 类体可以包含属性和方法

    pass  # 使用 pass 表示空体

\`\`\`

### 2. 初始化方法 (\`\_\_init\_\_\`)

\`\_\_init\_\_\` 方法是类的构造函数，用于初始化新创建的对象状态。它在创建类的新实例时自动调用。

\`\`\`python

class Person:

    def \_\_init\_\_(self, name, age):

        self.name = name  # 实例属性

        self.age = age    # 实例属性

\`\`\`

### 3. 定义方法

方法是与类关联的函数。它们可以访问和修改对象的状态。所有实例方法的第一个参数总是 \`self\`，代表实例本身。

\`\`\`python

class Person:

    def \_\_init\_\_(self, name, age):

        self.name = name

        self.age = age

    def greet(self):

        print(f"Hello, my name is {self.name} and I am {self.age} years old.")

\`\`\`

### 4. 创建实例

创建类的实例就是根据类的定义创建具体的对象。使用类名后跟一对括号，并传递必要的参数给 \`\_\_init\_\_\` 方法。

\`\`\`python

person1 = Person("Alice", 30)

person1.greet()  # 输出: Hello, my name is Alice and I am 30 years old.

\`\`\`

### 5. 访问属性和方法

你可以直接使用点符号（\`.\`）来访问实例的属性和调用方法。

\`\`\`python

print(person1.name)  # 输出: Alice

person1.greet()     # 调用方法

\`\`\`

### 6. 类属性 vs 实例属性

\- \*\*类属性\*\*：定义在类中但在方法之外，属于整个类而不是特定的实例。

\- \*\*实例属性\*\*：定义在 \`\_\_init\_\_\` 或其他方法内部，属于特定的实例。

\`\`\`python

class Person:

    species = "Homo sapiens"  # 类属性

    def \_\_init\_\_(self, name, age):

        self.name = name      # 实例属性

        self.age = age        # 实例属性

# 所有实例共享类属性

print(Person.species)         # 输出: Homo sapiens

person2 = Person("Bob", 25)

print(person2.species)      # 输出: Homo sapiens

print(person2.name)      # 输出bob

# 通过 self.\_\_class\_\_ 访问类属性

### 7. 静态方法和类方法

除了实例方法外，Python 还支持静态方法和类方法：

\- \*\*静态方法\*\*：使用 \`@staticmethod\` 装饰器定义，不接收隐式的第一个参数（如 \`self\` 或 \`cls\`），因此不能访问或修改类或实例的状态。

\- \*\*类方法\*\*：使用 \`@classmethod\` 装饰器定义，接收类作为第一个参数 \`cls\`，可以用来访问或修改类的状态。

\`\`\`python

class MyClass:

    @staticmethod

    def static\_method():

        print("This is a static method.")

    @classmethod

    def class\_method(cls):

        print(f"This is a class method of {cls.\_\_name\_\_}.")

MyClass.static\_method()  # 输出: This is a static method.

MyClass.class\_method()   # 输出: This is a class method of MyClass.

\`\`\`

### 8. 继承

继承允许一个类从另一个类那里获取属性和方法。子类可以扩展或覆盖父类的行为。

\`\`\`python

class Animal:

    def speak(self):

        return "Some sound"

class Dog(Animal):

    def speak(self):  # 方法重写

        return "Woof"

dog = Dog()

print(dog.speak())  # 输出: Woof

\`\`\`

### 总结

以上是 Python 中 \`class\` 的基础使用方法。通过定义类，我们可以创建结构化的代码，使得程序更易于理解、维护和扩展。类和对象的概念是构建复杂软件系统的基础，帮助我们更好地组织和管理代码。如果你刚开始学习面向对象编程，建议多实践这些基本概念，逐步掌握更高级的主题，如抽象基类、接口、组合等。

### 规定了必须实现的方法而不需要具体的实现逻辑(抽象基类)

如果你完全不懂编程，理解“规定了必须实现的方法而不需要具体的实现逻辑”可能会有些抽象。为了帮助你更好地理解这个概念，我们可以用现实生活中的例子来类比。

### 比喻：烹饪食谱

想象一下，你在准备一顿晚餐，并且有了一份食谱。这份食谱列出了你需要完成的一系列步骤（方法），比如“切菜”、“煮汤”和“摆盘”。但是，它并没有告诉你具体要切什么菜、煮什么汤或如何摆盘——这些细节取决于你想做什么菜肴以及你手头有什么食材。

#### 食谱相当于：

\- \*\*抽象基类\*\* 或 \*\*接口\*\*：它定义了你必须完成的任务（方法），但没有给出具体的做法。

#### 任务（如“切菜”）相当于：

\- \*\*抽象方法\*\*：它们是食谱中列出的步骤，但没有详细的执行方式。

#### 实际烹饪过程相当于：

\- \*\*具体类\*\*：当你决定做一道特定的菜肴时，你就创建了一个具体的类，它实现了食谱中所有的步骤（方法）。例如，如果你选择做意大利面，那么你会具体说明如何切洋葱、如何煮番茄酱以及如何装饰你的盘子。

### 应用到编程中

在编程里，我们也有类似的机制：

\- \*\*抽象基类或接口\*\* 告诉我们一个对象应该能够做什么（比如，“动物应该会发声”），但不告诉我们它是怎么做的。

\- \*\*抽象方法\*\* 是那些没有具体实现的方法名，比如 \`speak()\` 方法，它表示所有动物都应该能发出声音，但不同的动物会有不同的叫声。

\- \*\*具体类\*\* 提供了实际的实现，比如 \`Dog\` 类可能实现 \`speak()\` 方法为 “汪汪叫”，而 \`Cat\` 类则实现为 “喵喵叫”。

### 简单的例子

假设我们有一个名为 \`Animal\` 的抽象基类，它有一个抽象方法 \`speak()\`。然后我们有两个具体类 \`Dog\` 和 \`Cat\`，它们都继承自 \`Animal\` 并实现了 \`speak()\` 方法。

```python
```python
from abc import ABC, abstractmethod

# 定义一个抽象基类 Animal
class Animal(ABC):
    @abstractmethod              #这是一个装饰器，表明下面的方法是抽象的，所有继承自 Animal                                  #的具体类都必须实现这个方法。
    def speak(self):
        pass                     # 这里定义了 speak 方法，
                                 #但没有提供具体的实现逻辑（使用 pass 表示空操作）。
                                 #这意味 ”着任何继承自 Animal 的具体类都需要提供自己的 
                                 #speak 方法实现。”

# Dog 类实现了 speak 方法
class Dog(Animal):
    def speak(self):
        return "汪汪"

# Cat 类也实现了 speak 方法
class Cat(Animal):
    def speak(self):
        return "喵喵"

# 使用这些类
dog = Dog()
cat = Cat()

print(dog.speak())  # 输出: 汪汪
print(cat.speak())  # 输出: 喵喵
```
```

在这个例子中，\`Animal\` 类就像是一份食谱，它说所有的动物都应该会发声，但它没有告诉我们具体的声音是什么样的。\`Dog\` 和 \`Cat\` 类就像是根据食谱准备的具体菜肴，它们各自给出了自己的实现。

希望这个比喻和简单的例子可以帮助你更直观地理解“规定了必须实现的方法而不需要具体的实现逻辑”的含义。这种设计模式有助于确保代码结构清晰，并且让不同类型的对象可以以一致的方式被使用，同时保持灵活性。

### 继承

继承（Inheritance）是面向对象编程（OOP）中的一项核心特性，它允许一个类从另一个类那里获取属性和方法。通过继承，新类（子类或派生类）可以复用现有类（父类或基类）的代码，同时还可以添加新的功能或修改已有行为。这有助于提高代码的重用性和可维护性，并且简化了程序的设计。

在Python中，继承可以通过在类定义时将父类名放在括号内来实现，可以同时继承多个父类

```python
class ParentClass:
    def parent_method(self):
        print("This is a method from the parent class.")

class ChildClass(ParentClass):
    def child_method(self):
        print("This is a method from the child class.")
```

### 方法重写（Overriding）

如果子类中定义了一个与父类同名的方法，那么子类中的方法会覆盖父类中的方法。这种现象叫做方法重写。这允许子类改变或扩展其父类的行为。

```python
class Animal:
    def speak(self):
        return "Some sound"

class Dog(Animal):
    def speak(self):  # 方法重写
        return "Woof"

dog = Dog()
print(dog.speak())  # 输出: Woof
```

### 调用父类的方法

有时候，你可能想要调用父类中的方法，即使子类已经重写了该方法。这可以通过使用 `super()` 函数来实现。

```python
class Animal:
	def speak(self):
		return "Some sound"

class Dog(Animal):
	def speak(self):
		return super().speak() + ", but the dog says Woof"

dog = Dog()
print(dog.speak())  # 输出: Some sound, but the dog says Woof
```

### 为什么是self？

`class Cat(Animal):`

    `def speak(self):`

        `return "喵喵"`

在 Python 中，类的方法定义中使用 `self` 参数是因为 Python 的面向对象编程特性。当你在一个类内部定义方法时，`self` 是一个约定俗成的名字，用来表示实例本身。它作为第一个参数传递给每一个实例方法，使得方法可以访问实例的属性和其他方法。

### 为什么是cls?

在Python的类方法中，cls 是一个约定俗成的名字（类似于实例方法中的 self），用于指代类本身。当类方法被调用时，类本身会自动作为第一个参数传递给该方法，这个参数通常命名为 cls。这使得你可以在类方法内部引用类属性或调用其他类方法。

cls 在 \_\_new\_\_ 方法中的作用

特别地，在 \_\_new\_\_ 方法中，cls 指代的是正在被实例化的类。这是因为 \_\_new\_\_ 是一个静态方法（尽管它不需要使用 @staticmethod 装饰器），它负责创建类的新实例。当你尝试通过 MyClass() 创建一个对象时，实际上是先调用了 MyClass.\_\_new\_\_(cls, ...)，这里的 cls 就是 MyClass。

### \_\_new\_\_

\_\_new\_\_ 是一个在 Python 类中用于创建类实例的特殊静态方法。它在对象实例化过程中被调用，负责实际生成一个新的类实例，并将其返回。与 \_\_init\_\_ 方法不同，\_\_init\_\_ 是初始化一个已经创建的实例，而 \_\_new\_\_ 是负责创建这个实例。

\_\_new\_\_ 方法的工作流程

当你使用类名后跟括号（例如 MyClass()）来创建一个类的实例时，实际上是经历了一个两步的过程：

    调用 \_\_new\_\_ 方法：首先会调用 \_\_new\_\_ 方法来创建类的一个新实例。这个方法是静态的，默认情况下由 Python 的 object 基类提供实现。

    调用 \_\_init\_\_ 方法：一旦有了新的实例，就会调用该实例上的 \_\_init\_\_ 方法来进行初始化。

为什么需要重写 \_\_new\_\_ 方法？

通常情况下，你不需要重写 \_\_new\_\_ 方法，因为默认的行为对于大多数类来说都是足够的。然而，在某些特定场景下，如实现单例模式、不可变类型或当你要控制实例的创建过程时，就需要重写 \_\_new\_\_ 方法了。

# `**->**`

在Python 3.5及更高版本中，`->` 用于指定函数的返回值注解（return annotation）。这是类型提示（type hints）的一部分，也称为类型标注，它允许开发者为函数参数和返回值指定预期的数据类型。

类型提示是可选的，并不会影响程序的运行时行为；它们主要用于静态分析工具、IDE和其他开发工具来帮助发现潜在的错误或提供更好的代码完成建议等。此外，第三方库如 `mypy` 可以用来检查类型注解是否被正确使用。

# try 和 except

 是 Python 中用于异常处理的关键字。它们允许你定义一块代码，在执行这段代码时如果发生错误，可以捕获这些错误并进行处理，而不是让程序崩溃。通过这种方式，你可以编写更健壮、更能应对意外情况的代码。

```python
try:
    # 这里放置可能会引发异常的代码
    risky_operation()
except SomeExceptionType:
    # 如果在 try 部分引发了 SomeExceptionType 异常，则会执行这里的代码
    print("Caught an exception of type SomeExceptionType")



try:
    # 可能引发异常的操作
    operation()
except ValueError:
    print("Caught a ValueError")
except TypeError:
    print("Caught a TypeError")
else :
  print("right")   #没有异常时执行，可选


  

try:
    file = open('file.txt', 'r')
    # 文件读取操作...
except IOError:
    print("An IOError occurred.")
finally:
    file.close()  # 确保文件总是被关闭#无论是否异常都执行

  
  
```

捕获异常信息，当捕获异常时，可以通过 `as` 关键字将异常对象绑定到一个变量，从而获取有关异常的更多信息

```python
try:
    # 操作可能引发异常
    some_op()
except SomeExceptionType as e:
    print(f"Caught an exception: {e}")  # 打印异常信息
```

### raise

\`raise\` 是 Python 中的一个关键字，用于手动触发异常。当你希望在特定条件下中断程序的正常执行流程，并抛出一个异常时，你可以使用 \`raise\` 语句。这可以用来报告错误或特殊情况，使调用者能够处理这些情况。

### 使用方式

\`raise\` 可以以几种不同的方式使用：

1. \*\*直接抛出异常\*\*：你可以直接抛出一个内置的异常类型，如 \`ValueError\`, \`TypeError\` 等。

2. \*\*抛出自定义异常\*\*：你也可以定义自己的异常类（通常继承自 \`Exception\` 类），然后使用 \`raise\` 抛出它们。

3. \*\*重新抛出异常\*\*：在异常处理器中，如果你想在处理了异常之后再次抛出它，可以使用不带参数的 \`raise\`。

### 示例代码

#### 直接抛出异常

\`\`\`python

def check\_positive(num):

    if num <= 0:

        raise ValueError("The number must be positive.")

    return num

try:

    print(check\_positive(-1))

except ValueError as e:

    print(e)  # 输出: The number must be positive.

\`\`\`

#### 抛出自定义异常

首先，定义一个自定义异常类：

\`\`\`python

class MyCustomError(Exception):

    """A custom exception type."""

    pass

def risky\_function():

    raise MyCustomError("An error occurred in risky\_function.")

try:

    risky\_function()

except MyCustomError as e:

    print(e)  # 输出: An error occurred in risky\_function.

\`\`\`

#### 重新抛出异常

\`\`\`python

try:

    # 假设这里有一个函数调用，它可能抛出异常

    some\_function\_that\_raises()

except Exception as e:

    # 处理异常后，如果需要，可以再次抛出

    print("Caught an exception, re-raising it...")

    raise  # 这里会抛出原始异常

\`\`\`

### 注意事项

\- 当你抛出异常时，可以选择性地提供一个描述性的消息，这有助于调试和理解问题所在。

\- 如果你不捕获异常，它将传播到调用栈的上层，直到被捕获或者导致程序终止。

\- 使用 \`raise\` 语句来确保你的代码能够正确响应各种错误条件，这是一种良好的编程实践，有助于提高代码的健壮性和可维护性。

### \`\*\*kwargs\`

 是 Python 中用于函数定义的一个特殊语法，它允许你传递任意数量的关键字参数给函数。\`kwargs\` 是 "keyword arguments"（关键字参数）的缩写。当你不确定需要传递多少个关键字参数给函数时，或者你希望函数能够接受未来可能会添加的额外关键字参数，你可以使用 \`\*\*kwargs\`。

### 使用方式

\- \*\*在函数定义中\*\*：\`\*\*kwargs\` 用来接收所有未明确指定的关键字参数，并将它们作为字典传递给函数。

\- \*\*调用函数时\*\*：如果你有一个字典，并且想要将其所有的键值对作为关键字参数传递给一个函数，可以使用 \`\*\*\` 操作符来解包字典。

### 示例代码

#### 函数定义中的 \`\*\*kwargs\`

\`\`\`python

def my\_function(\*\*kwargs):

    for key, value in kwargs.items():

        print(f"{key} = {value}")

# 调用函数并传递多个关键字参数

my\_function(name="Alice", age=30, city="Beijing")

\`\`\`

这段代码会输出：

\`\`\`

name = Alice

age = 30

city = Beijing

\`\`\`

#### 解包字典为关键字参数

\`\`\`python

def greet(name, greeting="Hello"):

    print(f"{greeting}, {name}!")

# 定义一个字典，其中包含关键字参数

params = {"name": "Bob", "greeting": "Hi"}

# 使用 \*\* 来解包字典，作为关键字参数传递给函数

greet(\*\*params)

\`\`\`

这将会打印：

\`\`\`

Hi, Bob!

\`\`\`

### 注意事项

\- \`\*\*kwargs\` 必须是函数定义中的最后一个参数，因为它收集所有剩余的关键字参数。

\- 如果你的函数同时接受普通参数、\`\*args\` 和 \`\*\*kwargs\`，它们的顺序应该是这样的：普通参数 -> \`\*args\` -> \`\*\*kwargs\`。

\- 在函数内部，\`kwargs\` 是一个普通的 Python 字典，因此你可以像操作任何其他字典一样对其进行操作。

\- 当你不需要使用这些参数的名字时，通常使用 \`\*\*kwargs\` 作为参数名是一种惯例，但其实你可以使用任何有效的变量名，只要前面加上 \`\*\*\` 即可。

### 实际应用

\`\*\*kwargs\` 常见于库和框架的设计中，特别是那些需要高度灵活性和扩展性的部分。例如，许多图形用户界面（GUI）工具包允许你通过 \`\*\*kwargs\` 传递组件属性，而无需为每个可能的属性定义单独的参数。这使得 API 更加简洁和易于使用。

# JSON

### 基本结构

JSON 文件由键值对组成，其中键必须是字符串，而值可以是字符串、数字、数组、布尔值、null 或者另一个 JSON 对象。

### 注意事项

    键必须是字符串：所有的键都必须用双引号包裹。

    值的类型：根据需要选择合适的值类型（字符串、数字、布尔值、数组、对象或 null），并确保使用正确的语法。

    避免尾随逗号：虽然某些编程语言允许在最后一个元素后面加逗号，但标准 JSON 不允许这样做。

    保持格式一致：为了提高可读性，建议使用一致的缩进和换行符。

##   读取

### 一般步骤

    打开文件：使用适当的文件打开方法（如 open() 函数）打开包含 JSON 数据的文件。

    读取内容：从文件中读取数据。可以一次性读取整个文件内容，也可以逐行读取。

    解析 JSON：使用专门的库函数将读取到的字符串形式的 JSON 数据转换为程序中的数据结构。

    处理数据：一旦 JSON 数据被成功解析成相应的数据结构，就可以像操作普通的数据结构一样对其进行操作了。

在 Python 中读取 JSON 文件

Python 提供了一个内置模块 json，它包含了处理 JSON 数据的功能。下面是如何使用这个模块来读取 JSON 文件的例子。

示例 JSON 文件 (data.json)

假设我们有一个名为 data.json 的文件，其内容如下：

```json
{
    "name": "Tom",
    "age": 30,
    "isStudent": false,
    "address": {
        "street": "123 Main St",
        "city": "Anytown"
    },
    "phoneNumbers": [
        "123-456-7890",
        "098-765-4321"
    ],
    "spouse": null
}
```

使用 Python 读取 JSON 文件

```python
import json

# 打开并读取 JSON 文件
with open('data.json', 'r', encoding='utf-8') as file:
    data = json.load(file)  # 解析 JSON 数据

# 现在 data 是一个 Python 字典
print(data['name'])  # 输出: Tom
print(data['address']['city'])  # 输出: Anytown
print(data['phoneNumbers'][0])  # 输出: 123-456-7890
```

# （模块）[**rich**](https://rich.readthedocs.io/en/latest/index.html)

使用 Rich 库可以极大地提升你在终端应用中输出的内容的表现力。下面是一个简单的指南，帮助你开始使用 Rich。

### 安装 Rich

首先，你需要安装 Rich 库。可以通过 pip 来安装：

\`\`\`bash

pip install rich

\`\`\`

## ### 基本使用

Rich 提供了多种方式来增强你的终端输出。这里有几个基本的例子来展示如何使用它。

#### 1. 添加颜色和样式

你可以通过 \`rich.print\` 方法轻松地为文本添加颜色和样式。

\`\`\`python

from rich import print

print("\[bold magenta\]Hello, world!\[/bold magenta\]")

\`\`\`

在这个例子中，"Hello, world!" 将以粗体和洋红色显示。

#### 2. 使用 Console 对象

Rich 的 \`Console\` 类允许更细致的控制输出。

\`\`\`python

from rich.console import Console

console = Console()

console.print("Hello", "World!", style="bold underline red")

\`\`\`

这个例子将 "Hello World!" 打印为带有下划线的粗体红色文本。

## #### 3. 显示表格

Rich 可以非常方便地创建和打印表格。

\`\`\`python

from rich.table import Table

from rich.console import Console

table = Table(show\_header=True, header\_style="bold magenta")

table.add\_column("Date", style="dim", width=12)

table.add\_column("Title")

table.add\_column("Production Budget", justify="right")

table.add\_column("Box Office", justify="right")

table.add\_row(

    "Dec 20, 2019", "Star Wars: The Rise of Skywalker", "$275,000,000", "$375,126,118"

)

table.add\_row(

    "May 25, 2018",

    "\[red\]Solo\[/red\]: A Star Wars Story",

    "$275,000,000",

    "$392,714,407",

)

table.add\_row(

    "Dec 15, 2017",

    "Star Wars Ep. VIII: The Last Jedi",              #当传入数据集时，用\*解包数据集

    "$262,000,000",

    "\[bold\]$1,332,539,889\[/bold\]",

)

console = Console()

console.print(table)

\`\`\`

这段代码创建了一个表格，并填充了一些数据行，包括一些带有颜色和样式的单元格。

## #### 4. 进度条

这些只是 Rich 功能的一部分。根据你的需求，你可以探索更多高级用法，比如日志记录增强、渲染 Markdown 和 JSON 等等。希望这能帮助你入门！如果有任何具体的问题或需要进一步的帮助，请随时提问。

# （模块）[**argparse**](https://blog.csdn.net/RudeTomatoes/article/details/117003291)

## \`nargs\` 

是 Python 的 \`argparse\` 模块中的一个参数，用于指定命令行参数应当消耗的命令行参数个数。它允许你定义一个参数可以接受多少个值，并且可以根据需要灵活地调整这个数量。\`nargs\` 可以接受多种不同的值，包括整数、特殊字符（如 \`'?'\`, \`'\*'\`, \`'+'\`），每个都有其特定的意义和用途。

### \`nargs\` 的常见用法

#### 1. 整数值

你可以指定一个具体的整数值给 \`nargs\`，这表示该参数期望接收的确切数量的命令行参数。

\`\`\`python

import argparse

parser = argparse.ArgumentParser()

parser.add\_argument('--nums', nargs=3, type=int)

args = parser.parse\_args(\['--nums', '1', '2', '3'\])

print(args.nums)  # 输出: \[1, 2, 3\]

\`\`\`

在这个例子中，\`--nums\` 参数期望接收三个整数作为输入。

#### 2. \`'?'\`

当 \`nargs='?'\` 时，表示该参数是可选的，如果提供了，则只取一个值；如果没有提供，则使用默认值或 \`None\`。

\`\`\`python

parser.add\_argument('--optional', nargs='?', default='default\_value')

args = parser.parse\_args(\[\])

print(args.optional)  # 输出: default\_value

args = parser.parse\_args(\['--optional', 'value'\])

print(args.optional)  # 输出: value

\`\`\`

#### 3. \`'\*'\`

\`nargs='\*'\` 表示该参数可以接收零个或多个值，并将它们作为一个列表返回。

\`\`\`python

parser.add\_argument('--files', nargs='\*', type=str)

args = parser.parse\_args(\['--files', 'file1.txt', 'file2.txt'\])

print(args.files)  # 输出: \['file1.txt', 'file2.txt'\]

args = parser.parse\_args(\[\])

print(args.files)  # 输出: \[\]

\`\`\`

#### 4. \`'+'\`

\`nargs='+'\` 类似于 \`'\*'\`，但它至少要求提供一个值。

\`\`\`python

parser.add\_argument('numbers', nargs='+', type=int)

args = parser.parse\_args(\['1', '2', '3'\])

print(args.numbers)  # 输出: \[1, 2, 3\]

# 如果没有提供任何参数，则会报错

\`\`\`

#### 5. 特殊情况：解析剩余的所有参数

如果你想要某个参数吸收掉所有后续的命令行参数，可以结合 \`nargs=argparse.REMAINDER\` 使用。

\`\`\`python

parser.add\_argument('first\_arg')

parser.add\_argument('remaining\_args', nargs=argparse.REMAINDER)

args = parser.parse\_args(\['first', 'second', 'third', '--fourth'\])

print(args.first\_arg)         # 输出: first

print(args.remaining\_args)    # 输出: \['second', 'third', '--fourth'\]

\`\`\`

### 总结

\- \*\*整数\*\*：指定确切的数量。

\- \*\*\`'?'\`\*\*：零个或一个参数，默认值可用。

\- \*\*\`'\*'\`\*\*：零个或多个参数，返回列表。

\- \*\*\`'+'\`\*\*：一个或多个参数，返回列表。

\- \*\*\`argparse.REMAINDER\`\*\*：吸收所有后续参数，不论是什么。

通过合理利用 \`nargs\`，你可以创建非常灵活的命令行接口，适应各种不同的输入需求。根据你的应用逻辑选择合适的 \`nargs\` 值，可以让用户更方便地与你的程序进行交互。

# （模块）[**subprocess**](https://www.runoob.com/w3cnote/python3-subprocess.html)

# （模块）[**tqdm**](https://blog.csdn.net/wxd1233/article/details/118371404)

# （模块）[**re**](https://blog.csdn.net/guo_qingxia/article/details/113979135)

基本概念

    正则表达式：是一种用来匹配字符串的强大工具。它由普通字符（如字母、数字）和特殊字符（称为元字符）组成，这些元字符具有特殊的含义。

# [**with**](https://blog.csdn.net/zhaoxilengfeng/article/details/144382104)

with context\_manager as variable:

                # 执行代码块

其中，`context_manager` 是一个实现了上下文管理协议的对象，`variable` 是可选的，用于接收 `__enter__` 方法返回的值。

# [**单例模式**](https://www.cnblogs.com/huchong/p/8244279.html)

```python
class Logger(object):
    #一个单例日志记录器
    logger = None

    def __new__(cls, *args, **kwargs):
        if cls.logger is None:
            cls.logger = super(Logger, cls).__new__(cls)

            cls.logger = log_form = Table(show_header=True, header_style="bold blue", box=ASCII, show_lines=True)
            log_form.add_column('Library')
            log_form.add_column('Version')
            log_form.add_column('Info')

        return cls.logger # 返回已有的实例（无论是新创建的还是之前已经存在的）
```