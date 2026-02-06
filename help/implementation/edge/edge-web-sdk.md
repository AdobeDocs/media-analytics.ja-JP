---
title: Adobe Experience Platform Web SDKを使用したEdgeへの Web データの送信
description: Adobe Experience Platform Web SDKを使用して、Adobe ストリーミングメディアデータをExperience Platform Edgeに送信する方法について説明します。
feature: Streaming Media
role: User, Admin, Developer
exl-id: de40ebd9-46be-4a52-866f-7bb2589fce28
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 1%

---

# Adobe Experience Platform Web SDKを使用したEdgeへの Web データの送信

バージョン 2.20.0 以降は、Adobe Experience Platform `streamingMedia`Web SDK[&#x200B; の &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/web-sdk/home) コンポーネントを使用すると、web サイト上のメディアセッションに関連するデータを収集できます。 収集されたデータには、メディアプレイバック、一時停止、完了およびその他の関連イベントに関する情報を含めることができます。

データを収集したら、Adobe Experience PlatformやAdobe Analyticsに送信し、レポートを生成できます。 この機能は、web サイトでのメディア消費行動を追跡および把握するための包括的なソリューションを提供します。

Media JS SDKを使用しているお客様の場合、Web SDKは、Media JS SDKから Web SDKに移行するための移行パスを提供すると同時に、メディアイベントの処理などの既存の Media JS 機能のサポートを含みます。

## 前提条件 {#prerequisites}

Web SDKの `streamingMedia` コンポーネントを使用するには、次の前提条件を満たす必要があります。

* ストリーミングメディアデータをEdgeに送信する前に、まず [Edge Networkを使用したAdobe ストリーミングメディアサービスの実装 &#x200B;](/help/implementation/edge/implementation-edge.md) の手順を実行します。
* Adobe Experience PlatformやAdobe Analyticsにアクセスできることを確認します。
* Web SDK バージョン 2.20.0 以降を使用する必要があります。 最新バージョンのインストール方法については、[Web SDKのインストールの概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/web-sdk/install/overview) を参照してください。
* 使用しているデータストリームの「**[[!UICONTROL Media Analytics]](https://experienceleague.adobe.com/ja/docs/experience-platform/datastreams/configure)**」オプションを有効にします。
* データストリームで使用するスキーマに、メディアコレクションのスキーマフィールドが含まれていることを確認してください。
* Web SDK設定でストリーミングメディアサービスを設定します。このページの説明に従って、[&#x200B; タグ拡張機能 &#x200B;](#tag-extension) または [JavaScript ライブラリ &#x200B;](#library) を使用します。

ストリーミングメディアサービスの実装を Media JS から Web SDKに移行するには、このページで説明する手順に従います。

### 手順 1:Experience Platform Web SDKのインストール

Web プロパティに web SDKをインストールする方法については、[&#x200B; 専用ドキュメント &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/web-sdk/install/overview) を参照してください。

### 手順 2:Web SDK `streamingMedia` コンポーネントを設定する

**例**

以下のスニペットは、Media JS でメディアコレクションを設定する方法を示しています。

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "company.hb-api.omtrdc.net";
mediaConfig.playerName = "player_name";
mediaConfig.channel = "sample_channel";
mediaConfig.appVersion = "app_version";
mediaConfig.debugLogging = true;
mediaConfig.ssl = true;

ADB.Media.configure(mediaConfig, appMeasurement);
```

代わりに、次に示すように、Web SDKで `streamingMedia` コンポーネントを設定する必要があります。

```js
alloy("configure", {
  streamingMedia: {
    channel: "sample_channel",
    playerName: "player_name",
    appVersion: "app_version",
    mainPingInterval: 10,
    adPingInterval: 10
  }
});
```

設定方法について詳しくは、web SDK `streamingMedia` コンポーネント [&#x200B; ドキュメント &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/configure/streamingmedia) を参照してください。

### 手順 3:Media JS SDKから移行する際に、Media トラッカーインスタンスを取得する

Media JS SDKを使用しているお客様の場合、Web SDKは、Media JS SDKから Web SDKに移行するための移行パスを提供すると同時に、メディアイベントの処理などの既存の Media JS 機能のサポートを含みます。

[!DNL Web SDK] には、Media Analytics トラッカーを取得するコマンドが含まれています。 このコマンドを使用してオブジェクトインスタンスを作成し、[Media JS ライブラリ &#x200B;](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html) で提供される API と同じ API を使用してメディアイベントを追跡できます。

サポートされるメソッドについて詳しくは、[`getMediaAnalyticsTracker`](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/getmediaanalyticstracker) のドキュメントを参照してください。

以下のスニペットは、Media JS でメディアトラッカーインスタンスを取得する方法を示しています。

```javascript
var tracker = ADB.Media.getInstance();
```

代わりに、Web SDKで `getMediaAnalyticsTracker` コマンドを使用して、同じ結果を得ることができます（下図を参照）。

```js
// aquire Media Analytics APIs
const Media = await window.alloy("getMediaAnalyticsTracker", {});
// create a media tracker instance
const trackerInstance = Media.getInstance();
```

すべてのヘルパーメソッドは、`Media` オブジェクトで使用できます。 トラッカーメソッドは、以下に示すように、トラッカーインスタンスで使用できます。

```js
const mediaInfo = Media.createMediaObject(
  "video name",
  "player video",
  60,
  Media.StreamType.VOD,
  Media.MediaType.Video
);

const contextData = {
  isUserLoggedIn: "false",
  tvStation: "Sample TV station",
  programmer: "Sample programmer",
  assetID: "/uri-reference"
};

// Set standard Video Metadata
contextData[Media.VideoMetadataKeys.Episode] = "Sample Episode";
contextData[Media.VideoMetadataKeys.Show] = "Sample Show";

trackerInstance.trackSessionStart(mediaInfo, contextData);
```
