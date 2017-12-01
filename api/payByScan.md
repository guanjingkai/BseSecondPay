### 接口描述
主要用于商家`主动`展示付款码，用户通过`扫一扫`完成付款的场景
### 时序图
![](api/media/scan.png)
### 请求地址
> http(s)://api.huishouyin.cn/pay/scan

### 请求方式
`POST`
### 请求参数
|参数|类型|必填|最大长度|描述|
|-----|-----|-----|-----|-----|
|app_id|String|是|32|应用ID|
|sign|String|是|32|签名 [签名规则](/main/sign)|
|sign_type|String|是|32|签名加密类型 `MD5` `RSA`|
|order_id|String|是|128|业务单号|
|total_amount|String|是| - |订单总金额|
|store_info|object|否| - |店铺信息预留域|
|goods_list|Array|否||商品列表|

##### store_info 结构
|参数|类型|必填|最大长度|描述|
|-----|-----|-----|-----|-----|
|store_id|String|否| - |门店id|
|cashier_id|String|否| - |收银员id|
|waiter1_id|String|否| - |业务员1id|
|waiter2_id|String|否| - |业务员2id|
|terminal_id|String|否| - |终端id|

##### goods_list 结构
|参数|类型|必填|最大长度|描述|
|-----|-----|-----|-----|-----|
|barcode|String|否|32|国际条码|
|title|String|否|256|商品名称|
|num|int|否|32|商品数量|
|price|double|否| - |单价签名|
### 请求事例
```javascript
{
    app_id:'bT2CAkZUgoOr36BnZhuC1aTvXgxhvmhF',
    sign:'L4XYdVQWe0DROIQBxxtrYKWawTIrXofe',
    sign_type:'MD5',
    order_id:'2017102100151091',
    total_amount:11.00, 
    store_info:{
        store_id:'L4XYdVQWe0DROIQBxxtrYKWawTIrXofe',
        cashier_id:'5CDJVuPZ89l8hANqsJiU8zWDQ9rUATmg',
        waiter1_id:'HUpLsX7XQWFH3iktwFFMmi1GNdKH7Ef3',
        waiter2_id:'L4XYdVQWe0DROIQBxxtrYKWawTIrXofe',
        terminal_id:'bT2CAkZUgoOr36BnZhuC1aTvXgxhvmhF',
    },
    goods_list:[
        {
            barcode:'6983748939221',
            title:'可口可乐300ml',
            num:2,
            price:3.00
        },{
            barcode:'6987483920018',
            title:'康师傅big香辣牛肉面',
            num:1,
            price:5.00
        }
    ]
    
}
```
### 响应参数
|参数|类型|必填|最大长度|描述|
|-----|-----|-----|-----|-----|
|status|int|是|1|支付状态 `1000`成功|
|msg|String|是|1|返回消息|
|trade_no|String|是|64|联富通交易流水号|
|order_id|String|是|32|原业务单号|
|total_amount|double|是|-|订单总金额|
|payable_amount|double|是|-|应付金额，联富通会员系统的优惠券会产生优惠|
|pay_url|double|是|-|支付连接|
### 响应事例
```javascript
{
    code:1000,
    msg:'成功',
    data:{
        trade_no:'2017102100151091',
        order_id:'2017102100151091',
        total_amount:11.0,
        payable_amount:11.0
        pay_url:'http://www.liantuo.com/xxx/xxx/xxx'
    }
}
```
### 异常响应
|名称|描述|
|-----|-----|
|`2000`|签名错误|
|`3000`|APPID错误|
|`1003`|订单已支付|
### 异常响应事例
```javascript
{
    code:2000,
    msg:'签名错误',
    data:{
        
    }
}
```