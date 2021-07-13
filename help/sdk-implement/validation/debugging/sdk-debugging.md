---
title: SDK のデバッグ
description: メディアSDKで使用できるトラッキング/ログについて説明します。
uuid: a5972d87-c593-4b4f-a56f-dca6e25268e1
exl-id: c2de6454-8538-4d07-a099-e278b153d894
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 96%

---

# SDK のデバッグ{#sdk-debugging}

ログを有効／無効にすることができます。メディア SDK では、メディアトラッキングスタック全体にわたる広範なトレース／ログメカニズムを提供します。Config オブジェクトの `debugLogging` フラグを設定することで、ログを有効または無効にできます。

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

アプリケーションの開発中に Bloodhound を使用すると、サーバー呼び出しをローカルで表示できます。また、必要に応じてアドビの収集サーバーにデータを転送することもできます。

<!--
For more information about Bloodhound, see the following guides:

* [Bloodhound 3.x for Mac](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=2ahUKEwiimfSUypDpAhVZHzQIHS6WDQIQFjABegQIChAD&url=https%3A%2F%2Fmarketing.adobe.com%2Fresources%2Fhelp%2Fen_US%2Fmobile%2Fbloodhound%2F&usg=AOvVaw3t4s0gcvuWEpLIqBkhKdGH) 
* [Bloodhound 2.2 for Windows](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=3&cad=rja&uact=8&ved=0ahUKEwjil9aM87jRAhUExlQKHTYZCjoQFggoMAI&url=https%3A%2F%2Fmarketing.adobe.com%2Fresources%2Fhelp%2Fen_US%2Fmobile%2Fbloodhound_win_2x%2F&usg=AFQjCNEW-gZp1IdbifWFDgDNEaQcGlBobg&sig2=K0waTKxdMj_2kfNXdMI2yg)
-->

>[!IMPORTANT]
>
>Adobe Bloodhound は、2017 年 4 月 30 日（PT）をもって廃止されました。2017 年 5 月 1 日（PT）以降、追加の機能強化や追加のエンジニアリングまたは Adobe Expert Care のサポートは提供されません。

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

メディア SDK ライブラリのログ出力を使用して、実装を検証できます。文字列 `#track` についてログ全体を検索するとよいでしょう。これにより、アプリケーションによって呼び出されたすべての `track*()` をハイライトします。

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
