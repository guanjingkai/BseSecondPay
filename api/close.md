### 接口描述
用于交易创建后，用户在一定时间内`未进行支付`，可调用该接口直接将未付款的交易进行关闭。
### 请求地址
> http(s)://api.huishouyin.cn/pay/close

### 请求方式
`POST`
### 请求参数
|参数|类型|必填|最大长度|描述|
|-----|-----|-----|-----|-----|
|app_id|String|是|32|应用ID|
|sign|String|是|32|签名 详细见 [签名规则](/main/sign)|
|order_id|String|是|128|原支付业务单号|
|store_info|object|否| - |店铺信息预留域|

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
    order_id:'2017102100151091',
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
|status|int|是|1|1000关闭成功 |
|msg|String|是|1|返回信息|
|order_id|String|是|128|原支付业务单号|
### 响应事例
```javascript
{
    code:1000,
    msg:'关闭成功',
    data:{
        order_id:'2017102100151091'
    }
}
```
### 异常响应
|名称|描述|
|-----|-----|
|`1004`|订单已经关闭|
### 异常响应事例
```javascript
{
    code:1004,
    msg:'订单已经关闭',
    data:{
        
    }
}
```