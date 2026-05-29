---
title: JavaScript 3.x Media SDK API リファレンス
description: Media SDK JavaScript 3.x （ADB.MediaおよびADB.MediaConfig クラス）のAPI リファレンス。
feature: Streaming Media
role: User, Admin, Developer
exl-id: c3f8a2b5-1d4e-4f9a-8c7b-3a2d1f0e9b6c
source-git-commit: 1022e0851d58db0c9b523ebb7b52d379239a2e07
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 17%

---


# JavaScript 3.x Media SDK API リファレンス

>[!BEGINSHADEBOX]

このページでは、Analytics専用のJavaScript 3.x SDKについて説明します。 推奨される実装については、[Edge Networkを使用したストリーミングメディアの実装](/help/implementation/edge/edge-web-sdk.md)を参照してください。

>[!ENDSHADEBOX]

## ADB.Media

### 静的メソッド

+++configure

追跡用にMediaSDKを設定します。 このメソッドは、ページにトラッカーインスタンスを作成する前に1回呼び出す必要があります。

**構文**

```javascript
ADB.Media.configure(mediaConfig, appMeasurement);
```

| 変数名 | タイプ | 説明 |
|---|---|---|
| `mediaConfig` | `ADB.MediaConfig` | 有効なメディア設定 |
| `appMeasurement` | オブジェクト | AppMeasurement インスタンス |

**例**

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

+++

+++getInstance

再生セッションを追跡するメディアのインスタンスを作成します。 メディアを設定する前に呼び出された場合、`null`を返します。

**構文**

```javascript
ADB.Media.getInstance(trackerConfig)
```

| 変数名 | タイプ | 必須 | 説明 |
| :--- | :--- | :---: | :--- |
| `trackerConfig` | トラッカー設定 | いいえ | トラッカー設定オブジェクト。 |

**例**

```javascript
var tracker = ADB.Media.getInstance();
```

トラッカーインスタンスごとに`channel`または`playerName`を上書きするには、トラッカー設定オブジェクトで上書き値を渡します。

**トラッカー設定の例**

```javascript
const trackerConfig = {
  [Media.TrackerConfig.Channel]: "custom_channel_name",
  [Media.TrackerConfig.PlayerName]: "custom_player_name",
}
this._mediaTracker = Media.getInstance(trackerConfig);
```

+++

+++createMediaObject

メディア情報を含むオブジェクトを作成します。 無効なパラメーターが渡された場合は、空のオブジェクトを返します。

**構文**

```javascript
ADB.Media.createMediaObject(name, id, length, streamType, mediaType)
```

| 変数名 | タイプ | 説明 |
| :--- | :--- | :--- |
| `name` | string | メディア名を示す空でない文字列 |
| `id` | string | 一意のメディア識別子を示す空でない文字列 |
| `length` | number | メディアの長さを秒単位で示す正の数。 長さが不明な場合は`0`を使用します。 |
| `streamType` | string | メディアストリームタイプを示すストリームタイプまたは空でない文字列。 |
| `mediaType` | メディアタイプ | メディアの種類（オーディオまたはビデオ） |

**例**

```javascript
var mediaObject = ADB.Media.createMediaObject("video-name",
                                              "video-id",
                                              60.0,
                                              ADB.Media.StreamType.VOD,
                                              ADB.Media.MediaType.Video);
```

+++

+++createAdBreakObject

アドブレーク情報を含むオブジェクトを作成します。 無効なパラメーターが渡された場合は、空のオブジェクトを返します。

**構文**

```javascript
ADB.Media.createAdBreakObject(name, position, startTime);
```

| 変数名 | タイプ | 説明 |
| :--- | :--- | :--- |
| `name` | string | アドブレーク名（プレロール、ミッドロール、ポストロール）を示す空でない文字列 |
| `position` | number | コンテンツ内の広告ブレークの位置（1から始まる） |
| `startTime` | number | 広告ブレーク開始時の再生ヘッド値 |

**例**

```javascript
var adbreakObject = ADB.Media.createAdBreakObject("midroll", 2, 30.0);
```

+++

+++createAdObject

広告情報を含むオブジェクトを作成します。 無効なパラメーターが渡された場合は、空のオブジェクトを返します。

**構文**

```javascript
ADB.Media.createAdObject(name, id, position, length);
```

| 変数名 | タイプ | 説明 |
| :--- | :--- | :--- |
| `name` | string | 広告名を示す空でない文字列 |
| `id` | string | 広告IDを示す空でない文字列 |
| `position` | number | アドブレーク内の広告の位置（1から始まる） |
| `length` | number | 広告の長さを表す正の数 |

