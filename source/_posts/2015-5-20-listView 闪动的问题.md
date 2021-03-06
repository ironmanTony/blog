title: listView 闪动的问题
date: 2015-05-20 10:42:24
tags:
- android
---

我仿做一个网易新闻客户端，因为每一行有不同的内容，所以需要使用getItemViewType来区分不同的行的类型

然而我的东西出现了一个很奇怪的问题：
> 在滑动的时候会出现一行快速的闪动（快速变换不同的内容）

分析问题原因：
> 一开始以为我是因为在viewpager里嵌套viewpager惹的祸，
或者是使用开源的下拉刷新框架惹的祸，
或者是自己使用Viewholder的姿势不对，一开始主要是怀疑getView里面的东西用的不对。

求证过程：
> 我新写一个Activity并没用用到ViewPager，而且我也将原来的adapter的GetView方法重写，由于类型比较多，所以还将变量的名字改变了怕自己哪里写错了。但是依然还是闪动。

真实的原因：
> 然后我就发现我自己的Viewholder里面的组件也是static，因为Viewholder是要复用的，所以需要为static的，但是如果把里面的元素也写成是static的就会有问题。就像上面那样的闪动的问题。
