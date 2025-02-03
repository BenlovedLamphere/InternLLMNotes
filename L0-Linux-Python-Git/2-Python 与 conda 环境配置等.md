# Conda 虚拟环境



## 创建与管理虚拟环境

### 创建

``` bash
conda create --name myenv python=3.9
```

### 激活

``` bash
conda activate myenv
```

### 退出

``` bash
conda deactivate
```

### 其他常见的虚拟环境管理命令还有

``` bash
#查看当前设备上所有的虚拟环境
conda env list
#查看当前环境中安装了的所有包
conda list
#删除环境（比如要删除myenv）
conda env remove myenv
#经测试如下删除更好用：
conda remove --name myenv --all
```

### 如果要创建虚拟环境到指定目录

``` bash
conda create --prefix /root/envs/myenv python=3.9
```

### 激活指定目录下的 conda 环境

``` bash
conda activate /root/envs/myenv
```



## pip 安装 Python 依赖包

注意在使用conda的时候，我们需要先激活我们要用的虚拟环境，再在激活的虚拟环境中，使用pip来安装包。

### 使用 pip 安装包

``` bash
pip install <somepackage> # 安装单个包，<somepackage>替换成你要安装的包名
pip install pandas numpy # 安装多个包，如panda和numpy
pip install numpy==2.0 # 指定版本安装
pip install numpy>=1.19,<2.0 # 使用版本范围安装
```

### 使用 requirement.txt 文件安装所有依赖

requirements.txt在各种开源代码中经常可以看到，里面描述了运行该代码所需要的包和对应版本。

``` bash
pip install -r requirements.txt
```

比如以下就是我们接下来会接触到的LLM部署框架lmdeploy的requirements.txt 的一部分（只做展示，大家不用自行安装）

``` bash
accelerate>=0.29.3
mmengine-lite
numpy<2.0.0
openai
peft<=0.11.1
transformers
triton>=2.1.0,<=2.3.1;
```

### 将依赖安装到指定目录

为了节省大家的存储空间，本次实战营可以直接使用share目录下的conda环境，但share目录只有读权限，所以要安装额外的包时我们不能直接使用pip将包安装到对应环境中，需要安装到我们自己的目录下。

这时我们在使用pip的时候可以使用`--target`或`-t`参数来指定安装目录，此时pip会将你需要安装的包安装到你指定的目录下。

这里我们用本次实战营最常用的环境`/root/share/pre_envs/pytorch2.1.2cu12.1`来举例。

``` bash
# 首先激活环境
conda activate /root/share/pre_envs/pytorch2.1.2cu12.1

# 创建一个目录/root/myenvs，并将包安装到这个目录下
mkdir -p /root/myenvs
pip install <somepackage> --target /root/myenvs

# 注意这里也可以使用-r来安装requirements.txt
pip install -r requirements.txt --target /root/myenvs

```

要使用安装在指定目录的python包，可以在python脚本开头临时动态地将该路径加入python环境变量中去

``` bash
import sys  
  
# 你要添加的目录路径  
your_directory = '/root/myenvs'  
  
# 检查该目录是否已经在 sys.path 中  
if your_directory not in sys.path:  
    # 将目录添加到 sys.path  
    sys.path.append(your_directory)  
  
# 现在你可以直接导入该目录中的模块了  
# 例如：import your_module

```

### 在VS Code 中使用命令行监听端口进行 debug

``` bash
python -m debugpy --listen 5678 --wait-for-client ./test.py
```

如果没有安装 debugpy ，应当先 pip install 安装 debugpy。

如果提示 `Debugger warning: It seems that frozen modules are being used, which may make the debugger miss breakpoints. Please pass -Xfrozen_modules=off to python to disable frozen modules.` 可以加上 `-Xfrozen_modules=off` ：

``` bash 
python -m -Xfrozen_modules=off debugpy --listen 5678 --wait-for-client ./myscript.py
```

以上情况亲测无用。

使用如下命令行关闭文件验证：

``` bash
export PYDEVD_DISABLE_FILE_VALIDATION=1
```

然后再运行

``` bash
python -m debugpy --listen 5678 --wait-for-client ./test.py
```

运行后点击 vscode 中的运行绿色按钮，可正常运行，但断点会被忽略。

### 简化如上命令

在`linux`系统中，可以对 *~/.bashrc* 文件中添加以下命令

``` bash
alias pyd='python -m debugpy --wait-for-client --listen 5678'
```

然后执行

``` bash
source ~/.bashrc
```

这样之后使用 pyd 命令(你可以自己命名) 替代 python 就能在命令行中起debug了，之前的debug命令就变成了:

``` bash
pyd ./test.py
```

在书生的 api key（学习书生用）

``` javascript
eyJ0eXBlIjoiSldUIiwiYWxnIjoiSFM1MTIifQ.eyJqdGkiOiI4MDAwNDc2NiIsInJvbCI6IlJPTEVfUkVHSVNURVIiLCJpc3MiOiJPcGVuWExhYiIsImlhdCI6MTczODQ4NDU2MSwiY2xpZW50SWQiOiJlYm1ydm9kNnlvMG5semFlazF5cCIsInBob25lIjoiMTM2NDE5MTc3NTIiLCJ1dWlkIjoiZmZhNTNhNWItODIyZC00NTkyLTllNmYtNDhjN2ZmNDlkYTMxIiwiZW1haWwiOiIiLCJleHAiOjE3NTQwMzY1NjF9.GMzIyPzT5AwaEM3ZddUhzzPvw5tnzEeVJxtRdIF-tn7BaEFPiVcUYQBp1DIjBuCyH0Kb4HQimlVwe2_LBMkEtw
```



