---
title: python基础语法及规范
created: '2025-11-15T07:33:36.256Z'
modified: '2025-11-15T07:38:33.503Z'
---

python基础语法及规范

# 命名
Python 的命名规范主要遵循 PEP 8 风格指南，以下是主要的命名规则：
## 变量和函数命名
1. **小写字母与下划线** (snake_case)
- 变量名和函数名应全部小写，单词间用下划线分隔
- 例如：`first_name`, `calculate_total()`

2. **避免单个字符** (除了计数器和迭代器)
- 避免使用 `l`(小写L), `O`(大写O), `I`(大写i)等易混淆字符

## 类命名
1. **驼峰命名法** (PascalCase/CamelCase)
- 类名应使用首字母大写的驼峰命名法
- 例如：`ClassName`, `HttpClient`

2. **异常类名**
- 异常类名应以"Error"结尾
- 例如：`ValidationError`

## 常量命名
1. **全大写字母与下划线**
- 常量应全部大写，单词间用下划线分隔
- 例如：`MAX_CONNECTIONS`, `DEFAULT_TIMEOUT`

## 特殊命名约定
1. **私有成员**
- 单下划线前缀表示"保护"成员 (约定俗成，Python不强制)
- 例如：`_internal_variable`
- 双下划线前缀表示"私有"成员 (名称修饰)
- 例如：`__private_method`

2. **特殊方法**
- 双下划线前缀和后缀表示特殊方法
- 例如：`__init__`, `__str__`

## 模块和包命名
1. **模块名**
- 全小写，简短，可使用下划线
- 例如：`module.py`, `my_module.py`

2. **包名**
- 全小写，不使用下划线
- 例如：`package`, `mypackage`

## 文件命名规范
### 基本规则
1. **全小写字母**：文件名应全部使用小写字母
- 例如：`module.py` 而不是 `Module.py`

2. **使用下划线分隔单词** (snake_case)
- 例如：`data_processor.py` 而不是 `dataProcessor.py`

3. **简短而有意义**：文件名应简洁但能清楚表达内容
- 例如：`user_authentication.py` 比 `auth.py` 更明确

### 特殊文件类型

1. **测试文件**：以 `test_` 开头或 `_test.py` 结尾
- 例如：`test_models.py` 或 `models_test.py`

2. **配置文件**：常用 `config.py` 或 `settings.py`

3. **主程序入口**：常用 `main.py` 或 `app.py`

4. **初始化模块**：`__init__.py` (包目录中)
Python 中用于将一个目录标记为 Python 包（package） 的特殊文件
将`__init__.py`文件所在目录

### 避免使用的名称

1. **避免与 Python 关键字冲突**
- 例如：不要使用 `class.py`, `import.py` 等

2. **避免与标准库模块同名**
- 例如：不要使用 `os.py`, `sys.py` 等

3. **避免特殊字符和空格**
- 只使用字母、数字和下划线


