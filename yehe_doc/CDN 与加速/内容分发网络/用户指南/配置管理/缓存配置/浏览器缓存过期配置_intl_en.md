## Feature Overview

By configuring the browser cache validity, you can customize client browser cache policies to reduce origin-pull rate.

> ?When a request comes, if the requested resource is cached on the browser, it will be returned directly. If no, the request will be forwarded to CDN cache nodes. If the resource still cannot be found on the cache node, the request will be forwarded to the origin server.

## Configuration Guide

### Viewing the configuration

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, click **Manage** on the right of a domain name to enter its configuration page. Open the **Cache Configuration** tab to find the **Browser Cache Validity Configuration** section.
![](https://main.qcloudimg.com/raw/d74acc06100e385c87176d62459f12a6.png)





### Adding rules

Click **Add Rule** to add browser cache validity rules for specified file type, file directory, file path, and homepage.
<img src="https://main.qcloudimg.com/raw/d98a14185f9e9d41d682fb356601e9e5.jpg" style="height:220px"/>

- Follow origin server: follow the `Cache-Control` header of the origin server.
- Cache: set the cache validity of resources in a browser.
- No cache: do not cache the resources to the browser.



**Configuration limitations**

- Each domain name can have up to 20 rules. Only one "All Files" and "Homepage" rule can be added.
- You can adjust the priority for multiple rules. Rules at the bottom of the list have higher priority.
- In each rule of specified file type, file directory, and file path, up to 50 groups of content can be entered. Please use ";" to separate different content, e.g., Specified File Type: jpg;png.
- Chinese characters are not supported.
