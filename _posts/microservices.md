# microservices

## Martin Fowler的博客

https://martinfowler.com/articles/microservices.html

微服务是一种新的架构定义。（a definition of this new architectural term）

The term "Microservice Architecture" has sprung up over the last few years to describe a particular way of designing software applications as suites of independently deployable services. While there is no precise definition of this architectural style, there are certain common characteristics around organization around business capability, automated deployment, intelligence in the endpoints, and decentralized control of languages and data.

http://www.cnblogs.com/liuning8023/p/4493156.html

>> “微服务架构（Microservice Architecture）”一词在过去几年里广泛的传播，它用于描述一种设计应用程序的特别方式，作为一套独立可部署的服务。目前，这种架构方式还没有准确的定义，但是在围绕业务能力的组织、自动部署（automated deployment）、端智能（intelligence in the endpoints）、语言和数据的分散控制，却有着某种共同的特征。

## 深入理解microservices

http://microservices.io/

### What's

“微服务”也称为“微服务架构”。

一种由一系列实现各自业务的相互松散耦合的服务构成应用的架构方式。

可以实现大型复杂应用的持续交付/部署。使组织能够发展其技术栈。

### What's not

“微服务架构”不是银弹。有很多缺点，而且如果使用的话，你有很多问题需要解决。

### microservice architecture pattern language

微服务架构模式语言是应用微服务架构的模式集合。

它的2个目标：

1. 使您能够决定微服务是否适合您的应用程序
2. 使您能够成功地使用微服务架构

### 从单一架构模式开始

http://microservices.io/patterns/monolithic.html

优点

* 开发简单 - 目前开发工具和IDE很适合单一应用程序开发
* 部署简单 - 只需在相应地方部署打包的war文件或者目录
* 扩展简单 -  部署多个副本，运行在负载均衡后面

弊端

当应用变的庞大或者团队规模增长


### 微服务的代价

是否应该选择微服务架构？

https://martinfowler.com/bliki/MicroservicePremium.html

>> 是否使用微服务的支点是您正在考虑的系统的**复杂性**。微服务的方法都是关于处理一个复杂的系统，但为了这样做，这个方法引入了自己的一套复杂性。

![productivity-complexity](/images/productivity-complexity.png)

>> don't even consider microservices unless you have a system that's too complex to manage as a monolith.

The majority of software systems should be built as a single monolithic application. Do pay attention to good modularity within that monolith, but don't try to separate it into separate services.

### 权衡

https://martinfowler.com/articles/microservice-trade-offs.html