---
layout: post
title: nexus repository
categories: nexus
tags: nexus maven java
---

## 目录

1. [网页上传jar包](#网页上传jar包)
2. [maven发布jar](#maven发布jar)
3. [使用nexus私服](#使用nexus私服)

### 网页上传jar包

![nexus.jpg](/images/nexus.jpg)

### maven发布jar

(1).在maven的`conf/setting.xml`配置nexus私服的管理账号

```XML
<server>
    <id>nexus-releases</id>
    <username>user</username>
    <password>pwd</password>
</server>
<server>
    <id>nexus-snapshots</id>
    <username>user</username>
    <password>pwd</password>
</server>
```

id可自己定义一个名称,下面代码中的id必须与之对应

(2).在项目的pom.xml中配置

```XML
<distributionManagement>
    <repository>
        <id>nexus-releases</id>
        <name>Nexus Release Repository</name>
        <url>http://nexushost:28081/nexus/content/repositories/releases/</url>
    </repository>
    <snapshotRepository>
        <id>nexus-snapshots</id>
        <name>Nexus Snapshot Repository</name>
        <url>http://nexushost:28081/nexus/content/repositories/snapshots/</url>
    </snapshotRepository>
</distributionManagement>
```

(3).`mvn deploy`

在已经打包好的项目目录下运行`mvn deploy`发布jar到nexus服务

### 使用nexus私服

(1).在maven的`conf/setting.xml`的mirrors下配置nexus私服

```XML
<mirrors>
    <mirror>
      <id>nexus-central</id>
      <mirrorOf>*</mirrorOf>
      <url>http://nexushost:28081/nexus/content/repositories/central/</url>
    </mirror>
    <mirror>
      <id>nexus-releases</id>
      <mirrorOf>*</mirrorOf>
      <url>http://nexushost:28081/nexus/content/repositories/releases/</url>
    </mirror>
    <mirror>
      <id>nexus-snapshots</id>
      <mirrorOf>*</mirrorOf>
      <url>http://nexushost:28081/nexus/content/repositories/snapshots/</url>
    </mirror>
</mirrors>
```

其中central是个代理镜像仓库,默认路由映射到maven中央仓库,当下载中央仓库资源后会存储到该镜像仓库中

```
Repository ID: central
Repository Name: Central
Repository Type: proxy
Repository Policy: Release
Repository Format: maven2
Contained in groups: 
   Public Repositories
Remote URL: https://repo1.maven.org/maven2/
```

或者使用一个public mirror url代替

```XML
<mirror>
  <id>nexus-central</id>
  <mirrorOf>*</mirrorOf>
  <url>http://nexushost:28081/nexus/content/groups/public/</url>
</mirror>
```

(1')或者通过mirrors和profiles配置私服

```XML
<mirrors>
    <mirror>
      <id>central</id>
      <mirrorOf>*</mirrorOf>
      <name>Human Readable Name for this Mirror.</name>
      <url>http://localhost:8081/nexus/content/groups/public/</url>
    </mirror>
</mirrors>
<profiles>
    <profile>
      <id>nexus</id>
      <repositories>
        <repository>
          <id>nexus</id>
          <name>Nexus</name>
          <url>http://localhost:8081/nexus/content/groups/public/</url>
            <span></span><releases>
            <enabled>true</enabled>
          </releases>
          <snapshots>
            <enabled>true</enabled>
          </snapshots>
        </repository>
      </repositories>
    </profile>
</profiles>
```

(1'')或者在POM中配置Nexus私服

这样的配置只对当前的Maven项目有效

```XML
<repositories>
  <repository>
      <id>nexus</id>
      <name>Nexus Repository</name>
      <url>http://nexushost:28081/nexus/content/groups/public/</url>
      <releases>
          <enabled>true</enabled>
      </releases>
      <snapshots>
          <enabled>true</enabled>
      </snapshots>
  </repository>
</repositories>
```

(2).在pom下配置依赖即可


参考博客:

[http://tianweili.github.io/blog/2015/03/17/linux-nexus-maven-private-server/](http://tianweili.github.io/blog/2015/03/17/linux-nexus-maven-private-server/)
[http://my.oschina.net/liangbo/blog/195739](http://my.oschina.net/liangbo/blog/195739)
[http://www.cnblogs.com/quanyongan/archive/2013/04/24/3037589.html](http://www.cnblogs.com/quanyongan/archive/2013/04/24/3037589.html)
