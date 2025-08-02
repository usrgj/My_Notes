---
tags: [cpp]
title: c++内置库
created: '2025-07-20T08:46:33.986Z'
modified: '2025-07-28T06:55:27.986Z'
---

c++内置库
# 目录

[fstream](#fstream)
[string](#string)
[map](#map)


## [fstream](https://cppreference.cn/w/cpp/header/fstream)
### 用途
在 C++ 中， `<fstream>` 是标准库中用于文件输入输出操作的类。它提供了一种方便的方式来读写文件。

fstream是iostream库的一部分，支持文本和二进制文件的读写。

fstream类是iostream库中的一个类，它继承自istream和ostream类，这意味着它既可以用于输入也可以用于输出。

### 基本用法
```c++
#include<fstream>
using namespace std;
fstream name; //创建对象
name.open("filename",mode);//打开文件

fstream name("filename")//上面两步也可以简略成这种写法

name.close();//关闭文件
```

mode有
|mode|含义|
|---|---|
|`std::ios::in`|以输入模式打开文件。|
|`std::ios::out`|以输出模式打开文件。|
|`std::ios::app`|以追加模式打开文件。|
|`std::ios::ate`|打开文件并定位到文件末尾。|
|`std::ios::trunc`|打开文件并截断文件，即清空文件内容。|


## [string](https://cppreference.cn/w/cpp/header/string)
### 使用
```cpp
string a = "ahidfoa";
string c (a.begin(),a.end())//使用迭代器，对a指定范围复制，左闭右开

void func(string & s);//传引用，为地址，避免拷贝
func(s); //调用
```
### 函数
#### find()
查找单个字符或子串
```c++
string s = "hello";
s.find("llo");//返回3
s.find("e");//返回1
s.find("a");//string::npos
```
#### substr()
截取子串
```cpp
string a = "ahidfoa";
string b = a.substr(1,3)//从索引1的位置开始，截取3个字符
```
#### empty()
~~~c++
s.empty()//返回bool值，为空返回true，不为空返回false
~~~
#### clear()
```c++
s.clear();//等价于s = "";
```

# 容器类
## [map](https://cppreference.cn/w/cpp/container/map)

### 用途
在 C++ 中，`<map>` 是标准模板库（STL）的一部分，它提供了一种关联容器，用于存储键值对（key-value pairs）。

map 容器中的元素是按照键的顺序自动排序的，这使得它非常适合需要快速查找和有序数据的场景。
***定义和特性***
* 键值对：map 存储的是键值对，其中每个键都是唯一的。
* 排序：map 中的元素按照键的顺序自动排序，通常是升序。
* 唯一性：每个键在 map 中只能出现一次。
* 双向迭代器：map 提供了双向迭代器，可以向前和向后遍历元素。
### 基本语法
```c++
#include<map>
using namespace std;

map<key_type, value_type> map_name; //声明一个map容器，键的类型和值的类型

map_name[key] = value; //访问或插入元素
a = map_name[key]; //访问元素

//遍历
    map<char,int> a;
    a['a'] = 1;
    a['b'] = 2;
    a['c'] = 3;
    for (map<char, int>::iterator it = a.begin(); it != a.end(); ++it) {
        std::cout << it->first << " => " << it->second << std::endl;
    }
    /*输出
    a => 1
    b => 2
    c => 3
    */

```

### 函数
以`a`为容器名
|函数名|作用|
|---|---|
|`a.find(key)`|查找键，返回迭代器，不存在时返回`a.end()`|
|`a.erase(key)`|删除元素|
|`a.clear()`|清空容器|
|`a.size()`|返回容器大小，返回类型`size_t`|
|`a.at(key)`|通过键访问，返回键对应的值|
|`a.begin()`|返回指向开头的迭代器，可通过`a.begin()->first来访问键` `a.begin()->second来访问值`|
|`a.empty()`|检查是否为空，返回bool值|
|`a.contains(key)`(c++20)|检查是否含有特定键，返回bool值,复杂度为容器大小的对数|
|`a.count(key)`|查找`key`出现的次数，只能返回0或1|
|``||
|``||

