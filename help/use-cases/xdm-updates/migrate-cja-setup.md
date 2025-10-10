---
title: オーディエンスを新しい Adobe Analytics for Streaming Media データタイプに移行する
description: オーディエンスを新しい Adobe Analytics for Streaming Media データタイプに移行する方法を説明します
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: 67e67a4b-bd61-4247-93b7-261bd348d29b
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 1%

---

# 新しいストリーミングメディアフィールドを使用するようにCustomer Journey Analyticsを移行する

このドキュメントでは、「Media」と呼ばれるAdobe ストリーミングメディアサービスのデータタイプを使用するCustomer Journey Analytics設定を、「[&#x200B; メディアレポートの詳細 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/media-reporting-details) と呼ばれる新しい対応するデータタイプを使用するように更新する方法について説明します。

## Customer Journey Analyticsを移行

Customer Journey Analyticsの設定を「Media」という古いデータタイプから「[Media レポートの詳細 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/media-reporting-details)」という新しいデータタイプに移行するには、古いデータタイプを使用している次の設定を更新する必要があります。

* データビュー

* 派生フィールド

### データビューを移行

データ・ビューを新しいデータ・タイプに移行するには、次の手順に従います。

1. 非推奨の「メディア」データタイプを使用して、すべてのデータビューを見つけます。 これは、パスが `media.mediaTimed` で始まるすべてのフィールドです。

1. 次のいずれかの操作を行います。

   * これらのデータビューで、新しい「メディアレポートの詳細」データタイプのフィールドを挿入します。

   * 新しい「メディアレポートの詳細」データタイプが設定されている場合は、それを使用する派生フィールドを作成します。「メディアレポートの詳細」データタイプが設定されていない場合は、古い「メディア」データタイプにフォールバックします。

### 派生フィールドを移行

派生フィールドを新しいデータタイプに移行するには、次の手順に従います。

1. 非推奨の「メディア」データタイプを使用して、すべての派生フィールドを見つけます。 これは、パスが `media.mediaTimed` で始まるフィールドを含むすべての派生フィールドです。

1. 派生フィールドの古いフィールドをすべて、「メディアレポートの詳細」の新しい対応するフィールドに置き換えます。

古いフィールドと新しいフィールド間のマッピングについては、[&#x200B; オーディオおよびビデオパラメーター &#x200B;](https://experienceleague.adobe.com/ja/docs/media-analytics/using/implementation/variables/audio-video-parameters#content-id) ページの [&#x200B; コンテンツ ID](https://experienceleague.adobe.com/ja/docs/media-analytics/using/implementation/variables/audio-video-parameters) パラメーターを参照してください。 古いフィールドパスは「XDM フィールドパス」プロパティの下にあり、新しいフィールドパスは「レポート XDM フィールドパス」プロパティの下にあります。

![&#x200B; 新しい古い XDM フィールドのパス &#x200B;](assets/field-paths-updated.jpeg)

## 例

移行ガイドラインに従いやすくするために、古い非推奨（廃止予定）の「メディア」データタイプのフィールドを含むデータビューを含む次の例を考えてみましょう。 このデータビューでは、対応する新しいフィールドを追加する必要があります。

### データビューを更新

次のいずれかのオプションを使用して、データビューを更新できます。

#### オプション 1

1. 非推奨（廃止予定）のデータタイプの古いフィールドを使用している指標またはディメンションを見つけます。

   ![&#x200B; データビューの古いフィールドパス &#x200B;](assets/old-field-data-view.jpeg)

1. [&#x200B; チャプターパラメーター &#x200B;](https://experienceleague.adobe.com/ja/docs/media-analytics/using/implementation/variables/chapter-parameters#chapter-offset) 記事の [&#x200B; チャプターオフセット &#x200B;](https://experienceleague.adobe.com/ja/docs/media-analytics/using/implementation/variables/chapter-parameters) セクションで、対応する新しいフィールドを確認します。

1. データビュー内の対応する新しいフィールドを見つけます。

   ![&#x200B; データビューの新しいフィールドパス &#x200B;](assets/new-field-data-view.jpeg)

1. 新しいフィールドを指標またはディメンションにドラッグします。

1. 非推奨の「メディア」データタイプのフィールドを使用するすべての指標およびディメンションに対して、このプロセスを繰り返します。

#### オプション 2

このオプションは、特定のイベントに対して存在する値に基づいて、古いフィールドから値を選択する派生フィールドまたは新しいフィールドから値を選択する派生フィールドを作成します。 この派生フィールドは、使用されているプロジェクトの古い「メディア」データタイプを置き換えます。

新しい「メディアレポートの詳細」データタイプが設定されている場合はそのデータタイプを使用する「チャプター名」の派生フィールドを作成する場合、「メディアレポートの詳細」データタイプが設定されていない場合は古い「メディア」データタイプにフォールバックする場合：

1. 「Case When」句を派生フィールドにドラッグします。

   ![&#x200B; 新しいフィールドをカスタマイズしてデータビューを作成する &#x200B;](assets/create-derived-field2.jpeg)

1. [!UICONTROL **チャプターパラメーター**] ページの **チャプター名** パラメーターに示されているように、[&#x200B; レポート XDM フィールドパス &#x200B;](https://experienceleague.adobe.com/ja/docs/media-analytics/using/implementation/variables/chapter-parameters#chapter-name) の値を使用して [If](https://experienceleague.adobe.com/ja/docs/media-analytics/using/implementation/variables/chapter-parameters) 句に入力します。

   ![&#x200B; チャプター名 &#x200B;](assets/chapter-name.jpeg)

   ![&#x200B; チャプター名 &#x200B;](assets/chapter-name2.jpeg)

   ![&#x200B; 派生フィールドの条件 &#x200B;](assets/derived-field-condition.jpeg)

   ![&#x200B; 派生フィールドチャプター名 &#x200B;](assets/derived-field-chapter-name.jpeg)

1. 非推奨の「メディア」データタイプの古いフィールドを使用して、フォールバック値を入力します。

   ![&#x200B; フォールバック値 &#x200B;](assets/fallback-value.jpeg)

   ![&#x200B; フォールバック値 &#x200B;](assets/fallback-value2.jpeg)

   これが、派生フィールドの最終的な定義です。

   ![&#x200B; 派生フィールドの完成 &#x200B;](assets/derived-field-complete.jpeg)

1. 派生フィールドを更新するには、古い非推奨フィールド（`media.mediaTimed` で始まるパス）を使用している派生フィールドを見つけます。

   ![&#x200B; 派生フィールド &#x200B;](assets/old-derived-field.jpeg)

1. 更新する派生フィールドの上にマウスポインターを置き、「[!UICONTROL **編集**] アイコンを選択します。

1. 古いデータタイプ（`media.mediaTimed` で始まるパス）からすべてのフィールドを見つけ、新しい対応するフィールドに置き換えます。

   ![&#x200B; 古いデータタイプを持つフィールドを見つけます &#x200B;](assets/locate-fields-with-old-datatype.jpeg)

1. [&#x200B; ストリーミングメディアパラメーター &#x200B;](https://experienceleague.adobe.com/ja/docs/media-analytics/using/implementation/variables/audio-video-parameters#content-name-variable) 記事の [&#x200B; コンテンツ名（変数） &#x200B;](https://experienceleague.adobe.com/ja/docs/media-analytics/using/implementation/variables/audio-video-parameters#content-name-variable) セクションで、対応する新しいフィールドを確認します。

1. 古いフィールドを新しいフィールドに置き換えます。

   ![&#x200B; 新しいフィールド &#x200B;](assets/derived-field-new.jpeg)

1. 古い非推奨（廃止予定）の「メディア」データタイプのフィールドを使用して、すべての派生フィールドに対してこのプロセスを繰り返します。

   CJA設定の移行が完了しました。
