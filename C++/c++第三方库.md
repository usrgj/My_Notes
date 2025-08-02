---
tags: [cpp]
title: c++第三方库
created: '2025-07-21T14:11:54.030Z'
modified: '2025-07-22T03:49:43.212Z'
---

c++第三方库
# 目录

# [nlohmann/json](https://github.com/nlohmann/json)
让c++支持json
在release中下载json.hpp即可使用
### 基本用法
~~~c++
 //命名空间
using json = nlohmann::json;

//读取
ifstream ifs("package.json");
json data = json::parse(ifs);
//读取json的对象时，会按照键的字典序排序

//通过键访问值
data[name]

//通过迭代器访问键值对
for (auto it = data.begin(); it != data.end(); it++) {
        cout << it.key() << " " << it.value().dump() << endl;
    }
~~~

### 函数
在上面的命名空间下
|函数|作用|
|---|---|
|`json::array({value,value,...})`|创建并返回一个数组，留空时返回一个空数组|
|`json::({})`|留空时返回一个空对象|
|`json::object()`|返回一个空对象|
|``||
|``||
|``||
|``||

