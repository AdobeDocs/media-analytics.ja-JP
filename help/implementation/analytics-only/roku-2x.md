---
title: ストリーミングメディア用にRoku 2.xを設定する
description: SceneGraph チャネルを含む、Analyticsのみのストリーミングメディア実装用Roku用Adobe Media SDK 2.xをインストールして設定します。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 3%

---

# ストリーミングメディア用にRoku 2.xを設定する

Roku （`adbmobile.brs`）用Adobe Media SDK 2.xは、BrightScriptで記述されたRoku チャンネルからストリーミングメディアデータをAdobe Analyticsに直接送信します。 また、Adobe Audience Managerを通じてオーディエンスデータを収集し、メディアイベントを通じてエンゲージメントを測定します。

>[!NOTE]
>
>ここでは、Analytics専用のMedia SDK 2.x for Rokuについて説明します。 新しい実装の場合、Adobeでは、[Roku Edge SDK](/help/implementation/edge/roku.md)をお勧めします。この機能を使用すると、Adobe Analyticsに加えて、Customer Journey Analytics、Adobe Journey Optimizer、Real-Time CDPでデータを利用できます。

* **前提条件**:
   * [Analyticsのみの実装の概要](overview.md)を完了します。
   * [Roku](/help/getting-started/download-sdks.md)のMedia SDKをダウンロードします。
   * メディアプレーヤーに、プレイヤーイベントを登録するためのAPIと、メディア名や再生ヘッドの位置などのプレーヤー情報を提供するAPIを含めます。

## SDK のインストール

`AdobeMobileLibrary-2.*-Roku.zip` ダウンロードには、次の2つのコンポーネントが含まれています。

* `adbmobile.brs`: ライブラリファイル。 チャンネルの`pkg:/source/` ディレクトリにコピーします。
* `ADBMobileConfig.json`: アプリ用にカスタマイズされたSDK設定ファイル。

