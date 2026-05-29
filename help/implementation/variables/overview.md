---
title: ストリーミングメディア変数の概要
description: ストリーミングメディア変数の構成方法と、Adobe AnalyticsとCustomer Journey Analytics間でのマッピング方法について説明します。
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: 3dbbd5228fcd91cf78c0597dea656c06f367dd40
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