**例**

```javascript
var adObject = ADB.Media.createAdObject("ad-name", "ad-id", 1, 15.0)
```

+++

+++createChapterObject

章情報を含むオブジェクトを作成します。 無効なパラメーターが渡された場合は、空のオブジェクトを返します。

**構文**

```javascript
ADB.Media.createChapterObject(name, position, length, startTime)
```

| 変数名 | タイプ | 説明 |
| :--- | :--- | :--- |
| `name` | string | 章名を示す空でない文字列 |
| `position` | number | コンテンツ内の章の位置（1から始まる） |
| `length` | number | 章の長さを表す正の数 |
| `startTime` | number | チャプター開始時の再生ヘッド値 |

**例**

```javascript
var chapterObject = ADB.Media.createChapterObject("name", 1, 30.0, 0)
```

+++

+++createStateObject

状態情報を含むオブジェクトを作成します。 無効なパラメーターが渡された場合は、空のオブジェクトを返します。

**構文**

```javascript
ADB.Media.createStateObject(name)
```

| 変数名 | タイプ | 説明 |
| :--- | :--- | :--- |
| `name` | string | プレーヤーの状態または空でない文字列（状態名を示す） |

**例**

```javascript
var stateObject = ADB.Media.createStateObject("customstate");
```

+++

+++createQoEObject

QoE情報を含むオブジェクトを作成します。 無効なパラメーターが渡された場合は、空のオブジェクトを返します。

**構文**

```javascript
ADB.Media.createQoEObject(bitrate, startupTime, fps, droppedFrames)
```

| 変数名 | タイプ | 説明 |
| :--- | :--- | :--- |
| `bitrate` | number | 現在のビットレートを示す正の数値（不明な場合は0） |
| `startupTime` | number | 起動時間を示す正の数値（不明な場合は0） |
| `fps` | number | 現在のfpsを示す正の数（不明な場合は0） |
| `droppedFrames` | number | ドロップされたフレームの数を示す正の数（不明な場合は0） |

**例**

```javascript
qoeObject = ADB.Media.createQoEObject(10000000, 2, 23, 10);
```

+++

+++version

MediaSDK バージョンを返します。

**構文**

```javascript
ADB.Media.version
```

**例**

```javascript
console.log(ADB.Media.version);
```

+++

### インスタンスメソッド

+++trackSessionStart

再生を開始する意図を追跡します。 これにより、メディアトラッカーインスタンスでトラッキングセッションが開始されます。 メディアの再開も参照してください。

**構文**

```javascript
ADB.Media.trackSessionStart(mediaObject, contextData);
```

| 変数名 | 説明 | 必須 |
| :--- | :--- | :---: |
| `mediaObject` | `createMediaObject` メソッドを使用して作成されたメディア情報。 | はい |
| `contextData` | オプションのメディアコンテキストデータ： 標準メタデータキーの場合は、標準ビデオ定数または標準オーディオ定数を使用します。 | いいえ |

**例**

```javascript
var mediaObject = ADB.Media.createMediaObject("media-name", "media-id", 60, ADB.Media.StreamType.VOD, ADB.Media.MediaType.Video);

var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Episode] = "Sample Episode";
contextData[ADB.Media.VideoMetadataKeys.Show] = "Sample Show";
contextData["isUserLoggedIn"] = "false";
contextData["tvStation"] = "Sample TV Station";

tracker.trackSessionStart(mediaObject, contextData);
```

+++

+++trackPlay

前回の一時停止の後にメディアの再生または再開を追跡します。

**構文**

```javascript
ADB.Media.trackPlay();
```

**例**

```javascript
tracker.trackPlay();
```

+++

+++trackPause

メディアの一時停止を追跡します。

**構文**

```javascript
ADB.Media.trackPause();
```

**例**

```javascript
tracker.trackPause();
```

+++

+++trackComplete

トラックメディアが完了しました。 このメソッドは、メディアが完全に表示された場合にのみ呼び出します。

**構文**

```javascript
ADB.Media.trackComplete();
```

**例**

```javascript
tracker.trackComplete();
```

+++

+++trackSessionEnd

視聴セッションの終了を追跡します。 ユーザーが完了するメディアを表示しない場合でも、このメソッドを呼び出します。

**構文**

```javascript
ADB.Media.trackSessionEnd();
```

**例**

```javascript
tracker.trackSessionEnd();
```

+++

+++trackError

メディア再生のエラーを追跡します。

**構文**

```javascript
ADB.Media.trackError(errorId);
```

| 変数名 | 説明 | 必須 |
| :--- | :--- | :---: |
| `errorId` | エラー情報を含む空でない文字列 | はい |

