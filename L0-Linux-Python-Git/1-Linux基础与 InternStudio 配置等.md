# Linux 与 InternStudio && VS Code SSH 开发配置



## InternStudio 的开发机常用命令：

查看开发机名称：

``` bash 
hostname
```

查看开发机内核信息：

``` bash
uname -a
```

查看开发机版本信息：

``` bash
lsb_release -a
```

查看 GPU 信息：

``` bash
nvidia-smi
```

退出远程连接(两次 exit)：

``` bash
exit
```



## Linux 基础命令

- **创建文件**：可以使用 `touch` 命令创建空文件。
- **创建目录**：使用 `mkdir` 命令。
- **目录切换**：使用`cd`命令。
- **显示所在目录**：使用`pwd`命令。
- **查看文件内容**：如使用 `cat` 直接显示文件全部内容，`more` 和 `less` 可以分页查看。
- **编辑文件**：如 `vi` 或 `vim` 等编辑器。
- **复制文件**：用 `cp` 命令。
- **创建文件链接**：用`ln`命令。
- **移动文件**：通过 `mv` 命令。
- **删除文件**：使用 `rm` 命令。
- **删除目录**：`rmdir`（只能删除空目录）或 `rm -r`（可删除非空目录）。
- **查找文件**：可以用 `find` 命令。
- **查看文件或目录的详细信息**：使用`ls`命令，如使用 `ls -l`查看目录下文件的详细信息。
- **处理文件**：进行复杂的文件操作，可以使用`sed`命令。

### cp 与 ln 

**cp** 命令在后面课程中会经常用到，它是用来将一个文件或者目录复制到另一个目录下的操作，常用的使用有：

- 复制文件：cp 源文件 目标文件
- 复制目录：cp -r 源目录 目标目录

但是如果我们是要使用模型的话，这种操作会占用大量的磁盘空间，所以我们一般使用`ln`命令，这个就和windows的快捷方式一样。linux中链接分为两种 : **硬链接**(hard link)与**软链接**(symbolic link)，硬链接的意思是一个档案可以有多个名称，而软链接的方式则是产生一个特殊的档案，该档案的内容是指向另一个档案的位置。硬链接是存在同一个文件系统中，而软链接却可以跨越不同的文件系统。

所以我们一般使用软连接，它的常用的使用方法如下：

```
ln [参数][源文件或目录][目标文件或目录]
```



参数如下：

- -s：创建软链接（符号链接）也是最常用的；
- -f：强制执行，覆盖已存在的目标文件；
- -i：交互模式，文件存在则提示用户是否覆盖；
- -n：把符号链接视为一般目录；
- -v：显示详细的处理过程。
- 

### **mv 和 rm**

`mv`命令和`rm`命令的使用方式很相似，但是`mv`是用来移动文件或者目录的，同时还可以进行重命名。`rm`命令则是用来删除文件或者目录的。

常用的使用方法如下：

- **mv 命令**：

常用参数：

- `-i`：交互模式，覆盖前询问。
- `-f`：强制覆盖。
- `-u`：只在源文件比目标文件新时才进行移动。

使用示例：

- `mv file1.txt dir1/`：将文件 `file1.txt` 移动到目录 `dir1` 中。
- `mv file1.txt file2.txt`：将文件 `file1.txt` 重命名为 `file2.txt`。
- **rm 命令**：

常用参数：

- `-i`：交互模式，删除前询问。
- `-f`：强制删除，忽略不存在的文件，不提示确认。
- `-r`：递归删除目录及其内容。

使用示例：

- `rm file.txt`：删除文件 `file.txt`。
- `rm -r dir1/`：递归删除目录 `dir1` 及其所有内容。

删除目录的命令也可以使用`rmdir`。

### **find**



`find`命令是Linux系统中一个强大的文件搜索工具，它可以在指定的目录及其子目录中查找符合条件的文件或目录，并执行相应的操作。

以下是`find`命令的一些常见用法：

