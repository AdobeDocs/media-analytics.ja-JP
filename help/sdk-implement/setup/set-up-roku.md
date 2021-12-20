---
title: Roku 用 Media SDK のセットアップ方法
description: Roku で Media SDK アプリケーションをセットアップするには、次の手順に従います。
uuid: 904dfda0-4782-41da-b4ab-212e81156633
exl-id: b8de88d0-3a93-4776-b372-736bf979ee26
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 07192eca8bad89d005d88fa084ec891df346f96a
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 94%

---

# Roku のセットアップ{#set-up-roku}

## 前提条件 

* **ハートビート用の有効な設定パラメーターを取得** これらのパラメーターは、Media Analytics アカウントの設定後、アドビの担当者から取得できます。
* **メディアプレーヤーで以下の機能を設定します。**
   * _プレーヤーイベントをサブスクライブするための API_ - メディア SDK では、プレーヤーでイベントが発生する際に、シンプルな API のセットを呼び出す必要があります。
   * _プレーヤー情報を提供する API_ - メディア名や再生ヘッドなどの情報がこれに該当します。

Adobe Mobile Services は、モバイルアプリケーション用のモバイルマーケティング機能を Adobe Experience Cloud 上で統合する新しい UI を提供します。今回は、Adobe Analytics および Adobe Target ソリューションのアプリ分析およびターゲティング機能とのシームレスな統合を提供します。

