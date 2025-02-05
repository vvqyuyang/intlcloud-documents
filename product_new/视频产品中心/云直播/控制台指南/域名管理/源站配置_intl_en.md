## Operation Scenarios

If you have a self-built origin server and live stream source and want to live broadcast your content through Tencent Cloud, you can configure origin server information for your CSS playback domain name for origin-pull. After the configuration is successful, you can pull live streams from the origin server and distribute the live content through CSS. This document describes how to do so.

## Notes
- After the relevant configuration is finished, the origin server settings will take effect in **30 minutes**- **one hour**.
- After the origin server configuration is enabled, features such as transcoding, recording, screencapturing, porn detection, and watermark will become unavailable.

## Prerequisites
- You have logged in to the [CSS Console](https://console.cloud.tencent.com/live).
- You have built a live stream origin server.
- You have added a **playback domain name**.

## Directions
1. Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, click the **playback domain** to be configured or **Manage** on the right to enter the domain details page.
2. Select **Advanced Configuration** and view the **Origin Server Settings** tab.
3. Click **Edit** in the origin server settings module to configure the following origin server information:
 1. Toggle **Origin Server Settings** on.
 2. Select **Forwarding Protocol** and check **Playback Protocol**.
 3. Enter the **Master Origin Server Address** (either an IP or a domain name).
 4. Click **Save**.

>?**Forwarding Protocol** refers to the format supported by CSS when pulling streams from the origin server. **Playback Protocol** refers to the playback protocol used to distribute live content through CDN.
>- If the forwarding protocol is FLV or RTMP, the playback protocol can be FLV or HLS.
>- If the forwarding protocol is HLS, the playback protocol can only be HLS.
>- You can select only one forwarding protocol but multiple playback protocols.



![](https://main.qcloudimg.com/raw/aad1f61836b32b01822f945f8afa241e.png)