1. **按文件名查找**：使用`-name`选项按照文件名查找文件。例如，`find /path/to/directory -name "file.txt"`将在指定目录及其子目录中查找名为`file.txt`的文件。
2. **按文件类型查找**：使用`-type`选项按照文件类型查找文件。例如，`find /path/to/directory -type f`将查找指定目录及其子目录中的所有普通文件。
3. **按文件大小查找**：使用`-size`选项按照文件大小查找文件。例如，`find /path/to/directory -size +100M`将查找指定目录及其子目录中大于100MB的文件。
4. **按修改时间查找**：使用`-mtime`、`-atime`或`-ctime`选项按照文件的修改时间、访问时间或状态更改时间查找文件。例如，`find /path/to/directory -mtime -7`将查找指定目录及其子目录中在7天内修改过的文件。
5. **按文件权限查找**：使用`-perm`选项按照文件权限查找文件。例如，`find /path/to/directory -perm 755`将查找指定目录及其子目录中权限为755的文件。
6. **按用户或组查找**：使用`-user`或`-group`选项按照文件的所有者或所属组查找文件。例如，`find /path/to/directory -user username`将查找指定目录及其子目录中属于用户`username`的文件。
7. **执行操作**：使用`-exec`选项可以对找到的文件执行相应的操作。例如，`find /path/to/directory -name "*.txt" -exec rm {} \;`将删除找到的所有以`.txt`结尾的文件。

### **ls**



`ls`命令可以用来列出目录的内容以及**详细信息**。

常用参数及使用方法如下：

- `-a`：显示所有文件和目录，包括隐藏文件（以`.`开头的文件或目录）。
- `-l`：以长格式显示详细信息，包括文件权限、所有者、大小、修改时间等。
- `-h`：与`-l`结合使用，以人类可读的方式显示文件大小（如`K`、`M`、`G`等）。
- `-R`：递归列出子目录的内容。
- `-t`：按文件修改时间排序显示。、

### **sed**



`sed`命令是一种流编辑器，主要用于文本处理，在处理复杂的文件操作时经常用到，在后续的课程中会使用到，`sed`命令常用参数及使用示例如下：

- 参数说明：
  - `-e<script>` 或 `--expression=<script>`：直接在命令行中指定脚本进行文本处理。
  - `-f<script文件>` 或 `--file=<script文件>`：从指定的脚本文件中读取脚本进行文本处理。
  - `-n` 或 `--quiet` 或 `--silent`：仅打印经过脚本处理后的输出结果，不打印未匹配的行。
- 动作说明：
  - `a`：在当前行的下一行添加指定的文本字符串。
  - `c`：用指定的文本字符串替换指定范围内的行。
  - `d`：删除指定的行。
  - `i`：在当前行的上一行添加指定的文本字符串。
  - `p`：打印经过选择的行。通常与 `-n` 参数一起使用，只打印匹配的行。
  - `s`：使用正则表达式进行文本替换。例如，`s/old/new/g` 将所有 "InternLM" 替换为 "InternLM yyds"。

`grep`是一个强大的文本搜索工具。常用参数如下：

- `-i`：忽略大小写进行搜索。
- `-v`：反转匹配，即显示不匹配的行。
- `-n`：显示行号。
- `-c`：统计匹配的行数。



### 进程管理



**进程管理**命令是进行系统监控和进程管理时的重要工具，常用的进程管理命令有以下几种：

- **ps**：查看正在运行的进程
- **top**：动态显示正在运行的进程
- **pstree**：树状查看正在运行的进程
- **pgrep**：用于查找进程
- **nice**：更改进程的优先级
- **jobs**：显示进程的相关信息
- **bg 和 fg**：将进程调入后台
- **kill**：杀死进程

在开发机中还有一条特殊的命令`nvidia-smi`，它是 NVIDIA 系统管理接口（NVIDIA System Management Interface）的命令行工具，用于监控和管理 NVIDIA GPU 设备。它提供了一种快速查看 GPU 状态、使用情况、温度、内存使用情况、电源使用情况以及运行在 GPU 上的进程等信息的方法。

下面是关于各个命令使用示例：

- `ps`：列出当前系统中的进程。使用不同的选项可以显示不同的进程信息，例如：

```
ps aux  # 显示系统所有进程的详细信息
```



- `top`：动态显示系统中进程的状态。它会实时更新进程列表，显示CPU和内存使用率最高的进程。

```
top  # 启动top命令，动态显示进程信息
```


- `pstree`：以树状图的形式显示当前运行的进程及其父子关系。

```
pstree  # 显示进程树
```


- `pgrep`：查找匹配条件的进程。可以根据进程名、用户等条件查找进程。

```
pgrep -u username  # 查找特定用户的所有进程
```


- `nice`：更改进程的优先级。`nice`值越低，进程优先级越高。

```
nice -n 10 long-running-command  # 以较低优先级运行一个长时间运行的命令
```


- `jobs`：显示当前终端会话中的作业列表，包括后台运行的进程。

```
jobs  # 列出当前会话的后台作业
```


- `bg`和`fg`：`bg`将挂起的进程放到后台运行，`fg`将后台进程调回前台运行。

```
bg  # 将最近一个挂起的作业放到后台运行
fg  # 将后台作业调到前台运行
```


