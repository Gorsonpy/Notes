@[TOC](目录)



# 前言

&ensp;&ensp;其实我一直对VSCode有点畏难，因为当初配置VSCode的C++开发环境花费了我很长的时间，之前的账户上写C++相关的东西大部分都是在Dev(刷题)和VS(工程)。VSCode更多是作为一个工具人的身份(**懂得都懂**,你甚至可以用VSCode来写代码),最近因为原先的电脑账户设成了中文名，又不敢修改用户名怕把文件搞崩了，就新建了一个英文名的账户，这样只需要重新配置一下一些软件的设置就可以(因为平常东西大部分也是放在D盘和E盘)，借此机会顺便重新安装配置了一下VSCode(**~~因为原来的配置实在有一点乱，虽然能写代码但是很多东西没配清楚，比如中文乱码之类的问题~~**)，以后就用VSCode代替Dev来写题目了。这篇文章内容除了如何配置VSCode的C++环境(就是那几个json文件)，**还会重点探讨一些其他的细节让你用VSCode能用的更爽一些,注意是用的爽而不是仅仅能用的程度.**



# 卸载

&ensp;&ensp; **~~说起来也是挺离谱的，但是学装VSCode前最好先学一下怎么卸载~~**，因为这个VSCode安装配置确实很容易出错，如果有某个环节错了然后你进行不下去，你又不能确定是不是本身组件已经损坏出的问题，那建议还是卸载重装。这个卸载重装也是有讲究的，最稳妥的，保证清理干净的步骤可以参考这篇文章，我完全是跟着他走的，所以这里就不画蛇添足自加解说了，追求稳妥的可以自己下一个ccleaner来清除一下卸载后无用注册表信息(免费版的就够用了，真的神器强烈安利)。

