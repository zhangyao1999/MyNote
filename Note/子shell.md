## 启动.sh脚本的方式有三种
1 ./xx.sh
2 bash xx.sh 或者 sh xx.sh
3 . xx.sh 或者 source .sh

==. 和 source==都是shell的内嵌shell。

前俩种方式都是打开了一个子shell来执行脚本，执行完毕后关闭子shell，回到了父shell中，
而第三种这是直接在当前shell里执行，而无需打开子shell。这也是为什么我们修改完etc/profile之后 需要source一下的原因。

子shell与父shell的环境变量隔绝不可见。子shell中设置的环境变量，父shell不可见。

我们进入linux客户端后就启动了一个shell，然后再次输入bash 进入子shell，这是的子shell的ppid是父shell的pid，输入exit不会退出系统，只会退出子shell。
tbcs@kwephispre12534:~> ps -f
UID        PID  PPID  C STIME TTY          TIME CMD
tbcs     29354 29320  0 20:11 pts/6    00:00:00 -bash
tbcs     29442 29354  0 20:11 pts/6    00:00:00 ps -f
tbcs@kwephispre12534:~> ^C
tbcs@kwephispre12534:~> ps -f
UID        PID  PPID  C STIME TTY          TIME CMD
tbcs     29354 29320  0 20:11 pts/6    00:00:00 -bash
tbcs     29504 29354  0 20:12 pts/6    00:00:00 ps -f
tbcs@kwephispre12534:~> bash
tbcs@kwephispre12534:~> ps -f
UID        PID  PPID  C STIME TTY          TIME CMD
tbcs     ==29354== 29320  0 20:11 pts/6    00:00:00 -bash
tbcs     29507 ==29354==  0 20:12 pts/6    00:00:00 bash
tbcs     29540 29507  0 20:12 pts/6    00:00:00 ps -f
tbcs@kwephispre12534:~> exit
exit
tbcs@kwephispre12534:~>


