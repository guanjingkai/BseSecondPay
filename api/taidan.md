# 1.扫码获取订单成功
### 1.1原型/效果图
![](api/media/15127049143897.jpg)

### 1.2操作流程

### 1.3信息结构

### 1.4用例
|用例名称|进入设置主页面|
|-------|
|行为角色|餐台收银员|
|需求目的|查看全部明细|
|前置条件|小精灵服务台登录成功|
|后置条件|设置主页面入口|


### 1.5退出机制
|操作类型|目标控件|去向|
|-------|
|点击|左上角关闭按钮|展开对话框|
|点击|左上角关闭按钮|设置控件底色选中|
|鼠标悬停|非控件位置|关闭设置对话框|
|点击|设置|进入设置主页面|

### 1.6显示及排序机制
|内容控件|加载方式|显示内容|容量|排序机制|刷新机制|新数据加载|
|-------|
|订单明细|SPA异步加载|文字|6/不限|单价倒序|定时刷新|1s更新一次|

### 1.7缓存机制
无

### 1.8控件描述
|控件描述|控件类型|操作|触发源|触发时|触发后|备注|
|-------|
|设置|label|点击|控件本身|无|打开设置界面||
### 1.9临界值和数据验证
无

### 1.10异常处理
无