- `kill`：发送信号到指定的进程，通常用于杀死进程。

```
kill PID  # 杀死指定的进程ID
```


  - 注意，`kill` 命令默认发送 `SIGTERM` 信号，如果进程没有响应，可以使用`-9`使用`SIGKILL` 信号强制杀死进程：

```
kill -9 PID  # 强制杀死进程    
```


> `SIGTERM`（Signal Termination）信号是Unix和类Unix操作系统中用于请求进程终止的标准信号。当系统或用户想要优雅地关闭一个进程时，通常会发送这个信号。与`SIGKILL`信号不同，`SIGTERM`信号可以被进程捕获并处理，从而允许进程在退出前进行清理工作。（来源于网络）

### 以下是 `nvidia-smi` 命令的一些基本命令用法：

- 显示 GPU 状态的摘要信息：

```
nvidia-smi
```

​    

- 显示详细的 GPU 状态信息：

```
nvidia-smi -l 1
```

​    

  - 这个命令会每1秒更新一次状态信息。

- 显示 GPU 的帮助信息：

```
nvidia-smi -h
```

​    

- 列出所有 GPU 并显示它们的 PID 和进程名称：

```
nvidia-smi pmon
```

​    

- 强制结束指定的 GPU 进程：

```
nvidia-smi --id=0 --ex_pid=12345
```

​    

  - 这会强制结束 GPU ID 为 0 上的 PID 为 12345 的进程。

- 设置 GPU 性能模式：

```
nvidia-smi -pm 1
nvidia-smi -i 0 -pm 1
```

​    

  - 第一个命令会为所有 GPU 设置为性能模式，第二个命令只针对 ID 为 0 的 GPU。

- 重启 GPU：

```
nvidia-smi --id=0 -r
```

​    

  - 这会重启 ID 为 0 的 GPU。



### Conda 与 Shell 

查看版本：

``` bash
conda --version
```

查看 Conda 配置：

``` bash
conda config --show
```

设置国内镜像：

```bash
#设置清华镜像
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/pro
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2
```

创建虚拟环境：

``` bash
conda create -n name python=3.10
```

也可以同时安装必要的包：

``` bash
conda create -n name numpy matplotlib python=3.10（但是不建议大家这样用）
```

创建虚拟环境的常用参数如下：

- -n 或 --name：指定要创建的环境名称。
- -c 或 --channel：指定额外的软件包通道。
- --clone：从现有的环境克隆来创建新环境。
- -p 或 --prefix：指定环境的安装路径（非默认位置）。

查看有哪些虚拟环境：

``` bash
conda env list
conda info -e
conda info --envs
```

激活与退出虚拟环境：

``` bash
conda activate name (激活)
conda activate（退出）
conda deactivate（退出）
```

删除与导出虚拟环境：

``` bash
conda remove --name name --all （删除）
conda remove --name name  package_name（只删除某个虚拟环境中的某些包）
conda env export --name myenv > myenv.yml（获得/导出环境中的所有配置）
conda env create -f  myenv.yml（重新还原环境）
```



### conda和pip的区别

1. conda可以管理非python包，pip只能管理python包。
2. conda可以用来创建虚拟环境，pip不能，需要依赖virtualenv之类的包。
3. conda安装的包是编译好的**二进制文件**，安装包文件过程中会自动安装依赖包；pip安装的包是**wheel或源码**，装过程中不会去支持python语言之外的依赖项。
4. conda安装的包会统一下载到当前虚拟环境对应的目录下，下载一次多次安装。pip是直接下载到对应环境中。

> **Wheel** 是一种 Python 安装包的格式。
>
> 它是一种预编译的二进制分发格式，类似于 conda 中的已编译二进制文件。
>
> Wheel 格式的主要优点包括：
>
> 1. 安装速度快：因为已经进行了预编译，所以在安装时不需要像源码安装那样进行编译过程，节省了时间。
> 2. 一致性：确保在不同的系统和环境中安装的结果是一致的。
>
> 例如，如果您要安装一个大型的 Python 库，使用 Wheel 格式可以避免在不同的机器上因为编译环境的差异而导致的安装问题。而且，对于那些没有编译环境或者编译能力较弱的系统，Wheel 格式能够让安装过程更加顺畅。



### VI or VIM

#### 命令模式：: to 末行模式，i / a / o to 编辑模式，编辑模型 ESC to 命令模式。

删除一行：dd

复制一行：yy

粘贴：p

到行首：gg

到行尾 ：G

保存退出：ZZ

#### 末行模式：ESC to 命令模式

保存退出：:wq

不保存退出：:q!

保存：:w

查找：/

