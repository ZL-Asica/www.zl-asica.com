---
title: C++进行特定位数的四舍五入/向上取整/向下取整/截断
date: 2022-03-26 07:26:00
tags:
  - C++
categories: 代码
cover: https://fp1.fghrsh.net/2021/10/28/b3943f1893ee44bf1e909c3aa9e0341f.png!q80.jpeg
coverWidth: 1280
coverHeight: 720
---

## 1.C++的四舍五入/向上取整/向下取整/截断

我们在C++中有时会需要使用到数学运算，同样的可能会使用到标题提到的几种方式进行运算。实际上C++有一个库<cmath>可以直接实现这些方法操作。<!-- more -->

```cpp
#include <cmath>

int main()
{
    double a = 43.5555;

	// 四舍五入
    a = std::round(a);
    std::cout << a << std::endl; // 44.0000

	// 向下取整
    a = std::floor(a);
    std::cout << a << std::endl; // 43.0000

	// 向上取整
    a = std::ceil(a);
    std::cout << a << std::endl; // 44.0000

	// 截断
	a = std::trunc(a);
    std::cout << a << std::endl; // 43.0000

    return 0;
}
```

那么这就是最简单的四种算法在C++中的使用了。

## 2.C++中获取特定位数的方法

那么有时候我们进行这样的数学运算后，目的就是为了得到一个更方便看的数，那当然要取特定位数的小数了。写法规则如下(以四舍五入方法std::round做演示)。

```cpp
    a = std::round(a * 保留到几分位) / 保留到几分位; // 保留到十分位 = 保留两位小数
```

我们来一个保存两位小数(十分位)的实例来看一下。

```cpp
#include <iostream>
#include <cmath>

int main()
{
    double a = 43.5555;
    a = std::round(a * 10) / 10;
    std::cout << a << std::endl;

    return 0;
}
```

那么这样就可以非常轻松的在C++中获取到我们需要的小数位数了。

## 3.C++中对定位数的double进行输出的方法

我们上面说到了如何获取到特定的位数，但是这样获取到的还是double值，如果想要和std::string一起操作是会出现问题的。如果我们想要把这个double和其他的string放到一起的话，我们就需要按照如下代码进行操作。

```cpp
#include <iostream>
#include <cmath>
#include <string>

int main()
{
    double a = 43.5555;
    a = std::round(a * 10) / 10;
	// 先转换为std::string类型
    std::string tempre = std::to_string(a);
	// 对std::string类型进行10位小数的格式化（下面语句会输出10位小数）
    std::cout << tempre.substr(0, tempre.find(".") + 2) << std::endl;

    return 0;
}
```

这就是本文的全部内容了。
