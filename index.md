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

#### 安装node

[官网地址](https://nodejs.org/en/download/)

* OS:brew install node
* windows,linux参照官网

#### 安装appium

* 1: npm install -g cnpm --registry=https://registry.npm.taobao.org

* 2: cnpm install -g appium --no-cache

### python

方法请自行查找

### 运行

* git 源码
* cd Auto_Analysis
* python setup.py install
* python run.py

注:性能图片生成用到了matplotlib,如果setup未安装成功

* Linux:sudo apt-get install python-matplotlib

### 参数配置

## 执行的参数配置


* 配置 data/test_info.ini ,

```ini

[test_package_name]
# 应用包名
package_name = com.x.x.x

[test_install_path]
* 被测试应用地址
path = /Users/joko/Auto_Analysis/data/app.apk

[test_device]
* device信息存放地址
device = /Users/joko/Auto_Analysis/data/incidental/device_info.yaml

[test_case]
* 测试case存放地址
case = /Users/joko/Auto_Analysis/testcase
* 测试报告存放地址
log_file = /Users/joko/Auto_Analysis/result
* 错误图片展示地址
error_img = /Users/joko/Auto_Analysis/data/incidental/error.png

[minicap]
* minicap地址:用于截图
minicap_path = /Users/joko/Auto_Analysis/data/minicap/bin/{}/minicap
minitouch_path = /Users/joko/Auto_Analysis/data/minicap/minitouch/{}/minitouch
minicapso_path = /Users/joko/Auto_Analysis/data/minicap/shared/android-{}/{}/minicap.so

[test_db]
* 存放测试记录的db地址
test_result = /Users/joko/Auto_Analysis/data/incidental/test.db

```

注:windows路径也如此相同写法:d:/file/1.x

* 配置 data/appium_parameter.yaml

```yaml
---
-
 appPackage: 应用包名
 appActivity: 启动Activity名
 appWaitActivity: 等待的Activity名
 unicodeKeyboard: True
 resetKeyboard: True
 resetKeyboard: True
 noReset: False
```



### 用例编写

* 参见test_case_writing文档

### 测试报告

* 参见test_report文档

### 其他

* appium:appium_wiki文档

* 控件查找:controls_operations文档

* 如果想单线程运行,请运行:po.integration


### 测试用例编写规范

* 1: 需要了解yaml格式编写规范,建议使用pycharm编写,自带yaml文档检查器.
[yaml语法学习地址](http://www.ruanyifeng.com/blog/2016/07/yaml.html)
* 2: 用例名不可重复,会影响用例的继承

## 测试用例字段解释


| 字段                | 解释         | 演示        | 包含字段      | 是否必须 |
| ----------------- | ---------- | --------- | --------- | ---- |
| test_name         | 用例名        | login     | /         | 是    |
| test_id           | 用例id       | 0001      | /         | 否    |
| test_control_type | 查找控件方式     | xapth     | xpath, id | 否    |
| test_action       | 操作方法       | click     | 见下表       | 是    |
| test_control      | 控件         | com.xx.id | /         | 否    |
| test_text         | 断言、输入文本    | test      | /         | 否    |
| test_inherit      | 继承用例名      | login     | /         | 否    |
| test_range        | 循环本步骤次数    | 2         | /         | 否    |
| test_sleep        | 步骤执行后，等待秒  | 2         | /         | 否    |
| test_wait         | 配合断言，等待控件秒 | 30        | /         | 否    |


| test_action | 解释   | 所有字段                                     | 配合字段                                     | 辅助配合字段    |
| ----------- | ---- | ---------------------------------------- | ---------------------------------------- | --------- |
| click       | 点击   | click                                    | test_control_type，test_control           | /         |
| send_keys   | 发送文本 | send_keys                                | test_control_type，test_control，test_text | /         |
| swipe       | 滑动   | swipe_left,swipe_right,swipe_up,swipe_down | /                                        | /         |
| assert      | 断言   | assert                                   | test_control_type，test_control，test_text | test_wait |
| entity      | 实体按键 | entity_home，entity_back，entity_menu，entity_volume_up，entity_volume_down | /                                        | /         |

## 完整用例范例,用例名:login

```yaml
---
-
  test_name: 点击跳过
  test_id: 0001
  test_control_type: id
  test_action: click
  test_control: test.joko.com.myapplication:id/button1
-
  test_name: 输入帐号名
  test_id: 0002
  test_control_type: id
  test_action: send_keys
  test_control: test.joko.com.myapplication:id/editText
  test_text: 199999999
-
  test_name: 输入密码
  test_id: 0003
  test_control_type: id
  test_action: send_keys
  test_control: test.joko.com.myapplication:id/editText2
  test_text: 9999

-
  test_name: 点击登录
  test_id: 0004
  test_control_type: xpath
  test_action: click
  test_control: //android.widget.Button[contains(@text,'确定')]

-
  test_name: 向上滑动页面
  test_id: 0005
  test_action: swipe_up
  test_range: 3

-
  test_name: 向下滑动页面
  test_id: 0005
  test_action: swipe_down
  test_range: 3

```