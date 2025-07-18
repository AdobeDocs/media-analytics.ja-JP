---
title: Chromecast 用 Media SDK の設定方法
description: Chromecast で Media SDK アプリケーションをセットアップするには、次の手順に従います。
uuid: d664e394-02a2-4985-bbad-be1bcc44fb2b
exl-id: 5dfe3407-2858-48c0-a70c-8ea87967ac47
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 97%

---

# Chromecast 用 Mobile SDK v3.x の設定 {#set-up-chromecast}

ここでは、ストリーミングメディアコレクション用の Chromecast インストールを設定するための前提条件について説明します。

## 前提条件

* **有効な設定パラメーターの取得**

  これらのパラメーターは、Media Analytics アカウントの設定後、アドビ担当者から取得できます。
* **メディアプレーヤーへの下記 API の組み込み**

   * *プレーヤーイベントをサブスクライブするための API* - Media SDK では、プレーヤーでイベントが発生する際に、シンプルな API のセットを呼び出す必要があります。
   * *プレーヤー情報を提供する API* - メディア名や再生ヘッドなどの情報がこれに該当します。

Adobe Mobile Services は、モバイルアプリケーション用のモバイルマーケティング機能を Adobe Experience Cloud 上で統合する新しい UI を提供します。今回は、Adobe Analytics および Adobe Target ソリューションのアプリ分析およびターゲティング機能とのシームレスな統合を提供します。詳しくは、[Adobe Mobile Services のドキュメント](https://experienceleague.adobe.com/docs/mobile-services/using/home.html?lang=ja)を参照してください。

Experience Cloud ソリューション向けの Chromecast 用 Adobe Mobile ライブラリ v3.x を使用すると、JavaScript で記述された Chromecast アプリケーションを測定したり、Audience Management を通じてオーディエンスデータを利用および収集したり、ビデオエンゲージメントを測定したりできます。

## モバイルライブラリ／SDK 実装

1. ダウンロードした Chromecast ライブラリをプロジェクトに追加します。

   1. `AdobeMobileLibrary-Chromecast-[version]`.zip ファイルには、次のソフトウェアコンポーネントが含まれています。

      * を使用します`adbmobile-chromecast.min.js`。

        このライブラリファイルは、Chromecast アプリのソースフォルダーに含まれています。

      * `ADBMobileConfig` config

        アプリ用にカスタマイズされた SDK 設定ファイル。この SDK には、サンプルの `ADBMobileConfig` 実装が用意されています（`samples/` / 内）。アドビの担当者から、適切な設定を入手してください。

   1. このライブラリファイルを `index.html` ファイルに追加し、以下のように `ADBMobileConfig` グローバル変数を作成します（Adobe Mobile for Media Analytics の設定に使用されるグローバル変数には、`mediaHeartbeat` という専用のキーがあります）。

      ```js
      <script>
          var ADBMobileConfig = {
            "marketingCloud": {
              "org": "972C898555E9F7BC7F000101@AdobeOrg"
            },
            "target": {
              "clientCode": "",
              "timeout": 5
            },
            "audienceManager": {
              "server": "obumobile5.demdex.net"
            },
            "analytics": {
              "rsids": "example.sample.player",
              "server": "example.sc.omtrc.net",
              "ssl": true,
              "offlineEnabled": false,
              "charset": "UTF-8",
              "lifecycleTimeout": 300,
              "privacyDefault": "optedin",
              "batchLimit": 0,
              "timezone": "MDT",
              "timezoneOffset": -360,
              "referrerTimeout": 0,
              "poi": []
            },
            "mediaHeartbeat": {
              "server": "example.hb-api.omtrdc.net",
              "publisher": "972C898555E9F7BC7F000101@AdobeOrg",
              "channel": "test-channel-chromecast",
              "ssl": true,
              "ovp": "chromecast-player",
              "sdkVersion": "chromecast-sdk",
              "playerName": "Chromecast"
            }
          };
        </script>
      <script type="text/javascript" src="script/lib/adbmobile-chromecast.min.js"></script>
      ```

      >[!IMPORTANT]
      >
      >`mediaHeartbeat` を誤って設定した場合、メディアモジュールがエラー状態になり、トラッキングコールの送信が停止されます。

      mediaHeartbeat キーの ADBMobile 設定パラメーター：

   | 設定パラメーター | 説明     |
   | --- | --- |
   | `server` | バックエンドのトラッキングエンドポイントの URL を表す文字列。 |
   | `publisher` | コンテンツパブリッシャーの一意の ID を表す文字列。 |
   | `channel` | コンテンツ配信チャネルの名前を表す文字列。 |
   | `ssl` | SSL をトラッキングコールに使用するかどうかを示すブール値。 |
   | `ovp` | ビデオプレーヤープロバイダーの名前を表す文字列。 |
   | `sdkversion` | 現在のアプリケーションまたは SDK のバージョンを表す文字列。 |
   | `playerName` | プレーヤーの名前を表す文字列。 |


1. Experience Cloud 訪問者 ID を設定します。

   Experience Cloud 訪問者 ID サービスは、Experience Cloud ソリューション全体に汎用の訪問者 ID を提供します。訪問者 ID サービスは、Media Analytics およびその他の Marketing Cloud 統合に必要です。

   `ADBMobileConfig` 設定ファイルに `marketingCloud` 組織 ID が含まれていることを確認します。

   ```
   "marketingCloud": {
       "org": "YOUR-MCORG-ID"
   }
   ```

   Experience Cloud 組織 ID は、Adobe Experience Cloud 内の各クライアント企業を一意に識別するもので、`016D5C175213CCA80A490D05@AdobeOrg` のようになります。

   >[!IMPORTANT]
   >
   >「`@AdobeOrg`」が含まれている必要があります。

   設定が完了すると、Experience Cloud 訪問者 ID が生成され、すべてのヒットに含まれます。`custom` や `automatically-generated` などの他の訪問者 ID は、引き続きヒットごとに送信されます。

   **Experience Cloud 訪問者 ID サービスメソッド**

   >[!TIP]
   >
   >Experience Cloud 訪問者 ID メソッドの接頭辞は `visitor` です。

   | メソッド | 説明 |
   | --- | --- |
   | `getMarketingCloudID()` | 訪問者 ID サービスから Experience Cloud 訪問者 ID を取得します。<br/><br/>`ADBMobile.visitor.getMarketingCloudID();` |
   | `syncIdentifiers()` | Experience Cloud 訪問者 ID を使用して、各訪問者に関連付けることのできる追加の顧客 ID を設定できます。訪問者 API は、同じ訪問者に対して複数の顧客 ID と、異なる顧客 ID の範囲を区別するための顧客タイプ識別子を受け取ります。このメソッドは、JavaScript ライブラリの `setCustomerIDs()` に相当します。例：<br/><br/>`var identifiers = {};` <br/><br/>`identifiers["idType"] = "idValue";` <br/><br/>`ADBMobile.visitor.syncIdentifiers(identifiers);` |

1. メディアをトラッキングするには、MediaDelegate プロトコルを実装します。

   ```js
    var delegate = {
      // Replace <currentPlaybackTime> with the video player current playback time
      getCurrentPlaybackTime = function() {
        return <currentPlaybackTime>;
      },
      // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames> with the current playback QoS values.
      getQoSObject = function() {
         return ADBMobile.media.createQoSObject(<bitrate>, <startupTime>, <fps>, <droppedFrames>);
      }
    }
   
    ADBMobile.media.setDelegate(delegate);
   }
   ```

<!--   **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://experienceleague.adobe.com/docs/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html?lang=ja) -->
