## Configuration Overview
To control the source of access to your business resources, you can use the IP blocklist/allowlist feature in Tencent Cloud CDN.

By configuring an access control policy on IPs of user requests, you can effectively control the source of access, preventing hotlinking by malicious IPs, attacks, etc.

## Configuration Guide

### Viewing the configuration
Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of a domain name to enter its configuration page. Open the **Access Control** tab to see the **IP Blocklist/Allowlist Configuration** section. It is disabled by default.
![](https://main.qcloudimg.com/raw/f151317bd14f053a125bf0c3841da033.png)

### Enabling the configuration

Toggle on the switch, tick **Blocklist** or **Allowlist**, enter the list of IPs or IP ranges, and click **Save**:
![](https://main.qcloudimg.com/raw/0b278589542a7022b3525f80ecadd2e3.png)
**IP blocklist**
If a client IP hits the blocklist, a 403 error is returned when it tries to access the CDN node.
**IP allowlist**
If a client IP is not included in the allowlist, a 403 error is returned when it tries to access the CDN node.
**Configuration limitations**

- The IP blocklist and allowlist are mutually exclusive and cannot be configured at the same time.
- Up to 200 entries can be added to the blocklist and allowlist respectively.
- Only IP ranges `/8`, `/16`, and `/24` are supported.
- The format `IP:Port` is not supported here.

### Disabling the configuration
You can toggle off this feature directly. When the switch is off, this feature does not take effect in the production environment even if there is an existing configuration. If you toggle the switch on, the configuration will take effect across the entire network after the action is confirmed.
![](https://main.qcloudimg.com/raw/24a3de16131fd945c05307493eb768f0.png)

>!If your acceleration domain name is configured for global acceleration, the IP blocklist/allowlist will take effect globally. 

## Configuration Samples

Suppose that the IP blocklist/allowlist configuration of the domain name `www.test.com` is as follows:
![](https://main.qcloudimg.com/raw/29a9307902d03f686345eef2964c5ec2.png)
Then the actual access will be as follows:
1. When the client with IP `1.1.1.1` accesses `http://www.test.com/test.txt`, as the IP is in the allowlist, the requested content will be returned normally.
2. When the client with IP `2.1.1.1` accesses `http://www.test.com/test.txt`,  as the IP is not in the allowlist, a 403 status code will be returned.

