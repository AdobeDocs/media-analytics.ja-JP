---
title: ストリーミングメディア用の新しいAdobe Analytics データタイプへのオーディエンスの移行
description: 新しいAdobe Analytics for Streaming Media データタイプにオーディエンスを移行する方法について説明します
feature: Streaming Media
role: User, Admin, Developer
exl-id: 67e67a4b-bd61-4247-93b7-261bd348d29b
TQID: https://experienceleague.adobe.com/Y-Y-xWKm-zOzaQm8kMbgGx8r6BTNLl-Q5AltlF5v7aA
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 759
ht-degree: 1%

---

# Customer Journey Analyticsを移行して、新しいストリーミングメディアフィールドを使用する

このドキュメントでは、「Media」という名前のAdobe ストリーミングメディアサービスのデータタイプを使用するCustomer Journey Analyticsの設定を、「[Media Reporting Details](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)」という名前の新しい対応するデータタイプを使用するように更新する方法について説明します。

## Customer Journey Analyticsの移行

Customer Journey Analytics設定を「Media」という古いデータ型から「[Media Reporting Details](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)」という新しいデータ型に移行するには、古いデータ型を使用している次の設定を更新する必要があります。

* データビュー

* 派生フィールド

### データビューの移行

データビューを新しいデータタイプに移行するには：

1. 非推奨の「メディア」データタイプを使用して、すべてのデータビューを検索します。 これは、パスが`media.mediaTimed`で始まるすべてのフィールドです。

1. 次のいずれかの操作を行います。

   * これらのデータビューで、新しい「Media Reporting Details」データタイプからフィールドを挿入します。

   * 新しい「Media Reporting Details」データタイプが設定されている場合は使用する、新しい「Media Reporting Details」データタイプが設定されていない場合は古い「Media」データタイプにフォールバックする派生フィールドを作成します。

### 派生フィールドの移行

派生フィールドを新しいデータタイプに移行するには：

1. 非推奨の「メディア」データタイプを使用して、すべての派生フィールドを探します。 これは、パスが`media.mediaTimed`で始まるフィールドを含むすべての派生フィールドです。

1. 派生フィールドのすべての古いフィールドを、「Media Reporting Details」の新しい対応するフィールドに置き換えます。

古いフィールドと新しいフィールドの間のマッピングについては、[&#x200B; コンテンツ ID](/help/reporting/dimensions/content.md) パラメーターと、[&#x200B; ストリーミングメディアサービス &#x200B;](/help/media-overview.md)に記載されているストリーミングメディア変数の残りの部分を参照してください。 古いフィールドパスは「XDM フィールドパス」プロパティの下にあり、新しいフィールドパスは「レポート XDM フィールドパス」プロパティの下にあります。

![古いXDM フィールドパスと新しいXDM フィールドパス &#x200B;](assets/field-paths-updated.jpeg)

## 例

移行ガイドラインに従いやすくするために、古い非推奨の「メディア」データタイプのフィールドを含むデータビューを含む次の例を考えてみましょう。 このデータビューでは、対応する新しいフィールドを追加する必要があります。

### データビューの更新

次のいずれかのオプションを使用して、データビューを更新できます。

#### オプション 1

1. 非推奨のデータタイプから、古いフィールドを使用している指標またはディメンションを探します。

   ![&#x200B; データビューの古いフィールドパス &#x200B;](assets/old-field-data-view.jpeg)

1. [章オフセット &#x200B;](/help/reporting/dimensions/chapter-offset.md)記事の対応する新しいフィールドを確認してください。

1. データビューで、新しい対応するフィールドを見つけます。

   ![&#x200B; データビューの新しいフィールドパス &#x200B;](assets/new-field-data-view.jpeg)

1. 新しいフィールドを指標またはディメンションにドラッグします。

1. 非推奨の「メディア」データタイプのフィールドを使用するすべての指標とディメンションに対して、このプロセスを繰り返します。

#### オプション 2

このオプションは、特定のイベントに存在するフィールドに基づいて、古いフィールドの値または新しいフィールドの値を選択する派生フィールドを作成します。 この派生フィールドは、使用されているプロジェクトの古い「メディア」データタイプを置き換えます。

新しい「Media Reporting Details」データタイプが設定されている場合は「Chapter Name」の派生フィールドを作成する場合、または「Media Reporting Details」データタイプが設定されていない場合は古い「Media」データタイプにフォールバックする場合：

1. 「Case When」句を派生フィールドにドラッグします。

   ![新しいフィールドをカスタマイズしてデータビューを作成する](assets/create-derived-field2.jpeg)

1. [章名](/help/reporting/dimensions/chapter-name.md) ページに示すように、**レポート XDM フィールドパス**&#x200B;の値を使用して&#x200B;[!UICONTROL **If**]&#x200B;句を入力します。

   ![章名](assets/chapter-name.jpeg)

   ![章名](assets/chapter-name2.jpeg)

   ![派生フィールド条件](assets/derived-field-condition.jpeg)

   ![派生フィールドの章名](assets/derived-field-chapter-name.jpeg)

1. 非推奨の「メディア」データタイプの古いフィールドを使用してフォールバック値を入力します。

   ![&#x200B; フォールバック値](assets/fallback-value.jpeg)

   ![&#x200B; フォールバック値](assets/fallback-value2.jpeg)

   これが派生フィールドの最終的な定義です。

   ![派生フィールドが完了](assets/derived-field-complete.jpeg)

1. 派生フィールドを更新するには、古い非推奨フィールド（`media.mediaTimed`で始まるパス）を使用している派生フィールドを見つけます。

   ![派生フィールド &#x200B;](assets/old-derived-field.jpeg)

1. 更新する派生フィールドにマウスポインターを置き、[!UICONTROL **編集**] アイコンを選択します。

1. 古いデータタイプ（`media.mediaTimed`で始まるパス）のすべてのフィールドを見つけ、新しい対応するフィールドに置き換えます。

   ![古いデータ型を持つフィールドを探す](assets/locate-fields-with-old-datatype.jpeg)

1. [&#x200B; コンテンツ名](/help/reporting/dimensions/content-name.md)記事の対応する新しいフィールドを確認してください。

1. 古いフィールドを新しいフィールドに置き換えます。

   ![新しいフィールド &#x200B;](assets/derived-field-new.jpeg)

1. 古い非推奨の「メディア」データタイプのフィールドを使用して、すべての派生フィールドに対してこのプロセスを繰り返します。

   CJA設定の移行が完了しました。
