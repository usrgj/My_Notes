---
tags: [Matlab]
title: Matlab初级
created: '2025-09-09T08:33:41.088Z'
modified: '2025-11-24T07:06:05.537Z'
---

Matlab初级

# 基本语法
```

```
## 语句
```
```

# 逻辑运算符
|符号|含义|
|---|---|
|`&`|与|
|`~`|非|
|`|`|或|
|``||

# 数据类型
## 数字
## 字符与字符串
单引号
## 矩阵
```
A = [1 2 3; 4 5 6; 7 8 9]
B = [A A;A A]
A = 1:2:9 %作为为闭区间，中间为步长
%访问， ':'表示整行或整列
A(row, col)

%转置
A'

%求逆
inv(A)
```
### 运算
加减乘无不同
`.*`对应项相乘
`A / B`A乘以B的逆
`./`对应项相除


## 元胞数组
可以存储不同类型元素的数组， 每个元素本身以cell类型存储
在matlab中,普通的数组直接用字符串或者矩阵表示
下标从1开始
```
C = {1, 'hello', magic(3), {1, 2}}; 
C = cell(1,6) %一维六列空元胞数组 

C{1}%结果类型为数值本身类型
C(1)%结果类型为cell数组
```
## 结构体
更接近键值对
```
struct('name', {'a', 'b'} , age, 99)
%这种写法，也就是，name对应两个值

struct('name', {{'a', 'b'}} , age, 99)
%这种写法，name对应一个cell数组

```

# 程序结构
```octave
for i = begin:step:end_  %step为1时可以省略,闭区间
  statement;
end

for n = 1:5
  statement;
end

while condition
  statement;
end


if 条件1
    % 条件1为真时执行
elseif 条件2
    % 条件2为真时执行
elseif 条件3
    % 条件3为真时执行
else
    % 所有条件均为假时执行
end

switch 表达式
    case 候选值1
        % 表达式等于候选值1时执行
    case 候选值2
        % 表达式等于候选值2时执行
    ...
    otherwise
        % 所有case均不匹配时执行
end
```

# 基本绘图
## 二维
```
x = 0 : 0.01 : 2*pi; %定义横坐标
y = sin(x);
figure  %画布
plot(x,y) %绘图
title('y = sin(x)')
xlabel('x axis')
ylabel('y axis')
xlim([0 2*pi]) %规定x轴的绘制区间 
```
|函数|说明|
|---|---|
|`yyaxis()`|绘制多条线|
|`set(line, feature, value)`|设置线的样式|

## 三维
```
t = 0 : pi/50 : 10*pi;
plot3(sin(t), cos(t), t);
xlabel('');
ylabel('');
zlabel('');
```

## 通用
|函数|说明|
|---|---|
|`grid on`|启用网格|
|`axis square`|放缩成正方/立方坐标轴|


# 矩阵
## 引用
```python
A(1,1) #第m行第n列的元素
A(3) #通过下标访问，注意是列顺序
A(i, : ) #第i行的所有列
A([1,3], :) #1到3行
A( :, j) #第j列的所有行
A(:) #按列顺序平展成一列
```

## 函数
|函数|说明|
|---|---|
|`zeros(int,[int],[int])`|创建零矩阵，参数是行，列，维度|
|`rand(m,n)`|生成0~1的均匀分布的伪随机数|
|`randn(m,n)`|生成标准正态分布的伪随机数|
|`randi([min, max], m, n)`|生成均匀分布的伪随机整数|
|`magic(int)`|生成n阶幻方，魔方阵|
|`eye(int)`|生成n阶单位阵|
|`repmat(matrix, int, int)`|复制某矩阵整体，行重复次数，列重复次数|
|`ones(m,n)`|全一矩阵|
|`find(matrix > 20)`|查找某矩阵中所有符号条件的元素的下标，返回`[m,n]`|
|`linspace(begin, end, num)`|生成在闭区间内均匀的n个数|
|`reshape(A, m, n)`|将矩阵改变成目标现状|
|`fix(a+(b-a+1)*x)`|产生[a,b]上均匀分布的随机整数|
|`vander(int:int)`|范德蒙矩阵|
|`hilb(int)`|希尔伯特矩阵|
|`compan(p)`|伴随矩阵,p是多项式系数矩阵|
|`pascal(int)`|帕斯卡矩阵|
|`diag(vec)`|以一个向量为对角线元素，构建对角矩阵|
|`rot90(A,k)`|矩阵逆时针旋转90的k倍|
|`fliplr(A)`|矩阵左右翻转|
|`flipud(A)`|矩阵上下翻转|
|`inv(A)`|逆矩阵|
|`rank(A)`|矩阵的秩|
|``||
|``||
|``||