**例**

```javascript
tracker.trackError("errorId");
```

+++

+++trackEvent

メディアイベントを追跡する方法。

| 変数名 | 説明 |
| :--- | :--- |
| `event` | メディアイベント |
| `info` | `AdBreakStart` イベントの場合、アドブレーク情報は`createAdBreakObject` メソッドを使用して作成されます。 `AdStart` イベントの場合、広告情報は`createAdObject` メソッドを使用して作成されます。 `ChapterStart` イベントの場合、章情報は`createChapterObject` メソッドを使用して作成されます。 `StateStart`および`StateEnd` イベントの場合、状態情報は`createStateObject` メソッドを使用して作成されます。 これは他のイベントでは必要ありません。 |
| `contextData` | `AdStart`および`ChapterStart` イベントに対して、オプションのコンテキストデータを指定できます。 これは他のイベントでは必要ありません。 |

**構文**

```javascript
ADB.Media.trackEvent(event, info, contextData);
```

**例**

**AdBreaksのトラッキング**

```javascript
// AdBreakStart
  var adBreakObject = ADB.Media.createAdBreakObject("preroll", 1, 0)
  tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakObject);

// AdBreakComplete
  tracker.trackEvent(ADB.Media.Event.AdBreakComplete);
```

**広告のトラッキング**

```javascript
// AdStart
  var adObject = ADB.Media.createAdObject("ad-name", "ad-id", 1, 15.0);

  var adMetadata = {};
  // Standard metadata keys provided by adobe.
  adMetadata[ADB.Media.AdMetadataKeys.Advertiser]  ="Sample Advertiser";
  adMetadata[ADB.Media.AdMetadataKeys.CampaignId] = "Sample Campaign";
  // Custom metadata keys
  adMetadata["affiliate"] = "Sample affiliate";

  tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);

// AdComplete
  tracker.trackEvent(ADB.Media.Event.AdComplete);

// AdSkip
  tracker.trackEvent(ADB.Media.Event.AdSkip);
```

**章のトラッキング**

```javascript
// ChapterStart
  var chapterObject = ADB.Media.createChapterObject("chapter-name", 1, 60.0, 15.0);

  var chapterMetadata = {};
  chapterMetadata["segmentType"] = "Sample segment type";

  tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterObject, chapterMetadata);

// ChapterComplete
  tracker.trackEvent(ADB.Media.Event.ChapterComplete);

// ChapterSkip
  tracker.trackEvent(ADB.Media.Event.ChapterSkip);
```

**状態のトラッキング**

```javascript
// StateStart (ex: Mute is switched on)
  var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
  tracker.trackEvent(ADB.Media.Event.StateStart, stateObject);

// StateEnd (ex: Mute is switched off)
  tracker.trackEvent(ADB.Media.Event.StateEnd, stateObject);
```

**再生イベントのトラッキング**

```javascript
// BufferStart
  tracker.trackEvent(ADB.Media.Event.BufferStart);

// BufferComplete
  tracker.trackEvent(ADB.Media.Event.BufferComplete);

// SeekStart
  tracker.trackEvent(ADB.Media.Event.SeekStart);

// SeekComplete
  tracker.trackEvent(ADB.Media.Event.SeekComplete);
```

**ビットレート変更のトラッキング**

```javascript
// If the new bitrate value is available provide it to the tracker.
  var qoeObject = ADB.Media.createQoEObject(1000000, 2.4, 25, 10);
  tracker.updateQoEObject(qoeObject);

// Bitrate change
  tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

+++

+++updatePlayhead

現在のメディア再生ヘッドをメディアトラッカーに提供します。 正確なトラッキングを行うには、再生中に再生ヘッドが変更されるたびに、このメソッドを呼び出します。

**構文**

```javascript
ADB.Media.updatePlayhead(time);
```

| 変数名 | 説明 |
| :--- | :--- |
| `time` | 現在の再生ヘッド （秒単位）。 ビデオオンデマンド（VOD）の場合、値はメディア項目の先頭から秒単位で指定されます。 ライブストリーミングの場合、プレーヤーがコンテンツ時間に関する情報を提供しない場合、その日の午前0時UTCからの秒数として値を指定できます。 メモ：プログレスマーカーを使用する場合、コンテンツのデュレーションが必要です。また、再生ヘッドはメディアアイテムの先頭からの（0 から始まる）秒数で更新する必要があります。 |

**例**

```javascript
tracker.updatePlayhead(13.3);

