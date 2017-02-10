### Macaca介绍
Macaca 是一套面向用户端软件的测试解决方案，提供了自动化驱动，周边工具，集成方案，旨在解决终端上的测试、自动化、性能等方面的问题。阿里的移动端自动测试框架，同时支持android，iOS,PC端。        

官网：[https://macacajs.com/zh/](https://macacajs.com/zh/)          

#### 特点       

**多端支持**          
随着移动时代和智能终端时代的到来，为给用户带来更优质、完整的体验，我们的产品已经遍布各终端，同时单一的运行时架构往往不能满足工程的需要。Macaca 支持主流的移动技术平台 iOS，Android，以及两大平台的混合运行时 Webview，也支持以往的桌面端浏览器。

**标准化**        
Macaca 提供了标准化的驱动层，消除了各技术平台测试技术栈的差异。用户只需要遵从 W3C webdriver 标准 标准即可多端无忧，理解成本降低。


**集成和融合**                      
Macaca 提供了多种持续集成方案和功能模块，方便集成到研发和测试的各个环节。同时 Macaca 支持 Java, Node.js, Python 语言栈，给技术工程师以更多选择。        

**社区生态**          
Macaca 拥有庞大的用户群，自我生长的开源形态和优质的中文社区环境。       

#### 环境配置          

**安装 Node.js**        
请安装 Node.js v4.0 或者更高版本，装好 Node.js 后命令行里就已经集成了 npm 工具，为了提高安装模块的速度，请使用国内的 cnpm。

**iOS 环境**       
请安装 Xcode8 或者更高版本      

需要安装 usbmuxd 以便于通过 USB 通道测试 iOS 真机，不需要测试真机则不用安装      
$ brew install usbmuxd       
应用中如含有 WebView，请安装 ios-webkit-debug-proxy
$ brew install ios-webkit-debug-proxy

备注：使用brew命令需要安装Homebrew（一款常用的 MacOS 的包管理器），请按照官网提示安装。           
准备 App 包：如需要测试 iOS 应用，请使用 Scheme 设置为 debug 的 .app 包。
