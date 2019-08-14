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


!![](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b2/Ryan_Dahl.jpg/440px-Ryan_Dahl.jpg .img.alignleft.size-30.animated.fadeInUp.tobuild)
<br/>
:::{.content-left.animated.fadeInUp.tobuild}
Ryan Dahl 2009 年创建 Node.js
:::{.animated.fadeInUp.tobuild}
2012 年 Ryan Dahl 离开 Node.js 社区
:::{.animated.fadeInUp.tobuild}
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
由 Google 为 Chrome 开发的 Javascript 引擎, 核心工程师 Lars Bak 之前在 Sun 公司研究 Java 虚拟机，产出了 HotSpot 
:::


<slide class="bg-black-blue aligncenter" image="https://source.unsplash.com/C1HhAQrbykQ/ .dark">

## Javascript 引擎的执行速度

!![](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2017/02/01-01-perf_graph05.png .size-50.animated.fadeInUp.tobuild)


<slide class="bg-black-blue aligncenter" image="https://source.unsplash.com/C1HhAQrbykQ/ .dark">

## V8特点

<br/>
:::{.content-center.animated.fadeInUp.tobuild}
- JIT（Just-In-Time）编译，也就是即时编译，通过监听高频运行的代码，保存编译其结果进行优化，大大提高了 Javascript 的运行速度 （后来的 Javascript 都支持了 JIT） 
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
- 事件循环(Event Loop)

<slide class="bg-light aligncenter" image="https://source.unsplash.com/C1HhAQrbykQ/ .dark">
:::{.content-left.animated.fadeInLeft.toBuild}
#### 同步读取文件 {.content-center}
<br/>
<!-- :::{.content-center} -->
```js
const fs = require('fs')

// 读取文件的状态
let stats = fs.statSync('./a')

 //判断是否为文件
if (stats.isDirectory) {
    let data = fs.readFileSync('./a/e.md')
    console.log(data.toString())
}
```
:::

:::{.content-left.animated.fadeInRight.toBuild}
#### 异步读取文件 {.content-center}
<br/>
<!-- :::{.content-center} -->
```js
const fs = require('fs')

// 读取文件的状态
fs.stat('./a', (err, stats) => {
    if (err) return console.error(err)

    //判断是否为文件
    if (stats.isDirectory) {
        fs.readFile('./a/e.md', (err, data) => {
            console.log(data.toString())
        })
    }
})
```
:::


<slide class="bg-light aligncenter" image="https://source.unsplash.com/C1HhAQrbykQ/ .dark">

### 回调地狱问题
<br/>
:::{.content-center}
```js
step1(function (value1) {
    step2(value1, function(value2) {
        step3(value2, function(value3) {
            step4(value3, function(value4) {
                // Do something with value4
            });
        });
    });
});
```

<slide class="bg-light aligncenter" image="https://source.unsplash.com/C1HhAQrbykQ/ .dark">

### 使用 Promise

<br/>
:::{.content-center}
```js
step1()
.then(value1 => {
    return step2(value1)
})
.then(value2 => {
    return step3(value2)
})
.then(value3 => {
    return step4(value3)
})
```

<slide class="bg-light aligncenter" image="https://source.unsplash.com/C1HhAQrbykQ/ .dark">

### 使用 async/await
<br/>
:::{.content-center}
```js
async function start() {
    const value1 = await step1()
    const value2 = await step2(value1)
    const value3 = await step3(value2)
    const value4 = await step3(value3)
}
```


<slide class="bg-light aligncenter" image="https://source.unsplash.com/C1HhAQrbykQ/ .dark">

### Event Loop
<br/>

:::{.content-center}
- 所有任务都在主线程，形成一个执行栈
- 在主线程之外存在一个任务队列（Task Queue），系统将异步任务放到'任务队列'，然后主线程继续执行后续任务
- 一旦‘执行栈’中所有任务执行完成，系统会读取'任务队列'执行。如果异步任务以及结束了等待状态，就会从’任务队列‘进入执行队列，恢复执行
- 重复上面的第三步

<slide class="bg-light aligncenter" image="https://source.unsplash.com/C1HhAQrbykQ/ .dark">
### Event Loop
<br/>
<!-- :::{.content-center} -->
!![](https://uploads.toptal.io/blog/image/129650/toptal-blog-image-1556581249859-3d5f53eabb995a2cc7ea8328a78ca29e.png)




<slide class="bg-light aligncenter" image="https://source.unsplash.com/C1HhAQrbykQ/ .dark">

:::{.content-center}
```js
console.time('hello')
setTimeout(() => {
    console.timeEnd('hello')
}, 1000)
```




<slide class="bg-light aligncenter" image="https://source.unsplash.com/C1HhAQrbykQ/ .dark">

### Node.js 应用场景

!![](https://raw.githubusercontent.com/i5ting/How-to-learn-node-correctly/master/media/14912707129964/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202017-05-17%2007.25.05.png .content-left.size-50.animated.swing.tobuild)

<br/>
<br/>
<br/>

:::{.content-left.animated.swing}
- 跨平台桌面应用：使用electron/nw.js等框架, Node.js与操作系统互交提供统一的api，浏览器作为UI展示
- 前端工程化：React\Vue\Angular等主流框架使用的webpack/gulp等打包编译打包工具，使用Node.js构建
- Web应用开发：io密集型web应用，为前端提供Api接口
{.build}


<slide class="bg-light aligncenter" image="https://source.unsplash.com/C1HhAQrbykQ/ .dark">

### 创建 Node.js Web 服务
<br/>
:::{.content-center}
```js
const http = require('http')

const server = http.createServer((request, response) => {
    response.end('hello node')
})

server.listen(8080)
```

<slide class="bg-light aligncenter" image="https://source.unsplash.com/C1HhAQrbykQ/ .dark">

## 谢谢！{.text-landing.text-shadow}

