---
title: コンテンツ
description: コンテンツ IDでキーを設定して、再生された各メディアの一意の部分をレポートします。
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
source-wordcount: '251'
ht-degree: 7%
---

# コンテンツ

>[!BEGINSHADEBOX]

*このページでは、**コンテンツ**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[&#x200B; コンテンツ ID](/help/implementation/variables/core/content-id.md)を参照してください。*

>[!ENDSHADEBOX]

**コンテンツ** ディメンションは、セッション開始時に設定されたコンテンツ IDにキーを設定して、再生された各ユニークなメディアをレポートします。 これは、ストリーミングメディアのレポート用の主な内訳であり、ビデオ名、ビデオの長さ、アセット ID、最初の放送日、コンテンツの評価などの分類ディメンション用の結合キーです。

## このディメンションの入力方法

コンテンツは、セッション開始時にプレーヤーによって、アセットの安定した識別子として設定されます。 セッションの後続のイベントごとに、同じコンテンツ IDがレポートされます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.name`から自動的に収集されます。 訪問の期間を保持します。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.name`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `video`, `post_video` |
| Audience Manager | `c_contextdata.a.media.name` |

>[!IMPORTANT]
>
>コンテンツ IDが必要です。 未設定または空の場合、セッションはストリーミングメディアレポートから削除され、どのメディアレポートにも[!UICONTROL すべてのストリーミングメディア &#x200B;] セグメントにも表示されません。

## ディメンション項目

各アイテムは、セッション開始時に報告される一意のコンテンツ IDです。 同じアセットのセッションが時間の経過とともに1つの行項目にロールアップされるように、安定したID （内部CMS ID、EIDRやTMS/Gracenoteなどの業界ID、永続的なスラグなど）を使用します。

## 推奨セグメント

| セグメント | 規則 |
| --- | --- |
| [!UICONTROL すべてのストリーミングメディア &#x200B;] | コンテンツ （ID）が存在します |