// For live streams
var UTCTimeInSeconds = Math.floor(Date.now() / 1000)
var timeFromMidnightInSecond = UTCTimeInSeconds % 86400

tracker.updatePlayhead(timeFromMidnightInSecond);
```

+++

+++updateQoEObject

現在のQoE情報をメディアトラッカーに提供します。 正確なトラッキングを行うには、メディアプレーヤーが更新されたQoE情報を提供する際に、このメソッドを複数回呼び出します。

**構文**

```javascript
ADB.Media.updateQoEObject(qoeObject);
```

| 変数名 | 説明 |
| :--- | :--- |
| `qoeObject` | `createQoEObject` メソッドを使用して作成された現在のQoE情報。 |

**例**

```javascript
var qoeObject = ADB.Media.createQoEObject(1000000, 2.4, 25, 10);
tracker.updateQoEObject(qoeObject);
```

+++

+++破棄

トラッカーインスタンスを破棄します。

**構文**

```javascript
ADB.Media.destroy();
```

**例**

```javascript
tracker.destroy();
```

+++

### 定数

+++トラッカー設定

トラッカーインスタンスごとに設定できる設定キーを定義します。

```javascript
ADB.Media.TrackerConfig = {
  Channel: "media.channel",
  PlayerName: "media.playerName"
}
```

+++

+++メディアタイプ

現在追跡されているメディアのタイプを定義します。

```javascript
ADB.Media.MediaType = {
  Video: "video",
  Audio: "audio"
}
```

+++

+++ストリームタイプ

現在追跡されているコンテンツのストリームタイプを定義します。

```javascript
ADB.Media.StreamType = {
  VOD: "vod",
  Live: "live",
  Linear: "linear",
  Podcast: "podcast",
  Audiobook: "audiobook",
  AOD: "aod"
}
```

+++

+++標準メタデータキー

`ADB.Media.VideoMetadataKeys`、`ADB.Media.AudioMetadataKeys`および`ADB.Media.AdMetadataKeys`は、標準メタデータのコンテキストデータキー文字列を提供します。 キーとそれに対応するレポート変数の完全なリストについては、[標準メタデータ変数リファレンス ](/help/implementation/variables/standard-metadata/show.md)を参照してください。

+++

+++メディアイベント

トラッキングイベントのタイプを定義します。

```javascript
ADB.Media.Event = {
  AdBreakStart: "adBreakStart",
  AdBreakComplete: "adBreakComplete",
  AdStart: "adStart",
  AdComplete: "adComplete",
  AdSkip: "adSkip",
  ChapterStart: "chapterStart",
  ChapterComplete: "chapterComplete",
  ChapterSkip: "chapterSkip",
  SeekStart: "seekStart",
  SeekComplete: "seekComplete",
  BufferStart: "bufferStart",
  BufferComplete: "bufferComplete",
  BitrateChange: "bitrateChange",
  StateStart: "stateStart",
  StateEnd: "stateEnd"
}
```

+++

+++プレイヤーの状態

プレーヤーの状態を追跡するための標準値を定義します。

```javascript
ADB.Media.PlayerState = {
  FullScreen: "fullScreen",
  ClosedCaption: "closedCaptioning",
  Mute: "mute",
  PictureInPicture: "pictureInPicture",
  InFocus: "inFocus"
}
```

+++

+++メディアの再開

現在のトラッキングセッションが、以前に閉じられたセッションを再開していることを示す定数。 この情報は、トラッキングセッションを開始する際に提供する必要があります。

**構文**

```javascript
ADB.Media.MediaObjectKey = {
  MediaResumed: "resumed"
}
```

**例**

```javascript
var mediaObject = ADB.Media.createMediaObject("media-name", "media-id", 60, ADB.Media.StreamType.VOD, ADB.Media.MediaType.Video);

mediaObject[ADB.Media.MediaObjectKey.MediaResumed] = true;

tracker.trackSessionStart(mediaObject);
```

+++

## ADB.MediaConfig

| キー | 必須 | 説明 |
| :--- | :--- | :--- |
| `trackingServer` | はい | ダウンロードしたメディアトラッキングデータを送信するメディア収集API サーバーの名前を入力します。 この情報を入手するには、Adobeの担当者にお問い合わせください。 |
| `channel` | いいえ | チャネル名プロパティ |
| `playerName` | いいえ | 使用中のメディアプレーヤーの名前 |
| `appVersion` | いいえ | Media Player アプリケーション/SDKのバージョンを入力します |
| `debugLogging` | いいえ | Media SDK ログを有効または無効にします（デフォルト値：`false`） |
| `ssl` | いいえ | SSL経由でping送信します（デフォルト値：`true`） |
