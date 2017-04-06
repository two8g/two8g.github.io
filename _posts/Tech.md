
# Spring MVC

围绕一个servlet调度器调度请求和处理请设计，包括可配置的Handler Mappings(处理器映射),View resolution(视图处理). 还有本地化，时区和文件上传等。

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