### 1主时序图
![](main/media/tongbu.png)

### 2步骤描述
 
### 2.1 s1 用户下单
##### 2.1.1 步骤说明
用户进店后翻阅菜单，确认菜品后，完成点餐的操作
##### 2.1.2 用例说明
|用例名称|用户下单|
|-------|
|行为角色|门店顾客|
|需求目的|完成下单|
|前置条件|确认菜品|
|后置条件|通过收银台完成下单操作|
##### 2.1.3 数据流转
- 无

##### 2.1.4 异常说明
- 无

### 2.2 s2 创建新订单
##### 2.2.1 步骤说明
S1 确认下单后，收银软件会向其数据库的订单表，订单明细表中插入相应的数据
##### 2.2.2 用例说明
|用例名称|创建新订单|
|-------|
|行为角色|收银软件|
|需求目的|完成数据库的数据创建|
|前置条件|用户下单|
|后置条件|数据库数据创建成功|
##### 2.2.3 数据流转
- 无

##### 2.2.4 异常说明
- 无

### 2.3 s3 Insert触发器
##### 2.3.1 步骤说明
通过触发器来监控收银软件的订单变化，并通过Insert触发器来监控订单数据的变化，并同步到xjl_order订单库，实现对新订单的实时监控
##### 2.3.2 用例说明
|用例名称|Insert触发器|
|-------|
|行为角色|数据库|
|需求目的|监控新订单|
|前置条件|订单创建成功|
|后置条件|把新订单更新到xjl_order数据库|
##### 2.3.3 数据流转
本步骤是利用触发器的原理实现了数据的实时获取
>下面是 xjl_order 表所必须的业务类字段，仅供数据结构设计参考，详细可参考 联付通OpenAPi-订单-创建预支付单接口

|字段|含义|
|-----|-----|
|id|主键|
|order_id|订单id|
|order_type|订单类型`create`,`update`,`end`|
|create_time|订单创建时间|
|update_time|订单更新时间|
|total_amount|订单总金额|
> 支付完成的 订单的 order_type = create

##### 2.3.4 异常说明
- 无

### 2.4 s4 用户支付
##### 2.4.1 步骤说明
用户对订单进行支付
##### 2.4.2 用例说明
|用例名称|用户下单|
|-------|
|行为角色|门店顾客|
|需求目的|完成支付|
|前置条件|已完成下单操作|
|后置条件|支付成功|
##### 2.4.3 数据流转
- 无

##### 2.4.4 异常说明
- 无

### 2.5 s5 更新订单
##### 2.5.1 步骤说明
S5 支付成功后，收银软件会修改其数据库订单表的对应订单的相关字段值
##### 2.5.2 用例说明
|用例名称|修改订单状态|
|-------|
|行为角色|收银软件|
|需求目的|完成数据库的数据更新|
|前置条件|用户支付成功|
|后置条件|数据库数据修改成功|
##### 2.5.3 数据流转
- 无

##### 2.5.4 异常说明
- 无

### 2.6 s3 Update触发器
##### 2.6.1 步骤说明
通过触发器来监控收银软件的订单变化，并通过Update触发器来监控订单数据的变化，对支付成功的订单同步状态到xjl_order订单库的对应订单，实现对支付成功订单的实时监控
##### 2.6.2 用例说明
|用例名称|Update触发器|
|-------|
|行为角色|数据库|
|需求目的|监控订单更新|
|前置条件|订单更新成功|
|后置条件|把新支付成功的订单状同步到xjl_order表对应的订单|
##### 2.6.3 数据流转
本步骤是利用触发器的原理实现了数据的实时获取
>下面是 xjl_order 表所必须的业务类字段，仅供数据结构设计参考，详细可参考 联付通OpenAPi-订单-删除预支付单接口

|字段|含义|
|-----|-----|
|id|主键|
|order_id|订单id|
|order_type|订单类型`create`,`update`,`end`|
|create_time|订单创建时间|
|update_time|订单更新时间|
|total_amount|订单总金额|
> 支付完成的 订单的 order_type = end

##### 2.6.4 异常说明
- 无

### 2.7 s7 用户修改
##### 2.7.1 步骤说明
用户订单发生修改，如加菜减菜，或者收银台改价等情况
##### 2.7.2 用例说明
|用例名称|用户加菜/减菜|
|-------|
|行为角色|门店顾客|
|需求目的|完成对订单菜品的修改|
|前置条件|确认菜品|
|后置条件|通过收银台完成订单修改操作|

|用例名称|价格变更|
|-------|
|行为角色|门店服务人员|
|需求目的|完成对订单价格的修改|
|前置条件|订单参与店铺的活动，或者抹零等|
|后置条件|完成对订单的修改|

##### 2.7.3 数据流转
- 无

##### 2.7.4 异常说明
- 无

