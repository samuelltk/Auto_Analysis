## Macaca介绍
Macaca 是一套面向用户端软件的测试解决方案，提供了自动化驱动，周边工具，集成方案，旨在解决终端上的测试、自动化、性能等方面的问题。阿里的移动端自动测试框架，同时支持android，iOS,PC端。        

官网：[https://macacajs.com/zh/](https://macacajs.com/zh/)          

### 特点       

**多端支持**          
随着移动时代和智能终端时代的到来，为给用户带来更优质、完整的体验，我们的产品已经遍布各终端，同时单一的运行时架构往往不能满足工程的需要。Macaca 支持主流的移动技术平台 iOS，Android，以及两大平台的混合运行时 Webview，也支持以往的桌面端浏览器。

**标准化**        
Macaca 提供了标准化的驱动层，消除了各技术平台测试技术栈的差异。用户只需要遵从 W3C webdriver 标准 标准即可多端无忧，理解成本降低。


**集成和融合**                      
Macaca 提供了多种持续集成方案和功能模块，方便集成到研发和测试的各个环节。同时 Macaca 支持 Java, Node.js, Python 语言栈，给技术工程师以更多选择。        

**社区生态**          
Macaca 拥有庞大的用户群，自我生长的开源形态和优质的中文社区环境。       

### 环境配置          

**安装 Node.js**        
请安装 Node.js v4.0 或者更高版本，装好 Node.js 后命令行里就已经集成了 npm 工具，为了提高安装模块的速度，请使用国内的 cnpm。

**iOS 环境**       
1.请安装 Xcode8 或者更高版本      

2.需要安装 usbmuxd 以便于通过 USB 通道测试 iOS 真机，不需要测试真机则不用安装      
$ brew install usbmuxd       
应用中如含有 WebView，请安装 ios-webkit-debug-proxy            
$ brew install ios-webkit-debug-proxy         

备注：使用brew命令需要安装Homebrew（一款常用的 MacOS 的包管理器），请按照官网提示安装。           
准备 App 包：如需要测试 iOS 应用，请使用 Scheme 设置为 debug 的 .app 包。    

**安卓**          
1.安装 JDK         
2.配置 JAVA_HOME                                  
shell export JAVA_HOME=path/to/your/Java/Home                     
3.配置安卓sdk      
4.准备 App 包：如需要测试 Android 应用，请使用 .apk 格式的包。            

**命令行工具**         
安装macaca-cli         
$ npm i -g macaca-cli          
如果看到如下可爱的🐒，那恭喜你安装成功啦！重新安装则会覆盖更新。           
<img src="http://ww4.sinaimg.cn/large/6d308bd9gw1faie2w55hnj20rs0ov4fu.jpg" width="800">

**安装驱动（不同驱动适应不同平台的支持）**                                        
上述驱动可以按照自身需要选择性的安装，比如只需要测试 iOS平台用例，就执行iOS的安装命令：             
$ npm i macaca-ios -g     

**环境检查**     
通过 macaca doctor 可以检查环境是否配置成功       
$ macaca doctor           
如下图所示则表示环境均配置正常，如果有标红提示，则需要对应处理。                  
<img src="http://ww1.sinaimg.cn/large/6b65a607jw1fa3cqjexk2j21c20padqa.jpg" width="800">

#### 运行第一个测试案例        
首先下载案例app:mobile-app-sample-nodejs到本地                       

```
$ npm i macaca-cli macaca-ios -g
$ git clone https://github.com/macaca-sample/mobile-app-sample-nodejs.git --depth=1
$ cd mobile-app-sample-nodejs
# 安装项目依赖
$ npm i
$ macaca run --verbose
```


<img src="http://images2015.cnblogs.com/blog/46057/201606/46057-20160608194438090-960057521.gif" width="800">

**用例编写**         

```
var wd = require('macaca-wd');

var remoteConfig = {
  host: 'localhost',
  port: 3456
};

var driver = wd.promiseChainRemote(remoteConfig);

before(function() {
  return driver.init({
    platformName: 'desktop', // iOS, Android, Desktop
    browserName: 'chrome'    // Chrome, Electron
    app: path/to/app         // Only for mobile
  });
});

after(function() {
  return driver
    .sleep(1000)
    .quit();
});

it('#1 should', function() {

  ...

});
```


支持以下动作：             
1.点击       
2.输入值     
3.滑动     
4.长按       
5.可判断文字是否正确      
6.截图                          
7.drag       

元素查找方式：        
1.elementById       
2.elementByName        
3.elementByXPath        

#### 元素查看器             
安装                       
$ npm i app-inspector -g         

用法                    
直接 -u + 设备的 udid 即可                                  
$ app-inspector -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx       


Android 端      

<img src="http://ww4.sinaimg.cn/large/7dfcf2f7gw1f7bwlhpakwg20s40kge3k.gif" width="800"/>



iOS端

<img src="http://ww4.sinaimg.cn/large/7dfcf2f7gw1f7bwp1mgiyg20s40kg7wh.gif" width="800"/>        



#### 生成漂亮的测试报告

1.在测试目录下，安装mochawesome模块。（安装命令:npm install --save-dev mochawesome)            
2.在配置文件mocha.opts，增加--reporter mochawesome，如果已经有了这一项，修改即可。          
3.运行测试的时候，增加参数 --reporter mochawesome。(如：macaca run --verbose -d ./macaca-test/macaca-mobile-sample.test.js --reporter mochawesome）          

以上全部完成后，会在测试项目根目录下，多出来一个名字为mochawesome-reports的目录，这个就是生成的测试报告，在浏览器中打开，就可以看报告了。

以下就是最终的测试报告截图
<img src="https://testerhome.com/photo/2016/d9a4bb9f3c3a52c7b67445e83166d38a.png" width="800"/>

#### 原理浅析         

<img src="http://ww2.sinaimg.cn/large/6b65a607gw1fai803sahcj21ez0s1tis.jpg" width="800">      

**模块拆分讲解**           

**macaca**         
1.macaca-cli

Macaca提供的命令行工具

$macaca server 启动server

$macaca server --verbose 启动server并打印详细日志

$macaca doctor 检验当前macaca环境配置

2.app-inspector

macaca提供的元素查找工具，可以将app视图的结构以布局结构树的格式在浏览器上展示出来，用过点击某个元素，就可以方便的查询到该控件的基本信息，以方便查找。具体使用可参考官网: https://macacajs.com/inspector

3.UI Recorder

macaca提供的脚本录制工具，可以通过录制获得脚本，对于入门同学很有帮助。https://macacajs.com/recorder


**WebDriver-Server**

Macaca是按照经典的Server-Client设计模式进行设计的，也就是我们常说的C/S架构。WebDriver-server部分便充当了server这部分的角色，他的职责就是等待client发送请求并做出响应。

**WebDriver-Client**

client端简单来讲就是我们的测试代码，我们测试代码中的一些行为，比如控件查找、点击等，这些行为以http请求的方式发送给server,server接收请求，并执行相应操作，并在response中返回执行状态、返回值等信息。

也正是基于这种经典的C/S架构，所以client端具有跨语言的特点，macaca-wd，wd.java,wd.py分别是Macaca团队针对Js Java 以及Python的封装,只要能保证client端按照指定的要求发送Http请求，任意语言都可以。

**DriverList**

自动化要在不同的平台上跑，需要有对应平台的驱动，这部分驱动接收到来自server的操作命令，驱动各自平台的底层完成对应的操作。

**Macaca执行流程图**

了解了Macaca的组成模块以及他们各自的作用，下面我们看一下各个模块是如何组装起来实现自动化测试流程的
<img src="http://ww2.sinaimg.cn/large/6b65a607gw1fai80e6lxpj21ft0rhk0e.jpg" width="800">       


#### Macaca与Appium         
这种外部驱动instruments的server-client自动化测试框架，在iOS上实现方式非常受限的，所以其底层的实现方式是一致的。

而在应用级上的封装，二者均采用了Node.js作为开发语言，接口也基于web-driver实现，所以Macaca和Appium相似程度非常高。

**如何看待Macaca和Appium区别？**

以下是Macaca作者的设计思想为：appium 是个优秀的工具。但无法满足更轻、更快、更稳、更易集成、更贴合业务的高要求。          
可以认为Macaca是一个轻量级的Appium。当然，这就意味着很多Appium的功能会没有了。但这也造就了一个轻量级的，更易集成的框架。             


