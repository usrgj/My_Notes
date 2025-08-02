

# 快速IO



## 1.使用C风格的IO函数

**`scanf/printf`** 在未关闭同步时，通常比`cin/cout`更快，尤其在读取大量数据时。 **缺点**：类型安全性较低，且不支持自定义类型扩展。

**`fread/fwrite`** 对于二进制或大规模数据块读写，直接使用C的文件操作函数可能更快

## 2.第三方库

**`fast_io`库** 一个C++20的高性能IO库，直接绕过传统流机制，接近系统调用的速度。支持文件映射、Unicode等高级特性，性能远超`iostream`和`cstdio`。

## 3. 自定义快速读写函数

**基于`getchar/putchar`的优化** 通过逐字符处理实现高速读写，适用于整数类型。例如：

```c++
Cppint read() {
    int x = 0, w = 1;
    char ch = getchar();
    while (ch < '0' || ch > '9') {
        if (ch == '-') w = -1;
        ch = getchar();
    }
    while (ch >= '0' && ch <= '9') {
        x = x * 10 + (ch - '0');
        ch = getchar();
    }
    return x * w;
}
```

输出优化类似，使用`putchar`逐位输出。



# 链表

链表（Linked List）是一种常见的线性数据结构，它由一系列节点组成，每个节点包含两部分：数据元素和指向下一个节点的引用（或指针）。链表中的节点通过这种引用关系依次相连，形成一个链条状的数据结构。与数组不同，链表的元素在内存中不一定是连续存储的。

链表的主要优点是插入和删除操作比较方便，不需要移动其他元素，只需要改变相关节点的指针即可。但是查找操作效率相对较低，因为需要从头节点开始逐个遍历链表直到找到目标节点。

链表主要分为以下几种类型：

1. **单向链表（Singly Linked List）**：每个节点只包含指向下一个节点的指针，最后一个节点的指针为`nullptr`。
2. **双向链表（Doubly Linked List）**：每个节点包含指向前一个节点和指向下一个节点的两个指针，允许双向遍历链表。
3. **循环链表（Circular Linked List）**：链表中最后一个节点的指针指向第一个节点，形成一个环。可以是单向循环链表也可以是双向循环链表。

``` c++ 
#include <iostream>

struct Node {
    int data;
    Node* next;

    Node(int val) : data(val), next(nullptr) {}
};

class LinkedList {
private:
    Node* head;
public:
    LinkedList() : head(nullptr) {}

    // 在链表尾部添加新节点
    void append(int value) {
        Node* newNode = new Node(value);
        if (head == nullptr) {
            head = newNode;
        } else {
            Node* temp = head;
            while (temp->next != nullptr) {
                temp = temp->next;
            }
            temp->next = newNode;
        }
    }

    // 打印链表
    void printList() const {
        Node* temp = head;
        while (temp != nullptr) {
            std::cout << temp->data << " ";
            temp = temp->next;
        }
        std::cout << std::endl;
    }

    // 删除链表
    ~LinkedList() {
        while (head != nullptr) {
            Node* temp = head;
            head = head->next;
            delete temp;
        }
    }
};

int main() {
    LinkedList list;
    list.append(10);
    list.append(20);
    list.append(30);
    list.printList();
    return 0;
}
```

算法竞赛中，**用静态数组与下标的方式管理链式结构，尽量避免使用指针**。

``` c++ 
#include<cstdio>
struct Node {
    int val;
    int nex;    // 指针改为数组下标
};
Node lst[999];  // 提前开好足够题目使用的内存作为待用链表节点
int tp;         // 一个模拟内存控制的下标变量

int NewNode() {
    // 模拟新建一个节点，返回lst中的下标
    lst[tp].nex = -1;   // 用 -1 下标表达“空指针”的含义
    tp ++;              // 让 tp 指向下一个待使用的Node
    return tp - 1;      // tp刚刚++了，tp-1才是刚分配好的Node
}
void AddHead(int hp, int x) {
    // 将数 x 插入头节点下标为 hp 的链表开头——头插法
    int p = NewNode();
    lst[p].val = x;
    lst[p].nex = lst[hp].nex;
    lst[hp].nex = p;
}
void AddTail(int hp, int x) {
    // 将数 x 插入头节点为 head 的链表结尾——尾插法
    int p = NewNode(), r;
    for(r = hp; lst[r].nex != -1; r = lst[r].nex);  // 找到链表末尾
    lst[p].val = x;
    lst[p].nex = lst[r].nex;
    lst[r].nex = p;
    
}
int main() {
    tp = 0;     // 初始化节点分配下标为0
    int head = NewNode();
    AddHead(head, 1);
    AddHead(head, 3);
    AddTail(head, 4);
    for(int p = lst[head].nex; p != -1; p = lst[p].nex) {
        printf("%d ", lst[p].val);
    }
    return 0;
}

```

 



# 范围统计

## 树状数组（背）

前缀和方法存在以下不足：

- 每个序号“管理”整个前缀，涉及“下属”过多
- 每个序号被后续序号“管理”，更新要“汇报”的“上级”过多

改进思路是减少每个序号的“下级”与“上级”。我们采用以2的幂为单位的分级“管辖”方案：



## 线段树

​	树状数组能做的，线段树都能做

​	线段树本质是一个二叉树，每个节点管理它下面的节点，叶节点是原数组数据

![img](https://blog.csgrandeur.cn/2025-05-23-33-%E8%8C%83%E5%9B%B4%E7%BB%9F%E8%AE%A1/%E7%BA%BF%E6%AE%B5%E6%A0%91.svg)

``` c++
//完全二叉树写法
LL BuildSegTree(int now, int ls, int rs) {
    // now: 当前节点； [ls, rs) 左闭右开区间端点
    if(ls >= rs) return 0;
    if(ls == rs - 1) {return sum[now] = a[ls];}
    sum[now] = 0;
    int mid = ls + rs >> 1;
    sum[now] += BuildSegTree(now << 1, ls, mid);
    sum[now] += BuildSegTree(now << 1 | 1, mid, rs);
    return sum[now];
}

```

### 单点修改

### 区间查询

 ### 区间修改



## K-D树

相比于线段树，K-D树能出路多维数据



# 王枫好帅王枫好帅王枫好帅王枫好帅王枫好帅