### 2.8 s8 修改订单
##### 2.8.1 步骤说明
订单发生变更，收银软件会修改数据库的订单数据，或订单明细数据
##### 2.8.2 用例说明
|用例名称|修改订单|
|-------|
|行为角色|收银软件|
|需求目的|完成数据库的数据修改|
|前置条件|用户修改订单，或收银员修改价格|
|后置条件|数据库数据修改成功|
##### 2.2.3 数据流转
- 无

##### 2.2.4 异常说明
- 无

### 2.9 s9 Update触发器
##### 2.9.1 步骤说明
通过触发器来监控收银软件的订单变化，并通过Update触发器来监控订单数据，订单明细的变化，并同步到xjl_order订单库，实现对订单变化的实时监控
##### 2.9.2 用例说明
|用例名称|Update触发器|
|-------|
|行为角色|数据库|
|需求目的|监控订单变更|
|前置条件|订单变更成功|
|后置条件|把变更订的状态同步到xjl_order数据库|

|用例名称|Update触发器|
|-------|
|行为角色|数据库|
|需求目的|监控订单明细变更|
|前置条件|订单变更成功|
|后置条件|把明细变的更订的同步到xjl_order数据库|
##### 2.9.3 数据流转
本步骤是利用触发器的原理实现了数据的实时获取
>下面是 xjl_order 表所必须的业务类字段，仅供数据结构设计参考，详细可参考 联付通OpenAPi-订单-更新预支付单接口

|字段|含义|
|-----|-----|
|id|主键|
|order_id|订单id|
|order_type|订单类型`create`,`update`,`end`|
|create_time|订单创建时间|
|update_time|订单更新时间|
|total_amount|订单总金额|
> 加菜减菜，修改价格的 订单的 order_type = update

##### 2.9.4 异常说明
- 无

### 2.10 s10 小精灵服务台轮训数据
##### 2.10.1 步骤说明
小精灵服务台定时每1秒轮训一次xjl_order表，并查询所有数据
##### 2.10.2 用例说明
|用例名称|小精灵服务台轮训订单|
|-------|
|行为角色|小精灵服务台|
|需求目的|实现对xjl_order表的实时监控|
|前置条件|小精灵服务台正常运行|
|后置条件|获取订单数据 即S11|
##### 2.10.3 数据流转
本步骤是利用触发器的原理实现了数据的实时获取
>下面是 xjl_order 表所必须的业务类字段，仅供数据结构设计参考，详细可参考 联付通OpenAPi-订单-更新预支付单接口

|字段|含义|
|-----|-----|
|id|主键|
|order_id|订单id|
|order_type|订单类型`create`,`update`,`end`|
|create_time|订单创建时间|
|update_time|订单更新时间|
|total_amount|订单总金额|
> 加菜减菜，修改价格的 订单的 order_type = update

##### 2.10.4 异常说明
- 无

### 2.11 s12 s19 s26 小精灵服务台筛选订单
##### 2.10.1 步骤说明
小精灵服务台获取到订单后，要更加新增，修改，支付的顺序来分别处理订单，这一步完成订单的筛选工作，可以根据xjl_order表的order_type字段来筛选
##### 2.10.2 用例说明
|用例名称|小精灵服务台筛选订单|
|-------|
|行为角色|小精灵服务台|
|需求目的|完成对订单的筛选|
|前置条件|获取订单成功|
|后置条件|完成订单筛选|
##### 2.10.3 数据流转
- 无
##### 2.10.4 异常说明
- 无

### 2.12 s13 s20 获取订单明细
##### 2.12.1 步骤说明
小精灵服务台获取到订单后，在创建和更新两个环节，需要获取到订单明细
##### 2.12.2 用例说明
|用例名称|小精灵服务台获取订单明细|
|-------|
|行为角色|小精灵服务台|
|需求目的|完成订单明细获取|
|前置条件|获取订单成功|
|后置条件|完成订单明细获取 即 S14 S21|
##### 2.12.3 数据流转
- 无
##### 2.12.4 异常说明
- 无

### 2.13 s15 s22 s27 请求预付单API
##### 2.13.1 步骤说明
s15
>小精灵服务台遍历状态为create的订单，同时获取订单明细即s13-14，并请求联付通OpenApi 创建预支付单API。

s22
>小精灵服务台遍历状态为update的订单，同时获取订单明细即s13-14，并请求联付通OpenApi 更新预支付单API。

s27
>小精灵服务台遍历状态为end的订单，并请求联付通OpenApi 删除预支付单API。

##### 2.13.2 用例说明
|用例名称|小精灵服务台请求API|
|-------|
|行为角色|小精灵服务台|
|需求目的|完成接口请求|
|前置条件|获取订单和明细成功|
|后置条件|完成对预支付单API的请求，即s17 s24 s30|

##### 2.12.3 数据流转
- 无
##### 2.12.4 异常说明
- 无


### 2.13 s18 s25 s31 删除xjl_order订单数据
##### 2.13.1 步骤说明
根据s15 s22 s27 请求API返回的order_id，来删除xjl_order订单表里的指定数据。

