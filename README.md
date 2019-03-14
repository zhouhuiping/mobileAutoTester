# 自动化测试调研
目录：
1. 测试理论和现状
2. 前端测试分类
3. 什么样的项目适合自动化测试？
4. 如何去做前端UI自动化测试？
5. 现状问题总结
6. 参考资料

## 测试理论和现状

持续集成与自动化测试不再是新概念，而且持续集成与自动化测试在很多企业内部已开展实施，
> 在开发与测试之间，开发团队注重CI而很难实践的是Unit Test，测试团队则更注重CT而很难实践是UI automatic Tests。

![image](http://upload-images.jianshu.io/upload_images/2054612-1a163138ffcfcfa4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/647/format/jpg)

说到持续集成就不得不说自动化测试金字塔模型（Martin Fowler）

![image](https://upload-images.jianshu.io/upload_images/1430016-d8b2f2e82b547815.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/619)

该图说明了三个问题：

>- Unit Tests：一般情况下由开发团队完成，当然，如果有测试开发团队，这部分的内容会有开发团队与测试开发团队一同完成。
>- API Tests：由测试团队完成。这是重点，当下提供比较多的都是HTTP API，相对稳定，适合自动化测试。
>- UI Tests：GUI测试，由测试团队完成。在这个模型中该部分所占比例最少。

在金字塔模型中，是要告诉我们几个道理
>- 越底层，越稳定，越高效，越低成本，但是越底层越难实施，越底层的实现对技术专业性要求越高往往越专业的人才也意味着人力成本越高。
>- 综合金字塔模型，提出了橄榄模型，如上图：提高api测试的比例，该部分投资回报率最高；今天的重点是UI automatic Tests，它的投资回报率不如API测试但是它又是整个持续集成中不可缺少的环节。


## 前端测试分类
### 单元测试：

> 以模块为单元，测试你代码的本身，确保你编写的模块还有逻辑正确。只要输入的值不变，输出的值也应该不发生改变

### 前端自动化测试：

前端测试主要分五大方向测试，而这五大方向也分很多小方向测试，首先简单的介绍每个方向的概念
![image](https://image-static.segmentfault.com/414/902/4149020399-5aebbb51cb85e_articlex)


> **1.界面样式测试**
> - 固定界面样式测试：主要针对文字内容不变的区域，例如页面的页头，页脚这类结构、内容不变的区域，而测试一般通过截图对比解决。
> - 结构不变界面样式测试：主要针对结构不变的区域，例如新闻区域这类结构不变，内容变化的区域，这类测试一般通过DOM元素对比解决。
> - 计算样式测试：主要针对计算样式不变的区域，这类测试一般通过比较计算样式解决，但是这种测试不推荐，因为测试成本比较大。

> **2. 功能测试**
> - 服务器数据预期测试：主要针对用户在前端界面进行某种操作后，提交数据给后台后，测试后台能否返回预期的数据
> - 界面功能测试：主要针对用户在前端界面进行某种交互性操作后，测试能否获取预期的功能、界面交互

> **3. 多浏览器测试(兼容性测试)**
> - 多浏览器测试：基于界面样式测试、功能测试的基础上来进行不同浏览器的的测试，俗称兼容性测试。

> **4. 性能测试**
> - 白屏时间：用户浏览器输入网址后至浏览器出现至少1px画面为止。
> - 首屏时间：用户浏览器首屏内所有的元素呈现所花费时间。
> - 页面回归时间：用户浏览器非第一次加载所有的元素呈现所花费时间。
> - 用户可操作时间(dom ready) ：网站某些功能可以使用的时间。
页面总下载时间(onload):网站中所有资源加载完成并且可用时间。

> **5. 质量测试**
> - 雅虎网站优化规则


## 什么样的项目适合自动化测试？
![image](https://image-static.segmentfault.com/186/357/1863576993-5aebbb34d96ca_articlex)



## 如何去做前端UI自动化测试？
UI自动化测试面临的第一个问题，多技术，多平台。
>- 传统技术如Native、Hybrid和Web，还有electron，多平台如appium、selenium等等。
>- UI自动化测试面临的第一个问题，多技术，多平台。

下面主要讨论界面回归测试和功能测试
### 一、web端(headless chrome)
#### 界面ui视觉测试
#### 1.截屏比对（局部、整页）
工具选择和对比
##### 像素对比工具有哪些？


名称 | 地址
---|---
uber-archive/image-diff | https://github.com/uber-archive/image-diff
yahoo/blink-diff | https://github.com/yahoo/blink-diff
PhantomCSS | https://github.com/HuddleEng/PhantomCSS
pixelmatch | https://github.com/mapbox/pixelmatch

##### 比较常见出名的几个Headless Browser，有哪些？

名称 | 内核 | 地址
---|---|---
Puppeteer | Webkit  | [https://github.com/GoogleChro...](https://github.com/GoogleChrome/puppeteer)
Selenium | 多个浏览器 | https://github.com/SeleniumHQ/selenium
PhantomJS | Webkit  | http://phantomjs.org/
SlimerJS | Gecko  | [https://github.com/laurentj/s...](https://github.com/laurentj/slimerjs)
TrifleJS | IE  | [https://github.com/sdesalas/t...](https://github.com/sdesalas/trifleJS)


PhantomJS 基于 Webkit 内核，不支持 Flash 的播放；SlimerJS 基于火狐的 Gecko 内核，支持 Flash播放，并且执行过程会有页面展示。

#### 2.dom结构对比加css样式对比
#####   page-monitor 
> https://github.com/fouber/page-monitor

### 二、RN自动化测试
随着开发模式的逐渐成熟，对RN项目的自动化测试也在不断探索中慢慢完善， 最终选择了 Detox (by Wix) 做 E2E 自动化测试， Jest (FaceBook) + Enzyme (Airbnb) 做集成测试和单元测试。
https://github.com/wix/detox

### 三、客户端(多端)
#### 1.macaca进行移动端hybird自动化测试
https://macacajs.com/zh/guide/computer-vision.html#%E5%85%B6%E5%AE%83%E6%96%B9%E6%A1%88
>- macaca支持主流的移动技术平台iOS，Android，以及两大平台的混合运行时Webview，也支持以往的桌面端浏览器。
>- macaca提供Node.js, Java, Python 三大主流的语言栈，方便工程师和所在团队选择合适的开发语言。
>- Macaca 提供了标准化的驱动层，消除了各技术平台测试技术栈的差异。用户只需要遵从"W3C webdriver标准" 即可多端无忧，理解成本降低。

#### 2.Appium+WDA(webDriverAgent)
appium 是一个自动化测试开源工具，支持 iOS 平台和 Android 平台上的原生应用，web应用和混合应用。
http://appium.io/
#### 3.用例断言
>- 测试框架：Mocha、Jasmine、Jest、cucumber，karma等
>- 断言库：Should.js、chai、expect.js等
>- 代码覆盖率：istanbul等

#### 4.持续集成
工具会根据用户提交配置自动运行并将结果返还给用户。
如果能通过ci实现一系列的自动化部署测试等工作，使用上就更加顺畅了。


谈起ci肯定要介绍jenkins,稳定可靠，是很多大公司ci的首选。在前端的眼中它看起来会感觉。。丑了点和难用了点。。travis-ci比较小清新和直观易用


国外做的比较好的轻量级ci系统有:

- http://wercker.com/
- https://semaphoreci.com/
- https://codeship.com
- https://circleci.com/

良好的用户体验让人使用的心情愉悦没有障碍，如果想定制可以作为参考。

减小使用和维护成本
>- ##### 与构建工具结合
> webpack,将自动化测试与构建工具结合能更早的发现问题，也能减小使用和维护成本
>- ##### 与持续基础结合
> 与CI系统的结合能更大范围更有效的发挥自动化测试的作用
>- ##### 与工作流结合
> 与日常工作流结合同样是为了减少使用成本，如将结果通过自定义的方式反馈给用户等。
>- ##### 测试配置化
> 测试配置化能让用户使用和维护更加简单、大部分情况下只需要维护配置脚本即可

#### 5.理想中的自动化流程：
当App(iOS/Android)，以及H5，任意部分存在代码提交时，系统能自动拉取最新代码进行部署并执行自动化回归测试，及时地将执行情况反馈给开发人员。

![image](http://pic4.zhimg.com/ce453792a0ad8ee395399d6299448c3b_r.jpg)

目标确定后，便是分阶段进行实现，需要开发的模块包括：

> -  自动化测试平台（Automated Test Platform）：满足iOS/Android/H5的自动化功能测试，包括模拟器和真机的测试；
> - 测试管理平台（Test Management Platform）：实现自动化测试用例管理、手动下发测试任务、测试结果报表展现、Dashboard等功能；
> - 打包平台（Pack System）：实现iOS/Android的自动化构建；
> - 持续集成流程打通：对Jenkins进行二次开发，与测试管理平台打通，实现全流程的持续集成自动化测试。

#### 6.自动化测试工具对比

![image](http://ww4.sinaimg.cn/large/6b65a607jw1fai3td77vwj20rn0fiq72.jpg)

## 总结问题
### 测试提出的问题？
1. 投入产出比?
1. 全流程覆盖数据问题?
1. 用例变化的问题?
1. 清晰的目标是什么，做到什么程度?针对生产还是测试环境？
### 我们的问题？
1. 前端现在的单元测试还不充分
1. 测试覆盖率做到什么程度?
1. 流程自动化的瓶颈?
2. macaca有些文档并不是很详细
3. 如果做全端的测试，我们本身对ios和Android代码和一些技术配置并不是很熟悉

## 参考资料
> 前端自动化测试探索
> https://www.cnblogs.com/9988/p/5201347.html

> 前端自动化测试之视觉测试
> https://segmentfault.com/a/1190000014720175?utm_source=tag-newest

> 腾讯--移动APP自动化测试框架对比
> https://mp.weixin.qq.com/s/pu1TKZhNW2L2BmvpjGzLCw

> 美团--客户端自动化测试研究
> https://tech.meituan.com/2017/06/23/mobile-app-automation.html

> 美团终端主动监控平台的建设(2018.7)
https://juejin.im/post/5b4565cbe51d4519277b770a

> UI 自动化框架调研总结
https://testerhome.com/topics/6602

> 如何自动化测试 React Native 
https://tech.glowing.com/cn/react-native-automation-high-level-thoughts-and-e2e-testing/


