---
title: ストリーミングメディア変数の概要
description: ストリーミングメディア変数の構成方法と、Adobe AnalyticsとCustomer Journey Analytics間でのマッピング方法について説明します。
feature: Streaming Media
role: User, Admin, Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 2%
---

# ストリーミングメディア変数の概要

変数は、コンテンツ名、ストリームタイプ、広告名、再生品質など、メディアプレーヤーがストリームに関して提供するデータです。 ほとんどの変数はセッションの開始時に設定され、メディアバックエンドがセッションをクローズするまで通過します。このバックエンドでは、変数を使用してレポートで使用するディメンションと指標を設定します。 各変数ページでは、サポートされているすべての実装方法で変数を設定する方法を説明します。

## Adobeへの変数の送信方法

Adobeのアプリケーションやサービスごとに同じ値が格納されますが、その値のフォーマットは、送信場所によって異なります。 次の表に、各アプリケーションまたはサービスと、想定される変数形式を示します。 各変数ページのプロパティテーブルには、各形式で使用する正確な値が表示されます。

| データ形式 | 説明 |
| --- | --- |
| コンテキストデータ変数 | Adobe Analyticsに送信される書式は、`a.media`接頭辞（`a.media.name`など）が付いた名前になっています。 |
| XDM コレクションフィールド | Customer Journey Analyticsに送信されるフォーマットで、XDM フィールドパス（`xdm.mediaCollection.sessionDetails.name`など）として表されます。 |
| Audience Manager特性 | Audience Managerに転送されるフォーマットで、先頭に`c_contextdata` （`c_contextdata.a.media.name`など）が付いています。 |

>[!MORELIKETHIS]
>
>* [ イベントの概要](/help/implementation/events/overview.md)：変数を含むプレイヤーイベント
>* [ ディメンションの概要](/help/reporting/dimensions/overview.md)：変数が入力するレポートディメンション
>* [指標の概要](/help/reporting/metrics/overview.md)：変数が入力するレポート指標
