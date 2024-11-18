---
title: Java判断一个日期几个工作日后的日期（忽略节假日）
date: 2021-10-28 07:09:00
tags:
  - Java
categories: 代码
cover: https://fp1.fghrsh.net/2021/10/28/e4e3ecff577dd50be58abd67129c820a.png!q80.jpeg
coverWidth: 2000
coverHeight: 1120
---

## 1.前言

前几天写作业的时候碰到一道题目，题目大意如下

- 不同的物品配送速度不同，常规商品需要5个工作日，食品需要1个工作日，数码产品立即送达（通过邮箱）。根据用户的下单日期和类别判断哪天能送到（忽略节假日）。<!-- more -->

在网上搜了一圈发现基本上都是使用的各种非常复杂的方式并且有各种兼容性问题，基本上使用的都是数组+Calendar的形式来写的。这里根据教授的提示了解到了一种非常方便的形式来解决这个问题。

## 2.思路

### 1.题目分解

首先我们需要判断是什么类型的产品，然后再根据产品对日期进行处理并切返回给用户。

### 2.日期格式

这道题目是用的格式为yyyy-mm-dd，所以这道题我们也需要根据这个方式来写。

## 3.方法

根据教授的提示Java有一个非常适合解决这个问题的类 **_java.time.LocalDate_** 这里是官方文档[https://docs.oracle.com/javase/8/docs/api/java/time/LocalDate.html](https://docs.oracle.com/javase/8/docs/api/java/time/LocalDate.html 'https://docs.oracle.com/javase/8/docs/api/java/time/LocalDate.html') 有兴趣的可以自行查看。根据文档我们可以获得几个方法来帮我们解决问题。

**LocalDate**

```java
LocalDate a = LocalDate.of(2012, 6, 30);
// 这里就是把2021.6.30转换到了java.time可以识别的日期格式LocalDate。
```

**plusDays**

```java
a = a.plusDays(1);
// 此处的a就会变成2021.7.1，日期会自动更新到下一个月。
```

**getDayOfWeek**

```java
a.getDayOfWeek();
// 这里可以获取到a的日期对应的是星期几。该方法返回是周中哪天的枚举DayOfWeek。这就避免了对int值含义的混淆。如果你需要访问原始的int值，那么枚举提供了int值。
// 比如这里是2021.7.1，也就是星期四。
```

## 4.代码

下面是我们正式实现功能的函数

```java
public String purchase(String purchaseDate) {
	// 以食品类举例，配送时间为一个工作日，purchaseDate是String类别以格式为YYYY-MM-DD的日期。
	String[] strOfdate = purchaseDate.split("-", 3);
	// 以-分割用户输入的字符串保存到名为strOfdate的字符串数组中
	LocalDate finaldate = LocalDate.of(Integer.parseInt(strOfdate[0]), Integer.parseInt(strOfdate[1]), Integer.parseInt(strOfdate[2]));
	// 设定一个LocalDate变量，变量名为finaldate，将分割好的日期赋值给它
	int daycalc = 0;
	do {
		finaldate = finaldate.plusDays(1);
		// 把用户输入的日期加一天
		if ((finaldate.getDayOfWeek() != DayOfWeek.SATURDAY &&
			finaldate.getDayOfWeek() != DayOfWeek.SUNDAY)) {
			// 判断加了一天以后是否是周六或者周日，如果是就继续循环
			++daycalc;
			// 如果不是就把daycalc参数加一，计作一个工作日。
		}
	}while (daycalc < 1);
	// 当工作日等于1的时候停止循环
	return finaldate.toString();
	// 将日期转换为String类型返回给用户
}
```

如果有任何问题欢迎在下面留言，转载文章请保留本文链接及我的ID
ZL Asica