[<VSCode完美卸载>](https://www.cxyzjd.com/article/ZhaClew/103473489)



# 下载VSCode

&ensp;&ensp;**下载没啥可多说的，记得下载安装完先不着急打开**。

# 避免VSCode下载的插件强占C盘空间

&ensp;&ensp;VSCode安装的时候会询问你装在哪里，但实际上有一些地方(很占用空间的一个地方就是下载的插件保存位置，一个插件常常上百M)还是会强制装在C盘下，抢占系统盘空间(类似Chrome)，**可以用mklink建立符号链接解决这一类问题**.

**注意，刚安装完别打开VSCode，先来做这一步**:

管理员模式打开命令行:

```shell
mklink /d "C:\Users\你的用户名\.vscode\extensions" "D:\vscode\extensions"
```

做一些说明:

1. mklink的效果是把第一个文件位置变成快捷方式，后一个真正作为存储空间。所以这个方法真的特别好用，解决谷歌这类的强占空间的软件都可以用这种办法。
2. 第二个位置的地址你自己写，我这里只是一个示范，按照自己想装的位置写，**但是注意一定要提前创建好，该位置是存在的。**
3. **第一个位置相反，该文件夹要是尚未存在的，让系统帮你创建，否则会报错你该文件夹已经被创建。(所以上面要求你先不着急打开，因为你打开VSCode之后一旦下载插件了就会自动帮你创建extensions了，你就改不了了)。**
4. 两个地址之间有个空格。



# 配置C++环境

&ensp;&ensp;&ensp;这部分简略的说一下。

## 下载MingGW

&ensp;&ensp;首先要下载MingGW，我的建议是单独下载，**我知道这个地方网上很多人不会这样建议,而是会建议下载Dev/Clion, 用这两个软件自带的编译器。这个我只能说我试过dev的好像不行，Clion的没试过(也可能是我自己的问题)，单独另外下载MingGW是最保险的，仁者见仁。**

[<下载地址>](https://sourceforge.net/projects/mingw-w64/)



## 配置系统环境变量

  左下角搜索栏搜索env,

![image-20220210002541177](C:\Users\gorsonpy\AppData\Roaming\Typora\typora-user-images\image-20220210002541177.png)





![image-20220210000808607](C:\Users\gorsonpy\AppData\Roaming\Typora\typora-user-images\image-20220210000808607.png)



双击path进入，新建一条路径,&ensp;&ensp;将MingGW下载路径的bin加入系统环境变量的path里.即xx\\bin。

![image-20220210002659040](C:\Users\gorsonpy\AppData\Roaming\Typora\typora-user-images\image-20220210002659040.png)

# 下载C++插件

左边从上往下第五个就是下载插件的地方，搜索C++跳出来第一个就是，如果需要中文插件也可以一并下载了。



## 创建VSCode有效工作区

&ensp;&ensp;~~这个概念我自己编的~~，VSCode一个麻烦的地方就在于，他不像DEV或者VS那样，随便哪个地方创建C++文件，创完都能跑，他每个工作区都需要单独配置一次文件。所以强烈建议VSCode写的代码单独放在一个文件夹，这样不用多次配置。

1. 在你选好的地方创建一个文件夹，即你选定的“工作区”。比如我叫做VSCodeWorkPlace。

2. 用VSCode打开这个文件夹。

3. 在VSCode文件夹里创建一个叫做.vscode的子文件夹。在里面创建四个json文件。

   c_cpp_properties.json
   
   **注意路径要改成自己的，查看方法为命令行.**
   
   ```
   gcc -v -E -x c++ -
   ```
   
   底端那几行就是。
   
   ```json
   {
       "configurations": [
           {
               "name": "Win32",
               "includePath": [
                   "${workspaceRoot}",
                   "e:/mingw/include/**", //注意:从这一行开始往下的改成自己的路径
                   "e:/mingw/bin/../lib/gcc/mingw32/9.2.0/include/c++",
                   "e:/mingw/bin/../lib/gcc/mingw32/9.2.0/include/c++/mingw32",
                   "e:/mingw/bin/../lib/gcc/mingw32/9.2.0/include/c++/backward",
                   "e:/mingw/bin/../lib/gcc/mingw32/9.2.0/include",
                   "e:/mingw/bin/../lib/gcc/mingw32/9.2.0/../../../../include",
                   "e:/mingw/bin/../lib/gcc/mingw32/9.2.0/include-fixed"
               ],
               "defines": [
                   "_DEBUG",
                   "UNICODE",
                   "__GNUC__=6",
                   "__cdecl=__attribute__((__cdecl__))"
               ],
               "intelliSenseMode": "msvc-x64",
               "browse": {
                   "limitSymbolsToIncludedHeaders": true,
                   "databaseFilename": "",
                   "path": [
                       "${workspaceRoot}",
                       "e:/mingw/include/**", //注意:从这一行开始往下的改成自己的路径
                       "e:/mingw/bin/../lib/gcc/mingw32/9.2.0/include/c++",
                       "e:/mingw/bin/../lib/gcc/mingw32/9.2.0/include/c++/mingw32",
                       "e:/mingw/bin/../lib/gcc/mingw32/9.2.0/include/c++/backward",
                       "e:/mingw/bin/../lib/gcc/mingw32/9.2.0/include",
                       "e:/mingw/bin/../lib/gcc/mingw32/9.2.0/../../../../include",
                       "e:/mingw/bin/../lib/gcc/mingw32/9.2.0/include-fixed"
                   ]
               }
           }
       ],
       "version": 4
   }
   
   
   ```
   
   launch.json
   
   ```json
   {
     "version": "0.2.0",
     "configurations": [
       {
         "name": "(gdb) Launch", // 配置名称，将会在启动配置的下拉菜单中显示
         "type": "cppdbg", // 配置类型，这里只能为cppdbg
         "request": "launch", // 请求配置类型，可以为launch（启动）或attach（附加）
         "program": "${workspaceFolder}/exe/${fileBasenameNoExtension}.exe",// 将要进行调试的程序的路径
         "args": [],             // 程序调试时传递给程序的命令行参数，一般设为空即可
         "stopAtEntry": false, // 设为true时程序将暂停在程序入口处，一般设置为false
         "cwd": "${workspaceFolder}", // 调试程序时的工作目录，一般为${workspaceFolder}即代码所在目录
         "environment": [],
         "externalConsole": true, // 调试时是否显示控制台窗口，一般设置为true显示控制台
         "MIMode": "gdb",
         "miDebuggerPath": "E:/mingw/bin/gdb.exe", // miDebugger的路径，注意这里要与MinGw的路径对应
         "preLaunchTask": "g++", // 调试会话开始前执行的任务，一般为编译程序，c++为g++, c为gcc
         "setupCommands": [
           {
             "description": "Enable pretty-printing for gdb",
             "text": "-enable-pretty-printing",
             "ignoreFailures": true
           }
         ]
       }
     ]
   }
   
   ```
   
   settings.json
   
   ```json
   {
       "C_Cpp.intelliSenseEngineFallback": "Disabled", //最上面这两行是因为我的VSCode不知道为什么抽风,一直会报错cin和cout，推测作用是关闭错误提示
       "C_Cpp.intelliSenseEngine": "Tag Parser",  //  可以不要这两行
   
   
   
       "editor.fontSize": 20,
       "editor.mouseWheelZoom": true,
       "window.zoomLevel": 0,
       "files.autoGuessEncoding": true,
   
   
       "C_Cpp.errorSquiggles": "Enabled", // 是否使用默认图片
       "background.enabled": false
   }
   ```
   
   tasks.json
   
   ```json
   {
       "version": "2.0.0",
       "command": "g++",
       "args": [
           "-g",
           "${file}",
           "-o",
           "${workspaceFolder}/exe/${fileBasenameNoExtension}.exe"  //这个地方的作用是会把cpp文件编译后生成的exe单独放在一个文件夹
       ], // 编译命令参数
       "problemMatcher": {
           "owner": "cpp",
           "fileLocation": [
               "relative",
               "\\"
           ],
           "pattern": {
               "regexp": "^(.*):(\\d+):(\\d+):\\s+(warning|error):\\s+(.*)$",
               "file": 1,
               "line": 2,
               "column": 3,
               "severity": 4,
               "message": 5
           }
       }
   }
   
   ```

  

# VSCode闪退问题

&ensp;&ensp;VSCode一个比较让人诟病的地方就是会闪退，即调试完成后关闭控制台，通常的解决办法就是代码结尾必须加一行

```
system("pause");
```

可以说是非常不方便了.

一种解决办法是下载CodeRunner插件，用右上角的运行按钮不适用F5，直接在VSCode中运行不弹出黑框(类似IDEA)

![image-20220210164518485](C:\Users\gorsonpy\AppData\Roaming\Typora\typora-user-images\image-20220210164518485.png)



# 分离exe和cpp文件

&ensp;&ensp;经过我们在tasks.json中的设置，cpp文件和exe文件会分别放在两个文件夹里，大概长这样:

![image-20220210164721885](C:\Users\gorsonpy\AppData\Roaming\Typora\typora-user-images\image-20220210164721885.png)

# 中文乱码问题

&ensp;&ensp;最后讲一讲中文乱码问题，有两种办法:

# 更改右下角的编码:

&ensp;&ensp;![image-20220210161657359](C:\Users\gorsonpy\AppData\Roaming\Typora\typora-user-images\image-20220210161657359.png)

把UTF-8更改成GBK。

**这种做法的缺点是,有可能下次写个新的文件又要重新更改，没法根本解决.**

## 启用beta版

&ensp;&ensp;推测这种办法能够成功的原因是VSCode获取的编码支持来自于powershell/cmd。具体做法是打开控制面板-时钟和区域-区域-更改系统区域和设置-勾选启用bata版获取全球字符支持.

![image-20220210162320304](C:\Users\gorsonpy\AppData\Roaming\Typora\typora-user-images\image-20220210162320304.png)

**这种办法能够根本解决，但是存在一些副作用，电脑里少数文件，尤其是早版本的解压后文件名字可能出现乱码，我更改后有一段时间了，在可接受的范围内.建议自行斟酌影响.**
