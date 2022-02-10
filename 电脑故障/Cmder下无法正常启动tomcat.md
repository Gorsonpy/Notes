# 问题描述

&ensp;&ensp; 今天下载了Tomcat 8.5.75的版本，按照要求配置好JAVA_HOME和JRE_HOME之后，报错:![image-20220207230103115](C:\Users\gorsonpy\AppData\Roaming\Typora\typora-user-images\image-20220207230103115.png)

提示The system cannot find the path specified.


# 解决办法
&ensp;&ensp;一开始还以为是自己的环境变量位置配错了，后面发现是Cmder的原因。因为某种不可知的原因，Cmder似乎不能作为Tomcat的启动承载，而我之前把Cmder强制注册成默认终端取代了cmd，所以报错。改用powershell或者cmd后解决问题可以正常启动。
