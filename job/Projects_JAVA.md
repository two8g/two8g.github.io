# 我的项目经验

1. 搜索系统开发  

互联网教育行业拍照搜题神器涌现,公司题库资源发现新的利用价值;
公司决定实现App拍照搜索功能,而且期望搜索速度和准确度能与其它对手竞争;
和另外两名同事,攻关一个月.其中由我搭建了Solr分布式搜索引擎,完成索引词典建设和LaTeX公式分词算法.同时为其它有搜索需求的项目快速提供搜索实现;
服务支撑最高100万日访问,搜索响应时间平均在200ms,搜索结果第一命中率达到65%.该项目让我学习了倒排索引及向量空间打分模型.并在网上参与翻译了Solr使用指南.

2. "自由搭"生鲜O2O项目

客户进行生鲜O2O的投资创业项目,缺少有经验的软件开发团队.
工作外项目,项目来自西安,和朋友组建开发团队,3个月后完成软件交付.
我和另外两位成员去了解了项目情况,之后与客户详细讨论了需求及开发流程.与团队分析确定需求,分工和周期.我主要负责APP客户端后台开发.包括但不限于用户服务模块,内容展示模块,线上交易模块等的REST接口.其中应对需求修改,如新增下单规则限制,给出了合理的解决方法.
项目按时按需交付,而我也锻炼了需求分析能力,团队协作能力.熟练了Spring,Spring MVC,Hibernate开发技术.其次,了解了一点关于创业的知识.

3. 在线视频资源服务

产品用户不断增长,系统数据也逐渐具有利用价值,纯文字内容产品缺乏吸引力,缺少收费服务
公司希望利用用户数据及用户个性数据,生产相关教学视频并推送给用户,由此服务用户并获利.

我负责推荐算法及内容推送的开发,使用Spring MVC,Thymeleaf,Mybatis完成服务开发,并与基础服务,APP客户端和WEB前端对接.监控用户访问数据,统计产品交易成绩.开始服务响应时间长,于是使用Ehcache实现缓存加速,同时将web静态资源上传至CDN网络.
项目首月就完成300交易量,目前服务稳定运行.每日PV达140w+,峰值达200w+.为产品增加"收费会员"服务功能做铺垫.

4. 文档转码自动化(Converter)  

安全考虑,公司文本数据在部分场景下需要使用图像格式.部分场景需要转为其它文档格式(PDF,DOCX)转换,同时需要提供公共API服务;
由于我最熟悉LaTeX公式的MathJax渲染问题,项目由我负责完成.而文档转码存在公式转码问题和排版问题;
对于图像问题,我实验过Html2canvas和PhantomJS,效果不尽理想,Html2canvas存在浏览器应用必要条件,PhantomJS的内存和CPU消耗太大.最终实验了Cutycapt工具加XVFB虚拟显示方案,此方案效果和性能最好.为了处理文档转码问题,花了一个多月,对PANDOC(Haskell语言),Office XML和Xelatex排版系统的学习和实验,最终达到90+%的满意效果;
完美解决了HTML至图片的转码需求,文档转码最终也达到90%以上的满意效果.同时我也学习其它"牛逼"的语言.

5. 自动化部署  

项目需求不断变化,新功能开发测试至上线及稳定周期接近一个月;
老板希望新功能越快上线,测试希望有充足时间,开发希望服务快速部署和自动测试 ;
早在遇到这个问题之前,我就搭建了内网Maven仓库.再处理这个问题时,搭建Jenkins自动部署平台,实现应用快速自动化部署.同时,使用开源GitLab搭建内部代码仓库,为以后源码共享维护和CodeReview做准备;学习并分享git-flow工作流和issue协作方式,使得责任明确及问题持续跟踪.并尝试采用GitLab-CI完成自动打包与自动测试;
不仅规范了代码打包及分发.而且大幅减少了沟通成本,重复劳动和人为失误.内部的Git仓库也方便全体成员分享代码和学习,规范的工作流对项目的开发效率及迭代效率都有提升.

6. 服务日志监控系统  

服务日志分散在各服务器,服务出现异常状况后问题排查困难;
人工查看日志文件效率低,部分服务日志未分割,直接查看服务器日志存在危险;
花了两周时间,使用ELK(ElasticSearch+Logstash+Kibana)组合,同时采用轻量级的Filebeat将所有服务访问日志导入ELK系统中;
填补服务访问日志监控空白,异常排查分分钟搞定.还可以随时了解服务运行状态和服务压力,使得尽早发现和解决服务问题.