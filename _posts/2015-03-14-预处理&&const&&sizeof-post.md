---
layout: post
title: 预处理&&const&&sizeof
description: "人总是在选择中迷惘"
modified: 2015-03-16
tags: [程序基本功]
image:
  feature: abstract-3.jpg
  credit: dargadgetz
  creditlink: http://www.dargadgetz.com/ios-7-abstract-wallpaper-pack-for-iphone-5-and-ipod-touch-retina/
---

# 分享一下预处理&&const&&sizeof里一些小技巧

## define的用法
**1.用define声明一月有多少秒**

一开始很想这么写，感觉就是声明个常量。
{% highlight c++ %}
#define SECONDS_JANUARY 2678400
{% endhighlight %}
而下面的写法就明显好的多。
{% highlight c++ %}
#define SECONDS_JANUARY 60*60*24*31
{% endhighlight %}
这样的宏可以让计算表达式表现出程序员的意图和计算的方式。

**2.用define声明标准的宏MIN**

{% highlight c++ %}
#define MIN(A,B) ((A)<=(B))?(A):(B)
{% endhighlight %}
这里其实主要就是考察一下三重条件操作符，记得一定要括括号,这最好变成习惯，不然会引发如下错误。
{% highlight c++ %}
#define MUL(A,B) A*B
int main()
{
	int a = MUL(3+5,8) //希望的是(3+5)*8,最后得到3+5*8
}
{% endhighlight %}

## const的用法
**四个const区分**
{% highlight c++ %}
int b = 10;
const int *a = &b; //case 1
int const* a = &b; //case 2
int* const a = &b; //case 3
const int* const a = &b;//case 4
{% endhighlight %}

首先case 1 和 case 2是完全等价的。
如果const在星号左侧，const修饰的就是所指向的变量,如果const在星号右侧，修饰的就是指针本身。
所以如果是case1和case2的话，我们就不能修改指向的变量.

所以在case 1,case 2 下面的语句都是违法的.
{% highlight c++ %}
*a = 600;//不能修改
{% endhighlight %}

但如果要修改指针a指向的值得，以下语句可以代替达到这种效果。
{% highlight c++ %}
int b = 500;
const int* a = &b;
b = 30;//方法1 修改指向的内容
int c = 30;
a = &c; //方法2 指向新的内容
{% endhighlight %}

那如果是case3的话，也就是const在星号的右侧，说明指针本身是一个常亮。
那么就不能对指针本身做任何操作。例如以下的行为。
{% highlight c++ %}
int b = 50 , c = 20;
int* const a;//错误 必须初始化，不然就永远指向未知。
int* const a = &b; //正确，初始化
*a = 500 ; //正确，可以修改
cout << a++ << endl ;//错误，不能对a做指针操作
{% endhighlight %}

而case 4也很明显就是既不能修改值，也不能修改指针。

**为什么要用const成员函数呢？**

因为一些成员函数是不需要改变类中的数据成员的，它们是只读函数。所以如果加上const标示可以提高程序的可读性，也可以防止这些函数企图修改数据成员的值，让编译器报错。

让我们来看看以下两个const函数写法:
{% highlight c++ %}
int Point::GETY() const
{
	return yVAL;
}
//这个意思是const的成员函数，即函数不能修改数据成员。
const int Point::GETY()
{
	return yVAL;
}
//说明返回的值是一个const int.
{% endhighlight %}

**那么问题来了，#define和const 都能修饰常量，哪种更好？**

* const常量有数据类型，而define没有，编译器可以对前者做类型检查，而后者只是字符替换，所以可能会在替换中产生未知的bug([**边际效应**](http://zh.wikipedia.org/wiki/%E8%BE%B9%E9%99%85%E6%95%88%E7%94%A8))
* 有些集成化的调试工具会调试const常量，却无法调试宏

