---
title: Adobe Experience Platform Web SDKを使用したEdgeへのweb データの送信
description: Adobe Experience Platform Web SDKを使用して、Adobe ストリーミングメディアデータをExperience Platform Edgeに送信する方法について説明します。
feature: Streaming Media
role: User, Admin, Developer
exl-id: de40ebd9-46be-4a52-866f-7bb2589fce28
TQID: https://experienceleague.adobe.com/yr1qlonZDoevoT-vFo-WknObsb-CegTihWEFZN5TdAE
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 563
ht-degree: 6%

---

# Adobe Experience Platform Web SDKを使用したEdgeへのweb データの送信

バージョン 2.20.0以降、Adobe Experience Platform [Web SDK](https://experienceleague.adobe.com/ja/docs/experience-platform/web-sdk/home)の`streamingMedia` コンポーネントを使用すると、web サイト上のメディアセッションに関連するデータを収集できます。 収集されたデータには、メディアの再生、一時停止、完了、その他の関連イベントに関する情報が含まれます。

データを収集した後、それをAdobe Experience PlatformやAdobe Analyticsに送信してレポートを生成できます。 この機能は、web サイトでのメディア消費行動を追跡および把握するための包括的なソリューションを提供します。

Media JS SDKを使用しているお客様に対しては、Web SDKは、Media JS SDKからWeb SDKへの移行パスを提供しますが、Media イベントの処理などの既存のMedia JS機能のサポートも含まれています。

## 前提条件 {#prerequisites}

Web SDKの`streamingMedia` コンポーネントを使用するには、次の前提条件を満たす必要があります。

* Edgeにストリーミングメディアデータを送信する前に、まず[Edge Networkを使用したAdobe ストリーミングメディアサービスの実装](/help/implementation/edge/implementation-edge.md)の手順を完了してください。
* Adobe Experience PlatformやAdobe Analyticsへのアクセス権があることを確認します。
* Web SDK バージョン 2.20.0以降を使用する必要があります。 最新バージョンのインストール方法については、[Web SDK インストールの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/web-sdk/install/overview)を参照してください。
* 使用しているデータストリームの&#x200B;**[[!UICONTROL Media Analytics]](https://experienceleague.adobe.com/ja/docs/experience-platform/datastreams/configure)** オプションを有効にします。
* データストリームで使用されるスキーマに、メディア収集スキーマフィールドが含まれていることを確認します。
* このページに示すように、[&#x200B; タグ拡張機能](#tag-extension)または[JavaScript ライブラリ &#x200B;](#library)を使用して、Web SDK設定でストリーミングメディアサービスを設定します。

このページで説明する手順に従って、ストリーミングメディアサービスの実装をMedia JSからWeb SDKに移行します。

### 手順1:Experience Platform Web SDKのインストール

Web プロパティにWeb SDKをインストールする方法については、[専用ドキュメント &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/web-sdk/install/overview)を参照してください。

### 手順2: Web SDK `streamingMedia` コンポーネントを構成します。

**例**

次のスニペットは、Media JSでのメディア収集の設定方法を示しています。

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

代わりに、以下に示すように、Web SDKの`streamingMedia` コンポーネントを設定する必要があります。

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

構成方法の詳細については、Web SDK `streamingMedia` コンポーネント [&#x200B; ドキュメント &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/web-sdk/commands/configure/streamingmedia)を参照してください。

### 手順3:Media JS SDKから移行する際にMedia Tracker インスタンスを取得する

Media JS SDKを使用しているお客様に対しては、Web SDKは、Media JS SDKからWeb SDKへの移行パスを提供しますが、Media イベントの処理などの既存のMedia JS機能のサポートも含まれています。

Web SDKには、[`getMediaAnalyticsTracker`](https://experienceleague.adobe.com/ja/docs/experience-platform/web-sdk/commands/getmediaanalyticstracker) コマンドが含まれており、これを使用してオブジェクトインスタンスを作成できます。 次に、[3.x Media SDK](/help/implementation/media-sdk/setup/js-3x-api-reference.md)が提供するAPIと同じAPIを使用して、メディアイベントを追跡できます。

以下のスニペットは、Media JSでメディアトラッカーインスタンスを取得する方法を示しています。

```javascript
var tracker = ADB.Media.getInstance();
```

代わりに、Web SDKで`getMediaAnalyticsTracker` コマンドを使用して、次に示すように、同じ結果を得ます。

```js
// aquire Media Analytics APIs
const Media = await window.alloy("getMediaAnalyticsTracker", {});
// create a media tracker instance
const trackerInstance = Media.getInstance();
```

すべてのヘルパーメソッドは、`Media` オブジェクトで利用できます。 トラッカーのメソッドは、以下に示すように、トラッカーインスタンスで使用できます。

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
