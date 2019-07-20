---
seo-title: Chromecast のセットアップ
title: Chromecast のセットアップ
uuid: d664e394-02a2-4985- bbad- be1bcc44fb2b
translation-type: tm+mt
source-git-commit: bb3a303edba724c8f444d612b3be9d7250eea363

---


# Chromecast のセットアップ{#set-up-chromecast}

## FAQ

_Chromecast JavaScript SDK または標準の JavaScript SDK のどちらを使用すべきでしょうか。_

正しい回答は、以下の理由により"Chromecast"です。
* 標準の JS SDK の AppMeasurement および VisitorAPI ライブラリは、OTT プラットフォームでの動作が認定されていません。Chromecast JS SDK では、ビデオハートビートライブラリ（VHL）、Analytics および VisitorAPI が Chromecast 向けに認定された 1 つの統合 SDK に組み込まれています。
* この Chromecast SDK は標準の JS SDK より大幅に軽量です。これは、OTT プラットフォームで使用されるローエンドのハードウェアでは非常に重要です。

## 前提条件

* **ハートビートの有効な設定パラメーターの取得**&#x200B;これらのパラメーターは、メディア分析アカウントを設定した後、アドビの担当者から取得できます。
* **メディアプレーヤーで以下の機能を設定します。**
   * *プレーヤーイベントをサブスクライブするための API* - メディア SDK では、プレーヤーでイベントが発生する際に、シンプルな API のセットを呼び出す必要があります。
   * *プレーヤー情報を提供する API* - メディア名や再生ヘッドなどの情報がこれに該当します。

Adobe Mobile Services は、モバイルアプリ用のモバイルマーケティング機能を Adobe Experience Cloud 上で統合する新しい UI を提供します。今回は、Adobe Analytics および Adobe Target ソリューションのアプリ分析およびターゲティング機能とのシームレスな統合を提供します。Learn more at [Adobe Mobile Services documentation.](https://marketing.adobe.com/resources/help/en_US/mobile/)

Experience Cloud ソリューション用 Chromecast SDK 2.x を使用すると、JavaScript で記述された Chromecast アプリケーションを測定したり、Audience Management を使用してオーディエンスデータを利用および収集したり、ビデオハートビートを使用してビデオエンゲージメントを測定したりできます。

## SDK の実装

1. [ダウンロードした](../../sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211) Chromecast ライブラリをプロジェクトに追加します。

   1. `AdobeMobileLibrary-Chromecast-[version]`.zip ファイルには、次のソフトウェアコンポーネントが含まれています。

      *  を使用します`adbmobile-chromecast.min.js`。

         このライブラリファイルは、Chromecast アプリのソースフォルダーに含まれています。

      * `ADBMobileConfig` config

         アプリ用にカスタマイズされた SDK 設定ファイル。この SDK には、サンプルの `ADBMobileConfig` 実装が用意されています（`samples/` / 内）。アドビの担当者から、適切な設定を入手してください。
   1. このライブラリファイルを `index.html` ファイルに追加し、以下のように `ADBMobileConfig` グローバル変数を設定します（Adobe Mobile for Heartbeats の設定に使用するこのグローバル変数には、`mediaHeartbeat` という排他的なキーが存在します）。

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
              "rsids": "mobile5vhl.sample.player", 
              "server": "obumobile5.sc.omtrdc.net", 
              "ssl": false, 
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
              "server": "obumobile5.hb.omtrdc.net", 
              "publisher": "972C898555E9F7BC7F000101@AdobeOrg", 
              "channel": "test-channel-chromecast", 
              "ssl": false, 
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
      >If `mediaHeartbeat` is incorrectly configured, the media module (VHL) enters an error state and will stop sending tracking calls.

      mediaHeartbeat キーの ADBMobile 設定パラメーター：
   | 設定パラメーター | 説明     |
   | --- | --- |
   | `server` | バックエンドのトラッキングエンドポイントの URL を表す文字列。 |
   | `publisher` | コンテンツパブリッシャーの一意の識別子を表す文字列。 |
   | `channel` | コンテンツ配信チャネルの名前を表す文字列。 |
   | `ssl` | SSL をトラッキングコールに使用するかどうかを示すブール値。 |
   | `ovp` | ビデオプレーヤープロバイダーの名前を表す文字列。 |
   | `sdkversion` | 現在のアプリケーションまたは SDK のバージョンを表す文字列。 |
   | `playerName` | プレーヤーの名前を表す文字列。 |


1. Experience Cloud 訪問者 ID を設定します。

   Experience Cloud 訪問者 ID サービスは、Experience Cloud ソリューション全体に汎用の訪問者 ID を提供します。訪問者 ID サービスは、ビデオハートビートおよびその他の Experience Cloud 統合に必要です。

   Verify that your `ADBMobileConfig` config contains your `marketingCloud` organization ID.

   ```js
   "marketingCloud": { 
       "org": YOUR-MCORG-ID" 
   }
   ```

   Experience Cloud organization IDs uniquely identify each client company in the Adobe Marketing Cloud and appear similar to the following value: `016D5C175213CCA80A490D05@AdobeOrg`.

   >[!IMPORTANT]
   >
   >`@AdobeOrg`必ず含めてください。

   設定が完了すると、Experience Cloud 訪問者 ID が生成され、すべてのヒットに含まれます。Other Visitor IDs, such as `custom` and `automatically-generated`, continue to be sent with each hit.

   **Experience Cloud 訪問者 ID サービスメソッド**

   >[!TIP]
   >
   >Experience Cloud Visitor ID methods are prefixed with `visitor`.

   | メソッド | 説明 |
   | --- | --- |
   | `getMarketingCloudID()` | Retrieves the Experience Cloud Visitor ID from the Visitor ID service.  <br/><br/>`ADBMobile.visitor.getMarketingCloudID();` |
   | `syncIdentifiers()` | Experience Cloud 訪問者 ID とともに、各訪問者に関連付けることができる追加の顧客 ID を設定できます。訪問者 API は、同じ訪問者に対して複数の顧客 ID と、異なる顧客 ID の範囲を区別するための顧客タイプ識別子を受け取ります。このメソッドは、JavaScript ライブラリの `setCustomerIDs()` に相当します。For example: <br/><br/>`var identifiers = {};` <br/><br/>`identifiers["idType"] = "idValue";` <br/><br/>`ADBMobile.visitor.syncIdentifiers(identifiers);` |


<!--   **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://marketing.adobe.com/resources/help/en_US/mobile/signals_.html) -->