SceneGraph チャネルの場合は、`adbmobileTask.brs`と`adbmobileTask.xml`を`pkg:/components/` ディレクトリにコピーします。 [SceneGraph サポート ](#scenegraph)を参照してください。

## ADBMobileConfig.jsonの設定

設定JSONには、ストリーミングメディア用の排他的な`mediaHeartbeat` キーがあります。 プロジェクトソースに`ADBMobileConfig.json`を追加し、`mediaHeartbeat`、`marketingCloud`、`analytics`の値を設定します。

```json
{
  "analytics": {
    "rsids": "your-report-suite-id",
    "server": "your-analytics-server"
  },
  "marketingCloud": {
    "org": "YOUR-MCORG-ID@AdobeOrg"
  },
  "mediaHeartbeat": {
    "server": "your-namespace.hb-api.omtrdc.net",
    "publisher": "your-publisher-id",
    "channel": "sample-channel",
    "ssl": true,
    "ovp": "sample-ovp",
    "sdkVersion": "sample-sdk",
    "playerName": "Roku Player"
  }
}
```

| Config パラメーター | 説明 |
| --- | --- |
| `server` | メディアトラッキングエンドポイントのURL。 [Analyticsのみの実装の概要](overview.md)を参照してください。 |
| `publisher` | コンテンツパブリッシャーの一意のID。 |
| `channel` | コンテンツ配信チャネルの名前。 [ コンテンツチャネル ](/help/implementation/variables/core/content-channel.md)として報告されました。 |
| `ssl` | SSLを使用して呼び出しを追跡するかどうか。 |
| `ovp` | オンライン ビデオ プラットフォーム プロバイダーの名前。 |
| `sdkVersion` | アプリまたはSDKの現在のバージョン。 |
| `playerName` | プレイヤーの名前。 [ コンテンツプレーヤー名](/help/implementation/variables/core/content-player-name.md)として報告されました。 |

>[!IMPORTANT]
>
>`mediaHeartbeat`が正しく設定されていない場合、メディアモジュールはエラー状態になり、トラッキング呼び出しの送信を停止します。 `marketingCloud.org`の値に`@AdobeOrg`が含まれていることを確認してください。

## SDKの初期化とメッセージの処理

`ADBMobile()`のSDKのインスタンスを取得します。 Experience Cloud Visitor ID サービスは、すべてのヒットに含まれる訪問者IDを生成します。

>[!IMPORTANT]
>
>メインイベントループの`processMessages`と`processMediaMessages`を250 ミリ秒ごとに呼び出して、SDKがPingを適切に送信します。

```brightscript
adb = ADBMobile()

' In your main event loop, every ~250 ms:
adb.processMessages()
adb.processMediaMessages()
```

| メソッド | 説明 |
| --- | --- |
| `processMessages` | キューに入れたAnalytics イベントをSDKに渡します。 |
| `processMediaMessages` | キューに登録されたメディアイベント（自動pingを含む）をSDKに渡します。 |

## メディアイベントの追跡

SDK メソッドを呼び出して、各メディアイベントをトラッキングします。 正確な呼び出し、ビルダー、定数については、各[ イベント ](/help/implementation/events/overview.md)および[変数](/help/implementation/variables/overview.md) ページの&#x200B;**Roku 2.x** タブを参照してください。

一般的なセッションは、メディアオブジェクトを作成し、`mediaTrackSessionStart`を呼び出すことから始まります。

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("Mr. Robot", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

contextData = { "a.media.show": "Mr. Robot" }

adb.mediaTrackSessionStart(mediaInfo, contextData)
```

グローバル `adb_media_init_*` ビルダーは、トラッキング呼び出しで使用されるメディア、広告、広告区切り、章、およびQoS オブジェクトを作成します。

| Builder | 署名 |
| --- | --- |
| メディア | `adb_media_init_mediainfo(name, id, length, streamType, mediaType)` |
| 広告 | `adb_media_init_adinfo(name, id, position, length)` |
| 広告の時間 | `adb_media_init_adbreakinfo(name, startTime, position)` |
| チャプター | `adb_media_init_chapterinfo(name, position, length, startTime)` |
| QoS | `adb_media_init_qosinfo(bitrate, startupTime, fps, droppedFrames)` |

標準メタデータは、`a.media.*`個のキーの連想配列として渡されます（SDKでは、これらのキーに`MEDIA_VideoMetadataKeySHOW`などの名前付き定数も定義されています）。 各ディメンションに対応するキーについては、[変数](/help/implementation/variables/overview.md) ページを参照してください。

## Experience Cloud訪問者ID、プライバシー、ログの設定

`ADBMobile()` インスタンスの次のメソッドは、ID、プライバシー、デバッグを管理します。

| メソッド | 説明 |
| --- | --- |
| `visitorMarketingCloudID()` | Experience Cloud ID （ECID）を取得します。 |
| `visitorSyncIdentifiers(identifiers)` | 同じ訪問者に対して追加の顧客IDを設定します。 |
| `setAdvertisingIdentifier(rida)` | Advertising（RIDA）のRoku IDを設定します。 Roku [`getRIDA()`](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic) APIで取得します。 |
| `getAllIdentifiers()` | Analytics、訪問者、Audience Manager、カスタム IDなど、SDKによって保存されているすべてのIDを返します。 |
| `setPrivacyStatus(status)` | プライバシーステータスを設定します。 `adb.PRIVACY_STATUS_OPT_IN`または`adb.PRIVACY_STATUS_OPT_OUT`を渡します。 [ プライバシー](/help/implementation/opt-out-privacy.md)を参照してください。 |
| `getPrivacyStatus()` | 現在のプライバシーステータスを返します。 |
| `setDebugLogging(flag)` | デバッグログを有効または無効にします。 |
| `getDebugLogging()` | デバッグログが有効な場合、`true`を返します。 |

## SceneGraph サポート {#scenegraph}

Roku SceneGraph XML フレームワークは、従来のBrightScript SDK APIを直接呼び出すことはできません。これは、SDKがSceneGraph アプリで使用できないコンポーネント（スレッドなど）を使用しているためです。 このギャップを埋めるために、SDKは、同じAPIを公開するSceneGraph互換のインスタンスを返すコネクタと、データを返すAPIのコールバックメカニズムを提供します。

橋は3つの部分で構成されている：

* **`adbmobileTask`node**: バックグラウンド スレッドでSDK APIを実行し、シーンにデータを返すSceneGraph タスク ノード。
* **コネクタインスタンス**：すべてのレガシー公開APIをラップし、`adbmobileTask` ノードと通信します。
* **`API_RESPONSE`コールバック**: アプリが取得APIから戻り値を受信するために監視するフィールド。

SceneGraph チャネルでSDKを初期化するには：

1. シーンに`adbmobile.brs`を読み込む：

   ```brightscript
   <script type="text/brightscript" uri="pkg:/source/adbmobile.brs" />
   ```

1. `adbmobileTask` ノードを作成し、コネクタインスタンスを取得し、SceneGraph定数を読み込みます。

   ```brightscript
   m.adbmobileTask = createObject("roSGNode", "adbmobileTask")
   m.adbmobile = ADBMobile().getADBMobileConnectorInstance(m.adbmobileTask)
   m.adbmobileConstants = m.adbmobile.sceneGraphConstants()
   ```

1. データを返すAPIの応答オブジェクトを受信するコールバックを登録します。

   ```brightscript
   m.adbmobileTask.ObserveField(m.adbmobileConstants.API_RESPONSE, "onAdbmobileApiResponse")
   
   function onAdbmobileApiResponse() as void
       responseObject = m.adbmobileTask[m.adbmobileConstants.API_RESPONSE]
       if responseObject <> invalid
           methodName = responseObject.apiName
           retVal = responseObject.returnValue
           if methodName = m.adbmobileConstants.PRIVACY_STATUS
               print "Privacy status: " + retVal
           end if
       end if
   end function
   ```

コネクタインスタンス （`m.adbmobile`）は、従来のSDK （`mediaTrackSessionStart`、`mediaTrackPlay`、`mediaTrackPause`、`mediaTrackComplete`、`mediaTrackSessionEnd`、`mediaTrackError`、`mediaTrackEvent`、`mediaUpdatePlayhead`、および`mediaUpdateQoS`）と同じメディアメソッドを公開するため、イベントページとバリアブルページに表示される呼び出しは同じように機能します。 Setter APIは直接呼び出されます。getter APIは、`API_RESPONSE` コールバックを通じて値を返します。

## 次の手順

実装が完了したら、[Analyticsのみの実装用のレポートを設定できます](/help/reporting/setup/analytics-reporting.md)。

>[!MORELIKETHIS]
>
>* [ イベントの概要](/help/implementation/events/overview.md)
>* [変数の概要](/help/implementation/variables/overview.md)
>* [Edge六SDK](/help/implementation/edge/roku.md)
