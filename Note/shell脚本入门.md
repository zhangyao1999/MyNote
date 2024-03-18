## 首先新建一个以.sh后缀结尾的文件
```shell
#!/bin/bash
echo "Hello World !"
```
 - `#!` 是一个约定的标记，它告诉系统这个脚本需要什么解释器来执行，即使用哪一种 Shell。
 - echo 命令用于向窗口输出文本。
## 然后执行脚本
使用`chmod 777 *.sh` 命令使得文件可以直接通过./test.sh来执行。


也可以通过使用`bash test.sh` 或者 . xx.sh 或者source xx.sh（. 和 source 是shell的内嵌）来直接执行，这种情况下不需要设置权限。这里涉及到了[[子shell]]。

`./test.sh`来执行。*注意此处不可以直接输入`test.sh`这样的话编译器会去path环境变量下去找test.sh的可执行文件，结果自然是找不到的，要用`./test.sh`告诉是在当前文件下*。
## 多名令脚本实例
**在/Users/zhangyao/Documents/StudyShell目录下创建out.txt文件，并写入“你好！”**
```Shell
#!/bin/bash

cd /Users/zhangyao/Documents/StudyShell/

touch out.txt

echo "你好！" >> out.txt
```

