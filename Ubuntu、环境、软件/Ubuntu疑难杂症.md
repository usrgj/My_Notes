---
tags: [Ubuntu]
title: Ubuntu疑难杂症
created: '2025-04-27T08:51:57.459Z'
modified: '2025-07-25T07:47:29.099Z'
---

Ubuntu疑难杂症



# 安装[**cuda&cudnn**](https://blog.csdn.net/KRISNAT/article/details/134870009)

安装CUDA和cuDNN一般需要先后完成以下几步，并且具有先后顺序：

1.  安装显卡驱动，完成后nvidia-smi指令可以使用🚀；
    
2.  安装CUDA Toolkit，安装完成后nvcc -V指令正常输出🚀；
    
3.  安装cuDNN，安装完成后PyTorch可以调用相关的计算包🚀。
    

重要说明⁉️：我们常说的安装CUDA，实际上是指[安装CUDA Toolkit](https://so.csdn.net/so/search?q=%E5%AE%89%E8%A3%85CUDA%20Toolkit&spm=1001.2101.3001.7020)。nvidia-smi指令查看的是驱动版本的CUDA（我们用CUDA-driver表示）。nvcc -V查看的是PyTorch等深度学习环境调用的CUDA版本，也是我们常说的CUDA（我们用CUDA-dl表示）。这里只需要   cuda-driver>=cuda-dl即可

## 显卡驱动(待补充)

## [**cuda Toolkit**](https://developer.nvidia.com/cuda-toolkit-archive)

链接如上

1.一般没有安装时在终端输入`nvcc -V`会显示没有找到命令。

2.这时输入`nvidia-smi`，![截图 2025-02-23 16-21-43.png](https://qianwen.alicdn.com/note/7e817b0aac83da9aa9c5cf44b9684433/QReuoN4p5skGm5wD/b29e985ea18340baaaa6adc7e40b8518/%E6%88%AA%E5%9B%BE+2025-02-23+16-21-43.png)

在右上角可见当前驱动版本支持的cuda toolkit最大版本

3.进入链接，选择合适的版本之后，依次执行安装命令即可

（建议在指定文件夹内打开终端，再执行命令）![截图 2025-02-23 16-26-39.png](https://qianwen.alicdn.com/note/7e817b0aac83da9aa9c5cf44b9684433/QReuoN4p5skGm5wD/59c9aab7d15a4467bd8f446993a10bb6/%E6%88%AA%E5%9B%BE+2025-02-23+16-26-39.png)

4.找到根目录下的环境变量文件（我的是  .bashrc ）

在里面最后添加三条

`export PATH=$PATH:/usr/local/cuda-12.4/bin`

`export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-12.4/lib64`

`export CUDA_HOME=$CUDA_HOME:/usr/local/cuda-12.4`

(记得改成自己的版本，以下出现版本号也一样，不再赘述)

5.根目录下终端执行`source ~/.bashrc`（也就是激活自己的环境变量）

6.终端执行`nvcc -V`，输出正确信息即为成功

![截图 2025-02-23 16-34-27.png](https://qianwen.alicdn.com/note/7e817b0aac83da9aa9c5cf44b9684433/QReuoN4p5skGm5wD/f9aebeacf0a54c2dacbb4568107762e3/%E6%88%AA%E5%9B%BE+2025-02-23+16-34-27.png)

## [**cudnn**](https://developer.nvidia.com/rdp/cudnn-archive)

1.  如果你cuda toolkit是12的，就点击最新的12.x
    
2.  再选择适合自己的压缩包格式（tar）![.png](https://qianwen.alicdn.com/note/7e817b0aac83da9aa9c5cf44b9684433/QReuoN4p5skGm5wD/9e787f3794864e5c89513f2ac8143e84/.png)
    
3.  注册下载完后，终端进入到下载的文件夹
    
4.  依次执行
    

`tar -xf cudnn-linux-x86_64-8.9.7.29_cuda12-archive.tar.xz`

`sudo cp cudnn-linux-x86_64-8.9.7.29_cuda12-archive/include/* /usr/local/cuda-12.4/include`

`sudo cp cudnn-linux-x86_64-8.9.7.29_cuda12-archive/lib/libcudnn* /usr/local/cuda-12.4/lib64`

`sudo chmod a+r /usr/local/cuda-12.4/include/cudnn.h`

`sudo chmod a+r /usr/local/cuda-12.4/lib64/libcudnn*`

`cat /usr/local/cuda-12.4/include/cudnn_version.h | grep CUDNN_MAJOR -A 2`

![截图 2025-02-23 16-46-45.png](https://qianwen.alicdn.com/note/7e817b0aac83da9aa9c5cf44b9684433/QReuoN4p5skGm5wD/60a09f102dc047e495a264c5f213910e/%E6%88%AA%E5%9B%BE+2025-02-23+16-46-45.png)

如图即为成功

# 安装[**Cmake**](https://www.runoob.com/cmake/cmake-install-setup.html)

## 安装

下载[源码包](https://cmake.org/download/#latest)，解压进入目录，

命令行运行

`./bootstrap`

`make`

`sudo make install`

## 配置

# 安装gcc

[镜像站](https://mirrors.aliyun.com/gnu/gcc/?spm=a2c6h.25603864.0.0.7cd21de85nIQ5J)

*   解压源码包：
    

```plaintext
tar -xzvf gcc-14.0.0.tar.gz
cd gcc-14.0.0
```

### 下载 GCC 依赖项

GCC 编译需要一些额外的依赖库（如 GMP、MPFR、MPC 等）。运行以下命令自动下载并配置这些依赖：

```plaintext
./contrib/download_prerequisites
```

### 配置编译选项

1.  创建一个独立的构建目录（推荐）：
    

```plaintext
mkdir build
cd build
```

2.  配置 GCC 编译选项：
    

```plaintext
../configure --prefix=/usr/local/gcc-14 --enable-languages=c,c++ --disable-multilib
```

*   `--prefix=/usr/local/gcc-14`：指定安装目录。
    
*   `--enable-languages=c,c++`：只编译 C 和 C++ 编译器。
    
*   `--disable-multilib`：禁用多库支持（如果你不需要 32 位库）。
    

---

### 步骤 5：编译 GCC

1.  开始编译（使用多线程加速编译过程）：
    

```plaintext
make -j$(nproc)
```

*   `-j$(nproc)`：使用所有可用的 CPU 核心加速编译。
    

1.  编译过程可能需要较长时间（取决于你的硬件配置）。
    

---

### 步骤 6：安装 GCC

编译完成后，运行以下命令安装 GCC：

```plaintext
sudo make install
```
---

### 步骤 7：设置环境变量

1.  将 GCC 14 添加到系统的 PATH 中：
    

```plaintext
export PATH=/usr/local/gcc-14/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/gcc-14/lib64:$LD_LIBRARY_PATH
```

2.  将上述环境变量添加到 `~/.bashrc` 或 `~/.zshrc` 中，使其永久生效：
    

```plaintext
echo 'export PATH=/usr/local/gcc-14/bin:$PATH' >> ~/.bashrc
echo 'export LD_LIBRARY_PATH=/usr/local/gcc-14/lib64:$LD_LIBRARY_PATH' >> ~/.bashrc
source ~/.bashrc
```
---

### 步骤 8：验证安装

1.  检查 GCC 版本：
    

```plaintext
gcc --version
```

输出应显示 `gcc (GCC) 14.0.0`。

### 步骤 9：设置默认编译器（可选）

如果你希望将 GCC 14 设置为默认编译器，可以使用 `update-alternatives`：

1.  配置 `gcc` 和 `g++`：
    

```plaintext
sudo update-alternatives --install /usr/bin/gcc gcc /usr/local/gcc-14/bin/gcc 100
sudo update-alternatives --install /usr/bin/g++ g++ /usr/local/gcc-14/bin/g++ 100
```

2.  选择默认版本：
    

```plaintext
sudo update-alternatives --config gcc
sudo update-alternatives --config g++
```
---

### 注意事项

1.  编译时间：GCC 14 的编译可能需要较长时间（1-2 小时，取决于硬件配置）。
    
2.  磁盘空间：确保有足够的磁盘空间（至少 10GB）。
    
3.  兼容性：GCC 14 是最新版本，可能存在一些未修复的 bug。如果遇到问题，可以尝试使用较稳定的版本（如 GCC 13）。
    

---

# 快捷键

# 命令

### rm -rf <file\_path>

`rm -rf` 是 Linux 终端中一个非常强大且危险的命令，用于 强制删除文件或文件夹。

*   `rm`：`remove` 的缩写，用于删除文件或文件夹。
    
*   `-r`：`recursive` 的缩写，表示递归删除目录及其内容（即删除文件夹及其内部所有文件和子文件夹）。
    
*   `-f`：`force` 的缩写，表示强制删除，忽略不存在的文件或目录，并且不会提示确认。
