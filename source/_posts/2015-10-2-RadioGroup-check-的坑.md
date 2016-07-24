title: RadioGroup.check()的坑
date: 2015-09-29 11:40:43
tags: android
---
### 问题描述：
我使用RadioGroup.check()方法来初始化radioGroup，然后我在onCheckedChanged()里去根据选择的radioButton来发送网络请求，并且新建fragment。这时候我发现一个问题：这个radiobutton下的网络请求会发送两次，而且fragment也会创建两次，而且那个新建的fragment里还有很多的初始化过程和网络请求，所以会让用户一直处在等待的状态。

开始时候各种找原因，以为是我在哪里调用了太多次，还是共用layout文件有相同的id所以被别的地方的调用影响了？都不是，最后在stackoverflow上找到了答案：使用RadioGroup.check()会调用onCheckedChanged()方法三次，而我在onCheckedChanged()方法里判断了调用的是哪个id，然后发送请求创建fragmeng，所以只调用了两次。

### statckoverflow原文链接：
http://stackoverflow.com/questions/10263778/radiogroup-calls-oncheckchanged-three-times

![](/imgs/radiogroupChecks.png)

### RadioGroup.check()源码如下：
http://www.grepcode.com/file/repository.grepcode.com/java/ext/com.google.android/android/4.1.1_r1/android/widget/RadioGroup.java#RadioGroup.check%28int%29

![](/imgs/radiogroup2.png)

### 解决方法 ：    
使用radioBotton.setChecked()方法来解决

![](/imgs/radiogroup3.png)

