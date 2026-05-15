---
title: コンテンツセグメント
description: セッション中に表示された再生ヘッドの範囲を数分でレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 6%

---


# コンテンツセグメント

**コンテンツセグメント** ディメンションは、セッション中に表示された再生ヘッドの範囲を分単位でレポートします（例：`[0-5]`、分単位は0 ～ 5です）。 バックエンドは、再生中に報告された最小および最大の再生ヘッド値からセグメントを計算します。 [&#x200B; コンテンツセグメントビュー](/help/reporting/metrics/content-segment-views.md)指標と組み合わせて使用すると、長文コンテンツの視聴者が実際に使用している部分を分析できます。

## このディメンションの入力方法

コンテンツセグメントは、セッションのイベントで報告された再生ヘッド値からメディアバックエンドによって計算されます。 クライアントが設定したものではありません。 レポートされる値は、再生中に表示される再生ヘッドの値から派生します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.segment`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.segment`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videosegment`, `post_videosegment` |
| Audience Manager | `c_contextdata.a.media.segment` |

>[!IMPORTANT]
>
>セッション中に再生ヘッドが正しく報告されない場合、計算されたセグメントが不正確になる可能性があります。 ライブストリームの場合、セグメントは、セッション中に表示される相対的な再生ヘッド値から計算されます。

## ディメンション項目

各項目は、セッション中に表示される再生ヘッド値をカバーする文字列範囲です（例：`[0-5]`、`[5-10]`、`[10-15]`）。 粒度は5分で決まります。
