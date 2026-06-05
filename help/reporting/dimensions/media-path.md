---
title: メディアパス
description: パス分析用のトラフィック変数としてコンテンツ IDをキャプチャします。
feature: Dimensions
role: User, Admin
source-git-commit: 7b5232f25f3aa26e8566783557163f316af3fe57
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 5%

---


# メディアパス

**メディアパス** ディメンションは、コンテンツ IDをトラフィック変数（prop）としてキャプチャし、パス分析で使用できるようにします（次のコンテンツと前のコンテンツのフローレポートなど）。 これはAdobe Analyticsに固有のものです。Customer Journey Analyticsはトラフィック変数を保存せず、パスはContent （ID）ディメンションで直接実行されます。

## このディメンションの入力方法

メディアパスは、セッション開始時に設定されたコンテンツ IDから自動的に取得されます。 設定する個別の変数はありません。コンテンツ（ID）が入力されるたびに、データフィード列`videopath`が入力されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.name`からトラフィック変数（prop）として自動的に収集されます。 |
| Customer Journey Analytics | なし – パス分析には[Content](content.md)を使用します。 |
| データフィード | `videopath`, `post_videopath` |
| Audience Manager | `c_contextdata.a.media.name` |

>[!NOTE]
>
>Adobe Analytics propには100 バイトの制限があります。 100 バイトを超える値は切り捨てられます。

>[!IMPORTANT]
>
>パスレポートは、同じ訪問内のヒット間のprop値を比較します。 訪問中にコンテンツ（ID）が変更された場合（例えば、ビューアがあるコンテンツから別のコンテンツに移動した場合）、パスレポートはそのフローを示します。

## ディメンション項目

各項目は、訪問中に報告されたコンテンツ IDです。 フローパネルを使用して、コンテンツ間のナビゲーションパスを表示できます。
