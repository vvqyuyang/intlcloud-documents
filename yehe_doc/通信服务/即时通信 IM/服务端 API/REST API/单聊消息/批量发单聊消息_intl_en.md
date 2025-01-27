## Feature Description
- This API is used to send one-to-one messages to multiple users (up to 500) at a time.
- Compared with the API for sending one-to-one messages to one user, this API is more suitable for time-sensitive messages, such as marketing messages and system notifications.
- When the administrator specifies an account to send a message to multiple target accounts, the sender displayed to the recipients is not the administrator, but the account specified by the administrator.
- This API does not trigger callback requests.
- This API does not check whether the sender and the recipients are friends or blocklisted by either party or whether the recipients are muted.

>!When calling this API to batch send a message, you must specify whether to synchronize the message to the sender, which is the administrator account or the account specified by the administrator. Synchronization can be implemented via online terminals and roaming servers. This API provides the `SyncOtherMachine` parameter to determine whether to synchronize the message. For more information, please see **Sample request packet** below.

## API Call Description
### Sample request URL
```
https://console.tim.qq.com/v4/openim/batchsendmsg?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```
### Request parameters

The following table only describes the modified parameters when this API is called. For more information on other parameters, please see [RESTful API Introduction](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| v4/openim/batchsendmsg | Request API |
| sdkappid | The SDKAppID assigned by the IM console when an application is created |
| identifier | The app administrator account. For more information, please see the **App Admin** section in [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517). |
| usersig | The signature generated in the app administrator account. For details on how to generate the signature, please see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295 |

### Maximum call frequency

200 calls per second

### Sample request packets
Here, we use sending a text message as an example. To send messages of other types, set `MsgBody` to the corresponding message type. For more information, see [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527).

#### The administrator sends a message to multiple target accounts.

>!If you do not want to synchronize the message to `From_Account`, set `SyncOtherMachine` to `2`.
>To synchronize the message to `From_Account`, set `SyncOtherMachine` to `1`.

```
{
    "SyncOtherMachine": 2, // Do not synchronize the message to the sender.
    "To_Account": [ // A list of target accounts
        "bonnie",
        "rong"
    ],
    "MsgRandom": 19901224, // The random number of the message
    "MsgBody": [ // The body of the message
        {
            "MsgType": "TIMTextElem", // The type of the message. `TIMTextElem` indicates text messages.
            "MsgContent": {
                "Text": "hi, beauty" // The text of the message
            }
        }
    ]
}
```

#### The administrator specifies an account to send a message to multiple target accounts and sets the information of offline push.
`From_Account` is the sender specified by the administrator. The sender displayed to the recipients is not the administrator, but the account specified by the administrator. In the following JSON request, dave sends a message to bonnie and rong. When bonnie and rong receive the message, the message sender displayed to them is dave.
>!If you do not want to synchronize the message to `From_Account`, set `SyncOtherMachine` to `2`.
>To synchronize the message to `From_Account`, set `SyncOtherMachine` to `1`.

```
{
    "SyncOtherMachine": 1, // Synchronize the message to the sender.
    "From_Account": "dave",
    "To_Account": [
        "bonnie",
        "rong"
    ],
    "MsgRandom": 19901224,
    "MsgBody": [
        {
            "MsgType": "TIMTextElem",
            "MsgContent": {
                "Text": "hi, beauty"
            }
        }
    ],
    "OfflinePushInfo": {
        "PushFlag": 0,
        "Desc": "The content to be pushed offline",
        "Ext": "The passthrough content",
        "AndroidInfo": {
            "Sound": "android.mp3"
        },
        "ApnsInfo": {
            "Sound": "apns.mp3",
            "BadgeMode": 1, // If this field is not specified or is set to `0`, the message is counted. If this field is set to `1`, the message is not counted, that is, the icon number in the upper-right corner does not increase.
            "Title":"apns title", // APNs title
            "SubTitle":"apns subtitle", // APNs subtitle
            "Image":"www.image.com" // Image URL
        }
    }
}
```

### Request packet fields

| Field | Type | Required | Description |
|---------|---------|---------|---------|
| SyncOtherMachine | Integer | No | 1: synchronize the message to the online terminal and roaming server of `From_Account`. <br/>2: do not synchronize the message to `From_Account`. If this parameter is not specified, the message is synchronized to the roaming server of `From_Account` by default. |
| From_Account | String | No | The sender account specified by the administrator. To set the information of `From_Account`, the value of this parameter cannot be left empty. |
| To_Account | Array | Yes | The UserID of the recipient of the message |
| MsgRandom | Integer | Yes | The random number of the message. It is used by the backend for message deduplication within a second. Make sure the random number is entered. |
| MsgBody | Object | Yes | TIM message. For more information, please see [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527). |
| MsgType | String | Yes | The object type of the TIM message. Supported message objects include TIMTextElem (text message), TIMFaceElem (emoji message), TIMLocationElem (location message), and TIMCustomElem (custom message). |
| MsgContent | Object | Yes | The object of the TIM message. For more information, see [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527). |
| OfflinePushInfo | Object | No | The information of offline push. For more information, see [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527). |



### Sample response packets

- Response when the message was sent to all the target accounts
```
 {
    "ErrorInfo": "",
    "ActionStatus": "OK",
    "ErrorCode": 0,
    "MsgKey": "128493_903762_1572870301"
}
```

- Response when the message was not sent to some target accounts
```
{
    "ActionStatus": "SomeError",
    "ErrorCode": 0,
    "ErrorInfo": "",
    "MsgKey": "4852_28135_1579678877",
    "ErrorList": [ // A list of the accounts to which the message was not sent
        {
            "To_Account": "rong", // The account to which the message was not sent
            "ErrorCode":  70107 // Error code. 70107 indicates that the account does not exist.
        }
    ]
}
```

- Response when the message was sent to none of the target accounts
```
{
    "ActionStatus": "FAIL",
    "ErrorInfo": "invalid To_Account",
    "ErrorCode": 90012
}
```

### Response packet fields

| Field | Type | Description |
|---------|---------|---------|
| ActionStatus | String | Request result. `OK`: successful. `FAIL`: failed. |
| ErrorCode | Integer | The error code returned for the request. <li>If the message was sent to any account, the value is `0`.</li><li>If the message was sent to none of the target accounts, the value is not `0`.</li> |
| ErrorInfo | String | Error information |
| ErrorList | Array | A list of the target accounts to which the message was not sent or that do not exist. If the message was sent to all the target accounts, the value of this field is empty. |
| ErrorList.To_Account | String | The target account to which the message was not sent. |
| ErrorList.ErrorCode | Integer | The error code indicating that the message was not sent. If the error code is 70107, the account does not exist. |
| MsgKey | String | The unique identifier of the message. This field is required to recall a message. The value is a string of no more than 50 characters. |

## Error Codes

The returned HTTP status code for this API is always 200 unless a network error (such as error 502) occurs. The specific error code and details can be found in the response fields `ErrorCode` and `ErrorInfo` respectively.
For public error codes (60000 to 79999), please see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API:

| Error Code | Description |
| ------------- | ------------------------------------------------------------ |
| 70107 | The requested account does not exist. |
| 70169 | The server timed out. Try again later. |
| 90001 | Failed to parse the JSON request packet. Make sure the format is valid. |
| 90002 | The `MsgBody` in the JSON request packet does not meet message format requirements or `MsgBody` is not an array. For more information, please see the **Message Element TIMMsgElement** section in [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527#.E6.B6.88.E6.81.AF.E5.85.83.E7.B4.A0-timmsgelement). |
| 90007 | The `MsgBody` field in the JSON request packet is not an array. Change it to an array. |
| 90008 | The JSON request packet does not contain the `From_Account` field or the account specified in `From_Account` does not exist. |
| 90009 | The request requires app administrator permissions. |
| 90010 | The JSON request packet does not meet message format requirements. For more information, see the **Message Element TIMMsgElement** section in [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527#.E6.B6.88.E6.81.AF.E5.85.83.E7.B4.A0-timmsgelement). |
| 90011 | The number of target accounts exceeds 500. Delete some `To_Account`. |
| 90012 | The account specified in `To_Account` does not exist or has not been registered. Make sure the account has been imported to IM and is correctly spelled. |
| 90026 | The offline retention time of the message is incorrect. Messages cannot be retained offline for more than 7 days. |
| 90048 | The requested account does not exist. |
| 90992 | Internal service error. Try again. If this error code is returned for all requests and third-party callback is enabled, make sure the app server returns the callback results to the IM backend normally. |
| 91000 | Internal service error. Try again. |
| 93000 | The JSON packet exceeds the maximum size of 8 KB. |


## API Debugging Tool
Use the [RESTful API online debugging tool](https://29294-22989-29805-29810.cdn-go.cn/api-test.html#v4/openim/batchsendmsg) to debug this API.

## References
- Sending One-to-One Messages to One User ([v4/openim/sendmsg](https://intl.cloud.tencent.com/document/product/1047/34919))
- Sending Ordinary Messages in a Group ([v4/group_open_http_svc/send_group_msg](https://intl.cloud.tencent.com/document/product/1047/34959))
- Sending System Messages in a Group ([v4/group_open_http_svc/send_group_system_notification](https://intl.cloud.tencent.com/document/product/1047/34958))
- [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527)
