---
title: コンテンツセグメント
description: セッション中に表示された再生ヘッドの範囲を数分でレポートします。
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
source-wordcount: '202'
ht-degree: 6%
---

# コンテンツセグメント

**コンテンツセグメント** ディメンションは、セッション中に表示された再生ヘッドの範囲を分単位でレポートします（例：`[0-5]`、分単位は0 ～ 5です）。 バックエンドは、再生中に報告された最小および最大の再生ヘッド値からセグメントを計算します。 [ コンテンツセグメントビュー](/help/reporting/metrics/content-segment-views.md)指標と組み合わせて使用すると、長文コンテンツの視聴者が実際に使用している部分を分析できます。

## このディメンションの入力方法

コンテンツセグメントは、セッションのイベントで報告された再生ヘッド値からメディアバックエンドによって計算されます。 クライアントが設定したものではありません。 レポートされる値は、再生中に表示される再生ヘッドの値から派生します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.segment`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.segment`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `videosegment`, `post_videosegment` |
| Audience Manager | `c_contextdata.a.media.segment` |

>[!IMPORTANT]
>
>セッション中に再生ヘッドが正しく報告されない場合、計算されたセグメントが不正確になる可能性があります。 ライブストリームの場合、セグメントは、セッション中に表示される相対的な再生ヘッド値から計算されます。

## ディメンション項目

各項目は、セッション中に表示される再生ヘッド値をカバーする文字列範囲です（例：`[0-5]`、`[5-10]`、`[10-15]`）。 粒度は5分で決まります。
