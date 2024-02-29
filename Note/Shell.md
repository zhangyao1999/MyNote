## 概述
是一个命令行解释器，接受应用程序或者用的命令，来调动操作系统的内核。这里我们主要说的是为Shell编写的脚本程序，而不是开发Shell自身。Shell环境一般位于linux系统的`/bin/bash`。
## 第一个Shell脚本
- 首先新建一个以.sh后缀结尾的文件
```shell
#!/bin/bash
echo "Hello World !"
```
### 脚本解释
- `#!` 是一个约定的标记，它告诉系统这个脚本需要什么解释器来执行，即使用哪一种 Shell。
	- 这里可以通过`cat /etc/shells`命令查看这个系统有哪些shell，例如Mac系统下有这些新版的mac一般都是zsh linux 一般是bash。
	- 可以使用`echo $SHELL`命令查看当前系统使用哪种解析器。
- echo 命令用于向窗口输出文本。
### 执行脚本
- 使用`chmod 777 *.sh` 命令使得文件可以直接通过./test.sh来执行。
- 也可以通过使用`bash test.sh`来直接执行，这种情况下不需要设置权限。
- `./test.sh`来执行。*注意此处不可以直接输入`test.sh`这样的话编译器会去path环境变量下去找test.sh的可执行文件，结果自然是找不到的，要用`./test.sh`告诉是在当前文件下*。
### 多名令脚本实例
- **在/Users/zhangyao/Documents/StudyShell目录下创建out.txt文件，并写入“你好！”**
```Shell
#!/bin/bash

cd /Users/zhangyao/Documents/StudyShell/

touch out.txt

echo "你好！" >> out.txt
```
