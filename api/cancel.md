### 接口描述
支付交易返回`失败`或`支付系统超时`，调用该接口撤销交易。如果此订单用户支付失败，系统会将此订单关闭；如果用户支付`成功`，系统会将此订单资金退还给用户。 

!>注意：只有发生`支付系统超`时或者支付结果`未知`时可调用撤销，其他正常支付的单如需实现相同功能请调用申请退款API。提交支付交易后调用`交易状态`，没有明确的支付结果再调用`交易撤销`。
### 请求地址
> http(s)://api.huishouyin.cn/pay/cancel

### 时序图

>付款码支付

![](api/media/chexiao1.png)

>扫码支付/H5易支付

![](api/media/chexiao2.png)

### 请求方式
`POST`
### 请求参数
|参数|类型|必填|最大长度|描述|
|-----|-----|-----|-----|-----|
|app_id|String|是|32|应用ID|
|sign|String|是|32|签名`MD5(app_id=value&app_sercet=value&order_id=value&refund_amount=value)`|
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
|`1005`|订单已经撤销|
### 异常响应事例
```javascript
{
    code:1005,
    msg:'订单已经撤销',
    data:{
        
    }
}
```