詳しくは、[Adobe Mobile Services のドキュメント](https://experienceleague.adobe.com/docs/mobile-services/using/home.html?lang=ja)を参照してください。

Experience Cloud ソリューション用 Roku SDK 2.x を使用すると、BrightScript で記述された Roku アプリケーションを測定したり、Audience Management を使用してオーディエンスデータを利用および収集したり、ビデオハートビートを使用してビデオエンゲージメントを測定したりできます。

## SDK の実装

1. [ダウンロードした](/help/sdk-implement/download-sdks.md#download-2x-sdks) Roku ライブラリをプロジェクトに追加します。

   1. ダウンロードファイルの `AdobeMobileLibrary-2.*-Roku.zip` には、次のソフトウェアコンポーネントが含まれています。

      * `adbmobile.brs`：このライブラリファイルは、Roku アプリのソースフォルダーに含まれています。

      * `ADBMobileConfig.json`：アプリ用にカスタマイズされた SDK 設定ファイル。
   1. プロジェクトソースに、ライブラリファイルと JSON 設定ファイルを追加します。

      Adobe Mobile の設定に使用する JSON には、`mediaHeartbeat` という名前のメディアハートビート専用のキーがあります。メディアハートビートの設定パラメーターは、このキーに属しています。

      >[!TIP]
      >
      >サンプルの `ADBMobileConfig` JSON ファイルがパッケージに付属しています。設定については、アドビの担当者にお問い合わせください。

      次に例を示します。

      ```
      {
        "version":"1.0",
        "analytics":{
          "rsids":"",
          "server":"",
          "charset":"UTF-8",
          "ssl":true,
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
         "ssl":true,
         "ovp":"sample-ovp",
         "sdkVersion":"sample-sdk",
         "playerName":"roku"
         }    
      }
      ```

      | 設定パラメーター | 説明     |
      | --- | --- |
      | `server` | バックエンドのトラッキングエンドポイントの URL を表す文字列。 |
      | `publisher` | コンテンツパブリッシャーの一意の ID を表す文字列。 |
      | `channel` | コンテンツ配信チャネルの名前を表す文字列。 |
      | `ssl` | SSL をトラッキングコールに使用するかどうかを示すブール値。 |
      | `ovp` | ビデオプレーヤープロバイダーの名前を表す文字列。 |
      | `sdkversion` | 現在のアプリケーションまたは SDK のバージョンを表す文字列。 |
      | `playerName` | プレーヤーの名前を表す文字列。 |

      >[!IMPORTANT]
      >
      >`mediaHeartbeat` を誤って設定した場合、メディアモジュール（VHL）がエラー状態になり、トラッキングコールの送信が中止されます。


1. Experience Cloud 訪問者 ID を設定します。

   Experience Cloud 訪問者 ID サービスは、Experience Cloud ソリューション全体に汎用の訪問者 ID を提供します。訪問者 ID サービスは、ビデオハートビートおよびその他の Experience Cloud 統合に必要です。

   `ADBMobileConfig` 設定ファイルに `marketingCloud` 組織 ID が含まれていることを確認します。

   ```
   "marketingCloud": {
       "org": YOUR-MCORG-ID"
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
   >Experience Cloud 訪問者 ID メソッドのプレフィックスは `visitor` です。

   |  メソッド   | 説明 |
   | --- | --- |
   | `visitorMarketingCloudID` | 訪問者 ID サービスから Experience Cloud 訪問者 ID を取得します。<br/><br/>`ADBMobile().visitorMarketingCloudID()` |
   | `visitorSyncIdentifiers` | Experience Cloud 訪問者 ID を使用して、各訪問者に関連付けることのできる追加の顧客 ID を設定できます。訪問者 API は、同じ訪問者に対して複数の顧客 ID と、異なる顧客 ID の範囲を区別するための顧客タイプ識別子を受け取ります。このメソッドは、`setCustomerIDs` に対応します。例：<br/><br/>`identifiers={}` <br/>`identifiers["idType"]="idValue"` <br/>`ADBMobile().visitorSyncIdentifiers(identifiers)` |
   | `setAdvertisingIdentifier` | SDK で広告（RIDA）用に Roku ID を設定するために使用されます。例：<br/><br/> `ADBMobile().setAdvertisingIdentifier(`<br/>`"<sample_roku_identifier_for_advertising>")` <br/><br/><br/>Roku SDK [getRIDA()](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic) API を使用して、広告（RIDA）用の Roku ID を取得します。 |
   | `getAllIdentifiers` | Analytics、訪問者、Audience Manager、カスタム識別情報など、SDK に保存されているすべての識別情報のリストを返します。<br/><br/> `identifiers = ADBMobile().getAllIdentifiers()` |
   <!--
    Roku Api Reference:
    * [Integrating the Roku Advertising Framework](https://sdkdocs.roku.com/display/sdkdoc/Integrating+the+Roku+Advertising+Framework)  
    * [GetRIDA()](https://sdkdocs.roku.com/display/sdkdoc/ifDeviceInfo#ifDeviceInfo-GetRIDA())
    -->

   **その他のパブリック API**

   **DebugLogging**

   |  メソッド   | 説明 |
   | --- | --- |
   | `setDebugLogging` | SDK のデバッグログを有効または無効にするために使用します。  <br/><br/>`ADBMobile().setDebugLogging(true)` |
   | `getDebugLogging` | デバッグログが有効な場合は true を返します。  <br/><br/>`isDebugLoggingEnabled = ADBMobile().getDebugLogging()` |

   **PrivacyStatus**

   |  定数   | 説明 |
   | --- | --- |
   | `PRIVACY_STATUS_OPT_IN` | setPrivacyStatus を呼び出してオプトインを呼び出す際に渡す定数。 <br/><br/>`optInString = ADBMobile().PRIVACY_STATUS_OPT_IN` |
   | `PRIVACY_STATUS_OPT_OUT` | setPrivacyStatus を呼び出してオプトアウトする際に渡す定数。 <br/><br/>`optOutString = ADBMobile().PRIVACY_STATUS_OPT_OUT` |

   |  メソッド   | 説明 |
   | --- | --- |
   | `setPrivacyStatus` | SDK のプライバシーステータスを設定します。 <br/><br/>`ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)` |
   | `getPrivacyStatus` | SDK に設定されている現在のプライバシーステータスを取得します。 <br/><br/>`privacyStatus = ADBMobile().getPrivacyStatus()` |

   >[!IMPORTANT]
   >
   >SDK が ping を正しく送信するよう、250 ミリ秒ごとにメインイベントループで `processMessages` 関数と `processMediaMessages` 関数を呼び出すようにします。

   |  メソッド   | 説明 |
   | --- | --- |
   | `processMessages` | 処理する Analytics イベントを SDK に渡します。 <br/><br/>`ADBMobile().processMessages()` |
   | `processMediaMessages` | 処理するメディアイベントを SDK に渡します。<br/><br/>`ADBMobile().processMediaMessages()` |


<!--    **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://experienceleague.adobe.com/docs/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html) -->
