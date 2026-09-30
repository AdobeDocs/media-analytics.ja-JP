---
title: 分平均オーディエンス
description: コンテンツのランタイム全体で任意の時間に視聴している視聴者の平均数をレポートします。
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 12%
---

# 分平均オーディエンス

**分平均オーディエンス**&#x200B;指標は、コンテンツのランタイム全体で任意の分に視聴している視聴者の平均数をレポートします。 これは、異なる長さのコンテンツ間でメディアリーチを比較するために使用される標準的な「AMA」測定です。

## この指標の計算方法

メディア バックエンドは、セッションあたりの分平均オーディエンスを`Content time spent / Content length`として計算します。 セッション全体で合計した場合、合計はコンテンツの1分あたりの平均オーディエンスサイズを表します。 この指標は、クローズ呼び出しで報告されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.averageMinuteAudience`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.averageMinuteAudience`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| データフィード | `event_list`、`post_event_list` （[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)参照） |
| Audience Manager | `c_contextdata.a.media.averageMinuteAudience` |

>[!IMPORTANT]
>
>分平均オーディエンス数には、ゼロ以外の[ コンテンツ長](/help/reporting/dimensions/content-length.md)が必要です。 コンテンツの長さが未設定または0の場合、この指標はセッション用に生成されません。
