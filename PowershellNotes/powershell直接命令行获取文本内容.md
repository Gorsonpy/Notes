  @[TOC](目录)
  # 前言
  &ensp;&ensp;往常powershell都是直接用notepad方式打开某个文本，今天突发奇想，如果那个文本本身不是txt的，我又是只想读他的内容该怎么办? 


  # 目的
  &ensp;&ensp;![在这里插入图片描述](https://img-blog.csdnimg.cn/f2f1fea4ccfb46b08f97d07850a81d44.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAVHJlZVRyYXZlbGVy,size_20,color_FFFFFF,t_70,g_se,x_16) 这个目录下有一个Brand.java文件，我只是想要里面的代码(文本),不用记事本而是直接命令行读里面内容.

  # 操作
  ```
  get-content Brand.java
  ```
  即可直接在命令行打印内容。
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/44818428499d47a09627b96ec0f69666.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAVHJlZVRyYXZlbGVy,size_20,color_FFFFFF,t_70,g_se,x_16)

# 总结
PowerShell直接在界面获取文本内容方法:
1.get-content 当前路径下某文件名(含拓展名)/指定路径文件名(含拓展名)
2.get-content可以简写为cat.
