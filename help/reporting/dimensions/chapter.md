---
title: チャプター
description: 自動生成された章IDでキーを設定して、再生された各一意の章をレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 6%

---


# チャプター

**章** ディメンションは、自動生成された章IDでキーを設定した、再生された各一意の章をレポートします。 IDは、SDKまたはバックエンドによってコンテンツ ID、チャプターインデックス、チャプターの開始時間から構築されるので、同じコンテンツ上の同じチャプターの2つのセッションが1つの行アイテムにロールアップされます。 章の名前、章の長さ、章のオフセット、章の位置など、章レベルの分類の結合キーとしてディメンションを使用します。

## このディメンションの入力方法

`media.chapterStart`が起動すると、章IDが自動的に生成されます。 値は直接設定されず、章の位置、オフセット、コンテンツ IDから派生します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディアチャプター]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.chapter.name`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.ID`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| データフィード | `videochapter, post_videochapter` |

## ディメンション項目

各項目は一意の章IDです。 このIDは不透明で（通常はコンテンツ ID + インデックス + オフセットのハッシュ）、グループ化キーとして最も便利です。 [章名](chapter-name.md)と組み合わせると、わかりやすいラベルになります。
