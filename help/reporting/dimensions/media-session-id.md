---
title: メディアセッション ID
description: 各再生セッションを一意に識別します。
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
source-wordcount: '205'
ht-degree: 6%
---

# メディアセッション ID

**メディアセッション ID** ディメンションは、各再生セッションを一意に識別します。 バックエンドで生成され、セッション用に各イベントにスタンプが付けられます。 デバッグ用に単一セッションのイベントを分離したり、カスタム分析でセッションを重複排除したりするために使用します。

## このディメンションの入力方法

バックエンドが[&#x200B; セッション開始](/help/implementation/events/session/session-start.md) イベントを受信すると、セッション IDが自動的に生成されます。 Web SDKおよびMobile SDKの実装では、IDを取得して保持します。ダイレクト APIの実装では、`sessionStart`応答（Media Collection APIの`Location` ヘッダー、Media Edge APIの`media-analytics:new-session` ハンドル）からセッション IDを読み取り、後続のイベントに含める必要があります。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | `a.media.vsid`をeVarにマッピングする[処理ルール &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.ID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videosessionid`, `post_videosessionid` |
| Audience Manager | `c_contextdata.a.media.vsid` |

## ディメンション項目

各アイテムは、バックエンドによって生成された一意のセッション ID （通常は22文字の英数字の文字列）です。 「フィルター」または「検索」フィールドを使用して、特定のセッションを検索します。
