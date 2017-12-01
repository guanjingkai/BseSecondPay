### 接口描述
通过`原订单id`来查询订单状态
### 请求地址
> http(s)://api.huishouyin.cn/pay/check

### 请求方式
`POST`
### 请求参数
|参数|类型|必填|最大长度|描述|
|-----|-----|-----|-----|-----|
|app_id|String|是|32|应用ID|
|sign|String|是|32|签名 [签名规则](/main/sign)|
|sign_type|String|是|32|签名加密类型 `MD5` `RSA`|
|order_id|String|否|64|原支付业务单号|
|refund_order_id|String|否|64|退款单号|
|trade_no|String|否|64|联富通交易流水号|

!> (order_id 或 refund_order_id)  与 trade_no 至少有一个不为空

### 请求事例
```javascript
{
    app_id:'bT2CAkZUgoOr36BnZhuC1aTvXgxhvmhF',
    sign:'L4XYdVQWe0DROIQBxxtrYKWawTIrXofe',
    sign_type:'MD5',
    order_id:'2017102100151091',
}
```
### 响应参数
|参数|类型|必填|最大长度|描述|
|-----|-----|-----|-----|-----|
|status|int|是|1|1000 请求成功 |
|msg|String|是|1|返回消息|
|trade_no|String|是|64|联富通交易流水号|
|check_time|Date|是|32|检测时间 `2014-11-27 15:45:57`|
|order_id|String|是|128|原支付业务单号|
|order_status|String|是|32|订单状态 `1` 已支付 `2` 全部退款 `3`部分退款 `4` 已关闭 `5` 已撤销`0` 支付中`-1`支付失败 `-2`退款失败  `-3` 退款中 `-10`未知 |
### 响应事例
```javascript
{
    code:1000,
    msg:'查询成功',
    data:{
        trade_no:'2017102100151091',
        check_time:'2014-11-27 15:45:57',
        order_id:'2017102100151091',
        order_status:1
    }
}
```
### 异常响应
|名称|描述|
|-----|-----|
|`4001`|原订单不存在定|
### 异常响应事例
```javascript
{
    code:4001,
    msg:'原订单不存在',
    data:{
        
    }
}
```