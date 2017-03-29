---
layout: post
title: Object的一个getClass方法有多少知识
categories: java
tags: java object getClass 泛型
---

# Object的一个getClass方法有多少知识

`Object`类是所有类层级的根,包括数组.

主要定义的方法有`getClass`、`hashCode`、`equals`、`clone`,`toString`:

```java
public class Object{
    public final native Class<?> getClass();
    public native int hashCode();
    public boolean equals(Object obj) {
            return (this == obj);
        }
    protected native Object clone() throws CloneNotSupportedException;
    public String toString() {
        return getClass().getName() + "@" + Integer.toHexString(hashCode());
    }
}
```

其中`hashCode`、`equals`,`toString`都通过java代码提供实现.而`getClass`、`clone`是native,即由平台相关代码实现,其中`getClass`是`final`的.

下面依次讨论上面5个方法.

1. getClass方法

`getClass`方法定义如下

```java
public final native Class<?> getClass();
```

该方法获取的是Obejct的运行时的class,返回的一个Class对象,如何一个Obejct都关联一个`java.lang.Class`的实例的引用.
另外注意`Class<?>`的形式.实际表示是`Class<? extends |X|>`,其实. 其中`|X|`是对象的static type()的类型擦除结果.

这里设计两个概念*static type*和*类型擦除*. 先说*static type*,

*static type*字面理解即静态类型,那上面是静态类型呢?既然有静态类型,那是不是还有动态类型呢?

首先要指出,*static type*确切的说是*compile-time type*指编译时类型.而*dynamic type*(动态类型)是*runtime type*指运行时类型.
注意千万不要和静态类型语言和动态类型语言概念(两种语言分类)混淆.所以我们改用*compile-time type*和*runtime type*进行说明,避免混淆.
不过这里的*static type*与*静态类型语言*也有点关系. (我对这理解还不够深入,大家最好看看权威文档. 我主要参考了这个[讨论](http://stackoverflow.com/questions/14963943/what-is-the-difference-between-a-compile-time-type-vs-run-time-type-for-any-obje))


>> Java is a statically typed language, so the compiler will attempt to determine the types of everything and make sure that everything is type safe. Unfortunately static type inference is inherently limited. The compiler has to be conservative, and is also unable to see runtime information. Therefore, it will be unable to prove that certain code is typesafe, even if it really is.

意思是说,JAVA是静态类型语言.所以编译器需要尝试确认所有东西的的类型来保证类型安全.但是,静态类型语言的推到是有一定限制的.编译器采取保守手段, 它无法获得运行时信息. 所以, 编译器无法保证代码的类型安全, 即使代码确实是安全的.

>> The run time type refers to the actual type of the variable at runtime. As the programmer, you hopefully know this better than the compiler, so you can suppress warnings when you know that it is safe to do so.

运行时类型是指,代码时间运行时的类型. 作为程序员,你希望比编译器更好的清除代码,所以,当你知道代码是类型安全的时候你可以屏蔽警告.

我的理解是. *compile-time type*就是我们声明参数或变量时的类型.而*runtime type*就是实际运行时对象的真实类型. 而getClass方法返回的参数类型的只能是*compile-time type*. 因为前面说的,编译器获取不到运行时信息. 所以在使用getClass方法时,这样写是正确的:

```java
List<Integer> integerList = new ArrayList<>();
Class<? extends List> integerListClass = integerList.getClass();
ArrayList<Integer> integerList_1 = new ArrayList<>();
Class<? extends ArrayList> integerListClass_1 = integerList_1.getClass();
```

而下面这样的写法,是无法编译通过的.
```java
List<Integer> integerList = new ArrayList<>();
Class<? extends List> integerListClass = integerList.getClass();
```

理解了上面的静态类型和动态类型就非常容易理解JAVA面向对象的多态特性,以及类型转换知识.

然后说说*类型擦除*.*类型擦除*是JAVA泛型支持特性的知识.

>> Java泛型（generics）是JDK 5中引入的一个新特性，允许在定义类和接口的时候使用类型参数（type parameter）。声明的类型参数在使用时用具体的类型来替换。泛型最主要的应用是在JDK 5中的新集合类框架中.

而对于类型擦除,例如: List<String> 的类型擦除类型为 List.

以下代码是正确的:

```java
Object o = new Object();
Class oClass = o.getClass();
String s = "str";
Class sClass = s.getClass();
List<Integer> integerList = new ArrayList<>();
Class<? extends List> integerListClass = integerList.getClass();
ArrayList<Integer> integerList_1 = new ArrayList<>();
Class<? extends ArrayList> integerListClass_1 = integerList_1.getClass();
```

理解了静态类型/动态类型和类型擦除,以下代码就很容易明白了
```
Object oa = new Object();
Object ob = new Object();
Class oaClass = oa.getClass();
Class obClass = ob.getClass();
System.out.println(oaClass == obClass); //true

List<Integer> integerList = new ArrayList<>();
Class<? extends List> integerListClass = integerList.getClass();
ArrayList<Integer> integerList_1 = new ArrayList<>();
Class<? extends ArrayList> integerListClass_1 = integerList_1.getClass();
List<Integer> integerList_2 = new LinkedList<>();
Class<? extends List> integerListClass_2 = integerList_2.getClass();
List<String> stringList_3 = new ArrayList<>();
Class<? extends List> stringListClass_3 = stringList_3.getClass();

System.out.println(integerListClass == integerListClass_1); //true
System.out.println(integerListClass == integerListClass_2); //false
System.out.println(integerListClass == stringListClass_3); //true

System.out.println(integerListClass); // class java.util.ArrayList
System.out.println(integerListClass_2);// class java.util.LinkedList
System.out.println(stringListClass_3);// class java.util.ArrayList
```