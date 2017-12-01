### 接口描述
主要用于商家`主动`扫描/输入用户`付款码`完成收款的场景
### 时序图
![](api/media/fukuanma.png)
### 流程图
![](api/media/fukuanliucheng.jpg)
### 请求地址
> http(s)://api.huishouyin.cn/pay/qrcode

### 请求方式
`POST`
### 请求参数
|参数|类型|必填|最大长度|描述|
|-----|-----|-----|-----|-----|
|app_id|String|是|32|应用ID|
|sign|String|是|32|签名 [签名规则](/main/sign)|
|sign_type|String|是|32|签名加密类型 `MD5` `RSA`|
|order_id|String|是|128|业务单号|
|pay_code|String|是| - |微信或支付宝付款码|
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
    "app_id": "bT2CAkZUgoOr36BnZhuC1aTvXgxhvmhF",
    "sign": "L4XYdVQWe0DROIQBxxtrYKWawTIrXofe",
    "sign_type": "MD5",
    "order_id": "2017102100151091",
    "pay_code": "5CDJVuPZ89l8hANqsJiU8zWDQ9rUATmg",
    "total_amount": 11.00,
    "store_info": {
        "store_id": "L4XYdVQWe0DROIQBxxtrYKWawTIrXofe",
        "cashier_id": "5CDJVuPZ89l8hANqsJiU8zWDQ9rUATmg",
        "waiter1_id": "HUpLsX7XQWFH3iktwFFMmi1GNdKH7Ef3",
        "waiter2_id": "L4XYdVQWe0DROIQBxxtrYKWawTIrXofe",
        "terminal_id": "bT2CAkZUgoOr36BnZhuC1aTvXgxhvmhF"
    },
    "goods_list": [
        {
            "barcode": "6983748939221",
            "title": "可口可乐300ml",
            "num": 2,
            "price": 3.00
        }
    ]
}
```
### 响应参数
|参数|类型|必填|最大长度|描述|
|-----|-----|-----|-----|-----|
|status|int|是|11|支付状态 `1000`成功|
|msg|String|是|128|返回消息|
|trade_no|String|是|64|联富通交易流水号|
|order_id|String|是|64|原业务单号|
|pay_type|String|是|-| `0`微信 `1`支付宝|
|order_status|String|是|32|订单状态 `1` 已支付 `2` 全部退款 `3`部分退款 `4` 已关闭 `5` 已撤销`0` 支付中`-1`支付失败 `-2`退款失败  `-3` 退款中 `-10`未知 |
|total_amount|double|是|-|订单总金额|
|payable_amount|double|是|-|应付金额，联富通会员系统的优惠券会产生优惠|
|voucher_list|Array|是| - |微信或支付宝交易优惠券信息，按照第三方原路返回|
|real_amount|double|是|-|实付金额|
|voucher_list|Array|是| - |优惠信息|
##### voucher_list 结构 支付宝情况
|参数|类型|必填|最大长度|描述|
|-----|-----|-----|-----|-----|
|id|String|是| 32 |券id `	2015102600073002039000002D5O`|
|name|String|是| 64 |券名称 `XX超市5折优惠`|
|activity_id|String|`alipay` 空 `weixin` 是| 32 |活动id `	2015102600073002039000002D5O`|
|scope|String|是| 32 |当前有三种类型： `1` - 全场代金券 `2` - 折扣券 `3`- 单品优惠 |
|type|String|`alipay` 空 `weixin` 是| 32 | `COUPON` - 代金券 `DISCOUNT` - 优惠券|
|amount|double|是| - |优惠券面额，它应该会等于商家出资加上其他出资方出资 `10.00`|
|merchant_contribute|double|是| 9.2 |商家出资（特指发起交易的商家出资金额）|
|other_contribute|double|否| 9.2 |其他出资方出资金额，可能是支付宝，可能是品牌商，或者其他方，也可能是他们的一起出资|
|purchase_ant_contribute|double|`alipay` 是 `weixin` 空|9.2 |如果使用的这张券是用户购买的，则该字段代表用户在购买这张券时平台优惠的金额|

>!COUPON- 代金券，需要走结算资金的充值型代金券,（境外商户券币种与支付币种一致） DISCOUNT- 优惠券，不走结算资金的免充值型优惠券，（境外商户券币种与标价币种一致



!> 如果未支付成功  real_amount 返回 `0` 

### 响应事例
```javascript
{
    "code":1000,
    "msg":"支付成功",
    "data":{
        "trade_no":"2017102100151091",
        "order_id":"2017102100151091",
        "pay_type":1,
        "order_status":1,
        "total_amount":11.0,
        "payable_amount":10.0,
        "real_amount":9.0,
        "voucher_list":[{
                "id": "2015102600073002039000002D5O",
                "name": "XX超市5折优惠",
                "type": "1",
                "amount": 10,
                "merchant_contribute": 9,
                "other_contribute": 1,
                "purchase_ant_contribute": 0.82
        }]
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
    msg:"签名错误",
    data:{
        
    }
}
```