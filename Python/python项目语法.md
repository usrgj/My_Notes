---
title: python项目语法
created: '2025-11-15T07:49:18.534Z'
modified: '2025-11-15T08:37:10.444Z'
---

python项目语法

# 包
## 包定义
使用`__init__.py`在目录的路径下显式地将当前目录标示为包
（在新版的python中，即使不显式地标记为 Python 包，某些情况下也能导入）
```
package/
  __init__.py
  module.py

可以嵌套子包
mypackage/
  __init__.py
  main.py
  subpackage/
    __init__.py
    utils.py
    helpers/
      __init__.py
      math_ops.py
```
## 包导入
使用`from .func`是相对于该文件的路径，而使用`from func`则是相对于运行程序时的路径
**方法1**
```python
# 在init中声明后，直接导入
from package import func1, class1

# 没有声明，可以直接导入包中的模块,或其子包
from package.func import func1
```
**方法2**
将包路径加入sys.path
**方法3**
安装为本地包

## `__init__.py`解释
`__init__.py`不仅能将目录标记为包，还能在首次导入该包时执行`__init__.py`文件中的代码
```python
'''
main.py
package/
  __init__.py
  func.py
'''
#main.py
from package import b
b()

#__init__.py
from .func import b
print(1)

#func.py
def b():
  print(2)
```
```bash
>> python main.py
1
2
```
### 应该写的内容
暴露出简洁的api
包的基本信息
`__init_.py`应该只是包的名片，应该尽可可能减少在导入包时的行为

### 定义``__all__``控制 `from package import *` 的行为
```python
# package/__init__.py
from .core import func1
from .utils import func2

__all__ = ["func1"]  # 只允许 func1 被 import *

# main
from package import *  # 只导入 func1，func2 不会被导入
```







