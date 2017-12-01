### 接口描述
通过`原订单id`来查询订单状态
### 请求地址
> http(s)://api.huishouyin.cn/order/list

### 请求方式
`POST`
### 请求参数
|参数|类型|必填|最大长度|描述|
|-----|-----|-----|-----|-----|
|app_id|String|是|32|应用ID|
|sign|String|是|32|签名 [签名规则](/main/sign)|
|sign_type|String|是|32|签名加密类型 `MD5` `RSA`|
|start_time|int|否|11|开始时间，时间戳|
|end_time|int|否|11|结束时间，时间戳|
|pay_channel|int|否|11|渠道信息 `10` 全部 `0`微信 `1`支付宝 默认`10`|
|paid|int|是|1|是否付款成功 `10` 全部 `0`否 `1`是 默认`10`|
|refunded|int|是|1|是否有退款信息 无论退款是否成功 `10` 全部 `0`否 `1`是 默认`10`|
|page_limit|int|否|11|翻页每页条数,`<100` 默认`20`|
|page_num|int|否|11|翻页当前页数，`>=0`则翻页返回，`-1`忽略翻页信息 返回全部结果(时间跨度不得大于`24`小时)|
|return_type|int|否|128|返回格式 `0` json `1` txt `2` execl 默认`0`|
### 请求事例
>请求日对账单事例 返回execl

```javascript
{
    app_id:'app_id',
    sign:'L4XYdVQWe0DROIQBxxtrYKWawTIrXofe',
    sign_type:'MD5',
    start_time:1506787200,
    end_time:1506873600,
    paid:10,
    refunded:1,
    order_status:10,
    page_num:-1,
    return_type:2,
}
```
### 响应参数
|参数|类型|必填|最大长度|描述|
|-----|-----|-----|-----|-----|
|status|int|是|11|1000 请求成功 |
|msg|String|是|128|应用ID|
|total_num|int|是|11|总条数|
|page_limit|int|否|1|每页条数|
|page_num|int|是|1|当前页数|
|order_list|Array|是|1|订单列表|

##### order_list 结构
|参数|类型|必填|最大长度|描述|
|-----|-----|-----|-----|-----|
|app_id|String|是|32|订单所属app|
|trade_no|String|是|64|联富通交易流水号|
|order_id|String|是|64|原支付业务单号|
|order_status|String|是|32|订单状态 `1` 已支付 `2` 全部退款 `3`部分退款 `4` 已关闭 `5` 已撤销`0` 支付中`-1`支付失败 `-2`退款失败 `-10`未知 |
|pay_channel|int|否|11|渠道信息 `0`微信 `1`支付宝|
|create_time|Date|是|1|订单创建时间 `2014-11-27 15:45:57`|
|pay_time|Date|是|1|支付时间 `2014-11-27 15:45:57`|
|refund_time|Date|是|1|退款时间 `2014-11-27 15:45:57`|
|update_time|Date|是|1|最后更新时间 `2014-11-27 15:45:57`|
|total_amount|double|是|-|订单总金额|
|payable_amount|double|是|-|应付金额，联富通会员系统的优惠券会产生优惠|
|real_amount|String|是| - |实际支付金额|
|refund_amount|String|是| - |实际退款金额|
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

### 响应事例
```javascript
{
    code:1000,
    msg:'查询成功',
    data:{
        total_num:1000,
        page_num:-1,
        order_list:[
            {
                trade_no:'2017102100151091',
                order_id:'2017102100151091',
                app_id:'L4XYdVQWe0DROIQBxxtrYKWawTIrXofe',
                order_status:1,
                pay_channel:1,
                create_time:'2014-11-27 15:45:57',
                pay_time:'2014-11-27 15:45:57',
                refund_time:'2014-11-27 15:45:57',
                update_time:'2014-11-27 15:45:57',
                total_amount:1,
                payable_amount:1,
                real_amount:1,
                refund_amount:1,        
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
        ]
        
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