# 字符串
## 表示
```python matlab
a = 'I ''m string';

```
## 调用
```python matlab
a(1:3) #前三个字符

```
## 函数
|函数名/运算符|参数|作用|
|---|---|---|
|`eval()`|字符串|将字符串以命令执行（危险）|
|`strcmp()`|两个字符串||
|`findstr()`|||
|`strrep()`|||
|``|||


# 函数
## 定义与文件
```python
function [return] = func_name(arg)


#匿名函数
f=@(x,y)x^2+y^2;

>> f(3,4)
ans = 25
```

## 参数与变量
```python
#关键字
#narg
#对参数处理

```

# 数据统计分析
|函数名|参数|作用|
|---|---|---|
|`std()`||标准差|
|`corrcoef()`|一个或两个系数|相关系数|
|``|||
|``|||
|``|||
|``|||

## 多项式
|函数名|参数|作用|
|---|---|---|
|`conv()`|两个参数|多项式相乘|
|`deconv()`|被除数和除数|多项式相除，返回商和余|
|`polyder()`||求导，根据参数和返回接受的形式，可求积的导数，商的导数|
|`polyval()`|||
|`polyvalm()`|||
|`roots()`||多项式求根|
|``|||
|``|||

# 绘图

# 数值微分|数值积分
## 非线性齐次方程组

## 有约束最优化解
## 常微分方程求解

# 符号对象
1.  符号对象建立
`符号对象名 = sym(A)`
该函数建立单个符号对象，A可以是任意对象
	- `sin(sym(pi/3))`得到`ans = `$\frac{\sqrt3}{2}$
	- 可以看到，符号计算得到一个精确的数学表达式
2. 定义多个符号变量
`syms <name1> <name2> <name3> ...`
3. 符号变量四则运算
其结果仍然是一个符号表达式
4. 关系运算
结果是符号关系表达式
5. 定义域
`assume(x<0)`
使用assume()函数来对符号变量进行一些假设
6. 因式分解与展开
	- `factor(s)`
	- ``
	- ``
	- ``
7. 简化表达式
`simplify(s)`
8. 
9. 
## 符号矩阵
1. 定义
定义符号变量后
用符号变量表示矩阵中的元素，以构建符号矩阵

## 符号微积分
1. `diff(f, x)`,f是符号表达式,x是指定的求导变量
2. `int(g, x)`,g是被积函数, x是积分变量
3. 
4. 
## 级数
1. `symsum(f,value,begin,end)`
2. 泰勒级数
`taylor(f,value,a, Nmae,Value)`
a表示在a点展开，
配合`expend()`将结果展开（去掉括号）

## 符号方程求解
1. `solve(equation)`注意等于号是`==`,不写则默认等于0
可惜solve有时得到的结果是错误的

## 符号微分方程


# 图形对象
```matlab
handle1 = plot(...)
```
绘图函数会返回图形对象的句柄，可以访问和修改它们的属性

## 获取特定图形对象句柄的函数
```
gcf
gca
gco
findobj
```

## 属性
1. 常用公共属性
	- Children: 该对象的子对象句柄组成的一个向量
	- Parent: 该对象的父对象句柄
	- Type: 该对象的类型，只读属性
	- Tag: 标签，标识符
2. 常用动态属性
	- KeyPressFcn: 按下键盘按键时的响应
	- CreateFcn: 创建时的响应
	- DeleteFcn: 删除时的响应
	- ButtonDownFcn: 鼠标按下的响应

## 窗口
1. 创建
句柄变量 = figure(style1, style2, ....)
2. 属性

## 坐标
1. 创建
变量 = axes(style....)
2. 属性
	- ColorOrder: 绘制曲线的颜色出现顺序

## 曲线
1. 创建
变量 = line(x, y, z, style1, value1,....)

## 曲面
1. 创建
变量 = surface(x, y, z, c, style1, value1, .....)

# GUI
## 创建控件
对象 = uicontrol('Style', class, 属性1, value1)
### 静态属性
1. Position
2. String
3. Style
### 动态属性
1. 所有动态属性都使用句柄'Callback'
2. 回调函数的定义
function func (source, eventdata) 
end
## 创建菜单

# App设计
命令行输入appdesigner


# 命令行
|命令|作用|
|---|---|
|`clc`|清除命令行|
|`clear all`|清除workspace中的所有变量|
|``||
|``||

# 常用函数
|函数名|参数|作用|
|---|---|---|
|`exp()`|一个数组|e的指数|
|`round()`|一个数组|四舍五入|
|`fix()`|||
|`ceil()`|||
|`floor()`|||
|`mod()`|被除数，除数|取余|
|`disp()`||输出|
|`mean()`||算数平均值|
|`sum()`||求和|
|`prod()`||累积|
|`cumprod()`||累积乘积|
|``|||
|``|||
|``|||
|``|||

# 杂记
### 注释
$$
%aaa

%%将有下划线

%{
 
14ui
%}
$$
