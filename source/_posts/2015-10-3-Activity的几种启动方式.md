title: Activity的几种启动方式
date: 2014-09-18 23:46:13
tags: android
---
## 总结
------
### standard：
如果需要启动一个Activity，则会重新生成一个activity实例

### sigleTop:
如果需要启动的Activity刚刚好在栈顶，则不会再去创建Activity的实例,否则，创建Activity实例

### sigleTask
如果在同一个应用中启动Activity，如果栈中没有，则创建新实例；如果有则直接杀死之上的所有activity使需要启动的activity成为栈顶    
如果是在别的应用中启动该activity则会重新创建一个栈

### sigleInstance:
只有一个实例并且单独运行在一个task中，这个task只有这个实例，不允许有别的activity存在。

## 参考资料：
------
http://blog.csdn.net/shinay/article/details/7898492