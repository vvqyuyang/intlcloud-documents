﻿SDK 3.0 is a companion tool for the TencentCloud API 3.0 platform. You can use all [SMS APIs](https://intl.cloud.tencent.com/document/product/382/34689) through the SDK. The new SDK version is unified and features the same SDK usage, API call methods, error codes, and returned packet formats for different programming languages.
>!
>- SMS sending APIs
>One message can be sent to up to 200 numbers at a time.
>- Signature and body template APIs
>Individual users have no permission to use signature and body template APIs and can [manage SMS signatures](https://intl.cloud.tencent.com/document/product/382/35456) and SMS body templates only in the SMS Console. To use the APIs, change "Individual Identity" to "Organizational Identity".



## Prerequisites

- You have activated SMS. For detailed directions, please see [Getting Started with Mainland China SMS](https://intl.cloud.tencent.com/document/product/382/35449).
- If you need to send SMS messages in Mainland China, you need to purchase a Mainland China SMS package first.
- You have prepared the dependent environments: .NET Framework 4.5+ and .NET Core 2.1.
- You have obtained the `SecretID` and `SecretKey` on the **[API Key Management](https://console.cloud.tencent.com/cam/capi)** page in the CAM Console.
 - `SecretID` is used to identify the API caller.
 - `SecretKey` is used to encrypt the string to sign that can be verified on the server. **You should keep it private and avoid disclosure.**
- The call address of the SMS service is `sms.tencentcloudapi.com`.

## Relevant Documents
- For more information on the APIs and their parameters, please see [API Documentation](https://intl.cloud.tencent.com/document/product/382/34689).
- You can download the SDK source code [here](https://github.com/TencentCloud/tencentcloud-sdk-dotnet).

## Installing SDK
### Installing through NuGet (recommended)

1. Run the following installation command:
```
dotnet add package TencentCloudSDK --version 3.0.0
```
 Other information can be obtained through [NuGet](https://www.nuget.org/packages/TencentCloudSDK/).
2. Add the package through Visual Studio.

### Installing through source package
1. Go to the [GitHub code hosting page](https://github.com/tencentcloud/tencentcloud-sdk-dotnet) or [quick download address](https://tencentcloud-sdk-1253896243.file.myqcloud.com/tencentcloud-sdk-dotnet/tencentcloud-sdk-dotnet.zip) to download the latest code.
2. After decompressing, install it in the working directory.
3. Use Visual Studio 2017 to open the compilation.


## Sample Code
>?All samples are for reference only and cannot be directly compiled and executed. You need to modify them based on your actual needs. You can also use [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sms&Version=2019-07-11&Action=SendSms) to automatically generate the demo code as needed.

Each API has a corresponding request structure and a response structure. This document only lists the sample code of several common features. For more samples, please see [SDK for C# Samples](https://github.com/TencentCloud/tencentcloud-sdk-dotnet/blob/master/TencentCloudExamples/SendSms.cs).

### Applying for SMS template

```
using System;
using System.Threading.Tasks;
using TencentCloud.Common;
using TencentCloud.Common.Profile;
using TencentCloud.Sms.V20190711;
using TencentCloud.Sms.V20190711.Models;

namespace TencentCloudExamples
{
    class AddSmsTemplate
    {
        static void Main(string[] args)
        {
            try
            {
                /* Required steps:
                 * Instantiate an authentication object. The Tencent Cloud account key pair `secretId` and `secretKey` need to be passed in as the input parameters
                 * This example uses the way to read from the environment variable, so you need to set these two values in the environment variable in advance
                 * You can also write the key pair directly into the code, but be careful not to copy, upload, or share the code to others
                 * Query the CAM key: https://console.cloud.tencent.com/cam/capi
                 */
                Credential cred = new Credential {
                    SecretId = "xxx",
                    SecretKey = "xxx"
                };
                /*
                Credential cred = new Credential {
                    SecretId = Environment.GetEnvironmentVariable("TENCENTCLOUD_SECRET_ID"),
                    SecretKey = Environment.GetEnvironmentVariable("TENCENTCLOUD_SECRET_KEY")
                };*/

                /* Optional steps:
                 * Instantiate a client configuration object. You can specify the timeout period and other configuration items */
                ClientProfile clientProfile = new ClientProfile();
                /* The SDK uses `TC3-HMAC-SHA256` to sign by default
	             * Do not modify this field unless absolutely necessary */
                clientProfile.SignMethod = ClientProfile.SIGN_TC3SHA256;
                /* Optional steps
                 * Instantiate a client configuration object. You can specify the timeout period and other configuration items */
                HttpProfile httpProfile = new HttpProfile();
                /* The SDK uses the POST method by default
	             * If you need to use the GET method, you can set it here, but the GET method cannot handle some large requests */
                httpProfile.ReqMethod = "GET";
                /* The SDK has a default timeout period. Do not adjust it unless absolutely necessary
	             * If needed, check in the code to get the latest default value */
                httpProfile.Timeout = 10; // Request connection timeout period in seconds (60 seconds by default)
                /* The SDK automatically specifies the domain name. Generally, you don't need to specify a domain name, but if you are accessing a service in a finance AZ, you must manually specify the domain name
               * For example, the SMS domain name of the Shanghai Finance Zone is `sms.ap-shanghai-fsi.tencentcloudapi.com` */
                httpProfile.Endpoint = "sms.tencentcloudapi.com";
                // Proxy server. Set it when there is a proxy server in your environment
                httpProfile.WebProxy = Environment.GetEnvironmentVariable("HTTPS_PROXY");

                clientProfile.HttpProfile = httpProfile;
                /* Instantiate an SMS client object
	             * The second parameter is the region information. You can directly enter the string `ap-guangzhou` or import the preset constant */
                SmsClient client = new SmsClient(cred, "ap-guangzhou", clientProfile);

                /* Instantiate a request object. You can further set the request parameters according to the API called and actual conditions
	             * You can directly check the SDK source code to determine which attributes of `SendSmsRequest` can be set
	             * An attribute may be of a basic type or import another data structure
	             * You are recommended to use the IDE for development where you can easily redirect to and view the documentation of each API and data structure */
                AddSmsTemplateRequest req = new AddSmsTemplateRequest();
              
                /* Settings of a basic parameter:
	             * The SDK uses the pointer style to specify parameters, so even for basic parameters, you need to use pointers to assign values to them
	             * The SDK provides encapsulation functions for importing the pointers of basic parameters
	             * Help link:
	             * SMS Console: https://console.cloud.tencent.com/sms/smslist
	             * SMS helper: https://intl.cloud.tencent.com/document/product/382/3773 
	             */
                
			        	/* Template name */
                req.TemplateName = "Tencent Cloud";
                /* Template content */
                req.TemplateContent = "Your login verification code is {1}. Please enter it within {2} minutes. If the login was not initiated by you, please ignore this message.";
                /* SMS type. 0: general SMS; 1: marketing SMS */
                req.SmsType = 0;
                /* Whether it is Global SMS:
			       	   0: Mainland China SMS
			      	   1: Global SMS */
                req.International = 0;
                /* Template remarks, such as reason for application and use case */
                req.Remark = "xxx";
            
                // Initialize the request by calling the `AddSmsTemplate` method on the client object. Note: the request method name corresponds to the request object
                // The returned `resp` is an instance of the `AddSmsTemplateResponse` class which corresponds to the request object
                AddSmsTemplateResponse resp = client.AddSmsTemplate(req);

                // A string return packet in JSON format is output
                Console.WriteLine(AbstractModel.ToJsonString(resp));
            }
            catch (Exception e)
            {
                Console.WriteLine(e.ToString());
            }
            Console.Read();
        }
    }
}
```


### Sending SMS message

```
using System;
using System.Threading.Tasks;
using TencentCloud.Common;
using TencentCloud.Common.Profile;
using TencentCloud.Sms.V20190711;
using TencentCloud.Sms.V20190711.Models;

namespace TencentCloudExamples
{
    class SendSms
    {
        static void Main(string[] args)
        {
            try
            {
                /* Required steps:
                 * Instantiate an authentication object. The Tencent Cloud account key pair `secretId` and `secretKey` need to be passed in as the input parameters
                 * This example uses the way to read from the environment variable, so you need to set these two values in the environment variable in advance
                 * You can also write the key pair directly into the code, but be careful not to copy, upload, or share the code to others
                 * Query the CAM key: https://console.cloud.tencent.com/cam/capi
                 */
                Credential cred = new Credential {
                    SecretId = "xxx",
                    SecretKey = "xxx"
                };
                /*
                Credential cred = new Credential {
                    SecretId = Environment.GetEnvironmentVariable("TENCENTCLOUD_SECRET_ID"),
                    SecretKey = Environment.GetEnvironmentVariable("TENCENTCLOUD_SECRET_KEY")
                };*/

                /* Optional steps:
                 * Instantiate a client configuration object. You can specify the timeout period and other configuration items */
                ClientProfile clientProfile = new ClientProfile();
                /* The SDK uses `TC3-HMAC-SHA256` to sign by default
	             * Do not modify this field unless absolutely necessary */
                clientProfile.SignMethod = ClientProfile.SIGN_TC3SHA256;
                /* Optional steps
                 * Instantiate a client configuration object. You can specify the timeout period and other configuration items */
                HttpProfile httpProfile = new HttpProfile();
                /* The SDK uses the POST method by default
	             * If you need to use the GET method, you can set it here, but the GET method cannot handle some large requests */
                httpProfile.ReqMethod = "GET";
                /* The SDK has a default timeout period. Do not adjust it unless absolutely necessary
	             * If needed, check in the code to get the latest default value */
                httpProfile.Timeout = 10; // Request connection timeout period in seconds (60 seconds by default)
               /* The SDK automatically specifies the domain name. Generally, you don't need to specify a domain name, but if you are accessing a service in a finance AZ, you must manually specify the domain name
               * For example, the SMS domain name of the Shanghai Finance Zone is `sms.ap-shanghai-fsi.tencentcloudapi.com` */
                httpProfile.Endpoint = "sms.tencentcloudapi.com";
                // Proxy server. Set it when there is a proxy server in your environment
                httpProfile.WebProxy = Environment.GetEnvironmentVariable("HTTPS_PROXY");

                clientProfile.HttpProfile = httpProfile;
                /* Instantiate an SMS client object
	             * The second parameter is the region information. You can directly enter the string `ap-guangzhou` or import the preset constant */
                SmsClient client = new SmsClient(cred, "ap-guangzhou", clientProfile);

                /* Instantiate a request object. You can further set the request parameters according to the API called and actual conditions
	             * You can directly check the SDK source code to determine which attributes of `SendSmsRequest` can be set
	             * An attribute may be of a basic type or import another data structure
	             * You are recommended to use the IDE for development where you can easily redirect to and view the documentation of each API and data structure */
                SendSmsRequest req = new SendSmsRequest();
              
                 /* Settings of a basic parameter:
	             * The SDK uses the pointer style to specify parameters, so even for basic parameters, you need to use pointers to assign values to them
	             * The SDK provides encapsulation functions for importing the pointers of basic parameters
	             * Help link:
	             * SMS Console: https://console.cloud.tencent.com/sms/smslist
	             * SMS helper: https://intl.cloud.tencent.com/document/product/382/3773 
	             */
                
                req.SmsSdkAppid = "1400787878";
                /* The content of SMS signature should be encoded in UTF-8. You must enter an approved signature, which can be viewed in the [SMS Console] */
                req.Sign = "xxx";
                /* SMS code number extension, which is not activated by default. If you need to activate it, please contact [SMS Helper] */
                req.ExtendCode = "x";
                /* `senderid` for global SMS, which is not activated by default. If you need to activate it, please contact [SMS Helper] for assistance. This parameter should be left empty for Mainland China SMS */
                req.SenderId = "";
                /* User session content, which can carry context information such as user-side ID and will be returned as-is by the server */
                req.SessionContext = "";
                /* Target mobile number in the e.164 standard (+[country/region code][mobile number])
                 * Example: +8613711112222, which has a + sign followed by 86 (country/region code) and then by 13711112222 (mobile number). Up to 200 mobile numbers are supported */
                req.PhoneNumberSet = new String[] {"+8613711112222", "+8613711333222", "+8613711144422"};
                /* Template ID. You must enter the ID of an approved template, which can be viewed in the [SMS Console] */
                req.TemplateID = "449739";
                /* Template parameters. If there are no template parameters, leave it empty */
                req.TemplateParamSet = new String[] {"666"};


                // Initialize the request by calling the `SendSms` method on the client object. Note: the request method name corresponds to the request object
                // The returned `resp` is an instance of the `SendSmsResponse` class which corresponds to the request object
                SendSmsResponse resp = client.SendSms(req);

                // A string return packet in JSON format is output
                Console.WriteLine(AbstractModel.ToJsonString(resp));
            }
            catch (Exception e)
            {
                Console.WriteLine(e.ToString());
            }
            Console.Read();
        }
    }
}
```



### Pulling receipt status

```
using System;
using System.Threading.Tasks;
using TencentCloud.Common;
using TencentCloud.Common.Profile;
using TencentCloud.Sms.V20190711;
using TencentCloud.Sms.V20190711.Models;

namespace TencentCloudExamples
{
    class PullSmsSendStatus
    {
        static void Main(string[] args)
        {
            try
            {
                /* Required steps:
                 * Instantiate an authentication object. The Tencent Cloud account key pair `secretId` and `secretKey` need to be passed in as the input parameters
                 * This example uses the way to read from the environment variable, so you need to set these two values in the environment variable in advance
                 * You can also write the key pair directly into the code, but be careful not to copy, upload, or share the code to others
                 * Query the CAM key: https://console.cloud.tencent.com/cam/capi
                 */
                Credential cred = new Credential {
                    SecretId = "xxx",
                    SecretKey = "xxx"
                };
                /*
                Credential cred = new Credential {
                    SecretId = Environment.GetEnvironmentVariable("TENCENTCLOUD_SECRET_ID"),
                    SecretKey = Environment.GetEnvironmentVariable("TENCENTCLOUD_SECRET_KEY")
                };*/

                /* Optional steps:
                 * Instantiate a client configuration object. You can specify the timeout period and other configuration items */
                ClientProfile clientProfile = new ClientProfile();
                /* The SDK uses `TC3-HMAC-SHA256` to sign by default
	             * Do not modify this field unless absolutely necessary */
                clientProfile.SignMethod = ClientProfile.SIGN_TC3SHA256;
                /* Optional steps
                 * Instantiate a client configuration object. You can specify the timeout period and other configuration items */
                HttpProfile httpProfile = new HttpProfile();
                /* The SDK uses the POST method by default
	             * If you need to use the GET method, you can set it here, but the GET method cannot handle some large requests */
                httpProfile.ReqMethod = "POST";
                /* The SDK has a default timeout period. Do not adjust it unless absolutely necessary
	             * If needed, check in the code to get the latest default value */
                httpProfile.Timeout = 10; // Request connection timeout period in seconds (60 seconds by default)
                /* The SDK automatically specifies the domain name. Generally, you don't need to specify a domain name, but if you are accessing a service in a finance AZ, you must manually specify the domain name
               * For example, the SMS domain name of the Shanghai Finance Zone is `sms.ap-shanghai-fsi.tencentcloudapi.com` */
                httpProfile.Endpoint = "sms.tencentcloudapi.com";
                // Proxy server. Set it when there is a proxy server in your environment
                httpProfile.WebProxy = Environment.GetEnvironmentVariable("HTTPS_PROXY");

                clientProfile.HttpProfile = httpProfile;
               /* Instantiate an SMS client object
	             * The second parameter is the region information. You can directly enter the string `ap-guangzhou` or import the preset constant */
                SmsClient client = new SmsClient(cred, "ap-guangzhou", clientProfile);

                /* Instantiate a request object. You can further set the request parameters according to the API called and actual conditions
	             * You can directly check the SDK source code to determine which attributes of `SendSmsRequest` can be set
	             * An attribute may be of a basic type or import another data structure
	             * You are recommended to use the IDE for development where you can easily redirect to and view the documentation of each API and data structure */
                PullSmsSendStatusRequest req = new PullSmsSendStatusRequest();
              
                 /* Settings of a basic parameter:
	             * The SDK uses the pointer style to specify parameters, so even for basic parameters, you need to use pointers to assign values to them
	             * The SDK provides encapsulation functions for importing the pointers of basic parameters
	             * Help link:
	             * SMS Console: https://console.cloud.tencent.com/sms/smslist
	             * SMS helper: https://intl.cloud.tencent.com/document/product/382/3773 
	             */
                
				// Set the maximum number of pulled entries. Maximum value: 100
                req.Limit = 100;
                /* SMS application ID, which is the actual `SDKAppID` generated after an application is added in the [SMS Console], such as 1400006666 */
                req.SmsSdkAppid = "1400009099";

                // Initialize the request by calling the `PullSmsSendStatus` method on the client object. Note: the request method name corresponds to the request object
                // The returned `resp` is an instance of the `PullSmsSendStatusResponse` class which corresponds to the request object
                PullSmsSendStatusResponse resp = client.PullSmsSendStatus(req);

                // A string return packet in JSON format is output
                Console.WriteLine(AbstractModel.ToJsonString(resp));
            }
            catch (Exception e)
            {
                Console.WriteLine(e.ToString());
            }
            Console.Read();
        }
    }
}
```

### Collecting SMS message sending data
```
using System;
using System.Threading.Tasks;
using TencentCloud.Common;
using TencentCloud.Common.Profile;
using TencentCloud.Sms.V20190711;
using TencentCloud.Sms.V20190711.Models;

namespace TencentCloudExamples
{
    class SendStatusStatistics
    {
        static void Main(string[] args)
        {
            try
            {
                /* Required steps:
                 * Instantiate an authentication object. The Tencent Cloud account key pair `secretId` and `secretKey` need to be passed in as the input parameters
                 * This example uses the way to read from the environment variable, so you need to set these two values in the environment variable in advance
                 * You can also write the key pair directly into the code, but be careful not to copy, upload, or share the code to others
                 * Query the CAM key: https://console.cloud.tencent.com/cam/capi
                 */
                Credential cred = new Credential {
                    SecretId = "xxx",
                    SecretKey = "xxx"
                };
                /*
                Credential cred = new Credential {
                    SecretId = Environment.GetEnvironmentVariable("TENCENTCLOUD_SECRET_ID"),
                    SecretKey = Environment.GetEnvironmentVariable("TENCENTCLOUD_SECRET_KEY")
                };*/

                /* Optional steps:
                 * Instantiate a client configuration object. You can specify the timeout period and other configuration items */
                ClientProfile clientProfile = new ClientProfile();
                /* The SDK uses `TC3-HMAC-SHA256` to sign by default
	             * Do not modify this field unless absolutely necessary */
                clientProfile.SignMethod = ClientProfile.SIGN_TC3SHA256;
                /* Optional steps
                 * Instantiate a client configuration object. You can specify the timeout period and other configuration items */
                HttpProfile httpProfile = new HttpProfile();
                /* The SDK uses the POST method by default
	             * If you need to use the GET method, you can set it here, but the GET method cannot handle some large requests */
                httpProfile.ReqMethod = "POST";
                /* The SDK has a default timeout period. Do not adjust it unless absolutely necessary
	             * If needed, check in the code to get the latest default value */
                httpProfile.Timeout = 10; // Request connection timeout period in seconds (60 seconds by default)
                /* The SDK automatically specifies the domain name. Generally, you don't need to specify a domain name, but if you are accessing a service in a finance AZ, you must manually specify the domain name
               * For example, the SMS domain name of the Shanghai Finance Zone is `sms.ap-shanghai-fsi.tencentcloudapi.com` */
                httpProfile.Endpoint = "sms.tencentcloudapi.com";
                // Proxy server. Set it when there is a proxy server in your environment
                httpProfile.WebProxy = Environment.GetEnvironmentVariable("HTTPS_PROXY");

                clientProfile.HttpProfile = httpProfile;
                /* Instantiate an SMS client object
	             * The second parameter is the region information. You can directly enter the string `ap-guangzhou` or import the preset constant */
                SmsClient client = new SmsClient(cred, "ap-guangzhou", clientProfile);

               /* Instantiate a request object. You can further set the request parameters according to the API called and actual conditions
	             * You can directly check the SDK source code to determine which attributes of `SendSmsRequest` can be set
	             * An attribute may be of a basic type or import another data structure
	             * You are recommended to use the IDE for development where you can easily redirect to and view the documentation of each API and data structure */
                SendStatusStatisticsRequest req = new SendStatusStatisticsRequest();
              
                 /* Settings of a basic parameter:
	             * The SDK uses the pointer style to specify parameters, so even for basic parameters, you need to use pointers to assign values to them
	             * The SDK provides encapsulation functions for importing the pointers of basic parameters
	             * Help link:
	             * SMS Console: https://console.cloud.tencent.com/sms/smslist
	             * SMS helper: https://intl.cloud.tencent.com/document/product/382/3773 
	             */
                
				/* SMS application ID, which is the actual `SDKAppID` generated after an application is added in the [SMS Console], such as 1400006666 */
				req.SmsSdkAppid = "1400009099";
				// Set the maximum number of pulled entries. Maximum value: 100
				req.Limit = 5L;
				/* Offset, which is currently fixed at 0 */
				req.Offset = 0L;
				/* Start time of pull in the format of `yyyymmddhh` accurate to the hour */
				req.StartDateTime = "2019071100";
				/* End time of pull in the format of `yyyymmddhh` accurate to the hour
				 * Note: `EndDataTime` must be later than `StartDateTime` */
				req.EndDataTime = "2019071123";

                // Initialize the request by calling the `SendStatusStatistics` method on the client object. Note: the request method name corresponds to the request object
                // The returned `resp` is an instance of the `SendStatusStatisticsResponse` class which corresponds to the request object
                SendStatusStatisticsResponse resp = client.SendStatusStatistics(req);

                // A string return packet in JSON format is output
                Console.WriteLine(AbstractModel.ToJsonString(resp));
            }
            catch (Exception e)
            {
                Console.WriteLine(e.ToString());
            }
            Console.Read();
        }
    }
}
```

