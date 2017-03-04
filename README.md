# AutoBuildConfigSet-Demo
##需求分型
开发iOS工程的时候，有时候由于项目的需要，常常有测试环境，发布环境，企业环境等不同环境的配置问题。
这样在代码中就会有很多if-else判断处理逻辑，并且常常由于项目紧急上线导致某个参数忘记修改配置，导致生产事故的发生，这个问题一直比较困扰开发人员，导致开发的程序健壮性不强。

##解决方案
经查阅资料发现苹果提供了不同环境的统一配置方案，下面是我写的一个demo，用以配置不同的开发环境。

###### 1首先创建一个`Single View Application` ，生成PCH文件，并在`build setting`中配置pch文件路径，我的工程配置路径为`$(SRCROOT)/AutoBuildConfigSet-Demo/AutoBuildConfigSet-Demo.pch`
![1.png](http://upload-images.jianshu.io/upload_images/4919697-f797d847ad6a94f2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### 2 添加`Configuration Settings File `文件命名为`Enterprise`
![2.png](http://upload-images.jianshu.io/upload_images/4919697-e98ff814d040917d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### 3 重复步骤2 创建文件结构如下
![3.png](http://upload-images.jianshu.io/upload_images/4919697-40f340cb39d2d882.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### 4 在`PROJECT`下的`Configurations` 添加`Enterprise` 编译模式
![4.png](http://upload-images.jianshu.io/upload_images/4919697-8157c9fe3ec8687b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### 5 设置编译模式与我们创建的`Configuration Settings File`相对应，如下图
![5.png](http://upload-images.jianshu.io/upload_images/4919697-d9bd818e1f59fcc1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### 6 在`TARGETS` 下搜索`macros` 如下图
![6.png](http://upload-images.jianshu.io/upload_images/4919697-450704b24b34d54b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### 7 分别在对应的模式上面添加设置编译参数，
DEBUG_VERSION=1
ENTERPRISE_VERSION=1
RELEASE_VERSION=1
用以在pch文件中对各种编译宏的模式判断 ，如下图7，8，9
![7.png](http://upload-images.jianshu.io/upload_images/4919697-42cbd3af49fa6bfa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![8.png](http://upload-images.jianshu.io/upload_images/4919697-3de53bff7e07b143.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![9.png](http://upload-images.jianshu.io/upload_images/4919697-8cf93b618b6595ab.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### 8 PCH文件夹下添加如下内容
```
//测试环境
#ifdef DEBUG_VERSION

#define BASE_URL_STR @"http://www.baidu.com/"


//企业环境
#elif defined(ENTERPRISE_VERSION)
#define BASE_URL_STR @"http://www.google.com/"



//AppStore环境
#elif defined(RELEASE_VERSION)
#define BASE_URL_STR @"http://www.sina.com/"


```

![QQ20170303-225527.png](http://upload-images.jianshu.io/upload_images/4919697-7db16948db0d5318.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
###### 9 添加打印日志如下
![QQ20170303-225157.png](http://upload-images.jianshu.io/upload_images/4919697-4a25c48144aa58a7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### 10 调整编译的`schema`的编译模式为 `Enterprise`模式
![10.png](http://upload-images.jianshu.io/upload_images/4919697-a5f138f3382ea075.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
###### 11 查看打印日志
![11.png](http://upload-images.jianshu.io/upload_images/4919697-e642c0e21692aa54.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

[github demo 链接地址 ](https://github.com/Marviszhao/AutoBuildConfigSet-Demo.git)欢迎star，多多鼓励
