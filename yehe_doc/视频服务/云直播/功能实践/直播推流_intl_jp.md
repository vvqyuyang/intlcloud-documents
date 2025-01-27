CSSのサービスは本質的に放送プロセスであり、テレビ局のライブストリーミングプログラムがケーブルネットワークを介して何百万もの世帯に送信されることに類似しています。このプロセスを完結するには、CSSには収集とプッシュのためのデバイス（カメラに類似）、CSSサービス（テレビ局のケーブルネットワークに類似）および再生デバイス（テレビに類似）が必要です。収集とプッシュのデバイスおよび再生デバイスをスマートフォン、PC、Padなどのスマート端末およびWebブラウザとすることができ、弊社は対応するデバイスのプッシュソフトウェアのDemoも提供しています。
<span id="step1"></span>
## 準備
1. [Tencent CSSサービス](https://console.cloud.tencent.com/live?from=product-banner-use-lvb)をアクティブにします 。
2.  [【Domain Management】](https://console.cloud.tencent.com/live/domainmanage)を選択し、【ドメイン名の追加】をクリックして、ICP登録済みのプッシュドメイン名を追加します。
>? CSSはデフォルトのプッシュドメイン名を提供します。形式は`xxx.livepush.myqcloud.com`ですが、実際の業務でこのドメイン名をプッシュドメイン名として使用することはお勧めしません。

## プッシュアドレスの取得
CSSコンソールの【補助ツール】>[【アドレスジェネレーター】](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)に移動し、プッシュアドレスを生成します。設定は次のとおりです。
- 生成タイプの選択：**プッシュドメイン名**。
-ドメイン名管理で追加したプッシュドメイン名を選択します。
- カスタマイズされたカスタムストリーム名StreamNameを入力します（例：liveteststream）。
- アドレスの期限切れ時間を選択します（例：` 2019-10-18  23:59:59`）。
- 【アドレスの生成】をクリックします。

>!
>- ライブストリーミングのセキュリティを保護するために、システムは自動的にプッシュ認証を有効にします。[【Domain Management】](https://console.cloud.tencent.com/live/domainmanage)で変更するプッシュドメイン名を選択し、右側の【管理】をクリックして、ドメイン名詳細情報ページの【プッシュ設定】に移動し、認証設定情報をカスタマイズすることもできます。プッシュアドレスの形式は次のとおりです。
`rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`
>-  上記方法以外にも、CSSコンソールの[【Domain Management】](https://console.cloud.tencent.com/live/domainmanage)でプッシュドメイン名を選択して、【管理】をクリックし、【プッシュ設定】を選択して、プッシュアドレスの期限切れ時間とカスタマイズされたストリーム名StreamNameを入力し、【プッシュアドレスの生成】をクリックすると、プッシュアドレスを生成できます。
>- **長期的に有効なプッシュアドレス**が必要な場合は、[【Domain Management】](https://console.cloud.tencent.com/live/domainmanage)に移動し、プッシュドメイン名を選択して、【管理】をクリックし、【プッシュ設定】を選択して、【プッシュアドレスサンプルコード】のサンプルコードを参考に計算し生成することができます。具体的なクエリー方式については、 [プッシュサンプルコードのクエリー方法](https://intl.cloud.tencent.com/document/product/267/31059)をご参照ください。
## CSSプッシュ
業務のシナリオに応じて次の方式でCSSプッシュを実現できます。

### シナリオ1 ：PCプッシュ
PC（Windows/Mac）でプッシュする場合は、実際の状況に応じて [OBS](https://obsproject.com/download) または [XSplit](https://www.xsplit.com/zh-cn) のインストールを選択して、プッシュすることができます。 OBSはWindows、Mac、Linuxなどのシステムをサポートする無償オープンソースのビデオレコーディングおよびビデオリアルタイムストリームソフトウェアです。XSplitの使用は有償です。XSplitにはゲームライブストリーミング用の個別のインストールパッケージがあります。ゲームライブストリーミングでない場合は、BroadCasterの使用をお勧めします。

![](https://main.qcloudimg.com/raw/dcb203971ac99415258ea0b0ee1529a8.png)
ここではOBSプッシュのインストールを例示します。操作ステップは次の説明のとおりです。準備の完了したプッシュアドレスが次のとおりであると仮定します：

```
rtmp://3891.livepush.myqcloud.com/live/3891_test?bizid=3891&txSecret=xxx&txTime=58540F7F
```


1.  [OBSオフィシャルサイト](https://obsproject.com/download) に移動し、プッシュツールをダウンロードしインストールします。
2. OBSを開き、下部ツールバーの【コントロール】>【設定】をクリックし、ボタンを押して設定インターフェースに移動します。
3. 【プッシュ】をクリックし、プッシュ設定ページに移動して、次の設定を行います。
	1. サービスタイプ：カスタムを選択します。
	1. サーバーに `rtmp://3891.livepush.myqcloud.com/live/`のようにプッシュアドレスの前半部分を入力します。
	1. ストリームキーに`3891_test?bizid=3891&txSecret=xxx&txTime=58540F7F`のようにプッシュアドレスの後半部分を入力します。
	1. 右下隅の【OK】をクリックします。

![](https://main.qcloudimg.com/raw/7b5365a0be590c3694fbb6d0ded8e5e3.png)

4. ツールバーの【コントロール】>【プッシュ開始】をクリックすれば、プッシュテストを実行できます。OBS操作の詳細については、[OBSプッシュ](https://intl.cloud.tencent.com/document/product/267/31569)をご参照ください。

### シナリオ2：Webプッシュ
1.  CSSコンソールにログインします。
2. 【補助ツール】>[【Web プッシュ】](https://console.cloud.tencent.com/live/tools/webpush)を選択します。
3. Webプッシュのページで次の設定を行います。
	1. プッシュドメイン名を選択します。
	2. カスタマイズされたカスタムストリーム名StreamNameを入力します（例：liveteststream）。
	3. 期限切れ時間を選択します（例：`2019-10-30 23:59:59）。
	4.  【プッシュ開始】をクリックし、カメラの呼び出しが承認されると、プッシュを開始できます

>! Webプッシュ機能は、デバイスにカメラがインストールされている必要があり、かつブラウザがカメラ許可を呼び出すFlashプラグインをサポートしている必要があります。

![](https://main.qcloudimg.com/raw/9da7489bb2387049859131e792364124.png)

### シナリオ3：モバイルプッシュ
1. スマートフォンで2次元コードをスキャンし、ビデオクラウドツールキットをダウンロードしてインストールします。
2. ツールキットを開き、【MLVB】>【カメラプッシュ】を選択します。
3. [プッシュアドレス](#step1)を手動入力するか、または2次元コードをスキャンして入力します。
4. 左下隅のスタートボタンをクリックすれば、プッシュを開始することができます。

>? 事前にプッシュアドレスを準備していない場合は、カメラプッシュページでプッシュアドレス右側の【NEW】をクリックすれば、システムが自動的にプッシュアドレスを入力し、対応する再生アドレスが提供されます。この再生アドレスを介してライブストリーミングプッシュ機能を確認できます。

### シナリオ4：ライブストリーミングSDKプッシュ
ライブストリーミング機能を既存のアプリに統合するだけで良い場合は、次の手順に従い、迅速に目的を果たすことができます。
1. MLVB SDK開発キットをダウンロードします。
2. ドッキングドキュメントを参照してiOSまたはAndroidのアクセスを完了します。

CSS SDKはモバイル端末ライブストリーミングソリューションの集合であり、無償のソースコードの形式で表示されます。CSS（CSS）、VOD、IM、COS等のサービスを組み合わせて利用し、最適なライブストリーミングソリューションを構築します。

### シナリオ5：ミニプログラムプッシュ
1. モバイルWeChatサーチミニプログラムTencentVideo Cloudを開くか、または2次元コードをスキャンしてTencent Video Cloud WeChat Mini Programに移動します。
2. 【RTMPプッシュ】を選択し、プッシュ設定インターフェースに移動します。
3. [プッシュアドレス](#step1)を手動入力するか、または【スキャンコード読み取り】をタップし、スキャンして入力します。
4. 中央の【開始】をタップすれば、プッシュを開始することができます。

>? 事前にプッシュアドレスを準備していない場合は、Tencent Video Cloudミニプログラムを開き、【RTMPプッシュ】を選択し、RTMPページでプッシュアドレス右側の【自動生成】をタップすれば、システムがプッシュアドレスを自動作成し、同時に再生アドレスを生成します。


## よくあるご質問
- [CSS再生はどのように実現するのですか？](https://intl.cloud.tencent.com/document/product/267/31559)
- [プッシュURLはどのようにスプライスするのですか？](https://intl.cloud.tencent.com/document/product/267/32480)
- [ホットリンク防止はどのように計算するのですか？](https://intl.cloud.tencent.com/document/product/267/31560)
  

