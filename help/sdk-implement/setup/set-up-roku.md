---
seo-title: Roku のセットアップ
title: Roku のセットアップ
uuid: 904dfda0-4782-41da-b4ab-212e81156633
translation-type: tm+mt
source-git-commit: a3a81609046ab5e3c84fe4bf99c92c3dabc58247

---


# Roku のセットアップ{#set-up-roku}

## 前提条件

* **ハートビート用の有効な設定パラメーターの取得**&#x200B;これらのパラメーターは、メディア分析アカウントを設定した後、アドビの担当者から取得できます。
* **メディアプレーヤーで以下の機能を設定します。**
   * _プレーヤーイベントをサブスクライブするための API_ - メディア SDK では、プレーヤーでイベントが発生する際に、シンプルな API のセットを呼び出す必要があります。
   * _プレーヤー情報を提供する API_ - メディア名や再生ヘッドなどの情報がこれに該当します。

Adobe Mobile Services は、モバイルアプリ用のモバイルマーケティング機能を Adobe Experience Cloud 上で統合する新しい UI を提供します。今回は、Adobe Analytics および Adobe Target ソリューションのアプリ分析およびターゲティング機能とのシームレスな統合を提供します。

Learn more at [Adobe Mobile Services documentation.](https://marketing.adobe.com/resources/help/en_US/mobile/)

Experience Cloud ソリューション用 Roku SDK 2.x を使用すると、BrightScript で記述された Roku アプリケーションを測定したり、Audience Management を使用してオーディエンスデータを利用および収集したり、ビデオハートビートを使用してビデオエンゲージメントを測定したりできます。

## SDK の実装

1. [ダウンロードした](/help/sdk-implement/download-sdks.md#download-2x-sdks) Roku ライブラリをプロジェクトに追加します。

   1. The `AdobeMobileLibrary-2.*-Roku.zip` download file consists of the following software components:

      * `adbmobile.brs`:このライブラリファイルはRokuアプリのソースフォルダーに含まれます。

      * `ADBMobileConfig.json`:このSDK設定ファイルは、アプリ用にカスタマイズされています。
   1. プロジェクトソースに、ライブラリファイルと JSON 設定ファイルを追加します。

      Adobe Mobile の設定に使用する JSON には、`mediaHeartbeat` という名前のメディアハートビート専用のキーがあります。メディアハートビートの設定パラメーターは、このキーに属しています。

      >[!TIP]
      >
      >A sample `ADBMobileConfig` JSON file is provided with the package. 設定については、アドビの担当者にお問い合わせください。

      次に例を示します。

      ```
      {
        "version":"1.0", 
        "analytics":{
          "rsids":"",
          "server":"",
          "charset":"UTF-8", 
          "ssl":false, 
          "offlineEnabled":false, 
          "lifecycleTimeout":30, 
          "batchLimit":50, 
          "privacyDefault":"optedin", 
          "poi":[ ]
      },
      "marketingCloud":{
        "org":""
      },
      "target":{ 
        "clientCode":"", 
        "timeout":5
      },
      "audienceManager":{ 
        "server":""
      },
      "acquisition":{ 
        "server":"example.com",
        "appid":"sample-app-id"
      },
      
      "mediaHeartbeat":{ 
         "server":"example.com", 
         "publisher":"sample-publisher", 
         "channel":"sample-channel", 
         "ssl":false,
         "ovp":"sample-ovp", 
         "sdkVersion":"sample-sdk", 
         "playerName":"roku"
         }    
      }
      ```

      | 設定パラメーター | 説明     |
      | --- | --- |
      | `server` | バックエンドのトラッキングエンドポイントの URL を表す文字列。 |
      | `publisher` | コンテンツパブリッシャーの一意の識別子を表す文字列。 |
      | `channel` | コンテンツ配信チャネルの名前を表す文字列。 |
      | `ssl` | SSL をトラッキングコールに使用するかどうかを示すブール値。 |
      | `ovp` | ビデオプレーヤープロバイダーの名前を表す文字列。 |
      | `sdkversion` | 現在のアプリケーションまたは SDK のバージョンを表す文字列。 |
      | `playerName` | プレーヤーの名前を表す文字列。 |

      >[!IMPORTANT]
      >
      >If `mediaHeartbeat` is incorrectly configured, the media module (VHL) enters an error state and will stop sending tracking calls.


1. Experience Cloud 訪問者 ID を設定します。

   Experience Cloud 訪問者 ID サービスは、Experience Cloud ソリューション全体に汎用の訪問者 ID を提供します。訪問者 ID サービスは、ビデオハートビートおよびその他の Experience Cloud 統合に必要です。

   Verify that your `ADBMobileConfig` config contains your `marketingCloud` organization ID.

   ```
   "marketingCloud": {
       "org": YOUR-MCORG-ID"
   }
   ```

   Experience Cloud organization IDs uniquely identify each client company in the Adobe Marketing Cloud and appear similar to the following value: `016D5C175213CCA80A490D05@AdobeOrg`.

   >[!IMPORTANT]
   >
   >Ensure that you include `@AdobeOrg`.

   設定が完了すると、Experience Cloud 訪問者 ID が生成され、すべてのヒットに含まれます。Other Visitor IDs, such as `custom` and `automatically-generated`, continue to be sent with each hit.

   **Experience Cloud 訪問者 ID サービスメソッド**

   >[!TIP]
   >
   >Experience Cloud Visitor ID methods are prefixed with `visitor`.

   |  メソッド   | 説明 |
   | --- | --- |
   | `visitorMarketingCloudID` | Retrieves the Experience Cloud visitor ID from the visitor ID service.  <br/><br/>`ADBMobile().visitorMarketingCloudID()` |
   | `visitorSyncIdentifiers` | Experience Cloud 訪問者 ID とともに、各訪問者に関連付けることができる追加の顧客 ID を設定できます。訪問者 API は、同じ訪問者に対して複数の顧客 ID と、異なる顧客 ID の範囲を区別するための顧客タイプ識別子を受け取ります。このメソッドはに対応しま `setCustomerIDs`す。 For example: <br/><br/>`identifiers={}` <br/>`identifiers["idType"]="idValue"` <br/>`ADBMobile().visitorSyncIdentifiers(identifiers)` |
   | `setAdvertisingIdentifier` | SDK上の広告用Roku ID(RIDA)の設定に使用します。 For example: <br/><br/> `ADBMobile().setAdvertisingIdentifier(`<br/>  `"<sample_roku_identifier_for_advertising>")` Roku SDK <br/><br/><br/>getRIDA() [](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic) APIを使用して、広告用のRoku IDを取得します。 |

   <!--
    Roku Api Reference: 
    * [Integrating the Roku Advertising Framework](https://sdkdocs.roku.com/display/sdkdoc/Integrating+the+Roku+Advertising+Framework)  
    * [GetRIDA()](https://sdkdocs.roku.com/display/sdkdoc/ifDeviceInfo#ifDeviceInfo-GetRIDA())
    -->

<!--    **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://marketing.adobe.com/resources/help/en_US/mobile/signals_.html) -->
