### Appium介绍     
Appium作为一个开源的、跨平台的自动化测试工具，适用于测试原生或混合型移动App。 Appium的核心是一个web服务器，他使用WebDriver json wire协议，来驱动系统的UIAutomation库。WebDriver Json wire协议的Server端采用node.js封装了iOS UI Automation的接口，提供提供出一套RESTFul web service的接口，这样Client端以HTTP请求获得操纵UI的能力。

说到底，真正执行测试的还是 UIAutomation，Appium只是封装或解释了UIAutomation的执行脚本，作为UIAutomation和被测试APP的中间层传递消息。
<img src="https://whuhan2013.github.io/Auto_Analysis/p2.png" width="800">

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

**参考**           
[基于 appium 的自动化测试工具，支持多进程，性能采集分析等](https://testerhome.com/topics/6482)

## Auto_Analysis环境配置

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

## 测试用例编写规范

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
| test_control      | 控件         | com.xx.id | /         | 是    |
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
  test_name: 已有账号，去登录
  test_id: 0001
  test_control_type: text
  test_action: click
  test_control: 已有账号，去登录
-
  test_name: 输入帐号名
  test_id: 0002
  test_control_type: class
  test_action: send_keys
  test_control: android.widget.EditText
  test_text: samuel
  test_index: 0
-
  test_name: 输入密码
  test_id: 0003
  test_control_type: class
  test_action: send_keys
  test_control: android.widget.EditText
  test_text: 123456
  test_index: 1

-
  test_name: 登录
  test_id: 0004
  test_control_type: text
  test_action: click
  test_control: 登录

-
  test_name: 创建工单
  test_id: 0005
  test_control_type: id
  test_action: click
  test_control: 创建工单
-
  test_name: NancyCustomer1
  test_id: 0006
  test_control_type: text
  test_action: click
  test_control: NancyCustomer1
-
  test_name: 资产范围
  test_id: 0007
  test_control_type: text
  test_action: click
  test_control: 资产范围
  test_sleep: 3

-
  test_name: 楼宇BADGOOD
  test_id: 0008
  test_control_type: text
  test_action: click
  test_control: 楼宇BADGOOD  

-
  test_name: 5层公共照明
  test_id: 0009
  test_control_type: text
  test_action: click
  test_control: 5层公共照明 

-
  test_name: 完成
  test_id: 0010
  test_control_type: text
  test_action: click
  test_control: 完成 

-
  test_name: 执行人
  test_id: 0011
  test_control_type: text
  test_action: click
  test_control: 执行人 
  test_sleep: 3

-
  test_name: abcnew
  test_id: 0012
  test_control_type: text
  test_action: click
  test_control: abcnew

-
  test_name: 1234
  test_id: 0013
  test_control_type: text
  test_action: click
  test_control: 1234

-
  test_name: 完成
  test_id: 0014
  test_control_type: text
  test_action: click
  test_control: 完成 

-
  test_name: 工单任务
  test_id: 0015
  test_control_type: text
  test_action: click
  test_control: 工单任务 

-
  test_name: robotCreate
  test_id: 0016
  test_control_type: class
  test_action: send_keys
  test_control: android.widget.EditText
  test_text: his is robot create ticket2.

-
  test_name: 完成
  test_id: 0017
  test_control_type: text
  test_action: click
  test_control: 完成 

-
  test_name: 保存
  test_id: 0018
  test_control_type: text
  test_action: click
  test_control: 保存 
  

```

## 测试报告样式

#### 字段解释

* end time:测试结束时间
* 测试应用包名,测试应用版本号
* 设备名,磁盘状态 已用|可用,wifi名称,系统版本,分辨率
* all_case:用例总数,passed:通过数,failed失败数
* case_name:用例名
* case_result:用例结果
* case_img:用例执行后截图
* case_per:会比对上一次与本次的性能状态截图
* case_log:本case全量log
* case_filter_log:筛选后log


<img src="https://whuhan2013.github.io/Auto_Analysis/p1.png" width="800" height="600">