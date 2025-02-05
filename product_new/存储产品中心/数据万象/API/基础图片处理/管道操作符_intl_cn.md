## 功能概述
腾讯云数据万象的管道操作符`|`能够实现对图片按顺序进行多种处理。用户可以通过管道操作符将多个处理参数分隔开，从而实现在一次访问中按顺序对图片进行不同处理。处理图片原图大小不超过20MB、宽高不超过30000像素且总像素不超过2.5亿像素，处理结果图宽高设置不超过9999像素；针对动图，原图宽 x 高 x 帧数不超过2.5亿像素。

## 接口形式
用户在图片 URL 链接后以样式分隔符`?`与处理样式相连接，多个处理样式之间以管道操作符`|`分隔，样式按照先后顺序执行，目前最多支持三层管道。

## 示例
本次示例先将原图做50%的缩放，然后在右下角添加“数据万象”的文字水印。

假设原图 URL 为：
```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg
```

原图显示如下： 
![](https://main.qcloudimg.com/raw/52e4147a6febbc589505c67973edb394.png)

#### 缩放操作

首先增加缩放操作，则 URL 为：

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50p
```

图片显示如下：
![](https://main.qcloudimg.com/raw/f6ab90d8bb2cc1faa1aa3467216c450d.jpg)

#### 添加水印

使用管道操作符再添加文字水印的样式处理，则最终 URL 为：
```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50p|watermark/2/text/5pWw5o2u5LiH6LGh/fill/I0ZGRkZGRg==/fontsize/30/dx/20/dy/20
```

图片最终处理效果如下： 
![](https://main.qcloudimg.com/raw/8c44c8e3cda5f6311ebdd7e5b33b0480.jpg)
