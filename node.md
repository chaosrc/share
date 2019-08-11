title: Nodejs 分享
speaker: chao
plugins:
    - echarts

<slide class="bg-black-blue aligncenter" image="https://source.unsplash.com/C1HhAQrbykQ/ .dark">

# Nodejs 分享 {.text-landing.text-shadow}

By chao {.text-intro}

<!-- [:fa-github: Github](https://github.com/ksky521/nodeppt){.button.ghost} -->

<slide class="bg-black-blue aligncenter" image="https://source.unsplash.com/C1HhAQrbykQ/ .dark">

<!-- ## 创建 -->


!![](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b2/Ryan_Dahl.jpg/440px-Ryan_Dahl.jpg .img.alignleft.size-30)
<br/>
:::{.content-left}
Ryan Dahl 2009 年创建

2012 年 Ryan Dahl 离开 Node.js 社区

2018年创建 [Deno](https://github.com/denoland/deno)
:::



<slide class="bg-black-blue aligncenter" image="https://source.unsplash.com/C1HhAQrbykQ/ .dark">

## Node.js 组成
<br/>
!![](https://image.slidesharecdn.com/nodejs-140507132306-phpapp02/95/nodejs-code-tracing-2-638.jpg?cb=1427946166 .animated.fadeInUp.tobuild)


<slide class="bg-black-blue aligncenter" image="https://source.unsplash.com/C1HhAQrbykQ/ .dark">

## V8 引擎 {.animated.fadeInUp}
<br/>
:::{.animated.fadeInUp.content-center.tobuild}
由 Google 为 Chrome 开发的Javascript 引擎,核心工程师 Lars Bak 之前在 Sun公司研究Java 虚拟机，产出了 HotSpot 
:::


<slide class="bg-black-blue aligncenter" image="https://source.unsplash.com/C1HhAQrbykQ/ .dark">

## Javascript 引擎的执行速度

!![](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2017/02/01-01-perf_graph05.png .size-50.animated.fadeInUp.tobuild)


<slide class="bg-black-blue aligncenter" image="https://source.unsplash.com/C1HhAQrbykQ/ .dark">

## V8特点

<br/>
:::{.content-center.animated.fadeInUp.tobuild}
- JIT（Just-In-Time）编译，也就是即时编译，通过监听高频运行的代码，保存编译其结果进行优化，大大提供 Javascript 的运行速度 （后来的 Javascript 都支持了 JIT） 
- 垃圾回收，V8的垃圾回收借鉴了 Java VM 的精确垃圾回收管理，垃圾回收的效率远远高于其他引擎
- 其他优化，内联缓存提高属性访问、隐藏类对动态添加类属性的优化
- 遵循 ECMAScript，紧根 ECMAScript 最新标准，支持最新的语法


<slide class="bg-black-blue aligncenter" image="https://source.unsplash.com/C1HhAQrbykQ/ .dark">
<!-- ## Libuv -->

<br/>

:::{.size-20.content-center}
![](https://raw.githubusercontent.com/libuv/libuv/master/img/banner.png)
:::
:::{.content-center}
libuv 是一个专注与异步 I/O 的跨平台库，由 Ryan Dahl 为 Node.js 编写，libuv 由事件循环和线程池组成，负责所有 I/O 任务的分发与，也用于Luvit, Julia, pyuv等平台。


<slide class="bg-black-blue aligncenter" image="https://source.unsplash.com/C1HhAQrbykQ/ .dark">

## Node.js 的特点
<br/>
<br/>
<br/>

- 非阻塞异步 I/O 模型
- 事件驱动

<slide class="bg-light aligncenter" image="https://source.unsplash.com/C1HhAQrbykQ/ .dark">
比如异步读取文件
:::{.content-center}
```js
const fs = require('fs')

fs.readFile('./package.json', (err, data) => {
    console.log(data.toString())
})
```