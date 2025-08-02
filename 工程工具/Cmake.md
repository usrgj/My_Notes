---
tags: [tools]
title: Cmake
created: '2025-04-27T09:18:48.394Z'
modified: '2025-07-15T00:53:59.934Z'
---

[cmake --help](https://cmake.org/cmake/help/v3.31/guide/tutorial/index.html)

cmake支持跨平台

自动检查源文件和头文件之间的依赖关系，导出到Makefile里面

c和cpp文件都属于源文件

需要经过

1.  预处理
    
2.  编译
    
3.  汇编
    
4.  链接
    

这一套称为Toolchain

若是只有少量文件，可以通过命令直接生成可执行文件

但往往一个项目中有多个文件，使用命令有太多缺点

可以使用make构建工具

因此需要构建 构建系统的工具cmake

# make

需要一个构建脚本

脚本名为makefile

在makefile中写一系列命令，告诉编译器如何编译文件

在命令行执行命令`make`就会自动执行makefile中的若干指令

但由于在不同平台的命令往往不同，make也就不支持跨平台

因此诞生cmake，能自动匹配平台生成makefile

# [**cmake**](https://subingwen.cn/)

脚本名为CMakeLists.txt包含一系列指令

执行命令`cmake`就能生成makefile文件

再执行`make`命令

但cmake的强大远不于此

cmake还能生成库文件，包括动态库和静态库

## 命令行参数

### \-B 

指定输出文件的目录名

# CMakeLists.txt

## 注释

     使用 # 进行 行注释，可以放在任何位置。

## cmake\_minimum\_required：

指定使用的 cmake 的最低版本，必须放在文件的第一行

```cmake
cmake_minimum_required(VERSION 3.15)

cmake_minimum_required(VERSION 3.15...3.25)
```

## project：

定义工程名称，并可指定工程的版本、工程描述、web主页地址、支持的语言（默认情况支持所有语言），如果不需要这些都是可以忽略的，只需要指定出工程名字即可。

```cmake
project(<项目名>
        [VERSION <版本号>]
        [DESCRIPTION <项目描述>]
        [LANGUAGES <语言列表>...]  # 如 C CXX ASM Python等
)

project(MyApp
    VERSION 1.0.0               # 版本号（会生成变量 MyApp_VERSION）
    DESCRIPTION "A cool app"     # 项目描述（CMake 3.12+）
    LANGUAGES CXX               # 明确指定使用C++（避免隐式启用C语言）
)
```

## add\_executable：

定义工程会生成一个可执行程序

```cmake
add_executable(将生成的可执行程序名 源文件名称)
#可以有多个源文件，用空格隔开
```

## set()：

### 定义变量

```cmake
set(<变量名> <值> [CACHE <类型> <描述> [FORCE]])  # 设置普通变量或缓存变量
set(ENV{<环境变量名>} <值>)                        # 设置环境变量

#定义变量，变量的值都是字符串,变量名可以使用小写
set(MY_VAR "Hello World")  # 创建变量 MY_VAR
set(SRC_LIST add.c 
              div.c 
              main.c
              mult.c
              sub.c
)#定义源代码列表

#变量的调用${变量名}
add_executable(app ${SRC_LIST})
```

### 设置环境变量

```cmake
set(CMAKE_CXX_STANDARD 11)  # 全局设置C++11，指定出要使用c++11标准编译程序，

add_executable(my_app main.cpp)
target_compile_features(my_app PRIVATE cxx_std_11)#精准控制

```

### 指定输出路径

```cmake
set(HOME /home/robin/Linux/Sort)#储存路径
set(EXECUTABLE_OUTPUT_PATH ${HOME}/bin)#拼接，设置路径，若路径不存在，会自动生成
```

## 搜索文件

### aux\_source\_directory

可以查找某个路径下的所有源文件，命令格式为：

```cmake
aux_source_directory(<目录路径> <变量名>)

aux_source_directory(src SOURCES)  # 将 src 目录下所有源码路径存入 SOURCES
add_executable(my_app ${SOURCES})

#
   # 仅识别CMake默认认定的源文件扩展名（如 .c, .cpp），无法自定义过滤条件
    #例如：无法排除特定文件（如测试文件 test_*.cpp）

```

### file

####  收集文件：`file(GLOB)`

```cmake
file(GLOB/GLOB_RECURSE 变量名 要搜索的文件路径和文件类型)#变量无需使用set创建，
#使用recurse会递归搜索
Cmakefile(GLOB SOURCES "src/*.cpp" "include/*.h")  # 手动指定通配符
#关于要搜索的文件路径和类型可加双引号，也可不加:
```

*   优势：
    
    *   支持通配符（`*.cpp`, `**/*.cpp` 递归搜索等）
        
    *   可精确控制需要包含的文件类型
        
*   缺点：
    
    *   新增文件时需重新生成构建系统（CMake不会自动检测新增文件）
        
    *   需要手动维护过滤规则
        

#### 其他文件操作

```cmake
Cmakefile(COPY data/ DESTINATION ${CMAKE_BINARY_DIR}/data)  # 复制目录
file(READ config.json CONTENT)                          # 读取文件内容
file(GLOB_RECURSE ALL_HEADERS "include/**/*.h")         # 递归搜索头文件
```

## 包含头文件

在编译项目源文件的时候，很多时候都需要将源文件对应的头文件路径指定出来，这样才能保证在编译过程中编译器能够找到这些头文件，并顺利通过编译。在CMake中设置要包含的目录也很简单，通过一个命令就可以搞定了，他就是`include_directories`

```cmake
include_directories(headpath)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)
```

## 生成库和指定生成路径

在linux系统，动态库后缀为.so,静态库后缀为.a,

linux下动态库默认有执行权限，静态库没有

### 生成：add\_library()

```cmake
#生成的库文件名为 lib+名字+.a/.so
#第二个参数为STATIC生成静态，为SHARE生成动态
add_library(库名称 STATIC 源文件1 [源文件2] ...)
```

### 指定路径

```cmake
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)
#这个方法对动静都适用
```

## 链接库

### link\_libraties()

用于设置全局链接库，这些库会链接到之后定义的所有目标上。(全局设置)

```cmake
link_libraries(<static lib> [<static lib>...])
#可以使用完整的库文件名，也可以只使用库名
link_libraries(libfmt1.a fmt2)
#用于设置全局链接库，这些库会链接到之后定义的所有目标上。
```

### target\_link\_libraries()

精准链接到一个目标

```cmake
target_link_libraries(
    <target> 
    <PRIVATE|PUBLIC|INTERFACE> <item>... 
    [<PRIVATE|PUBLIC|INTERFACE> <item>...]...)

    
#用于指定一个目标（如可执行文件或库）在编译时需要链接哪些库。它支持指定库的名称、路径以及链接库的顺序。

   # target：指定要加载的库的文件的名字
    #    该文件可能是一个源文件
     #   该文件可能是一个动态库/静态库文件
      #  该文件可能是一个可执行文件
  #权限可选，默认pubilc
  #后接库名

```

动态库的链接具有传递性，如果动态库 A 链接了动态库B、C，动态库D链接了动态库A，此时动态库D相当于也链接了动态库B、C，并可以使用动态库B、C中定义的方法。

```cmake
target_link_libraries(A B C)
target_link_libraries(D A)
```

    动态库在生成可执行程序的链接阶段不会被打包到可执行程序中，当可执行程序被启动并且调用了动态库中的函数的时候，动态库才会被加载到内存

因此，在cmake中指定要链接的动态库的时候，应该将命令写到生成了目标之后：

### 设置链接路径

```cmake
link_directories(<lib path>)
#这个对动态库和静态库都适用
```

## 日志

### message()

```cmake
message([STATUS|WARNING|AUTHOR_WARNING|FATAL_ERROR|SEND_ERROR] "message to display" ...)
#(无) ：重要消息
#STATUS ：非重要消息
#WARNING：CMake 警告, 会继续执行
#AUTHOR_WARNING：CMake 警告 (dev), 会继续执行
#SEND_ERROR：CMake 错误, 继续执行，但是会跳过生成的步骤
#FATAL_ERROR：CMake 错误, 终止所有处理过程
```

CMake的命令行工具会在stdout上显示STATUS消息，在stderr上显示其他所有消息。CMake的GUI会在它的log区域显示所有消息。

## 变量操作

### list类型

在CMake中，使用set命令可以创建一个list。一个在list内部是一个由分号;分割的一组字符串。例如，set(var a b c d e)命令将会创建一个list:a;b;c;d;e，但是最终打印变量值的时候得到的是abcde。

### 追加

**set**

```cmake
set(变量名1 ${变量名1} ${变量名2} ...)
```

**list**

```cmake
list(APPEND <list> [<element> ...])

list(APPEND SRC_1 ${SRC_1} ${SRC_2} ${TEMP})
#list命令的功能比set要强大，字符串拼接只是它的其中一个功能，所以需要在它第一个参数的位置指定出我们要做的操作，APPEND表示进行数据追加，后边的参数和set就一样了。
```

### 移除

**list**

```cmake
list(REMOVE_ITEM <list> <value> [<value> ...])

list(REMOVE_ITEM SRC_1 ${PROJECT_SOURCE_DIR}/main.cpp)
 
```

## [**list**](https://subingwen.cn/cmake/CMake-primer/#2-8-2-%E5%AD%97%E7%AC%A6%E4%B8%B2%E7%A7%BB%E9%99%A4)

## [**宏定义**](https://subingwen.cn/cmake/CMake-primer/#2-9-%E5%AE%8F%E5%AE%9A%E4%B9%89)

在gcc/g++命令中通过参数 -D指定出要定义的宏的名字，这样就相当于在代码中定义了一个宏，其名字为DEBUG。

 在CMake中我们也可以做类似的事情，对应的命令叫做add\_definitions:

```cmake
add_definitions(-D宏名称 -D宏2)
```

|  **特性**  |  `add_definitions`  |  `add_compile_definitions`  |
| --- | --- | --- |
|  **用途**  |  全能型：宏定义、编译选项、包含路径等  |  仅宏定义  |
|  **作用域**  |  全局（影响所有目标）  |  全局（影响所有目标）  |

## cmak嵌套

```cmake
add_subdirectory(source_dir [binary_dir] [EXCLUDE_FROM_ALL])
add_subdirectory(calc)
```

*   `source_dir`：指定了`CMakeLists.txt`源文件和代码文件的位置，其实就是指定子目录
    
*   `binary_dir`：指定了输出文件的路径，一般不需要指定，忽略即可。
    
*   `EXCLUDE_FROM_ALL`：在子路径下的目标默认不会被包含到父路径的`ALL`目标里，并且也会被排除在IDE工程文件之外。用户必须显式构建在子路径下的目标。
    

*   根节点`CMakeLists.txt`中的变量全局有效
    
*   父节点`CMakeLists.txt`中的变量可以在子节点中使用
    
*   子节点`CMakeLists.txt`中的变量只能在当前节点中使用
    

# CMake常用宏

### 1.CMAKE\_CURRENT\_SOURCE\_DIR    表示当前访问的 CMakeLists.txt 文件所在的路径

`${CMAKE_CURRENT_SOURCE_DIR}`

### 2.EXECUTABLE\_OUTPUT\_PATH 表示设置可执行文件的生成路径

`set (EXECUTABLE_OUTPUT_PATH ./build)`

### 3.LIBRARY\_OUTPUT\_PATH 设置库文件生成路径，对动静都适用

`set(LIBRARY_OUTPUT_PATH ./build)`

### 4.PROJECT\_SOURCE\_DIR     使用cmake命令后紧跟的目录，一般是工程的根目录

### 5.PROJECT\_BINARY\_DIR     执行cmake命令的目录

### 6.CMAKE\_CURRENT\_BINARY\_DIR     target 编译目录

### 7.PROJECT\_NAME     返回通过PROJECT指令定义的项目名称

### 8.CMAKE\_BINARY\_DIR     项目实际构建路径，假设在build目录进行的构建，那么得到的就是这个目录的路径

1.  `**set(CMAKE_CXX_STANDARD 23)**`  
    全局设置 C++ 编译标准为 C++23（现代项目建议用 `target_compile_features` 替代）。
    
2.  `**set(CMAKE_CXX_STANDARD_REQUIRED ON)**`  
    强制要求编译器必须支持指定 C++ 标准（否则报错）。
    
3.  `**set(CMAKE_CXX_EXTENSIONS ON)**`  
    启用编译器扩展（如 GNU 的 `-std=gnu++23`，**建议关闭**以提升跨平台性）。
    
4.  `**set(CMAKE_CXX_FLAGS "-Wall -Wextra -Wpedantic")**`  
    全局添加编译警告选项（可能覆盖默认设置，建议用 `add_compile_options` 或 `target_compile_options`）。
    
5.  `**set(BUILD_SHARED_LIBS OFF)**`  
    设置默认生成静态库（`.a/.lib`），但应显式声明库类型（如 `add_library(... STATIC)`）。
    
6.  `**set(POSITION_INDEPENDENT_CODE ON)**`  
    全局启用位置无关代码（PIC，通常用于共享库，建议仅对特定目标启用）。
    

|  **变量名**  |  **作用**  |  **注意事项**  |
| --- | --- | --- |
|  `CMAKE_RUNTIME_OUTPUT_DIRECTORY`  |  可执行文件（如 `.exe`）输出到 `build/bin`  |  需手动处理动态库依赖（Windows 的 `.dll` 需复制到此处或设置 `PATH`）  |
|  `CMAKE_LIBRARY_OUTPUT_DIRECTORY`  |  动态库（如 `.so`/`.dll`）输出到 `build/lib`  |  建议与静态库分开目录（如 `lib/shared` 和 `lib/static`）避免同名冲突  |
|  `CMAKE_ARCHIVE_OUTPUT_DIRECTORY`  |  静态库（如 `.a`/`.lib`）输出到 `build/lib`  |  若同时生成同名静态/动态库，需修改目标名称（如 `mylib_static` 和 `mylib`）  |
|  `CMAKE_INSTALL_PREFIX`  |  安装目录根路径设为 `build/install`（默认在系统目录）  |  适用于本地测试安装流程，正式发布时应设为系统路径（如 `/usr/local` 或 `C:\Program Files`）  |
|   |   |   |

# g++/gcc

## 参数

### \-c

`g++ -c main.cpp`生成obj文件，而不是可执行文件，可避免多次重复编译

### \-std=

1. `-std=` 的作用

`-std=` 允许你明确告诉编译器使用哪个 C 或 C++ 标准来编译你的代码。例如：

*   如果你想使用 C++11 的特性，就需要指定 `-std=c++11`。
    
*   如果你不指定 `-std=`，编译器通常会使用默认的标准（可能是较旧的版本）。
    

---

2. 常见的 C++ 标准

以下是一些常见的 C++ 标准及其对应的 `-std=` 选项：

|  标准  |  选项  |  描述  |
| --- | --- | --- |
|  C++98  |  `-std=c++98`  |  最早的 C++ 标准，现代代码中很少使用。  |
|  C++11  |  `-std=c++11`  |  引入了 `auto`、范围 `for` 循环、智能指针等现代特性。  |
|  C++14  |  `-std=c++14`  |  对 C++11 的小幅改进，增加了泛型 Lambda 等功能。  |
|  C++17  |  `-std=c++17`  |  引入了结构化绑定、`std::optional`、`std::filesystem` 等新特性。  |
|  C++20  |  `-std=c++20`  |  引入了概念（Concepts）、范围（Ranges）、协程（Coroutines）等新特性。  |
|  C++23  |  `-std=c++23`  |  最新标准（截至 2023 年），增加了更多现代化特性。  |

---

3. 常见的 C 标准

如果你编写的是 C 语言代码，可以使用以下标准：

|  标准  |  选项  |  描述  |
| --- | --- | --- |
|  C89/C90  |  `-std=c89`  |  最早的 C 标准，现代代码中很少使用。  |
|  C99  |  `-std=c99`  |  引入了 `inline`、`bool`、变长数组等功能。  |
|  C11  |  `-std=c11`  |  引入了多线程支持、`_Generic` 等功能。  |
|  C17  |  `-std=c17`  |  对 C11 的小幅改进，没有引入重大新特性。  |

---

4. 示例

假设你有一个 C++ 文件 `main.cpp`，并且你想使用 C++17 标准来编译它，可以这样写：

```powershell
g++ -std=c++17 main.cpp -o my_program
```

这会使用 C++17 标准编译 `main.cpp`，并生成可执行文件 `my_program`。

---

5. 默认标准

如果你不指定 `-std=`，编译器会使用默认的标准。例如：

*   较新的 GCC 版本（如 GCC 11 或更高版本）默认使用 `-std=gnu++17`（C++17 的 GNU 扩展版本）。
    
*   较旧的 GCC 版本可能默认使用 `-std=gnu++14` 或 `-std=gnu++11`。
