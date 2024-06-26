---
title: Adobe Experience Platform Web SDK を使用したEdgeへの web データの送信
description: Adobe Experience Platform Web SDK を使用して、AdobeストリーミングメディアデータをExperience PlatformEdgeに送信する方法について説明します。
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: de40ebd9-46be-4a52-866f-7bb2589fce28
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# Adobe Experience Platform Web SDK を使用したEdgeへの web データの送信

バージョン 2.20.0 以降、 `streamingMedia` Adobe Experience Platformコンポーネント [Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home) を使用すると、web サイト上のメディアセッションに関連するデータを収集できます。 収集されたデータには、メディアプレイバック、一時停止、完了およびその他の関連イベントに関する情報を含めることができます。

データを収集したら、Adobe Experience PlatformやAdobe Analyticsに送信し、レポートを生成できます。 この機能は、web サイトでのメディア消費行動を追跡および把握するための包括的なソリューションを提供します。

Media JS SDK を使用している顧客の場合、Web SDK は、Media JS SDK から Web SDK に移行するための移行パスを提供します。一方、メディアイベントの処理など、既存の Media JS 機能のサポートも含まれます。

## 前提条件 {#prerequisites}

を使用するには `streamingMedia` web SDK のコンポーネントです。次の前提条件を満たす必要があります。

* ストリーミングメディアデータをEdgeに送信する前に、まずの手順を実行します。 [Experience PlatformEdgeと Streaming Media Collection アドオンのインストール](/help/implementation/edge/implementation-edge.md).
* Adobe Experience PlatformやAdobe Analyticsにアクセスできることを確認します。
* Web SDK バージョン 2.20.0 以降を使用する必要があります。 を参照してください。 [Web SDK インストールの概要](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview) を参照して、最新バージョンのインストール方法を確認してください。
* を有効にする **[[!UICONTROL Media Analytics]](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)** 使用しているデータストリームのオプション。
* データストリームで使用するスキーマに、メディアコレクションのスキーマフィールドが含まれていることを確認してください。
* このページで示されているように、次のいずれかを使用して、Web SDK 設定でストリーミングメディア機能を設定します。 [タグ拡張機能](#tag-extension) または [JavaScript図書館](#library).

ストリーミングメディアコレクションアドオンの実装を Media JS から Web SDK に移行するには、このページで説明する手順に従います。

### 手順 1:Experience PlatformWeb SDK のインストール

を参照してください。 [専用ドキュメント](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview) web プロパティに Web SDK をインストールする方法を説明します。

### 手順 2:Web SDK の設定 `streamingMedia` コンポーネント。

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

代わりに、を設定する必要があります `streamingMedia` web SDK のコンポーネント（以下の例に示す）。

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

Web SDK を参照 `streamingMedia` component [詳細を見る](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/configure/streamingmedia) 設定方法について詳しくは、を参照してください。

### 手順 3:Media JS SDK から移行する際に、Media トラッカーインスタンスを取得する

Media JS SDK を使用している顧客の場合、Web SDK は、Media JS SDK から Web SDK に移行するための移行パスを提供します。一方、メディアイベントの処理など、既存の Media JS 機能のサポートも含まれます。

[!DNL Web SDK] media Analytics トラッカーを取得するコマンドが含まれています。 このコマンドを使用してオブジェクトインスタンスを作成し、から提供されるのと同じ API を使用することができます。 [Media JS ライブラリ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)、メディアイベントを追跡

を参照してください。 [`getMediaAnalyticsTracker`](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/getmediaanalyticstracker) サポートされる方法の詳細に関するドキュメント。

以下のスニペットは、Media JS でメディアトラッカーインスタンスを取得する方法を示しています。

```javascript
var tracker = ADB.Media.getInstance();
```

代わりに、を使用します `getMediaAnalyticsTracker` と Web SDK でコマンドを使用して、同じ結果を得ることができます（下図を参照）。

```js
// aquire Media Analytics APIs
const Media = await window.alloy("getMediaAnalyticsTracker", {});
// create a media tracker instance
const trackerInstance = Media.getInstance();
```

すべてのヘルパーメソッドは、 `Media` オブジェクト。 トラッカーメソッドは、以下に示すように、トラッカーインスタンスで使用できます。

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
