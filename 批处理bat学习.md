## 批处理bat学习 (2018.6.29)
* [批处理常用命令总结 - 批处理命令简介](http://xstarcd.github.io/wiki/windows/windows_cmd_summary_commands.html)

1. `@`
*  在批处理中隐藏命令行本身的回显
2. `rem`
* 在批处理文件或配置文件中加入注释
```
当echo状态为关闭（echo off）时rem和@rem 作用相同，均无显示 
当echo状态为开启（echo on ）时
命令提示符后将显示出 rem注释的内容，@rem 则不显示该命令行。
```
```
test.bat的内容为:
@rem my name is Galen!
pause

execute后的结果是：

C:\Users\dglong\Desktop>pause
请按任意键继续. . .

```
```
test.bat的内容为:
rem my name is Galen!
pause

execute后的结果是：


C:\Users\dglong\Desktop>rem my name is Galen!

C:\Users\dglong\Desktop>pause
请按任意键继续. . .
```
3. `copy`
```
* 把 P2.py从F盘的Galen目录下复制到F盘根目录下

@echo off
:begin
copy F:\Galen\P2.py F:\
pause
```
4. `start`
```
调用外部程序，所有的DOS命令和命令行程序都可以由start命令来调用。 如：start calc.exe 即可打开Windows的计算器
```
5. `set`
* set : 显示批处理当前已定义的所有变量及其值
* set s : 显示所有以s开头的变量及值
* set aa=abcd : 此句命令便可向变量aa赋值abcd
* set aa=   : 此句命令即可删除变量aa
* set/? : set的完整说明
```
批处理中的变量是不区分类型的，不需要像C语言中的变量那样还要区分int、float、char等。比如执行set aa=345后，变量aa的值既可以被视为数字345，也可以被视为字符串345
```
```
注：如果对某一命令还不是很熟悉，可以在命令行窗口下输入：命令名/?的方式来获得帮助
```
6. `echo`
```
@                    #关闭单行回显
echo off             #从下一行开始关闭回显
@echo off            #从本行开始关闭回显。一般批处理第一行都是这个
echo on              #从下一行开始打开回显
echo                 #显示当前是 echo off 状态还是 echo on 状态
echo.                #输出一个"回车换行"，一般就是指空白行
echo hello world     #输出hello world
```
7. `dir`
```
dir                 #显示当前目录中的文件和子目录
dir /a              #显示当前目录中的文件和子目录，包括隐藏文件和系统文件
dir c: /a:d         #显示 C 盘当前目录中的目录
dir c:/ /a:-d       #显示 C 盘根目录中的文件dir d:/mp3 /b/p     #逐屏显示 d:/mp3 目录里的文件，只显示文件名，不显示时间和大小
dir *.exe /s        #显示当前目录和子目录里所有的.exe文件其中 * 是通配符，代表所有的文件名，还一个通配符 ? 代表一个
                    #任意字母或汉字如 c*.* 代表以 c 开头的所有文件?.exe 代表所有文件名是一个字母的.exe文件如果指定的目录或文件
                    #不存在，将返回 errorlevel 为1;

# 每个文件夹的 dir 输出都会有2个子目录 . 和 ... 代表当前目录.. 代表当前目录的上级目录
dir .               #显示当前目录中的文件和子目录
dir ..              #显示当前目录的上级目录中的文件和子目录
```
8. `cd`
* cd mp3              #进入当前目录中的mp3 目录
* cd ..               #进入当前目录中的上级目录
* cd  \               #进入根目录
* cd                  #显示当前目录

9. `md : 创建目录`
* md abc       : #在当前目录里建立子目录 abc
* md f:\a\b\c  : #如果 d:/a 不存在，将会自动创建

10. `rd : 删除目录`
* rd f:\a\b\c  ： 删除目录c

11. `call : 调用另一个批处理程序`
* [批处理命令——call 和 start](http://www.cnblogs.com/Braveliu/p/5078283.html)
* call test.bat

12. `del : 删除文件`
* del d:\test.txt
* del d:\test\*.*

13. `ren : 文件重命名`
* ren 1.txt 2.bak     #把 1.txt 更名为 2.bak

14. `type : 显示文件内容`
* type  C:\Users\dglong\Desktop\echo.txt

15. `cls : 清屏cmd界面`
```
echo on
dir
pause
cls
pause
type  C:\Users\dglong\Desktop\echo.txt
pause
```
12. `title : 设置cmd窗口的标题`
* title 新标题        #设置cmd窗口的标题栏变了

13. `find (外部命令)查找命令`
```
find "abc" c:/test.txt      在 c:/test.txt 文件里查找含 abc 字符串的行如果找不到，将设 errorlevel 返回码为1
find /i "abc" c:/test.txt   查找含 abc 的行，忽略大小写
find /c "abc" c:/test.txt   显示含 abc 的行的行数
```

14. `tree : 显示目录结构`
* tree f:

15. `&  : 顺序执行多条命令，而不管命令是否执行成功`
* title Galen & type  C:\Users\dglong\Desktop\echo.txt

16. `&& : 顺序执行多条命令，当碰到执行出错的命令后将不执行后面的命令`
* title Galen && type  C:\Users\dglong\Desktop\echo.txt

17. `> 和 >>` 
* > 清除文件中原有的内容后再写入
* >> 追加内容到文件末尾，而不会清除原有的内容主要将本来显示在屏幕上的内容输出到指定文件中指定文件如果不存在，则自动生成该文件

```
echo hello world>c:/test.txt   生成c:/test.txt文件，内容为hello world这个格式在批处理文件里用得很多，可以生成.reg .bat .vbs 等临时文件
type c:/test.txt >prn          屏幕上不显示文件内容，转向输出到打印机
echo hello world>con           在屏幕上显示hello world，实际上所有输出都是默认 >con 的
copy c:/test.txt f: >nul       拷贝文件，并且不显示"文件复制成功"的提示信息，但如果f盘不存在，还是会显示出错信息
copy c:/test.txt f: >nul 2>nul 不显示"文件复制成功"的提示信息，并且f盘不存在的话，也不显示错误提示信息
```

18. `命令行参数`
```
%0 %1 %2 %3 %4 %5 %6 %7 %8 %9 %*命令行传递给批处理的参数
%0 批处理文件本身
%1 第一个参数
%9 第九个参数
%* 从第一个参数开始的所有参数
```