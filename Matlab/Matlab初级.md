---
tags: [Matlab]
title: Matlab初级
created: '2025-09-09T08:33:41.088Z'
modified: '2025-09-10T03:27:03.732Z'
---

Matlab初级

# 数据类型
## 数字
## 字符与字符串
单引号
## 矩阵
```
A = [1 2 3; 4 5 6; 7 8 9]
A = 1:2:9 %作为为闭区间，中间为步长
%访问， ':'表示整行或整列
A(row, col)

%转置
A'

%按列顺序平展成一列
A(:)

%求逆
inv(A)
```
### 运算
加减乘无不同
`.*`对应项相乘
`A / B`A乘以B的逆
`./`对应项相除

|函数|说明|
|---|---|
|`zeros(int,int,int)`|创建零矩阵，参数是行，列，维度|
|`rand(m,n)`|生成0~1的均匀分布的伪随机数|
|`randn(m,n)`|生成标准正态分布的伪随机数|
|`randi([min, max], m, n)`|生成均匀分布的伪随机整数|
|`magic(int)`|生成n阶幻方|
|`eye(int)`|生成n阶单位阵|
|`repmat(matrix, int, int)`|复制某矩阵整体，行重复次数，列重复次数|
|`ones(m,n)`|全一矩阵|
|`find(matrix > 20)`|查找某矩阵中所有符号条件的元素的下标，返回`[m,n]`|
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
```
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



# 命令行
|命令|作用|
|---|---|
|`clc`|清除命令行|
|`clear all`|清除workspace中的所有变量|
|``||
|``||


# 杂记
### 注释
$$
%aaa

%%将有下划线

%{
 
14ui
%}
$$
