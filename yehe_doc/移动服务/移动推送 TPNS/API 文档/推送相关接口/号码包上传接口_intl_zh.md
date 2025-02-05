## 接口说明

**请求方式**：POST。

```plaintext
服务地址/v3/push/package/upload
```
接口服务地址与服务接入点一一对应，请选择与您的应用服务接入点对应的 [服务地址](https://intl.cloud.tencent.com/document/product/1024/38517)。

**接口功能**：用户需要通过文件的方式，对批量账号上传号码包文件。然后对号码包中的文件进行推送。号码包推送接口主要包括号码包上传接口、以及号码包推送接口。

>!
> - 账号包文件名：长度限制为 [1, 100]。
> - 账号包格式及大小： 支持 `zip\txt\csv` 文件；大小保持在100MB以内。
> - `zip` 压缩包中可包含：单个 `.txt` 或 `.csv` 文件（不能嵌套文件夹）。
> - .`txt` 文件要求：（1）编码为 UTF-8；（2）每行一个账号，账号长度限制为 [2, 100]。
> - .`csv` 文件要求：（1）只能有一列；（2）每行一个账号，账号长度限制为 [2, 100]。



## 请求参数  

| 参数名  | 类型  | 是否必须  | 参数说明  |
| --- | --- | --- | --- |
| file  | form-data | 是  | <li>账号包格式及大小： 支持 `zip\txt\csv` 文件；大小保持在100MB以内<li>`zip` 压缩包中可包含：单个 `.txt` 或 `.csv` 文件（不能嵌套文件夹）<li>.`txt` 文件要求：（1）编码为 UTF-8；（2）每行一个账号，账号长度限制为 [2, 100]<li> .`csv` 文件要求：（1）只能有一列；（2）每行一个账号，账号长度限制为 [2, 100] |



## 响应参数

| 参数名  | 类型  | 是否必须  | 参数说明  |
| --- | --- | --- | --- |
| retCode   | Integer  | 是   | 错误码   |
| errMsg   | String   | 是   | 请求出错时的错误信息   |
| uploadId    | Integer   | 是   | 当上传文件成功时，将反馈一个正整数 uploadId ，代表上传文件 ID，提供给后续号码包接口进行推送   |


## 请求示例


#### Curl  示例

``` xml
curl -X POST 
https://api.tpns.tencent.com/v3/push/package/upload 
   
-H 'Authorization: Basic  应用的认证信息' 
-F 'file=@C:\上传文件绝对路径'
```

#### Python  示例
``` python
import requests

url = "https://api.tpns.tencent.com/v3/push/package/upload"

files = {'file':open('文件名', 'rb')}
upload_data={"fileName":"文件绝对地址"}

headers = {
    'Authorization': "Basic 应用鉴权信息",
    }

response = requests.request("POST", url, data=upload_data, headers=headers, files=files, verify=False)
print(response.text.encode('utf-8'))
```

>! 应用的认证信息，参见 [Basic Auth 认证](https://intl.cloud.tencent.com/document/product/1024/34672) 文档。
>
