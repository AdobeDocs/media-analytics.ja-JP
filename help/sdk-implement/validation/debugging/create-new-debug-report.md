---
seo-title: 新しいデバッグレポートの作成
title: 新しいデバッグレポートの作成
uuid: 438fde3d-98f9-46d1-9672-75d204361568
translation-type: tm+mt
source-git-commit: f2b08663a928e27625a9ff63f783c510f41e7a8c

---


# 新しいデバッグレポートの作成{#create-a-new-debug-report}

新しいデバッグレポートを作成するには：

1. In [!UICONTROL Create New Debug Report] select the following:

   ![](assets/create-new-debug-report.png)

1. 次の情報を各フィールドに入力します。

   * **Name this reports** - 認定中にプレーヤーを簡単に追跡し、ブランドとプラットフォームを分けておくことができるようにプレーヤー名と日付を入力します。
   * **Adobe Analytics**

      * [!UICONTROL User Name ]および[!UICONTROL  Shared Secret] - これらのフィールドはオプションですが、Adobe Debug に Web サービス API の資格情報を追加すると、レポートスイートの変数名と変数設定を表示できます。

         次のいずれかの方法でアクセスできます。

         * [!UICONTROL Analytics／管理者／カンパニー設定／Web サービス]
         * [!UICONTROL Analytics／管理者／ユーザー管理／ユーザー／個々のユーザーの設定]新しいユーザーの Web サービス API の資格情報を作成するには、[!UICONTROL ユーザー管理]でユーザーを **Web サービスアクセス**&#x200B;ユーザーグループに追加します。
      * [!UICONTROL デフォルトのエンドポイント] — このフィールドのデータはアドビから提供され、変更できません。
      * [!UICONTROL Extra Endpoint] — 使 `CNAMES`用する場合は、 `metrics.companyname.com`
   * **ビデオハートビート(Media Analytics)**

      * [!UICONTROL デフォルトのエンドポイント] — このフィールドのデータはアドビから提供され、変更できません。
      * [!UICONTROL 追加のエンドポ] イント `CNAMES`— トラッキングサーバー用に追加します(例： `metrics.companyname.com`)。



