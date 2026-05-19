---
title: SDK のデバッグ
description: Media SDK で使用できるトラッキングとログについて説明します。
uuid: a5972d87-c593-4b4f-a56f-dca6e25268e1
exl-id: c2de6454-8538-4d07-a099-e278b153d894
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/H62IoGbWZ3JPApfb-wFlt9P-oa3rD1kCzalpXEQ4Km0
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: e992d880-33bc-4949-a648-aa7d410276cd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 221
ht-degree: 100%

---

# SDK のデバッグ{#sdk-debugging}

ログを有効／無効にすることができます。 メディア SDK では、メディアトラッキングスタック全体にわたる広範なトレース／ログメカニズムを提供します。 Config オブジェクトの `debugLogging` フラグを設定することで、ログを有効または無効にできます。

## デバッグログのサンプルコード

### Android

```java
// Media Heartbeat initialization
MediaHeartbeatConfig config = new MediaHeartbeatConfig();
config.debugLogging = true;

// Use this space for setting other config values
MediaHeartbeat _heartbeat = new MediaHeartbeat(this, config);
```

### iOS

```
// Media Heartbeat Initialization
ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init];
config.debugLogging = YES;

// Use this space for setting other config values
ADBMediaHeartbeat *_mediaHeartbeat =  
[[ADBMediaHeartbeat alloc] initWithDelegate:self config:config];
```

### JavaScript

```js
// Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
mediaConfig.debugLogging = true;
this._mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
```

### OTT（Chromecast、Roku）

ADBMobile ライブラリでは、`setDebugLogging` メソッドを利用してデバッグのログを記録できます。 すべての実稼働アプリケーションに対してデバッグのログを `false` に設定してください。

#### Roku

```
ADBMobile().setDebugLogging(true)
```

#### Chromecast

```
ADBMobile.config.setDebugLogging(true)
```

## ログメッセージ

以下に、ログメッセージの形式を示します。

```js
Format: [<timestamp>] [<level>] [<tag>] [<message>]
Example: [16:10:29 GMT­0700 (PDT).245] [DEBUG] [plugin::player] Resolving qos.startupTime: 0
```

* **timestamp：**&#x200B;現在の CPU 時間です（タイムゾーンは GMT）。
* **level：** 4 つのメッセージレベルが定義されています。
   * INFO（情報）- 通常、アプリケーションからの入力データ（プレーヤー名、ビデオ ID などの検証）
   * DEBUG（デバッグ）- 開発者がより複雑な問題をデバッグするために使用する、デバッグログ
   * WARN（警告）- 潜在的な統合／設定エラーまたはハートビート SDK バグを示す
   * ERROR（エラー）- 重要な統合エラーまたはハートビート SDK バグを示す
* **tag：**&#x200B;ログメッセージを発行したサブコンポーネントの名前（通常、クラス名）
* **message：**&#x200B;実際のトレースメッセージ

メディア SDK ライブラリのログ出力を使用して、実装を検証できます。 文字列 `#track` についてログ全体を検索するとよいでしょう。 これにより、アプリケーションによって呼び出されたすべての `track*()` をハイライトします。

例えば、`#track` でフィルターしたログは以下のようになります。

```js
[16:10:29 GMT­0700 (PDT).222] [INFO] [plugin::player] #trackVideoLoad()
[16:10:29 GMT­0700 (PDT).230] [INFO] [plugin::player] #trackSessionStart()
[16:10:29 GMT­0700 (PDT).250] [INFO] [plugin::player] #trackPlay()
[16:10:29 GMT­0700 (PDT).759] [INFO] [plugin::player] #trackChapterStart()
[16:10:44 GMT­0700 (PDT).769] [INFO] [plugin::player] #trackAdStart()
[16:10:59 GMT­0700 (PDT).752] [INFO] [plugin::player] #trackAdComplete()
[16:10:59 GMT­0700 (PDT).770] [INFO] [plugin::player] #trackChapterStart()
[16:11:29 GMT­0700 (PDT).734] [INFO] [plugin::player] #trackPause()
[16:11:29 GMT­0700 (PDT).764] [INFO] [plugin::player] #trackComplete()
[16:11:29 GMT­0700 (PDT).766] [INFO] [plugin::player] #trackVideoUnload()
```
