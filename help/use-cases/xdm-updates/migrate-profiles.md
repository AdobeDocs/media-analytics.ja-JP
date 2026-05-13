---
title: プロファイルを新しいストリーミングメディアフィールドに移行する
description: プロファイルを新しいストリーミングメディアフィールドに移行する方法を説明します
feature: Streaming Media
role: User, Admin, Developer
exl-id: 0f75e594-5216-4ac1-91bd-fa89ab4b2110
TQID: https://experienceleague.adobe.com/c1WHnEeZnI3PP6aO40pDHpJCi2Z0ERiNY8lCj4wyMiU
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 533
ht-degree: 0%

---

# プロファイルを新しいストリーミングメディアフィールドに移行

このドキュメントでは、ストリーミングメディアデータに対してAdobe Analyticsが有効になっているAdobe Data Collection フローの上に存在するプロファイルフィルタリングサービスを移行するプロセスについて説明します。 この移行は、プロファイルフィルタリングサービスを「Media」というAdobe ストリーミングメディアサービスのデータタイプを使用して変換し、「[Media Reporting Details](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)」という新しい対応するデータタイプを使用します。

## プロファイルの移行

プロファイルフィルタリングを「メディア」と呼ばれる古いデータタイプから「[ メディアレポートの詳細](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)」と呼ばれる新しいデータタイプに移行するには、既存のプロファイルフィルタリングルールを編集する必要があります。

1. Adobe Experience Platformの「[!UICONTROL **ソース**]」セクションで、「[!UICONTROL **データフロー**]」タブに移動します。

1. Adobe Data Collectionを使用して、Adobe AnalyticsからAdobe Experience Platformにストリーミングメディアデータを読み込むデータフローを見つけます。

1. 非推奨フィールドを含むすべてのカスタムルールを、新しいXDM オブジェクトの新しい対応するフィールドに置き換えることで、[!UICONTROL **データフローの更新**]&#x200B;を選択して、プロファイルフィルタリングの設定を変更します。

1. 非推奨の「メディア」オブジェクトのフィールドを含むフィルターを探します。

1. 新しい「Media Reporting Details」オブジェクトからフィールドを追加して、これらのフィルターを追加します。

1. 2つのフィールド間にOR演算子を使用します。

1. プロファイルが期待どおりに動作していることを確認します。

古いフィールドと新しいフィールドの間のマッピングについては、[ コンテンツ ID](/help/reporting/dimensions/content.md) パラメーターと、[ ストリーミングメディアサービス ](/help/media-overview.md)に記載されているストリーミングメディア変数の残りの部分を参照してください。 古いフィールドパスは「XDM フィールドパス」プロパティの下にあり、新しいフィールドパスは「レポート XDM フィールドパス」プロパティの下にあります。

## 例

移行ガイドラインに簡単に従えるように、単一のプロファイルフィルタリングルールを含む次のデータフローの例を考えてみましょう。 この場合、ルールは1つしかないため、移行ガイドラインを1回だけ適用する必要があります。

1. Adobe Experience Platformの「[!UICONTROL **ソース**]」セクションで、「[!UICONTROL **データフロー**]」タブに移動します。

1.Adobe AnalyticsからAdobe Analyticsを介してAdobe Experience Platformにストリーミングメディアデータを読み込むデータフローを見つけます。

1. 次の画像に示すように、**[!UICONTROL データフローを更新]**&#x200B;を選択して編集UIに入ります。

   ![AEP データフロープロファイル ](assets/aep-dataflow-profile.jpeg)

1. 「**[!UICONTROL 次へ]**」を選択して、「フィルター」タブに移動します。

   ![AEP データフローフィルタータブ ](assets/aep-dataflow-filtering-profile.jpeg)

1. 「**[!UICONTROL フィルタリング]**」タブで、`media.mediaTimed` フィールドに依存するフィルタリングルールを特定します。

   ![AEP データフローフィルタールール ](assets/dataflow-filtering-rules-profile.jpeg)


   meda.mediaTimed オブジェクトを使用する各フィルターについて、[ ストリーミングメディアサービス ](/help/media-overview.md)に記載されているストリーミングメディア変数を使用して、`mediaReporting` オブジェクト内の対応するフィールドを検索し、古いフィールドと新しいフィールドの間をマッピングします。 古いフィールドパスは「XDM フィールドパス」プロパティの下にあり、新しいフィールドパスは「レポート XDM フィールドパス」プロパティの下にあります。 例えば、[Media Starts](/help/reporting/metrics/media-starts.md)の場合、`media.mediaTimed.impressions.value`の通信相手は`mediaReporting.sessionDetails.isViewed`です。

   ![新しいXDM フィールドと古いXDM フィールド ](assets/xdm-fields-new-and-old.jpeg)

1. 関連する`mediaReporting` フィールドをフィルタリングルールにドラッグし、2つのルール間でOR演算子を使用します。 新しいフィールドを使用する場合は、既存のルールと同じルールを追加します。

   ![ フィルタールールを追加](assets/add-filter-rules.jpeg)

1. **[!UICONTROL 次へ]**&#x200B;を選択して変更を保存します。
