---
tags: [tools]
title: Conan
created: '2025-07-13T08:51:43.401Z'
modified: '2025-07-27T11:31:14.985Z'
---

Conan
[Tutorial](https://docs.conan.org.cn/2/tutorial.html#google_vignette)

# 目录
[0简介](#0简洁)
[1安装](#1安装)
[2使用包](#2使用包)
[3创建包](#3创建包)
* [创建](#创建)
* [根目录下的配方](#根目录下的配方)
* [测试创建成功](#测试创建成功)
* [源代码](#源代码)
* [依赖项](#依赖项)
* [准备构建](#准备构建)
* [构建](#构建)
* [打包文件](#打包文件)
* [使用端信息](#使用端信息)
[流程](#流程)
[方法](#方法)
[散的知识点](#散的知识点)

# 0简介
Conan属于包管理器。但与传统包管理器（如 APT、pip、npm 等）定位不同，主要专注于 C/C++ 生态的二进制包管理，并解决 C/C++ 特有的复杂依赖和跨平台构建问题。

* 传统包管理器：直接安装“开箱即用”的软件或库（如 apt install git 或 pip install numpy）。

* Conan：专注于 C/C++ 项目的依赖管理，需与构建工具（如 CMake）配合使用，解决头文件、库路径、编译选项等问题。


# 1安装
~~~
pip install conan
~~~
~~~
//更新
pip install conan --upgrade  # Might need sudo
~~~

# 2使用包
[返回目录](#目录)

## 流程
基本结构
~~~chart
.
├── CMakeLists.txt
├── conanfile.py
└── src
    └── main.c
~~~
基本流程
在根目录下运行
~~~bash
conan install . --output-folder build --build=missing #使用 Conan 安装 包 并生成 CMake 查找此库和构建我们项目所需的文件。我们将在 *build* 文件夹中生成这些文件。
cd build
source conanbuild.sh #激活虚拟环境
cmake .. -DCMAKE_TOOLCHAIN_FILE=conan_toolchain.cmake -DCMAKE_BUILD_TYPE=Release
make #linux使用，跨平台通用用 cmake --build .
./bin_file
source deactivate_conanbuild.sh #解除虚拟环境
~~~

`conanfile.py`称为“conan配方”。它既可以用于使用包（如本例），也可以用于创建包。对于我们当前的情况，它将定义我们的依赖项（包括库和构建工具）以及修改选项和设置如何使用这些包的逻辑。在使用此文件创建包的情况下，它可以定义（除其他外）如何下载包的源代码，如何从这些源代码构建二进制文件，如何打包二进制文件，以及为未来使用者提供如何使用包的信息

~~~python
from conan import ConanFile # 导入类

class CompressorRecipe(ConanFile): # 继承父类ConanFile
    settings = "os", "compiler", "build_type", "arch"
    generators = "CMakeToolchain", "CMakeDeps"

    def requirements(self):
        self.requires("zlib/1.3.1")

    def build_requirements(self):
        self.tool_requires("cmake/3.27.9")
~~~

声明了一个继承自 ConanFile 类的新类。这个类具有不同的类属性和方法

* settings 类属性定义了项目范围的变量，例如编译器、其版本或操作系统本身，这些变量在构建项目时可能会改变。这与 Conan 如何管理二进制兼容性有关，因为这些值将影响 Conan 包的 包 ID 值。我们稍后将解释 Conan 如何使用此值来管理二进制兼容性。

* generators 类属性指定当我们调用 conan install 命令时将运行哪些 Conan 生成器。在这种情况下，我们添加了 CMakeToolchain 和 CMakeDeps，就像在 conanfile.txt 中一样。

* 在 requirements() 方法中，我们使用 self.requires() 方法声明 zlib/1.2.11 依赖项。

* 在 build_requirements() 方法中，我们使用 self.tool_requires() 方法声明 cmake/3.22.6 依赖项。

## layout()
~~~python
import os

from conan import ConanFile


class CompressorRecipe(ConanFile):
    settings = "os", "compiler", "build_type", "arch"
    generators = "CMakeToolchain", "CMakeDeps"

    def requirements(self):
        self.requires("zlib/1.2.11")
        if self.settings.os == "Windows":
            self.requires("base64/0.4.0")

    def build_requirements(self):
        if self.settings.os != "Windows":
            self.tool_requires("cmake/3.22.6")

    def layout(self):
        # We make the assumption that if the compiler is msvc the
        # CMake generator is multi-config
        multi = True if self.settings.get_safe("compiler") == "msvc" else False
        if multi:
            self.folders.generators = os.path.join("build", "generators")
            self.folders.build = "build"
        else:
            self.folders.generators = os.path.join("build", str(self.settings.build_type), "generators")
            self.folders.build = os.path.join("build", str(self.settings.build_type))
~~~
在 layout() 方法中定义了 self.folders.generators 属性。这是 Conan 生成的所有辅助文件（CMake 工具链和 cmake 依赖文件）的放置文件夹。

# 3创建包

* 使用 `source()` 方法从外部仓库检索源代码并对这些源代码应用补丁。

* 在 `requirements()` 方法中为你的 Conan 软件包添加依赖项。

* 使用 `generate()` 方法准备软件包构建，并自定义工具链。

* 在 `configure()` 和 `config_options()` 方法中配置设置和选项，以及它们如何影响软件包的二进制兼容性。

* 使用 `build()` 方法自定义构建过程并启动你正在打包的库的测试。

* 使用 `package()` 方法选择将包含在 Conan 软件包中的文件。

* 在 `package_info()` 方法中定义软件包信息，以便此软件包的使用者可以使用它。

## 创建
```bash
conan new cmake_lib -d name=<package_name> -d version=1.0
```
name为hello为例，生成以下文件结构
```
.
├── CMakeLists.txt
├── conanfile.py
├── include
│   └── hello.h
├── src
│   └── hello.cpp
└── test_package
    ├── CMakeLists.txt
    ├── conanfile.py
    └── src
        └── example.cpp
```

* `conanfile.py`：在根文件夹中，有一个 conanfile.py，它是主要的配方文件，负责定义包的构建和使用方式。

* `CMakeLists.txt`：一个简单的通用 CMakeLists.txt，其中不包含任何 Conan 特定的内容。

* `src 和 include` 文件夹：包含简单 C++ “hello” 库的文件夹。

* `test_package` 文件夹：包含一个示例应用程序，该应用程序将要求并链接到所创建的包。这不是强制性的，但它有助于检查我们的包是否正确创建。

## 根目录下的配方
|类型|参数|含义|
|---|---|---|
|包定义|`name`|一个字符串，定义包名，最少 2 个字符，最多 100 个小写字符。它应该以字母数字字符或下划线开头，并且可以包含字母数字、下划线、+、.、- 等字符|
||`version`|一个字符串，可以取任何值，与 `name` 属性的约束相同。如果版本遵循语义化版本控制形式 `X.Y.Z-pre1+build2`，则该值可以用于通过版本范围而不是精确版本来要求此包|
|元数据属性|`description`|包的描述|
||`author`|打包库的作者|
||`license`|许可证|
||`url`||
||`topics`||
|配置|`settings`|项目范围的配置，不能在食谱中设置默认值。例如操作系统、编译器或构建配置等，这些将是多个 Conan 包的通用配置|
||`options`|包特定的配置，可以在食谱中设置默认值。在这种情况下，我们可以选择将包创建为共享库或静态库，默认是静态库|
||`exports_sources`|定义哪些源文件是 Conan 包的一部分。这些是你想要打包的库的源文件|
||``||



* `config_options()` 方法（与 configure() 方法一起）允许微调二进制配置模型。例如，在 Windows 上没有 fPIC 选项，因此可以将其移除。

* `layout()` 方法声明了我们期望找到源文件以及构建过程中生成文件的目标位置。示例目标文件夹包括生成的二进制文件以及 Conan 生成器在 generate() 方法中创建的所有文件。在这种情况下，由于我们的项目使用 CMake 作为构建系统，我们调用 cmake_layout()。调用此函数将设置 CMake 项目的预期位置。

* `generate()` 方法准备从源文件构建包。在这种情况下，它可以简化为属性 generators = "CMakeToolchain"，但为了展示这个重要方法而保留。在这种情况下，执行 CMakeToolchain 的 generate() 方法将创建一个 conan_toolchain.cmake 文件，将 Conan 的 settings 和 options 转换为 CMake 语法。CMakeDeps 生成器是为了完整性而添加的，但在食谱中添加 requires 之前并非严格必要。

* `build()` 方法使用 CMake 包装器来调用 CMake 命令。这是一个薄层，在这种情况下，它将传递参数 -DCMAKE_TOOLCHAIN_FILE=conan_toolchain.cmake。它将配置项目并从源代码构建它。

* `package()` 方法将构建文件夹中的 artifact（头文件、库）复制到最终的包文件夹。这可以通过简单的“copy”命令完成，但在本例中，它利用了现有的 CMake 安装功能。如果 CMakeLists.txt 没有实现它，很容易在 package() 方法中使用 copy() 工具编写一个等效实现。

* `package_info()` 方法定义了消费者在使用此包时必须链接“hello”库。也可以定义其他信息，例如 include 或 lib 路径。此信息用于生成器（如 CMakeDeps）创建的文件，供消费者使用。这是关于当前包的通用信息，无论消费者使用何种构建系统，也无论我们在 build() 方法中使用了何种构建系统，这些信息都对消费者可用。

## 测试创建成功
根目录下
```bash
conan create . 
```
`create`命令和`install`命令可以接受相同的参数

## 源代码
### 本地源代码
使用`exports_sources`属性,例如
```python
exports_sources = "CMakeLists.txt", "src/*", "include/*"
```

### 远程仓库的zip文件
使用`source`方法和`get()工具`例如
```python
def source(self):
    # Please, be aware that using the head of the branch instead of an immutable tag
    # or commit is strongly discouraged, unsupported by Conan and likely to cause issues
    get(self, "https://github.com/conan-io/libhello/archive/refs/heads/main.zip",
              strip_root=True)
```
该工具将首先**下载**我们作为参数传入的 URL 中的 zip 文件，然后**解压**它。请注意，我们传入了strip_root=True参数，以便如果所有解压后的内容都在一个单独的文件夹中，所有内容都会被移动到父文件夹中

### git仓库的分支获取源代码
使用`git()`工具
```python
....
from conan.tools.scm import Git
...

class helloRecipe(ConanFile):
    name = "hello"
    version = "1.0"

    ...

    def source(self):
        git = Git(self)
        git.clone(url="https://github.com/conan-io/libhello.git", target=".")

    ...
```

### 使用`conandata.yml`文件
在配方的相同文件夹下，创建一个`conandata.yml`文件，conan将自动导出和解析
例如
```yml
#yml
sources:
  "1.0":
    url: "https://github.com/conan-io/libhello/archive/refs/heads/main.zip"
    sha256: "7bc71c682895758a996ccf33b70b91611f51252832b01ef3b4675371510ee466"
    strip_root: true
  "1.1":
    url: ...
    sha256: ...
```
```python
#recipe
def source(self):
    get(self, **self.conan_data["sources"][self.version])
    # Equivalent to:
    # data = self.conan_data["sources"][self.version]
    # get(self, data["url"], sha256=data["sha256"], strip_root=data["strip_root"])

```
配方不需要为代码的每个版本进行修改。我们可以将指定版本的所有keys（url、sha256和strip_root）作为参数传递给get函数，在这种情况下，这允许我们验证下载的 zip 文件是否具有正确的sha256.

## 依赖项
与使用包非常相似
### 根目录下的配方
```python
# 配方
...
from conan.tools.build import check_max_cppstd, check_min_cppstd
...

class helloRecipe(ConanFile):
    ...
    generators = "CMakeDeps"
    ...

    def validate(self):
        check_min_cppstd(self, "11")
        check_max_cppstd(self, "20")

    def requirements(self):
        self.requires("fmt/8.1.1")

    def source(self):
        git = Git(self)
        git.clone(url="https://github.com/conan-io/libhello.git", target=".")
        # Please, be aware that using the head of the branch instead of an immutable tag
        # or commit is not a good practice in general
        git.checkout("require_fmt")
```


首先，我们设置了`generators`类属性，以便让 Conan 调用CMakeDeps生成器。在之前的配方中，由于我们没有依赖项，所以不需要这样做。CMakeDeps将生成 CMake 查找fmt库所需的所有配置文件。

接下来，我们使用`requires()`方法将fmt依赖项添加到我们的包中。

请注意，我们在`source()`方法中添加了一行。我们使用`Git().checkout()`方法检出require_fmt分支中的源代码。此分支包含源代码中用于为库消息添加颜色的更改，以及***CMakeLists.txt***中声明我们正在使用fmt库的更改。

最后，请注意我们向配方添加了`validate()`方法。我们之前在使用包部分中使用此方法来针对不支持的配置引发错误。在这里，我们调用函数`check_min_cppstd()`和`check_max_cppstd()`来验证我们的设置中至少使用 C++11 且最多使用 C++20 标准。

### 头文件传递
默认情况下，Conan 假定所需的依赖项头文件是当前包的实现细节，以促进低耦合和封装等良好的软件工程实践。在上述示例中，fmt纯粹是hello/1.0包的实现细节。hello/1.0的消费者将不知道任何关于fmt的信息，也无法访问其头文件，如果hello/1.0的消费者尝试添加#include <fmt/color.h>，它将失败，因为无法找到这些头文件。

但是，如果hello/1.0包的公共头文件中包含对fmt头文件的#include，这意味着这些头文件必须向下传播，以允许hello/1.0的消费者成功编译。由于这不是默认的预期行为，配方必须将其声明为
```python
class helloRecipe(ConanFile):
    name = "hello"
    version = "1.0"

    def requirements(self):
        self.requires("fmt/8.1.1", transitive_headers=True) #这将把必要的编译标志和头文件includedirs传播给hello/1.0的消费者。
```

## 准备构建
重点关注配方的`generate()`方法。此方法的目的是生成在运行构建步骤时可能需要的所有信息。这意味着诸如：
* 写入在构建步骤中使用的文件，例如注入环境变量的脚本、传递给构建系统的文件等。
* 配置工具链以根据设置和选项提供额外信息，或者从 Conan 默认生成但可能不适用于某些情况的工具链中删除信息。

### 根目录配方
```python
from conan.tools.build import check_max_cppstd, check_min_cppstd
...

class helloRecipe(ConanFile):
    ...
    # 声明新选项 “with_fmt”
    options = {"shared": [True, False],
               "fPIC": [True, False],
               "with_fmt": [True, False]}

    default_options = {"shared": False,
                       "fPIC": True,
                       "with_fmt": True}
    ...

    def validate(self):
        if self.options.with_fmt:
            check_min_cppstd(self, "11")
            check_max_cppstd(self, "14") # 规定fmt为true时c++的最高和最低标准，不满足标准将无法编译

    def source(self):
        git = Git(self)
        git.clone(url="https://github.com/conan-io/libhello.git", target=".")
        # Please, be aware that using the head of the branch instead of an immutable tag
        # or commit is not a good practice in general
        git.checkout("optional_fmt")

    def requirements(self):
        if self.options.with_fmt:
            self.requires("fmt/8.1.1") # fmt为true时安装fmt

    def generate(self):
        tc = CMakeToolchain(self)
        if self.options.with_fmt:
            tc.variables["WITH_FMT"] = True # fmt为true时，将值为 True 的 WITH_FMT 变量注入到 CMakeToolchain 中，以便我们可以在 hello 库的 CMakeLists.txt 中使用它来添加 CMake fmt::fmt 目标。
        tc.generate()

```

### 运行
```bash
conan create . --build=missing -o with_fmt=True
```

## 构建
使用`build()`方法完成

* 构建并运行测试
* 条件性地修补源代码
* 条件性地选择您想要使用的构建系统

## 打包文件
更详细地解释 CMake.install() 的用法，以及如何修改此方法以执行以下操作：

* 使用 conan.tools.files 工具从构建文件夹复制生成的工件到包文件夹
* 复制包许可证
* 管理符号链接的打包

### 使用cmake安装步骤
这将在不改变您的 ***CMakeLists.txt*** 的情况下工作，因为 Conan 会将 `CMAKE_INSTALL_PREFIX` CMake 变量设置为指向配方（recipe）的 `package_folder` 属性。然后，只需在 ***CMakeLists.txt*** 中对创建的目标调用 `install()`，Conan 就足以将构建的工件移动到 Conan 本地缓存中的正确位置。
```python
def package(self):
    copy(self, "LICENSE", src=self.source_folder, dst=os.path.join(self.package_folder, "licenses")) # cmakelist不会将许可证复制到包文件夹下
    cmake = CMake(self)
    cmake.install()
```
 ### 运行
 ```bash
 conan create . --build=missing -tf=""
 ```
## 使用端信息
Conan 包在 Conan 本地缓存中最终的结构如下：
```
.
├── include
│   └── hello.h
└── lib
    └── libhello.a

```
想要链接此库的消费者将需要一些信息：

* Conan 本地缓存中 include 文件夹的位置，用于搜索 hello.h 文件。
* 要链接的库文件的名称（libhello.a 或 hello.lib）
* Conan 本地缓存中 lib 文件夹的位置，用于搜索库文件。

使用`package_info()`方法和`cpp_info`属性

```python

    name = "hello"
    def package_info(self):
        self.cpp_info.libs = ["hello"]
```
我们将一个 hello 库添加到 cpp_info 的 libs 属性中，以告诉消费者他们应该链接该列表中的库。

我们**没有添加**关于库和头文件打包所在的 lib 或 include 文件夹的信息。cpp_info 对象提供了 .includedirs 和 .libdirs 属性来定义这些位置，但 Conan 默认将其值设置为 lib 和 include，因此在这种情况下不需要添加这些。如果您将包文件复制到不同的位置，那么您必须明确设置这些




# [方法](https://docs.conan.org.cn/2/reference/conanfile/methods.html)

## lay_out()
cmake预定义配方
~~~python
    def layout(self):
        cmake_layout(self)
~~~

## validate()
**validate()** 方法 在 Conan 加载 conanfile.py 时进行评估，您可以使用它来检查输入设置。例如，如果您的项目不支持 macOS 上的 armv8 架构，您可以抛出 ConanInvalidConfiguration 异常，使 Conan 返回一个特殊的错误代码。这将表明用于设置或选项的配置不受支持。

## generate()
在某些情况下，Conan 包包含对使用它们所封装的库有用甚至必要的文件。这些文件可能包括配置文件、资产，以及项目正确构建或运行所需的特定文件。使用 **generate()** 方法，您可以将这些文件从 Conan 缓存复制到您的项目文件夹中，确保所有必需的资源都可以直接使用。


# 散的知识点
### 默认配置文件
Conan profile 允许用户定义一组配置，例如编译器、构建配置、架构、共享或静态库等。Conan 默认不会自动检测 profile，因此我们需要创建一个。要让 Conan 根据当前操作系统和已安装的工具尝试猜测 profile，请运行
~~~bash
conan profile detect --force
~~~
这将根据环境检测操作系统、构建架构和编译器设置。它还将默认将构建配置设置为 *Release*。生成的 profile 将存储在 Conan 主文件夹中，名称为 *default*，并且默认情况下将在所有 Conan 命令中使用，除非通过命令行指定了另一个 profile。

~~~bash
conan --profile=<指定配置，无该参数时为默认配置>
~~~

检查配方和包二进制文件是否在本地缓存中
```bash
conan list <package_name> # 留空则列出所有本地缓存包
conan list "<package>/<version>:*"#更详细的内容
```

