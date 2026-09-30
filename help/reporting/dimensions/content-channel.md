---
title: コンテンツチャネル
description: 各セッションが再生された配布ステーション、ネットワーク、またはプロパティを報告します。
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
source-wordcount: '163'
ht-degree: 8%
---

# コンテンツチャネル

>[!BEGINSHADEBOX]

*このページでは、**コンテンツチャネル**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[&#x200B; コンテンツチャネル &#x200B;](/help/implementation/variables/core/content-channel.md)を参照してください。*

>[!ENDSHADEBOX]

**コンテンツチャネル** ディメンションは、各セッションが再生された配布ステーション、ネットワーク、またはプロパティをレポートします。 ネットワークまたはプロパティのセクションごとに再生を分割する場合に使用します。

## このディメンションの入力方法

チャネルは、セッション開始時にプレーヤーによって設定され、セッションの期間にわたって保持されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.channel`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.channel`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videochannel`, `post_videochannel` |
| Audience Manager | `c_contextdata.a.media.channel` |

>[!IMPORTANT]
>
>チャネルが設定されていない場合、ディメンションはそのセッションに対して未入力になります。

## ディメンション項目

各アイテムは、セッション開始時に設定されたリテラル文字列です。 任意の文字列を使用できます。 一般的な値は、ネットワーク名、サイトパスの一部、または内部プロパティ識別子です。
