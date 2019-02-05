---
title: Ingress多重连法
categories:
- ingress
description: Ingress多重连法总结
tags:
- ingress
- 教程
---

## 何为多重

所谓多重，就是在有限portal（以下简称po）之间尽可能地创建更多的control field(以下简称cf)，以此在这有限的po间获得更多的ap。

因为：

* 在所有游戏操作中Establish a control field可获得1250ap，是获得ap做多的操作
* 在Ingress里规定了在一个field里面是不能连线的，所以field里面要新增加link，只能从外部（边缘）连向里面

所以平面上的四个点，可能构成的多重最小集合为下图：

![field1](/images/ingress-field/field1.png)

![field1](/images/ingress-field/field2.png)
![field1](/images/ingress-field/field3.png)
![field1](/images/ingress-field/field4.png)

总个4个cf，外面一个大的，中间三个小的。

## 多重连法

当我们来到一片po群想在这里做多重的时候，先在po群里找出一排相对有序的点，选择其中靠外的po，暂且取名为B，在有序点外选择一个与B相对的po，取名为A，我们将在这片区域创建多重。
![po群](/images/ingress-field/1-1.png)

根据每个po所拥有钥匙的数量，基本上可分为三种情况:

### 一、有底边两个顶点足够的钥匙

即有A、B两个点的大量钥匙，首先A、B先连起来，接着在离A、B最近的有序点连接A、B，构成第一个cf。
![1-2](/images/ingress-field/1-2.png)

紧接着下一个有序点连接A、B构成第二个cf。
![1-3](/images/ingress-field/1-3.png)

连第一个有序点，一分为二，同时创建两个cf。
![1-4](/images/ingress-field/1-4.png)

后面的有序点依次连上，一层一层构成一个整体的多重。
![1-5](/images/ingress-field/1-5.png)

### 二、有底边其中一个顶点足够的钥匙

即有A点大量的钥匙，由于B点缺少足够钥匙，所有只能从B点处连出，首先从B点往其它各点连线。
![2-1](/images/ingress-field/2-1.png)

第一个有序点连接A，构成第一个cf。
![2-2](/images/ingress-field/2-2.png)

紧接着第二个有序点连A，连上一个有序点，构成一个小多重。
![2-3](/images/ingress-field/2-3.png)

后面的点依次连上，一层一层构成一个整体多重。
![2-4](/images/ingress-field/2-4.png)

### 三、底边两个顶点钥匙不足

即A、B两个点的钥匙不足，此时只能寻求从A、B两个点连出线，首先B点往各个有序点连出线。
![3-1](/images/ingress-field/3-1.png)

接着相邻有序点两两之间连上构成cf，此时你会发现，现在这片po就好像一个大多重其中一个顶点被打掉后的样子，而我们接下来的任务就是修复它。
![3-2](/images/ingress-field/3-2.png)

开始进行修复，在A点往B点及有序点中最外的点连线，构成最大层cf。
![3-3](/images/ingress-field/3-3.png)

A点连接倒数第二个有序点，一分为二创建两个cf。
![3-4](/images/ingress-field/3-4.png)

依次由A点从大到小连，构成一个整体多重。
![3-5](/images/ingress-field/3-5.png)

## 总结

现实情况中往往没有一整排刚好的po，大多数情况是根据钥匙的数量三种方法交叉着运用，大多重里面还嵌套着小多重。而何为有序点集合，何为有序点外的A点也是根据需要动态变化的。
