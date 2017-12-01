## 自行实现签名
>如果未使用联富通开放平台SDK，需要自行实现签名过程。

### 如何签名？

### 1.筛选并排序

获取所有请求参数，不包括`字节类`型参数，如文件、字节流，剔除`sign`字段，剔除值为`空`的参数，并按照第一个字符的键值`ASCII`码递增排序（字母升序排序），如果遇到相同字符则按照第二个字符的键值ASCII码递增排序，以此类推。

### 2.拼接

将排序后的参数与其对应值，组合成“参数=参数值”的格式，并且把这些参数用&字符连接起来，此时生成的字符串为待签名字符串。

例如下面的请求示例，参数值都是示例，开发者参考格式即可：

```javascript
    app_id:'bT2CAkZUgoOr36BnZhuC1aTvXgxhvmhF',
    sign:'L4XYdVQWe0DROIQBxxtrYKWawTIrXofe',
    order_id:'2017102100151091',
    total_amount:11.00, 
    store_info:{
        store_id:'L4XYdVQWe0DROIQBxxtrYKWawTIrXofe',
        cashier_id:'5CDJVuPZ89l8hANqsJiU8zWDQ9rUATmg',
        terminal_id:'bT2CAkZUgoOr36BnZhuC1aTvXgxhvmhF',
    },
    goods_list:[
        {
            barcode:'6983748939221',
            title:'可口可乐300ml',
            num:2,
            price:3.00
        }
    ]
```
!> 注意在生成代签名字符串的时候，要把`app_sercet`加入其中


则待签名字符串为：
```javascript
    app_id=bT2CAkZUgoOr36BnZhuC1aTvXgxhvmhF&app_sercet=bT2CAkZUgoOr36BnZhuC1aTvXgxhvmhF&goods_list=[{barcode:'6983748939221',title:'可口可乐300ml',num:2,price:3.00}]&order_id=2017102100151091&store_info={store_id:'L4XYdVQWe0DROIQBxxtrYKWawTIrXofe',cashier_id:'5CDJVuPZ89l8hANqsJiU8zWDQ9rUATmg',terminal_id="bT2CAkZUgoOr36BnZhuC1aTvXgxhvmhF"}&total_amount=11.00
```
### 3.签名生成
##### 3.1MD5 加密签名
把生成的`待签名字符串`使用MD5进行加密（大写），结果如下
```
90C04D45B9BA45D098303D8176C38ABC
```
然后对其进行Base64转码
```
OTBDMDRENDVCOUJBNDVEMDk4MzAzRDgxNzZDMzhBQkM=
```

##### 3.2RSA 加密签名
!> 公私密钥加密 二期公测

### 4.把生成的签名赋值给sign参数，拼接到请求参数中。