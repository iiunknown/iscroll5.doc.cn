# iScroll 5 API 中文版

[Gitbook发布版本](http://iiunknown.gitbooks.io/iscroll-5-api-cn/content/)

[![Build Status](https://www.gitbook.io/button/status/book/iiunknown/iscroll-5-api-cn)](https://www.gitbook.io/book/iiunknown/iscroll-5-api-cn/activity)

## 前言
最近项目上需要使用[iScroll](http://iscrolljs.com)，在中文圈里找了找，只找到了iScroll 4的中文版API。加上最近开始使用github（准确说，github账号是很多年前注册的，一直在企业应用里摸爬滚打，荒废了账号很长时间，是理由吗？是理由吗？），出于对开源社区的敬意，我突然觉得应该做点啥，于是先挑一个简单点儿的，把iScroll 5的API翻译一下，方便中文用户使用。

##搭后语
iScroll对于我来讲典型的应用场景位于移动设备的App，基于Cordova/Phonegap + JQM + iScroll开发移动设备上的App，对于以数据呈现为主体的企业应用来讲无疑是一个多快好省的解决方案。这三驾马车前两个可以堂而皇之的称之为`开发框架`，iScroll只能称之为工具，尽管如此，iScroll带来的强大的滚动功能，能节省我们在项目开发上的部分时间（这也是开源社区的力量），所以也值得我花时间理解作者的代码和文档。如果您认同这种功劳苦劳，请到[**github**](https://github.com/iiunknown/iscroll5.doc.cn)上给我一个star。由于才疏学浅，在翻译过程中难免会有错误或者瑕疵，请在[**issure**](https://github.com/iiunknown/iscroll5.doc.cn/issues)中提出，我会及时更正。

下面，我们开始iScroll之旅，请系好安全带。

##iScroll简介
iScroll是一个高性能，资源占用少，无依赖，多平台的javascript滚动插件。

它可以在桌面，移动设备和智能电视平台上工作。它一直在大力优化性能和文件大小以便在新旧设备上提供最顺畅的体验。

iScroll不仅仅是 滚动。它可以处理任何需要与用户进行移动交互的元素。在你的项目中包含仅仅4kb大小的iScroll，你的项目便拥有了滚动，缩放，平移，无限滚动，视差滚动，旋转功能。给它一个扫帚它甚至能帮你打扫办公室。

即使平台本身提供的滚动已经很不错，iScroll可以在此基础上提供更多不可思议的功能。具体来说：

* 细粒度控制滚动位置，甚至在滚动过程中。你总是可以获取和设置滚动器的x，y坐标。
* 动画可以使用用户自定义的擦出功能（反弹'bounce'，弹性'elastic'，回退'back'，...）。
* 你可以很容易的挂靠大量的自定义事件（onBeforeScrollStart, *
* 开箱即用的多平台支持。从很老的安卓设备到最新的iPhone，从Chrome浏览器到IE浏览器。

