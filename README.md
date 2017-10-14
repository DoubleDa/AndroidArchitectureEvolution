# AndroidArchitectureEvolution

A Android Architecture Evolution Project.

## 原始架构

```java
-adapter
	-MainAdapter.java
-api
	-NewsApi.java
-base
	-BaseActivity.java
    -BaseFragment.java
    -BaseAdapter.java
-beans
	-NewsBean.java
-constants
	-Constants.java
-db
	-DBHelper.java
-image.loader
	-GlideUtils.java
-injection
	-NewsComponent.java
-net
	-OkHttpUtils.java
-service
	-NewsUpdateService.java
-ui
	-activity
    	-NewsListActivity.java
    -fragment
    	-NewsDetailFragment.java
-utils
	-SPUtils.java
-view
	-NewsRefreshView.java
-XApplication.java
```

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