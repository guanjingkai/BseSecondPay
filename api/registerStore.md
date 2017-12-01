### 接口描述
普通/子商户创建并进件，进件资料需要联富通审核
### 请求地址
> http(s)://api.huishouyin.cn/register/store

### 请求参数

|参数|类型|必填|最大长度|描述|
|-----|-----|-----|-----|-----|
|app_id|String|是|32|服务商ID|
|sign|String|是|32|签名 [签名规则](/main/sign)|
|sign_type|String|是|32|签名加密类型 `MD5` `RSA`|
|group_id|String|集团调用否|32|集团(核心商户)ID，门店所属集团(核心商户),若传0则使用默认集团ID，集团商户调用本API不需要传本字段|
|register_no|String|是|64|进件流水号，保持`唯一`|
|register_info|object|是| - |进件信息|
|pay_set|object|是| - |支付配置|
|settlement_info|object|是| - |结算商户信息|

##### register_info 结构
|参数|类型|必填|最大长度|描述|
|-----|-----|-----|-----|-----|
|full_name|String|是|64|门店全名|
|name|String|是|64|门店简称|
|country_id|num|是|64|国家ID|
|province_id|num|是|64|省份ID 详细见 [附录-省市区编码](file/area)|
|city_id|num|是|64|城市ID 详细见 [附录-省市区编码](file/area)|
|area_id|num|是|64|区域ID 详细见 [附录-省市区编码](file/area)|
|trade_type|num|是|64|经营类目，传三级编号 详细见 [附录-经营类目](file/tradeType)|
|contact_type|num|是|1|联系人类型 `1` 法人 `2` 实际控制人 `3` 代理人 `4` 其他|
|contact_name|String|是|32|联系人姓名|
|contact_ID|String|是|32|联系人身份证号码|
|contact_phone|String|否|64|联系人电话|
|contact_mobile|String|是|64|联系人手机|
|contact_email|String|否|64|联系人邮箱|
|business_license_type|num|是|1|门店营业执照类型 `1` 营业执照 `2` 营业执照(多证合一) `3` 事业单位法人证书 |
|business_license_no|String|是|64|营业执照编号|
|business_license_img|String|是| - |营业执照图片|
|legal_person_name|String|是|32|法人姓名|
|legal_person_ID|String|是|32|法人身份证号码|
|legal_person_ID_a|String|是| - |法人身份证正面|
|legal_person_ID_b|String|是| - |法人身份证背面|
|remark|String|否|64|备注|
##### pay_set 结构
|参数|类型|必填|最大长度|描述|
|-----|-----|-----|-----|-----|
|alipay_rate|num|否|9.2|支付宝支付费率 单位 ‰|
|wechat_rate|num|否|9.2|微信支付费率 单位 ‰|
!> `alipay_rate` 与 `wechat_rate` 不可同时为空,具体数值参考联富通与服务商合同
##### settlement_info 结构
|参数|类型|必填|最大长度|描述|
|-----|-----|-----|-----|-----|
|bank|num|是|11|开户行联行号 详细见 [附录-银行联行号](file/brandID)|
|card_num|String|是|32|银行卡号|
|account_type|num|是|1|账户类型 `1` 个人 `2` 企业|
|account_holder|String|是|32|开户人名称|
### 请求事例
```javascript
{
    app_id:'5CDJVuPZ89l8hANqsJiU8zWDQ9rUATmg',
    sign:'5CDJVuPZ89l8hANqsJiU8zWDQ9rUATmg',
    sign_type:'MD5',
    group_id:'5CDJVuPZ89l8hANqsJiU8zWDQ9rUATmg',
    register_no:'5CDJVuPZ89l8hANqsJiU8zWDQ9rUATmg',
    store_info:{
        store_full_name:'北京够百特静安有限公司',
        store_name:'够百特静安店铺',
        country_id:'86',
        province_id:'100',
        city_id:'10010',
        area_id:'1001010',
        trade_type:'223',
        contact_type:'1',
        contact_name:'雷丘',
        contact_ID:'210281199201091234',
        business_license_type:'1',
        business_license_no:'1878thjirhs0f9041415',
        business_license_img:'http://www.qiniu.com/b.png',
        legal_person_name:'雷丘',
        legal_person_ID:'210281199201091234',
        legal_person_ID_a:'http://www.qiniu.com/b.png',
        legal_person_ID_b:'http://www.qiniu.com/b.png',
    },
    pay_set:{
        alipay_rate:2.5，
        wechat_rate：2.5
    },
    settlement_info:{
        bank:'102100099996',
        card_num:'6222345778878556646',
        account_type:1,
        account_holder:'雷丘',
    }
}
```
### 响应参数

|参数|类型|必填|最大长度|描述|
|-----|-----|-----|-----|-----|
|status|int|是|1|进件状态 `1000`成功|
|msg|String|是|1|返回消息|进件成功|
|register_no|String|是|64|进件流水号，保持`唯一`|
|app_id|String|是|32|该门店(应用的)AppID|
|app_sercet|String|是|32|该门店(应用的)AppSercet|
|alipay_rate|num|否|9.2|支付宝费率|
|wechat_rate|num|否|9.2|微信费率|
### 响应事例
```javascript
{
    code:1000,
    msg:'进件成功',
    data:{
        register_no:'5CDJVuPZ89l8hANqsJiU8zWDQ9rUATmg',
        app_id:'L4XYdVQWe0DROIQBxxtrYKWawTIrXofe',
        app_sercet:'HUpLsX7XQWFH3iktwFFMmi1GNdKH7Ef3',
        alipay_rate:'2.5',
        wechat_rate:'2.5',
    }
}
```
### 异常响应事例
```javascript
{
    code:6001,
    msg:'店铺编号重复',
    data:{
        store_id:'5CDJVuPZ89l8hANqsJiU8zWDQ9rUATmg'
    }
}
```
### 异常值
|名称|描述|解决方法|
|-----|-----|-----|
|`6000`|进件失败|重新进件|
|`6001`|进件流水号|更新进件流水号|
|`6002`|集团不存在|检测集团ID|
|`6003`|进件中|调用进件状态查询接口|
