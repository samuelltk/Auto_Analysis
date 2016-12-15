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