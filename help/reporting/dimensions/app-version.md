---
title: アプリバージョン
description: 各ストリーミングセッションに使用されるメディアプレーヤーアプリケーションのバージョンを報告します。
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 4%
---

# アプリバージョン

>[!BEGINSHADEBOX]

*このページでは、**アプリのバージョン**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[&#x200B; アプリのバージョン &#x200B;](/help/implementation/variables/core/app-version.md)を参照してください。*

>[!ENDSHADEBOX]

**App version** ディメンションは、SDKの初期化時に設定されたMedia Player アプリケーションのバージョン文字列をレポートします。 このツールを使用すれば、どのプレイヤーバージョンがアクティブに使用されているかを特定し、品質や行動の変化を特定のリリースに関連付け、広く使用されているバージョンのサポートを優先させることができます。

>[!NOTE]
>
>このディメンションは、AdobeのSDK ライブラリではなく、**media player アプリケーション**&#x200B;のバージョンをキャプチャします。 Adobe独自のSDK ライブラリバージョンは、個別の内部フィールドとして自動的に収集されます。

## このディメンションの入力方法

アプリのバージョンは、SDKの初期化時に1回設定され、セッション開始リクエストごとに自動的に含まれます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | Edgeの実装時に、XDM フィールドマッピングによって自動的に収集されます。 Analyticsのみの実装の場合は、[処理ルール &#x200B;](https://experienceleague.adobe.com/ja/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/processing-rules.md)を使用して、コンテキストデータ `media.sdkVersion`をカスタム eVarにマッピングします。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.appVersion`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | 専用のデータフィード列はありません。 Analyticsのみの実装の場合は、処理ルールで設定されたカスタム eVarのデータフィード列を使用します。 |
| Audience Manager | `c_contextdata.media.sdkVersion` （Analyticsのみの実装） |

## ディメンション項目

各項目は、SDKの初期化時に設定されたリテラルバージョン文字列です。 実装全体で一貫したバージョン管理スキームを使用することで、バージョン文字列がレポートで予測可能にロールアップされます。
