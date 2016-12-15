### Appium介绍     
Appium作为一个开源的、跨平台的自动化测试工具，适用于测试原生或混合型移动App。 Appium的核心是一个web服务器，他使用WebDriver json wire协议，来驱动系统的UIAutomation库。WebDriver Json wire协议的Server端采用node.js封装了iOS UI Automation的接口，提供提供出一套RESTFul web service的接口，这样Client端以HTTP请求获得操纵UI的能力。

说到底，真正执行测试的还是 UIAutomation，Appium只是封装或解释了UIAutomation的执行脚本，作为UIAutomation和被测试APP的中间层传递消息。

appium的优缺点

优点：     
（1） 跨平台 - appium可以很好的融合在addroid和iOS系统之间     
（2） 支持多种语言 - 支持各种语言对appium的脚本编写，但是好像oc的支持不太好     
（3） 不依赖源代码 - 不用依赖于源码的支持，这是一个很突出的亮点     
（4） 开源 - 这个说主要也不算主要，因为appium是给予UIAutomaiton之上的，而UIAutomation不是开源的   

缺点：     
（1） 环境配置较繁琐 - 配置及其繁琐，而且问题较多，需要你耐心的就一点点解决，iOS版本更为严重     
（2） 不支持自定义控件     
（3） UIWebView的状态不可访问      
（4） 无法脱机跑，需要连着Mac机器 - 这是iOS自动化框架共有的硬伤       
（5） 支持系统效率慢 - 这是我认为这个框架比较严重的伤，由于不是苹果公司自有的框架，在支持上总慢一两个月，所以很多人在适配新系统的时候比较头疼 Appium是由client和server组成，client提供多种语言的API，这些API是对WebDriver的扩展和封装，利用这些API就可以快速编写测试用例；client和server间通过符合Mobile JSON Wire Protocol的http请求进行交互。   

Appuim还提供一个第三文的工具Appium Inspector


## Auto_Analysis配置文档

- [环境配置](https://whuhan2013.github.io/Auto_Analysis/run)      
- [参数配置](https://whuhan2013.github.io/Auto_Analysis/parameter_configuration)     
- [用例编写](https://whuhan2013.github.io/Auto_Analysis/test_case_writing)   
- [测试报告](https://whuhan2013.github.io/Auto_Analysis/test_report)

### 其他

* [appium:appium_wiki文档](https://whuhan2013.github.io/Auto_Analysis/appium_wiki)

* [控件查找:controls_operations文档](https://whuhan2013.github.io/Auto_Analysis/controls_operations)