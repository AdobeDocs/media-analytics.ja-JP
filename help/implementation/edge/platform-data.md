---
title: XDM レポートスキーマ
description: Adobe Experience PlatformでExperience Eventsを生成するMedia Edge API イベントと、MediaReporting XDM スキーマを使用して実装を検証する方法について説明します。
feature: Streaming Media
role: User, Admin, Developer
exl-id: c3a4d31b-8f9e-4d7a-9b2e-1a5f0e8c7d39
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 267532dfbe6dc3f7bcff0991536ae3baf6eff053
workflow-type: tm+mt
source-wordcount: 763
ht-degree: 4%

---


# XDM レポートスキーマ

Adobe Experience Platform Edge Networkを使用してメディアトラッキングイベントを送信する場合、Media Analytics バックエンドは、それらのイベントを処理し、計算されたエクスペリエンスイベントをPlatform データセットに書き込みます。 どのイベントがAdobe Experience Platformに到達し、どのようなバックエンド処理が必要になるかを把握することは、Customer Journey AnalyticsやAdobe Analyticsでの実装を検証し、正確なレポートを作成するのに役立ちます。

2つの異なるXDM スキーマが、コレクションとレポートパイプラインの異なる部分で使用されます。

| スキーマ | 名前空間 | 方向 | 目的 |
|---|---|---|---|
| メディアコレクション | `xdm.mediaCollection` | Client → Adobe | 各トラッキングイベントに対してプレイヤーが送信する情報。 [変数](/help/implementation/variables/)によって使用されます。 |
| メディアレポート | `xdm.mediaReporting` | Adobe → Platform | バックエンドが処理後にデータセットに書き込むもの。 [&#x200B; ディメンション &#x200B;](/help/reporting/dimensions/overview.md)および[指標](/help/reporting/metrics/overview.md)によって使用されます。 |

`mediaReporting`に存在するが、`mediaCollection` ペイロードに存在しないフィールドは、セッション内のイベントの完全なシーケンスから派生します。 これらのフィールドは、Adobeによって生成されます。

## Platform データセットに書き込むイベント

追跡可能な12種類のイベントタイプのうち、データセットに書き込む個々のエクスペリエンスイベントを生成するのは5種類のみです。

| イベントタイプ | データセットに含まれる | メモ |
|---|---|---|
| [&#x200B; セッション開始](/help/implementation/events/session/session-start.md) | はい | セッションが初期化されたときに書かれます |
| [広告の開始](/help/implementation/events/ads/ad-start.md) | はい | 個々の広告が開始されたときに作成されます |
| [Ad complete](/help/implementation/events/ads/ad-complete.md) | はい | 広告が完了するまで再生されるときに記述されます |
| [章完了](/help/implementation/events/chapters/chapter-complete.md) | はい | 章が完了するまで再生されるときに書かれます |
| [&#x200B; セッション完了](/help/implementation/events/session/session-complete.md) | はい | セッションが終了したときに書き込まれます。最も豊富な計算フィールドセット |
| [&#x200B; プレイ &#x200B;](/help/implementation/events/playback/play.md) | いいえ | `timePlayed`の計算に使用 |
| [開始を一時停止](/help/implementation/events/playback/pause-start.md) | いいえ | `pauseCount`と`pauseTime`の計算に使用しました |
| [Ping](/help/implementation/events/playback/ping.md) | いいえ | ハートビート。セッションが非アクティブであることを検出するために使用されます |
| [&#x200B; バッファー開始](/help/implementation/events/playback/buffer-start.md) | いいえ | QoE バッファー指標の計算に使用 |
| [&#x200B; ビットレート変更](/help/implementation/events/playback/bitrate-change.md) | いいえ | QoE ビットレート指標の計算に使用 |
| [状態の開始](/help/implementation/events/player-state/state-start.md) | いいえ | プレーヤーの状態指標の計算に使用されます |
| [&#x200B; エラー](/help/implementation/events/error.md) | いいえ | QoEで`errorCount`を計算するために使用 |

## バックエンドで計算されたフィールド

次のフィールドは`mediaReporting` ペイロードに表示されますが、コレクションペイロードの一部ではありません。 バックエンドでは、イベント全体のシーケンスからバックエンドを導き出します。

**セッションレベル** （`sessionComplete`に表示）:

| フィールド | 説明 |
|---|---|
| `xdm.mediaReporting.sessionDetails.timePlayed` | 広告を除く、再生されたメインコンテンツの合計秒数 |
| `xdm.mediaReporting.sessionDetails.totalTimePlayed` | 広告を含む合計経過秒数 |
| `xdm.mediaReporting.sessionDetails.uniqueTimePlayed` | 重複排除された秒：複数回閲覧されたインターバルは1回のみカウントされます |
| `xdm.mediaReporting.sessionDetails.averageMinuteAudience` | `timePlayed`をコンテンツの長さで割りました |
| `xdm.mediaReporting.sessionDetails.estimatedStreams` | 推定される同時ストリーム |
| `xdm.mediaReporting.sessionDetails.adCount` | 開始した広告の数 |
| `xdm.mediaReporting.sessionDetails.chapterCount` | 開始した章の数 |
| `xdm.mediaReporting.sessionDetails.pauseCount` / `xdm.mediaReporting.sessionDetails.pauseTime` | 一時停止の頻度と合計一時停止の期間 |
| `xdm.mediaReporting.sessionDetails.hasProgress10` ... `xdm.mediaReporting.sessionDetails.hasProgress95` | 進捗マイルストーンフラグ （10%、25%、50%、75%、95%） |
| `xdm.mediaReporting.sessionDetails.hasSegmentView` | 少なくとも1 フレームのコンテンツが表示されたかどうか |
| `xdm.mediaReporting.sessionDetails.isCompleted` / `xdm.mediaReporting.sessionDetails.isPlayed` | 完了フラグと開始フラグ |
| `xdm.mediaReporting.sessionDetails.secondsSinceLastCall` | 最後のpingからセッション終了までの時間 |
| `xdm.mediaReporting.sessionDetails.segment` | コンテンツセグメントブラケット （例：`[0-1]`） |

**広告レベル** （`adComplete`に表示）:

| フィールド | 説明 |
|---|---|
| `xdm.mediaReporting.advertisingDetails.timePlayed` | 広告コンテンツの再生時間（秒） |
| `xdm.mediaReporting.advertisingDetails.isCompleted` | 広告が完了するまで再生されたかどうか |

**章レベル** （`chapterComplete`に表示）:

| フィールド | 説明 |
|---|---|
| `xdm.mediaReporting.chapterDetails.timePlayed` | 章コンテンツの再生時間（秒） |
| `xdm.mediaReporting.chapterDetails.isCompleted` | 章が完了するまで再生されたかどうか |
| `xdm.mediaReporting.chapterDetails.isStarted` | 章が開始されたかどうか |

**QoE** （`sessionComplete`に集計）:

| フィールド | 説明 |
|---|---|
| `xdm.mediaReporting.qoeDataDetails.bitrateAverage` | セッション全体の平均ビットレート |
| `xdm.mediaReporting.qoeDataDetails.bitrateAverageBucket` | バケット化された平均ビットレート範囲 |
| `xdm.mediaReporting.qoeDataDetails.bitrateChangeCount` | ビットレートの変更数 |
| `xdm.mediaReporting.qoeDataDetails.errorCount` | エラー数 |
| `xdm.mediaReporting.qoeDataDetails.droppedFrames` | ドロップされたフレームの合計 |
| `xdm.mediaReporting.qoeDataDetails.playerSdkErrors` | プレーヤーのエラーコードの配列 |
| `xdm.mediaReporting.qoeDataDetails.hasErrorImpactedStreams` | エラーが発生したかどうか |
| `xdm.mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams` | ドロップしたフレームが発生したかどうか |
| `xdm.mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams` | ビットレートの変更が発生したかどうか |

## ダウンロード済みコンテンツ

[&#x200B; ダウンロード済みエンドポイント &#x200B;](/help/use-cases/track-downloaded-content.md)を使用して追跡されたセッションの場合、バックエンドは`sessionStart`のレポートイベントに`xdm.mediaReporting.sessionDetails.isDownloaded`から`true`に自動的に設定します。 ダウンロードされたセッションの他のすべてのレポートイベントは、ライブセッションと同じスキーマに従います。 CJAまたはAdobe Analyticsのこのフィールドを使用して、ダウンロードした再生をフィルタリングまたはセグメント化します。

コレクションの実装の詳細については、Media Edge API リファレンスの[&#x200B; ダウンロード済みエンドポイント &#x200B;](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/downloaded/)を参照してください。

## 実装の検証

Media Edge APIを介してイベントを送信した後、次のいずれかの方法を使用してデータが正しく検出されたかどうかを確認します。

**Adobe Experience Platform データセット プレビュー**

1. [CX Enterprise](https://experience.adobe.com)で、**[!UICONTROL データセット]**&#x200B;に移動し、ストリーミングメディアデータセットを選択します。
2. **[!UICONTROL データセットのプレビュー]**&#x200B;を選択すると、最近取り込まれたエクスペリエンスイベントが表示されます。
3. `media.sessionStart`や`media.sessionComplete`などの`eventType`の値が、入力された`mediaReporting` フィールドに表示されていることを確認します。

**Customer Journey Analytics データセット インスペクション**

1. CJAで、ストリーミングメディアデータセットに関連付けられている接続を開きます。
2. 「**データセットを追加**」を選択し、スキーマを調べて、`mediaReporting` フィールドが期待されるディメンションと指標にマッピングされていることを確認します。

**Adobe Analyticsの処理ルール （Analyticsの宛先を使用している場合）**

Analytics ソースコネクタを介してデータを受け取るAdobe Analytics レポートスイートの場合、処理ルールを使用して、`mediaReporting`個のコンテキストデータ変数をカスタム propまたはeVarにマッピングできます。 `isDownloaded` フラグは`a.media.downloaded`として利用できます。

## XDM ペイロードの例

次の例は、Platform データセットに書き込まれた各レポートイベントの完全な`mediaReporting` XDM構造を示しています。 `_{tenantName}` プロパティは、任意のカスタムフィールドに対する組織のテナント名前空間を表します。

+++media.sessionStart

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "mediaReporting": {
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "isViewed": true,
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "hasResume": false,
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.sessionStart",
    "_id": "0[...]0",
    "timestamp": "YYYY-11-20T12:43:35Z"
  }
}
```

+++

+++media.adStart

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "environment": {
      "browserDetails": {},
      "ipV4": "130.248.81.10"
    },
    "mediaReporting": {
      "advertisingDetails": {
        "advertiser": "Adobe Marketing",
        "podPosition": 1,
        "placementID": "placementID",
        "example": "https://example.com",
        "playerName": "HTML5 player",
        "campaignID": "Adobe Analytics",
        "name": "/uri-reference/001",
        "length": 10,
        "siteID": "siteID",
        "isStarted": true,
        "creativeID": "creativeID",
        "friendlyName": "Ad 1"
      },
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "pev3": "videoAd",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      },
      "advertisingPodDetails": {
        "offset": 0,
        "ID": "3d594614f445f6b00014e9b77730b833_1",
        "friendlyName": "Mid-ad"
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.adStart",
    "_id": "d[...]0",
    "timestamp": "YYYY-11-20T12:43:56Z"
  }
}
```

+++

+++media.adComplete

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "mediaReporting": {
      "advertisingDetails": {
        "advertiser": "Adobe Marketing",
        "podPosition": 1,
        "placementID": "placementID",
        "example": "https://example.com",
        "playerName": "HTML5 player",
        "campaignID": "Adobe Analytics",
        "length": 10,
        "creativeID": "creativeID",
        "timePlayed": 7,
        "name": "/uri-reference/001",
        "siteID": "siteID",
        "friendlyName": "Ad 1",
        "isCompleted": true
      },
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "pev3": "videoAd",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      },
      "advertisingPodDetails": {
        "offset": 0,
        "ID": "3d594614f445f6b00014e9b77730b833_1",
        "friendlyName": "Mid-ad"
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.adComplete",
    "_id": "f[...]0",
    "timestamp": "YYYY-11-20T12:44:03Z"
  }
}
```

+++

+++media.chapterComplete

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2",
      "customTest": "myCustomValue1"
    },
    "environment": {
      "browserDetails": {},
      "ipV4": "130.248.81.10"
    },
    "mediaReporting": {
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "pev3": "video",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      },
      "chapterDetails": {
        "timePlayed": 10,
        "offset": 0,
        "length": 10,
        "index": 1,
        "ID": "3d594614f445f6b00014e9b77730b833_1",
        "isStarted": true,
        "friendlyName": "Chapter 1",
        "isCompleted": true
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.chapterComplete",
    "_id": "a[...]0",
    "timestamp": "YYYY-11-20T12:44:24Z"
  }
}
```

+++

+++media.sessionComplete

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "environment": {
      "browserDetails": {},
      "ipV4": "130.248.81.10"
    },
    "mediaReporting": {
      "qoeDataDetails": {
        "playerSdkErrors": ["test-buffer-start"],
        "bitrateAverageBucket": "0-99",
        "bitrateChangeCount": 1,
        "droppedFrames": 30,
        "hasErrorImpactedStreams": true,
        "hasBitrateChangeImpactedStreams": true,
        "hasDroppedFrameImpactedStreams": true,
        "bitrateAverage": 35,
        "timeToStart": 1,
        "errorCount": 1
      },
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "hasProgress10": true,
        "pev3": "video",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "episode": "4933",
        "pauseTime": 3,
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "segment": "[0-1]",
        "season": "1521",
        "showType": "sitcom",
        "pauseCount": 1,
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "uniqueTimePlayed": 47,
        "totalTimePlayed": 55,
        "author": "test-author",
        "hasProgress25": true,
        "feed": "sourceFeed",
        "timePlayed": 48,
        "name": "test-name",
        "publisher": "test-media-publisher",
        "hasPauseImpactedStreams": true,
        "averageMinuteAudience": 0.48,
        "artist": "test-artist",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "hasSegmentView": true,
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "friendlyName": "test-friendly-name",
        "isCompleted": true,
        "playerName": "HTML5 player",
        "album": "test-album",
        "chapterCount": 1,
        "length": 100,
        "adCount": 1,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "secondsSinceLastCall": 51,
        "assetID": "/uri-reference",
        "isPlayed": true,
        "estimatedStreams": 1,
        "firstDigitalDate": "releaseDate"
      },
      "states": [
        {
          "isSet": true,
          "name": "mute",
          "count": 1,
          "time": 3
        },
        {
          "isSet": true,
          "name": "pictureInPicture",
          "count": 1,
          "time": 3
        }
      ]
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.sessionComplete",
    "_id": "a[...]0",
    "timestamp": "YYYY-11-20T12:44:40Z"
  }
}
```

+++

+++media.sessionStart （ダウンロード済みコンテンツ）

[&#x200B; ダウンロード済みエンドポイント &#x200B;](/help/use-cases/track-downloaded-content.md)を使用して追跡されたセッションは、同じレポートスキーマに従い、1つの主な違いがあります。`xdm.mediaReporting.sessionDetails.isDownloaded`は、`sessionStart` レポートイベントで`true`に設定されています。 その他のすべてのイベントタイプは、上記のライブコンテンツの例と同じです。

```json
{
  "xdm": {
    "mediaReporting": {
      "customMetadata": [
        {
          "name": "customData",
          "value": "example"
        }
      ],
      "playhead": 0,
      "sessionDetails": {
        "ID": "d8a25708a6b0be83975e32e2f422105ed62f51ff67e6d82d898657534ab9244f",
        "channel": "channel",
        "contentType": "VOD",
        "length": 100,
        "name": "123456789",
        "playerName": "playerName",
        "isDownloaded": true
      }
    },
    "eventType": "media.sessionStart",
    "timestamp": "YYYY-09-26T15:52:24Z",
    "identityMap": {
      "ECID": [
        {
          "id": "51910389753901685456014889838591030721"
        }
      ]
    },
    "implementationDetails": {
      "version": "0.0.1",
      "environment": "browser",
      "name": "https://ns.adobe.com/experience/edge"
    }
  }
}
```

+++
