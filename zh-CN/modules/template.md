---
root: false
name: 视图
sort: 5
---

# 模板引擎

框架默认采用的是JSP引擎进行处理，按照惯例， Blade 轻松整合了 Java 常用的几个模板引擎到 web 应用。

- `blade-jetbrick`：基于jetbrick-template模板引擎的扩展，也是本人最喜爱的模板引擎
- `blade-velocity`：基于velocity模板引擎的扩展
- `blade-beetl`：基于beetl模板引擎的扩展

## JSP渲染

默认使用了JSP引擎进行渲染，那么在开发 web 应用的时候应该注意什么呢？

- 默认的jsp视图目录是 `WEB-INF`
- Servlet3中使用EL表达式需要设置 `isELIgnored="false"`

**模板目录**

默认所有视图文件存放在`webapp`下的`WEB-INF`文件夹下，可进行设置：

```java
// 设置模板文件目录
blade.viewPrefix("/WEB-INF/views/");
```

**如何输出到页面？**

```java
public void index(Request request, Response response){
    request.attribute("name", "jack");
    response.render("index");
}
```

`blade`框架内置了JSP渲染，所以你看到的 `response.render("index")` 代码是可以返回到 `WEB-INF/index.jsp` 文件上的，
这个文件在哪里，请看前面的 **模板目录**。

当然`blade`还支持类似spring的`ModelAndView`，怎么使用呢，

```java
public void index(Request request, Response response){
    ModelAndView modelAndView = new ModelAndView("index");
    modelAndView.add("name", "jack");
    response.render(modelAndView);
}
```

喏，很简单吧。什么意思呢？
`ModelAndView`是一个视图模型对象，在spring里出现，里面也就是存放视图和数据而已，
你可以看它的源码，用`Map`存放数据，`String`变量存放视图文件。


## 配置模板引擎

```java
// 设置模板引擎
JetbrickRender jetbrickRender = new JetbrickRender();
jetEngine = jetbrickRender.getJetEngine();
blade.viewEngin(jetbrickRender);
```

其他更多操作就遵循模板的使用方法即可。
