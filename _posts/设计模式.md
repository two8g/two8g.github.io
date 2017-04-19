# 设计模式归纳总结

https://quanke.gitbooks.io/design-pattern-java/content 的归纳总结

## 基础知识

### 概述

#### 招式和内功

招式：Java、C#、C++等编程语言，Eclipse、Visual
Studio等开发工具，JSP、ASP.net等开发技术，Struts、Hibernate、JBPM等框架技术；
内功：数据结构、算法、设计模式、重构、软件工程等

#### 模式由来

Christopher Alexander（克里斯托弗.亚历山大）——模式之父(The father of
patterns)

#### 软件模式引入

最早将模式的思想引入软件工程方法学 1991-1992年 以“四人组(Gang of
Four，简称GoF，分别是Erich Gamma, Richard Helm, Ralph Johnson和John
Vlissides)”自称的四位著名软件工程学者

旨在用模式来统一沟通面向对象方法在**分析**、**设计**和**实现**间的鸿沟

#### 软件模式基础结构

1. 问题描述【待解决的问题是什么】
2. 前提条件【在何种环境或约束条件下使用】
3. 解法【如何解决】
4. 效果【有哪些优缺点】

#### 设计模式

在软件模式中，设计模式是研究最为深入的分支，设计模式用于在特定的条件下为一些重复出现的软件设计问题提供合理的、有效的解决方案，它融合了众多专家的设计经验

1995年， GoF将收集和整理好的23种设计模式汇编成Design Patterns: Elements of
Reusable Object-Oriented
Software【《设计模式：可复用面向对象软件的基础》】一书，该书的出版也标志着设计模式正式成为面向对象(Object
Oriented)软件工程的一个重要研究分支。

#### 设计模式要素

1. 模式名称(Pattern Name)
2. 问题(Problem)
3. 解决方案(Solution)
4. 效果(Consequences)

#### 设计模式用途分类

- 创建型(Creational)--描述如何创建对象（5种）
- 结构型(Structural)--描述如何实现类或对象的组合（7种）
- 行为型(Behavioral)--描述类或对象的交互及职责（11种）

#### 设计模式一览表


| 类型                         |                   模式名称                    | 学习难度 | 使用频率 |
|:----------------------------|:-------------------------------------------:|-------:|:--------|
| 创建型模式 Creational Pattern |          单例模式 Singleton Pattern           |  ★☆☆☆☆ | ★★★★☆   |
| 创建型模式 Creational Pattern |     简单工厂模式 Simple   Factory Pattern     |  ★★☆☆☆ | ★★★☆☆   |
| 创建型模式 Creational Pattern |      工厂方法模式 Factory Method Pattern      |  ★★☆☆☆ | ★★★★★   |
| 创建型模式 Creational Pattern |   抽象工厂模式 Abstract  Factory   Pattern    |  ★★★★☆ | ★★★★★   |
| 创建型模式 Creational Pattern |          原型模式 Prototype Pattern           |  ★★★☆☆ | ★★★☆☆   |
| 创建型模式 Creational Pattern |          建造者模式 Builder Pattern           |  ★★★★☆ | ★★☆☆☆   |
| 结构型模式 Structural Pattern |          适配器模式 Adapter Pattern           |  ★★☆☆☆ | ★★★★☆   |
| 结构型模式 Structural Pattern |           桥接模式 Bridge  Pattern            |  ★★★☆☆ | ★★★☆☆   |
| 结构型模式 Structural Pattern |          组合模式 Composite  Pattern          |  ★★★☆☆ | ★★★★☆   |
| 结构型模式 Structural Pattern |          装饰模式 Decorator  Pattern          |  ★★★☆☆ | ★★★☆☆   |
| 结构型模式 Structural Pattern |           外观模式 Façade  Pattern            |  ★☆☆☆☆ | ★★★★★   |
| 结构型模式 Structural Pattern |          享元模式 Flyweight  Pattern          |  ★★★★☆ | ★☆☆☆☆   |
| 结构型模式 Structural Pattern |            代理模式 Proxy  Pattern            |  ★★★☆☆ | ★★★★☆   |
| 行为型模式 Behavioral Pattern | 职责链模式 Chain  of Responsibility   Pattern |  ★★★☆☆ | ★★☆☆☆   |
| 行为型模式 Behavioral Pattern |           命令模式 Command  Pattern           |  ★★★☆☆ | ★★★★☆   |
| 行为型模式 Behavioral Pattern |        解释器模式 Interpreter  Pattern        |  ★★★★★ | ★☆☆☆☆   |
| 行为型模式 Behavioral Pattern |         迭代器模式 Iterator  Pattern          |  ★★★☆☆ | ★★★★★   |
| 行为型模式 Behavioral Pattern |         中介者模式 Mediator  Pattern          |  ★★★☆☆ | ★★☆☆☆   |
| 行为型模式 Behavioral Pattern |          备忘录模式 Memento  Pattern          |  ★★☆☆☆ | ★★☆☆☆   |
| 行为型模式 Behavioral Pattern |         观察者模式 Observer  Pattern          |  ★★★☆☆ | ★★★★★   |
| 行为型模式 Behavioral Pattern |            状态模式 State  Pattern            |  ★★★☆☆ | ★★★☆☆   |
| 行为型模式 Behavioral Pattern |          策略模式 Strategy  Pattern           |  ★☆☆☆☆ | ★★★★☆   |
| 行为型模式 Behavioral Pattern |     模板方法模式 Template  Method Pattern     |  ★★☆☆☆ | ★★★☆☆   |
| 行为型模式 Behavioral Pattern |          访问者模式 Visitor  Pattern          |  ★★★★☆ | ★☆☆☆☆   |


