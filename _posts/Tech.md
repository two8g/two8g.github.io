
# Spring MVC

围绕一个servlet调度器调度请求和处理请求设计，包括可配置的Handler Mappings(处理器映射),View resolution(视图处理). 还有本地化，时区和文件上传等。

默认的处理器基于@Controller和@RequestMapping注解。同时支持RESTful Web服务。

设计原则"ocp" "Open for extension, closed for modification".

controller 负责准备Model Map数据，选择视图名称，也可以直接输出至响应流完成请求。
View resolution 处理页面渲染，高度可配置，文件后缀

DispatcherServlet  "Front Controller"设计

```
    ————————————————————————————————————————————————————
    |                     Delegate    Handle request    |
    |   _________________ Request   ~~~~~~~~~~~~~~~~~   |
Request |               |---------->(               )   |
————|——>|Front Contrller|           (   Cotroller   )   |
    |   |_______________|<---model--(~~~~~~~~~~~~~~~)   |
    |       ^         |   Delegate       create model
    |       |         |    rending
    |       |       model of response
    | Return|control  |
    |       |         |
    |   ____|__Render\/response
    |   |                   |
    |   |   View template   |
    |   |___________________|            Servlet engine |
    |___________________________________________________|
```

## Spring

为开发Java应用程序提供全面的基础架构支持

例如事务，无需操作事务API

一个Java应用程序通常由合作形成应用程序的对象组成。因此应用程序中的对象彼此具有依赖关系。
Java平台缺少将基本构建块组织成一个整体的方法。
虽然可以使用设计模式来组合各种类和实体组成一个应用，你必须组合它们。设计模式是简单的。

IoC组件提供将不同组件组合成一个正式使用的完整应用的形式化手段来解决。