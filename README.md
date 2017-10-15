# AndroidArchitectureEvolution

A Android Architecture Evolution Project.


[TOC]



## 原始架构

![](http://oqle0m5m6.bkt.clouddn.com/img_first_android_architecture.png)

![](http://oqle0m5m6.bkt.clouddn.com/%E5%8E%9F%E5%A7%8BMVC%E6%A1%86%E6%9E%B6.png)


在比较原始的Android项目开发中通常采用基于MVC的架构设计，代码糅合在同一个Module中，相关包介绍如下：

- adapter

	适配器，包括与ListView、GridView、RecyclerView、ViewPager相关的适配器都存放在此包中。
- api

	Api，此包存放与Api相关的类，包括Api接口拼接、Api接口配置等。
- base

	基类，此包存放与Activity、Fragment、Adapter等相关的基类。
- beans

	数据Model，此包存放与数据序列化和反序列化相关的Model。
- constants

	常量，常量数据存放在此包中，比如界面跳转标志、应用打点字段名称、业务相关常量等。
- db

	数据持久化，此包存放与数据持久化相关的类，比如Android提供的原生SQLite数据库操作类、封装开源数据库GreenDao、第三方数据库Relam操作类等。
- image.loader

	图片加载，此包存放自实现的图片加载框架，或者是封装开源图片加载框架，比如Glide、Android-Universal-Image-Loader、Fresco、Picasso。
- injection

	依赖注入，此包存放与依赖注入相关的类，比如Dagger2、Butterknife相关。
- net

	网络操作，此包存放与网络操作相关的类，基于Apache的HttpClient的网络请求封装、基于Java的HttpUrlConnection相关的网络操作，还有基于开源网络请求框架的网络操作类封装，比如基于OkHttp、Retrofit。这儿说明的都是基于Http相关的网络请求框架，如果服务器进行了Https操作，在此可以添加Https证书相关的类。基于UDP、RTMP等相关的网络操作类也在此。
- service

	Service，与Service相关的操作类存放于此。
- ui

	UI，与MVC中View层相关的类存放于此，包括Activity、Fragment；在UI包中依据不同的业务模块进行划分。
- utils

	工具类，存放常用工具类，包括与SharedPreferences相关的SPUtils、与Log打印相关的类LogUtils、与数学计算相关的类MathUtils、与屏幕尺寸相关的ScreenUtils、文件操作相关的FileUtils、与json数据解析相关的JsonUtils、与Toast相关的ToastUtils等。
- view

	视图，此包存放与自定义View和自定义UI组件相关的类。

## 模块化架构

![](http://oqle0m5m6.bkt.clouddn.com/%E6%A8%A1%E5%9D%97%E5%8C%96%E5%BC%80%E5%8F%91%E6%9E%B6%E6%9E%84.png)

模块化架构思路：

- 基础组件层之开源库

	优秀开源库的选择能使我们项目开发便捷和快速，在App开发中经常会引入很多开源库，比如：响应式编程相关的RxJava、RxAndroid、RxBus、RxLifecycle，消息通信相关的EventBus、Otto，注解框架相关的Butterknife、Dagger2，数据解析相关的Gson、fastjson，数据库相关的Realm、ActiveAndroid、GreenDAO、 DBFlow、SugarORM，网络访问相关的OkHttp、retrofit，图片加载相关的Android-Universal-Image-Loader、Glide、Fresco、Picasso，多媒体操作相关的android-multipicker-library、Android-Image-Cropper、uCrop、android-UniversalMusicPlayer、PhotoView、ijkplayer，设备相关的zxing、zbar、barcodescanner，内存检测相关的leakcanary，日志打印相关的logger。

- 基础组件层之封装库

	拿到开源库进行二次封装是一个很好的开发习惯，比如图片加载框架，不进行二次封装，如果遇到因为框架的功能不足换图片加载框架时，不得不对每一个进行图片加载功能的地方进行替换，这样做工作量很大，而且改来改去搞不好衍生出Bug，类似的还有对地图进行二次封装；还有就是为了统计App点击事件和监控App的性能，进行App的埋点操作时，也需要进行二次封装，通过二次封装降低模块之间的耦合，避免因为埋点导致App奔溃。

- 业务组件层

	在对基础组件进行封装之后，接下来对业务组件进行封装。业务组件包括独立不能成为模块，但在各个模块常用的功能模块，比如分享组件、支付组件、时间选择组件、地址选择组件、广告组件、Html5活动页面组件、Native商品列表组件、各种Dialog组件等。

- 业务模块层

	具体的业务逻辑这个层实现，比如首页模块、一级分类模块、二级分类模块、购物车模块、个人中心模块、订单模块、充值模块等。



## 组件化架构

组件化框架架构图：

![](http://oqle0m5m6.bkt.clouddn.com/%E7%BB%84%E4%BB%B6%E5%8C%96%E6%A1%86%E6%9E%B6%E5%9B%BE%20%281%29.png)

- App

	应用在release环境唯一的Application，通过添加依赖的形式引用各个组件，各个组件Application类中的工作都可以添加到app的Application类中实现。

- 各个组件

	将各个功能模块拆分成组件，这些组件可以单独设置为一个Applicationm进行开发、测试，各个组件的开发不会相互影响，实现了功能的并行开发，各个组件之间可以通过约定俗成的方式进行通信。

- 依赖库

	各个组件依赖库，组件功能不同依赖库随之不同，按需依赖。

- 具体依赖组件

	依赖库，包括基础功能依赖组件、公共功能依赖组件等。

## 插件化架构

插件化框架图：

![](http://oqle0m5m6.bkt.clouddn.com/%E6%8F%92%E4%BB%B6%E5%8C%96%E5%BC%80%E5%8F%91%E6%9E%B6%E6%9E%84.png)

- Host

	宿主，加载各个插件的容器。

- Plugin

	插件，将功能制作成一个插件，通过插件化加载框架加载到宿主，实现插件功能。

目前市面上的插件化框架如下，其中各有所长：

- RePlugin

	一个灵活的、稳定的、易于使用的Android插件框架，来自360。

- VirtualAPK

	一个功能强大且轻量级的Android插件化框架，来自滴滴。

- Atlas

	一个强大的Android动态组件框架，来自阿里。

## 多进程架构


多进程架构图：

![](http://oqle0m5m6.bkt.clouddn.com/%E5%A4%9A%E8%BF%9B%E7%A8%8B%E6%9E%B6%E6%9E%84%20%281%29.png)

多进程架构的优势：


- 提高各个进程的稳定性，单一进程崩溃后不影响整个程序。
- 对于内存的时候更可控，可以通过手工释放进程，达到内存优化目的。
- 基于独立的JVM，各个模块可以充分解耦。
- 只保留daemon进程的情况下，会使应用存活时间更长，不容易被回收掉。

## 参考文献

- [Android彻底组件化方案实践](http://www.jianshu.com/p/1b1d77f58e84)
- [Android架构思考(模块化、多进程)](http://blog.csdn.net/nexttake/article/details/55211012)
- [Android彻底组件化demo发布](http://www.jianshu.com/p/59822a7b2fad)
- [微信Android模块化架构重构实践](http://geek.csdn.net/news/detail/208980)
- [Android多进程使用场景](http://blog.csdn.net/qq_27489007/article/details/54377655)