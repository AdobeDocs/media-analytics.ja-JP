---
title: SDK のデバッグ
description: このトピックでは、Media SDKで使用できるトラッキング/ログについて説明します。
uuid: a5972d87-c593-4b4f-a56f-dca6e25268e1
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# SDK のデバッグ{#sdk-debugging}

ログを有効または無効にすることができます。 Media SDKは、メディアトラッキングスタック全体に広範なトレース/ログメカニズムを提供します。 You can enable or disable logging by setting the `debugLogging` flag on the Config object.

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

### OTT(Chromecast、Roku)

ADBMobile ライブラリでは、`setDebugLogging` メソッドを利用してデバッグのログを記録できます。すべての実稼働アプリケーションに対してデバッグのログを `false` に設定してください。

#### Roku

```
ADBMobile().setDebugLogging(true)
```

#### Chromecast

```
ADBMobile.config.setDebugLogging(true)
```

## Adobe Bloodhound を使用した Chromecast アプリケーションのテスト

アプリケーションの開発中に Bloodhound を使用すると、サーバー呼び出しをローカルで表示できます。また、必要に応じてアドビの収集サーバーにデータを転送することもできます。Bloodhound について詳しくは、以下のガイドを参照してください。

* [Bloodhound 3.x for Mac](https://marketing.adobe.com/resources/help/en_US/mobile/bloodhound/)
* [Bloodhound 2.2 for Windows](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=3&cad=rja&uact=8&ved=0ahUKEwjil9aM87jRAhUExlQKHTYZCjoQFggoMAI&url=https%3A%2F%2Fmarketing.adobe.com%2Fresources%2Fhelp%2Fen_US%2Fmobile%2Fbloodhound_win_2x%2F&usg=AFQjCNEW-gZp1IdbifWFDgDNEaQcGlBobg&sig2=K0waTKxdMj_2kfNXdMI2yg)

>[!IMPORTANT]
>
>Adobe Bloodhound は、2017 年 4 月 30 日をもって廃止されました。2017 年 5 月 1 日以降、追加の機能強化や追加のエンジニアリングまたは Adobe Expert Care のサポートは提供されません。

## ログメッセージ

以下に、ログメッセージの形式を示します。

```js
Format: [<timestamp>] [<level>] [<tag>] [<message>] 
Example: [16:10:29 GMT­0700 (PDT).245] [DEBUG] [plugin::player] Resolving qos.startupTime: 0
```

* **timestamp：**&#x200B;これは、現在の CPU 時間です（タイムゾーンは GMT）。
* **level：** 4 つのメッセージレベルが定義されています。
   * INFO - 通常、アプリケーションからの入力データ（プレーヤー名、ビデオ ID などの検証）
   * DEBUG - 開発者がより複雑な問題をデバッグするために使用する、デバッグログ
   * WARN - 潜在的な統合／設定エラーまたはハートビート SDK バグを示す
   * ERROR - 重要な統合エラーまたはハートビート SDK バグを示す
* **tag：**&#x200B;ログメッセージを発行したサブコンポーネントの名前（通常、クラス名）
* **message：**&#x200B;実際のトレースメッセージ

Media SDKライブラリのログ出力を使用して、実装を検証できます。 A good strategy is to search through the logs for the string `#track`. This will highlight all the `track*()` calls made by your application.

For instance, this is what the logs filtered for `#track` could look like:

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

