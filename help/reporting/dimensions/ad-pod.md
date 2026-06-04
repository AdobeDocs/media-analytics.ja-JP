---
title: 広告ポッド
description: 自動生成されたポッド IDでキーを設定した、各一意の広告枠をレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 7%

---


# 広告ポッド

**広告ポッド** ディメンションは、自動生成されたポッド IDでキーが設定された各一意の広告枠をレポートします。 セッション内のすべての広告は親の広告ポッドに属し、ポッドグループは複数の広告を連続して再生します。 ディメンションを使用して、広告ブレークでエンゲージメントを分割し、[&#x200B; ポッド名](pod-name.md)と[&#x200B; ポッド位置](pod-position.md)の分類の結合キーとして使用します。

## このディメンションの入力方法

広告ポッド IDは、[広告ブレーク開始](/help/implementation/events/ads/ad-break-start.md) イベントが発生したときに、SDKによって自動的に生成されます。 直接API実装では、ブレイクインデックスと開始時間から構築するか、カスタムポッド IDを指定します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア広告]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.ad.pod`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingPodDetails.ID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| データフィード | `videoadpod`, `post_videoadpod` |
| Audience Manager | 該当なし |

## ディメンション項目

各項目は一意の広告ポッド IDです。 このIDは不透明で（通常はセッション ID、コンテンツ ID、区切りインデックスのハッシュ）、フレンドリーラベルの[Pod name](pod-name.md)と組み合わせると、グループ化キーとして最も便利です。
