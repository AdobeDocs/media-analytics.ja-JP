---
title: オプトアウトとプライバシーの設定
description: オプトイン、オプトアウトおよびプライバシーの取り扱い方法を説明します。
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
exl-id: 64f5ef2b-7850-43d8-8f32-3d008ea4f156
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/eF09wxu2mIUoFph5EdHz5y0XtcpXHHLINqSGLQEMoHU
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 3fd9ffcb997e1570abb983107e69d183b1c8b311
workflow-type: tm+mt
source-wordcount: 798
ht-degree: 3%

---

# オプトアウトとプライバシーの設定

ユーザーがトラッキングをオプトアウトすると、ストリーミングメディアライブラリは直ちにすべてのデータ収集アクティビティを停止します。 セッション開始の呼び出しも、ハートビート pingも、イベント追跡データがそのユーザーのAdobe data collection サーバーに送信されることはありません。

## オプトアウトとオプトイン

オプトアウト制御は、デバイスまたはブラウザーごとに実行されます。 ユーザーの同意の尊重は、実施組織の責任です。 Adobeのプライバシー慣行の概要については、[Adobe Privacy Center](https://www.adobe.com/jp/privacy.html)を参照してください。

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

Web SDKは、`setConsent` コマンドを使用して設定された同意設定を尊重します。 同意が`"out"`に設定されている場合、Web SDKは、ストリーミングメディアトラッキング呼び出しを含むすべてのイベントのEdge Networkへの転送を停止します。 同意の状態は、セッション間のブラウザーストレージに保持されます。

オプトアウトを実装する前に、Web SDKがストリーミングメディアコンポーネントで設定されていることを確認します。 詳しくは、[Web SDKの設定](../implementation/edge/web-sdk.md)を参照してください。

Adobe 2.0の同意標準を使用して、同意をオプトアウトに設定します。

```javascript
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "2.0",
    value: {
      collect: { val: "n" }
    }
  }]
});
```

同意値：

* `"y"`：オプトイン （データ収集が許可されています）
* `"n"`：オプトアウトされました（データ収集は抑制されました）
* `"p"`：保留中（ユーザーの決定を待っています。解決するまでデータは収集されません）

トラッキングを復元するには、`"y"`を`collect.val`値として`setConsent`を再度呼び出します。

IAB TCF 2.0を含むその他の形式については、Web SDK ドキュメントの[setConsent コマンド &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/setconsent)を参照してください。

>[!TAB iOS]

Adobe Experience Platform Mobile SDKは、`MobileCore.setPrivacyStatus()`を使用して設定されたプライバシーステータスを尊重します。 ステータスを`.optedOut`に設定すると、Streaming Mediaを含むすべてのAEP拡張機能のすべてのデータ収集が抑制されます。 ステータスはアプリセッション間で保持されます。

```swift
MobileCore.setPrivacyStatus(.optedOut)
```

トラッキングを復元するには、プライバシーステータスを`.optedIn`に戻します。

```swift
MobileCore.setPrivacyStatus(.optedIn)
```

詳しくは、AEP Mobile SDK ドキュメントの[&#x200B; プライバシーとGDPR](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/#setprivacystatus)を参照してください。

>[!TAB Android]

Adobe Experience Platform Mobile SDKは、`MobileCore.setPrivacyStatus()`を使用して設定されたプライバシーステータスを尊重します。 ステータスを`MobilePrivacyStatus.OPT_OUT`に設定すると、Streaming Mediaを含むすべてのAEP拡張機能のすべてのデータ収集が抑制されます。 ステータスはアプリセッション間で保持されます。

```kotlin
MobileCore.setPrivacyStatus(MobilePrivacyStatus.OPT_OUT)
```

トラッキングを復元するには、プライバシーステータスを`MobilePrivacyStatus.OPT_IN`に戻します。

```kotlin
MobileCore.setPrivacyStatus(MobilePrivacyStatus.OPT_IN)
```

詳しくは、AEP Mobile SDK ドキュメントの[&#x200B; プライバシーとGDPR](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/#setprivacystatus)を参照してください。

>[!TAB Edge六]

Roku Edge SDKは、Adobe 2.0同意標準で`setConsent()`を使用しています。 `collect.val`を`"n"`に設定すると、ストリーミングメディアイベントを含むすべてのデータ収集が即座に停止されます。

同意値：

* `"y"`：オプトイン （データ収集が許可されています）
* `"n"`：オプトアウトされました（データ収集は抑制されました）
* `"p"`：保留中（ユーザーの決定を待っています。解決するまでデータは収集されません）

```brightscript
currentDate = CreateObject("roDateTime")
timestampInISO8601 = currentDate.ToISOString("milliseconds")

collectConsentNo = {
  "consent": [{
    "standard": "Adobe",
    "version": "2.0",
    "value": {
      "metadata": { "time": timestampInISO8601 },
      "collect": { "val": "n" }
    }
  }]
}

m.aepSdk.setConsent(collectConsentNo)
```

トラッキングを復元するには、`collect.val`を`"y"`に設定し、もう一度`setConsent()`に電話してください。

`updateConfiguration()`と`ADB_CONSTANTS.CONFIGURATION.CONSENT_DEFAULT` キーを使用して、SDK初期化時にデフォルトの同意値を設定することもできます。 詳しくは、[Roku Edge SDK ドキュメント &#x200B;](https://github.com/adobe/aepsdk-roku)を参照してください。

>[!TAB Media Edge API]

Media Edge APIは、サーバーサイドの実装です。 SDKレイヤーによって同意が自動的に適用されることはありません。API呼び出しを行う前にアプリケーションでユーザーの同意ステータスを確認し、オプトアウトしたユーザーのリクエストを処理する必要があります。

完全なオプトアウトの場合、オプトアウトしたユーザーの`/va/v2/sessions` エンドポイント（またはその後のイベントエンドポイント）にPOSTしないでください。

```javascript
// Check consent status before initiating a media session
if (userHasOptedOut) {
  // Do not call the Media Edge API
  return;
}

// Only call the API for users who have not opted out
fetch("https://edge.adobedc.net/va/v2/sessions", {
  method: "POST",
  body: JSON.stringify(sessionStartPayload)
});
```

詳しくは、[Media Edge API リファレンス &#x200B;](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/)を参照してください。

>[!ENDTABS]

## 従来の実装タイプ （Analyticsのみ）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Media SDK JS 3.x ライブラリは、Adobe Visitor API （Identity Service）のオプトアウト状態に延期されます。 ユーザーがVisitor APIを使用してオプトアウトすると、Media SDKはすべてのトラッキング呼び出しを自動的に抑制します。

```javascript
var visitor = Visitor.getInstance("YOUR_ORG_ID@AdobeOrg");
visitor.setOptOut(true);
```

`YOUR_ORG_ID@AdobeOrg`をAdobe Admin Consoleの組織IDに置き換えます。

トラッキングを復元するには、`false`を`setOptOut()`に渡します。

詳しくは、[Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=ja)を参照してください。

>[!TAB Chromecast]

Chromecast Media SDK 3.xは、`ADBMobile.config.setPrivacyStatus()`を使用して設定されたプライバシーステータスを尊重します。 ステータスを`PRIVACY_STATUS_OPT_OUT`に設定すると、すべてのデータ収集が抑制されます。

```javascript
ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_OUT);
```

トラッキングを復元するには、ステータスをオプトインに戻します。

```javascript
ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_IN);
```

`ADBMobileConfig` オブジェクトのSDK初期化時に、デフォルトのプライバシーステータスを設定することもできます。

```javascript
var ADBMobileConfig = {
  "analytics": {
    "privacyDefault": "optedout"
  }
};
```

>[!TAB Roku 2.x]

Roku 2.x SDKは、`setPrivacyStatus`を使用して設定されたプライバシーステータスを尊重します。 ステータスを`PRIVACY_STATUS_OPT_OUT`に設定すると、すべてのデータ収集が抑制されます。

```brightscript
adb = ADBMobile()
adb.setPrivacyStatus(adb.PRIVACY_STATUS_OPT_OUT)
```

トラッキングを復元するには、ステータスをオプトインに戻します。

```brightscript
adb = ADBMobile()
adb.setPrivacyStatus(adb.PRIVACY_STATUS_OPT_IN)
```

`ADBMobileConfig.json` ファイルのSDK初期化時に、デフォルトのプライバシーステータスを設定することもできます。

```json
"analytics": {
  "privacyDefault": "optedout"
}
```

>[!TAB Media Collection API]

Media Collection APIは、サーバーサイド実装です。 アプリケーションは、API呼び出しを行う前にユーザーの同意ステータスを確認し、オプトアウトしたユーザーのリクエストを抑制する必要があります。

完全なオプトアウトの場合、オプトアウトしたユーザーのセッションエンドポイントにPOSTしないでください。

CCPAの下での部分的なオプトアウトの場合は、`sessionStart`要求の`params` オブジェクトにオプトアウトフラグを含めます。

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "analytics.optOutServerSideForwarding": true,
    "analytics.optOutShare": true
  }
}
```

* `analytics.optOutServerSideForwarding`: Adobe Analyticsと他のExperience Cloud ソリューション （Audience Managerなど）間で共有されるデータをオプトアウトするには、`true`に設定します。
* `analytics.optOutShare`：他のAdobe Analytics クライアントとのフェデレーションデータ共有をオプトアウトするには、`true`に設定します。

使用可能なパラメーターの完全なリストについては、[Media Collection API リクエストパラメーターのリファレンス &#x200B;](../implementation/media-collection-api/mc-api-ref/mc-api-req-params.md)を参照してください。

>[!ENDTABS]

