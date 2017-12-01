### 接口描述
主要用于商家`主动`扫描/输入用户`付款码`完成收款的场景
### 时序图
![](api/media/refund.png)
### 请求地址
> http(s)://api.huishouyin.cn/pay/refund

### 请求方式
`POST`
### 请求参数
|参数|类型|必填|最大长度|描述|
|-----|-----|-----|-----|-----|
|app_id|String|是|32|应用ID|
|sign|String|是|32|签名 [签名规则](/main/sign)|
|sign_type|String|是|32|签名加密类型 `MD5` `RSA`|
|order_id|String|否|64|原支付业务单号|
|refund_order_id|String|否|64|退款业务单号|
|trade_no|String|否|128|联富通交易流水号|
|refund_amount|String|是| - |实际退款金额，如传`0`则代表全额退款，退款金额不得大于实际支付金额|
|store_info|object|否| - |店铺信息预留域|

!> order_id 与 trade_no 至少有一个不为空

!> order_id refund_order_id 需要保证`全局唯一`，开发者可以才用业务单号+随机变量等形式来避免重复

##### store_info 结构
|参数|类型|必填|最大长度|描述|
|-----|-----|-----|-----|-----|
|store_id|String|否| - |门店id|
|cashier_id|String|否| - |收银员id|
|terminal_id|String|否| - |终端id|
### 请求事例
```javascript
{
    app_id:'bT2CAkZUgoOr36BnZhuC1aTvXgxhvmhF',
    sign:'L4XYdVQWe0DROIQBxxtrYKWawTIrXofe',
    sign_type:'MD5',
    order_id:'2017102100151091',
    refund_amount:11.00，
    store_info:{
        store_id:'L4XYdVQWe0DROIQBxxtrYKWawTIrXofe',
        cashier_id:'5CDJVuPZ89l8hANqsJiU8zWDQ9rUATmg',
        terminal_id:'bT2CAkZUgoOr36BnZhuC1aTvXgxhvmhF',
    }
}
```
### 响应参数
|参数|类型|必填|最大长度|描述|
|-----|-----|-----|-----|-----|
|status|int|是|11|退款状态1000退款成功 |
|msg|String|是|128|返回消息|
|trade_no|String|是|128|联富通交易流水号|
|refund_amount|String|是|11|退款金额 `88.88`|
|refund_time|Date|是|32|退款时间 `2014-11-27 15:45:57`|
|order_id|String|是|128|原支付业务单号|
|refund_order_id|String|否|32|退款业务单号|
### 响应事例
```javascript
{
    code:1000,
    msg:'退款成功',
    data:{
        trade_no:'2017102100151091',
        refund_amount:'88.88',
        refund_time:'2014-11-27 15:45:57',
        order_id:'2017102100151091',
        refund_order_id:'2017102100151091'
    }
}
```
### 异常响应
|名称|描述|
|-----|-----|
|2001|退款金额大于实际金额|
### 异常响应事例
```javascript
{
    code:'2001',
    msg:'退款金额大于实际金额',
    data:{
        
    }
}
```