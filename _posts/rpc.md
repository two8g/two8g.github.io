

# 远程过程调用

## 本地服务

自己写单个项目,比如一个hello的服务类.先定义一个HelloService接口:

```JAVA
public interface HelloService {
	String sayHello(String name);
}
```

接着写出实现类:

```JAVA
public class HelloServiceImpl implements HelloService {
    @Override
    public String sayHello(String name) {
        String result = "hello " + name;
        System.out.println(result);
        return result;
    }
}
```

然后就可以本地调用了:

```JAVA
public class HelloWorldTest(){
	public static void main(String[] args){
		HelloService helloService = new HelloServiceImpl();
		helloService.sayHello("world");
	}
}
```

这种服务的提供方和消费方都是本地程序.

## 基于HTTP协议的Web Service

随着项目的扩大,项目开始进行业务拆分及封装。
一个项目需要调用另外一个项目的服务,同时也可能给其它项目提供服务。

于是,一种简单的做法是,将项目部署成一个基于HTTP协议的Web Service
服务的提供方server需要向外发布所提供服务的HTTP调用接口约定文档。如：

```
GET /server-url/server-name?name={name} HTTP/1.1
Host server-host
```

```
HTTP/1.1 200 OK

Hello {name}
```

此时服务消费方client通过发送HTTP请求获取服务的结果

### 优点
	跨平台
### 缺点
	client调用复杂,每调用一个服务都要写一坨网络通信的代码,容易出错;性能不如基于TCP协议的RPC(两方面 传输方式及序列化)
	
如果有一种方式能让我们像调用本地服务一样调用远程服务，而让调用者对网络通信这些细节透明，那么将大大提高生产力，比如服务消费方在执行helloWorldService.sayHello(“test”)时，实质上调用的是远端的服务。这种方式其实就是RPC（Remote Procedure Call Protocol），在各大互联网公司中被广泛使用，如阿里巴巴的hsf、dubbo（开源）、Facebook的thrift（开源）、Google grpc（开源）、Twitter的finagle等。
转自[占利军博客](http://www.cnblogs.com/LBSer/p/4853234.html)
