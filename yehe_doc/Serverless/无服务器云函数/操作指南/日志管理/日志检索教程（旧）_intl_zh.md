
>?云函数 SCF 于2021年01月29日起全量接入腾讯云 [日志服务 CLS](https://intl.cloud.tencent.com/document/product/614)，在此之后创建的函数调用日志将默认投递至 CLS，且支持日志实时输出。若您的函数于2021年01月29日前创建，且需进行日志检索，请参考本文档使用该功能。






云函数查询中的“高级检索”功能支持关键词搜索，您可以使用查询语法组合关键词进行检索。

## 查询语法

检索支持以下查询语法：

| 语法      | 语义                                                         |
| --------- | ------------------------------------------------------------ |
| key:value | 键值搜索格式。其中 value 支持 `?`、`*` 模糊搜索，若 key 或 value 中包含空格、冒号等关键字符，则需用引号包括。目前已支持的 key 列表请参见 [预置 key](#key)。 |
| AND       | 与逻辑操作符，例如 `SCF_RequestId:85a82ecf-xxx AND SCF_Duration:1`。 |
| OR        | 或逻辑操作符，例如 `SCF_RequestId:85a82ecf-xxx OR SCF_Duration:1`。 |
| NOT       | 非逻辑操作符，例如 `SCF_RequestId:85a82ecf-xxx NOT SCF_Duration:1`。 |
| TO        | 范围逻辑操作符，例如 `SCF_Duration:[0.1 TO 1.0]`。          |
| 'a'       | 字符 a 将被视为普通字符，不会作为语法关键词处理。            |
| "A"       | A 中的所有关键词都将被视为普通字符，不会作为语法关键词处理。 |
| \         | 转义符号，转义后的字符表示符号本身，例如 `url:\/images\/favicon.ico"`。 |
| *         | 通配符查询，匹配零个、单个、多个字符，例如 `host:www.test*.com`。 |
| ?         | 通配符查询，匹配单个字符，例如 `host:www.te?t.com`。         |
| :>        | 范围操作符，针对数值类型的字段，表示大于某个数值，例如 `SCF_Duration:>1`。 |
| :>=       | 范围操作符，针对数值类型的字段，表示大于等于某个数值，例如 `SCF_Duration:>=1`。 |
| :<        | 范围操作符，针对数值类型的字段，表示小于某个数值，例如 `SCF_Duration:<1`。 |
| :<=       | 范围操作符，针对数值类型的字段，表示小于等于某个数值，例如 `SCF_Duration:<=1`。 |
| :        | 冒号，表示作用于的 key 字段，即键值检索，例如 `SCF_RequestId:85a82ecf-xxx` 或 `SCF_Duration:1`。 |



>!
>- 语法操作符区分大小写。例如 AND、OR 表示检索逻辑运算符，而 and、or 视为普通词组。
>- 多个检索语句用空格连接时，视为“或”逻辑，例如 `warning error` 表示包含 `warning` 或 `error` 关键字的结果。
>- 语法中的字符均为保留字符，若检索关键字中包含这些语法保留字符，均需要转义。
>- 使用键值检索时（形如 key：value），键名（key）必须在 [已支持的 key 列表](#key) 中。


<span id="key"></span>
## 预置 key

| Key           | 类型   | 含义           | 查询示例          |
| ------------- | ------ | -------------- | ----------------- |
| SCF_RequestId | text   | 请求 ID        | SCF_RequestId:123 |
| SCF_Duration  | double | 运行时间（ms） | SCF_Duration:>20  |



## 示例

- 查询包含关键词 error 或者 fail 的日志：
```
error OR fail
```

- 查询指定请求里包含 error 关键词的日志：
```
SCF_RequestId:123 AND error
```

- 查询运行时间大于 20 ms 且包含 error 关键词的日志：
```
SCF_Duration:>20 AND error
```




>?如果需要对请求日志进行去重，可以检索 “Report RequestId”。例如，想查看运行时间大于 20 ms 的请求有哪些，则可以使用：
```
"Report RequestId" AND SCF_Duration:>20
```






## 常见问题

#### 1. 为什么页面提示“检索语法不合法”？

请注意检索时不能以 `*` 或 `？`作为开头。

#### 2. 为什么日志里有匹配的关键词，但检索不到？

- 请注意大小写是否匹配。
- 请确认检索内容和语法关键词之间是否有空格。正确示例 `SCF_Duration:>20` ，错误示例`SCF_Duration : > 20`。
