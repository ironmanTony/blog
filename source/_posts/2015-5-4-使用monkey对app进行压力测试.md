title: 使用monkey对app进行压力测试
date: 2015-05-4 10:42:24
tags:
---
其实monkey压力测试也不需要怎么去配置，只是有一些参数。

-----------
* 使用adb shell来连接一个模拟器或者真机。    
直接adb shell

* 使用monkey -p packagename -v times 随机生成times个event来测试packagename的default界面。     
>比如：monkey -p com.tencent.mobileqq -v 5000    
对qq来进行压力测试。

  或者monkey -p packagename --pct-touch 100 -v times。`-v times`是一定要带上的。

---------------
## 这些命令都简单，但是我现在想要获取到qq的包名。

使用命令`pm list packages -f `就可以获取到设备上所有已经安装的包名。    
这样就获取到qq的包名为：com.tencent.mobileqq
这样我就可以使用monkey来玩qq了。     

----------
本来想用这种方式来测试一下是否可以用monkey来抢微信红包，     
然后我就运行了`monkey -p com.tencent.mm --pct-touch 100 -v 2000`结果加了好多好友而且还没有发送成功。。。