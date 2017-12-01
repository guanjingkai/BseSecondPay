### 接口描述
通过`店铺ID`来查询进件状态

### 请求地址
> http(s)://api.huishouyin.cn/register/check

### 请求方式
`POST`
### 请求参数
|参数|类型|必填|最大长度|描述|
|-----|-----|-----|-----|-----|
|app_id|String|是|32|应用ID|
|sign|String|是|32|签名 [签名规则](/main/sign)|
|sign_type|String|是|32|签名加密类型 `MD5` `RSA`|
|register_no|String|否|64|进件流水号|

### 请求事例
```javascript
{
    app_id:'bT2CAkZUgoOr36BnZhuC1aTvXgxhvmhF',
    sign:'L4XYdVQWe0DROIQBxxtrYKWawTIrXofe',
    sign_type:'MD5',
    register_no:'2017102100151091',
}
```
### 响应参数
|参数|类型|必填|最大长度|描述|
|-----|-----|-----|-----|-----|
|status|int|是|1|1000 请求成功 |
|msg|String|是|1|返回消息|
|register_type|String|是|64|进件状态 `1` 审核成功 `2` 进件失败 `0` 审核中 `-1` 进件失败 |
|register_no|String|是|64|进件流水号`唯一`|
|app_id|String|是|32|该门店(应用的)AppID|
|app_sercet|String|是|32|该门店(应用的)AppSercet|
|alipay_rate|num|否|9.2|支付宝费率|
|wechat_rate|num|否|9.2|微信费率|
### 响应事例
```javascript
{
    code:1000,
    msg:'查询成功',
    data:{
        register_type:1
        register_no:'5CDJVuPZ89l8hANqsJiU8zWDQ9rUATmg',
        app_id:'L4XYdVQWe0DROIQBxxtrYKWawTIrXofe',
        app_sercet:'HUpLsX7XQWFH3iktwFFMmi1GNdKH7Ef3',
        alipay_rate:'2.5',
        wechat_rate:'2.5',
    }
}
```
### 异常响应
|名称|描述|
|-----|-----|
|`6004`|店铺ID不存在|
### 异常响应事例
```javascript
{
    code:6004,
    msg:'店铺ID不存在',
    data:{
        
    }
}
```