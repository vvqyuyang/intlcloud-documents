If you're unable to watch the CSS and have no idea what goes wrong with it, you can identify the cause of the problem in a short time by following the steps below:
![](https://main.qcloudimg.com/raw/54668f50b8e89909e6fc1600485723cc.png)

## Step 1. Check the playback URL
First of all, check whether the playback URL is correct. An incorrect URL is the most likely cause of most problems. Tencent Cloud's CSS URLs include push URL and playback URL. You need to first verify whether **the push URL is accidentally used CSSas the playback URL**.
![diff](https://main.qcloudimg.com/raw/44951fab55d1a8228bbc332d2713d9cf.png)
>**Playback URL for Mini CSS:**
>The playback URL for Mini CSS can be obtained through debugging. You can search for the keyword **startPlay** in the global search, then set a debugging breakpoint, where the RTMP SDK is called by Mini CSS. The parameter startPlay is the playback URL.

## Step 2. Check the video stream
A correct playback URL does not always mean a normal playback. Next, you need to check whether the video stream is normal:
- In **CSS**, the CSS URL becomes unavailable once the VJ stops the push.
- In **VOD**, if the video files have been removed, watching videos is also impossible.

A frequently used solution is making a check using VLC, an open-source player on PC that supports many protocols.
![](//mc.qcloudimg.com/static/img/7923a14be5525bd37719c18d54243403/image.png)

## Step 3. Check the player
If there's no problem with the video stream, then you need to check whether the player is normal on a case-by-case basis:

### 3.1 Web browser (A)
- **Format**: Mobile browsers only support playback URLs in **HLS (m3u8) and MP4** formats.
- **HLS (m3u8)**: Tencent Cloud HLS protocol is based on "Lazy Start". In short, Tencent Cloud only starts the transcoding for HLS format when a viewer requests a playback URL in an HLS format. The purpose is to prevent waste of resources. But it also creates a problem: **The playback URL in an HLS format cannot be played until 30 seconds after the first user in the world initiates a request**.

### 3.2 RTMP SDK (B)
If RTMP SDK DEMO works normally for playback, it's recommended to check whether the interfacing logic is incorrect by referring to the RTMP SDK playback document [iOS] & [Android].

## Step 4. Check for firewall blocking (C)
It is common that the corporate network environments of many customers restrict video playback through firewalls that detect whether the resources requested by HTTP are streaming media resources (After all, no boss wants his employees to watch videos during working hours). The fact that you can watch the CSS normally over 4G network but cannot watch it over your company's Wi-Fi network indicates your company has imposed restrictions on the network policies. In this case, contact the administrator for a special treatment of your IP.

## Step 5. Check the pusher (D)
If the CSS URL does not work and there is no possibility of firewall blocking described in Step 4, it is likely that the push is unsuccessful. Go to Why the Push is Unsuccessful for a further troubleshooting.



