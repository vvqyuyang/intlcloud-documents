## Monthly Subscription

### Expiration alert

You will receive an alert within 7 days before your CCN instance expires.

### Expiration handling
1. Within 24 hours after expiration, the system automatically renews the account if auto-renewal is enabled and the account balance is sufficient.
2. Twenty four hours later, the cross-region bandwidth drops to 10 Kbps if the account is not renewed.
![](https://main.qcloudimg.com/raw/49be4e1ed5ff3b5695a9f40557e6a106.png)

## Pay-As-You-Go by Monthly 95th Percentile
### Overdue payment alert
1. Overdue payment notification: you will receive a notification when your account balance becomes negative.
2. Overdue payment pre-alert: this feature is disabled by default. <!-- To subscribe this service, please refer to [Balance Alert Guideline]().-->

### Overdue payment policy
The overdue payment policy is applied from the moment when the balance drops to 0. The details are as follows:
1. Within seven days, Cloud Connect Network (CCN) is still available for the account.
2. Seven days later, the CCN instance becomes unavailable and the cross-region bandwidth drops to 0 Kbps if your account balance is still negative. However, the CCN instance retains and resumes service once you top up your account.
![](https://main.qcloudimg.com/raw/f98537d47bd8dc290ba75db851f45ef1.png)

>?
>- If the non-stop feature is enabled, you can still use the product after your account becomes overdue, and the billing continues. To enable this feature, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>- The pay-as-you-go CCN instance billed by monthly 95 percentile will be charged between 8 and 10 AM on the first day of the next month.
>For example, if you use such a CCN instance in November 2019, you will be charged between 8 and 10 AM on December 1, 2019.
>- All operations and status changes will be notified to Tencent Cloud account creator, global resource collaborators, and financial collaborators via email, SMS, etc.
