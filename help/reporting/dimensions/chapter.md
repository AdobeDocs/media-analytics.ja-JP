---
title: チャプター
description: 自動生成された章IDでキーを設定して、再生された各一意の章をレポートします。
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
source-wordcount: '196'
ht-degree: 9%
---

# チャプター

**章** ディメンションは、自動生成された章IDでキーを設定した、再生された各一意の章をレポートします。 IDは、SDKまたはバックエンドによってコンテンツ ID、チャプターインデックス、チャプターの開始時間から構築されるので、同じコンテンツ上の同じチャプターの2つのセッションが1つの行アイテムにロールアップされます。 章の名前、章の長さ、章のオフセット、章の位置など、章レベルの分類の結合キーとしてディメンションを使用します。

## このディメンションの入力方法

[章の開始](/help/implementation/events/chapters/chapter-start.md) イベントが発生すると、章IDが自動的に生成されます。 値は直接設定されず、章の位置、オフセット、コンテンツ IDから派生します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディアチャプター]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.chapter.name`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.ID`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| データフィード | `videochapter`, `post_videochapter` |
| Audience Manager | 該当なし |

## ディメンション項目

各項目は一意の章IDです。 このIDは不透明で（通常はコンテンツ ID + インデックス + オフセットのハッシュ）、グループ化キーとして最も便利です。 [章名](chapter-name.md)と組み合わせると、わかりやすいラベルになります。
