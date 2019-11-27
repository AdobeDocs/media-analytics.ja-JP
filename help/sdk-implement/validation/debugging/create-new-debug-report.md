---
title: 新しいデバッグレポートの作成
description: ここでは、新しいデバッグレポートの作成方法について説明します。
uuid: 438fde3d-98f9-46d1-9672-75d204361568
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 新しいデバッグレポートの作成 {#create-a-new-debug-report}

新しいデバッグレポートを作成するには：

1. 「[!UICONTROL Create New Debug Report]」で、以下を選択します。

   ![](assets/create-new-debug-report.png)

1. 次の情報を各フィールドに入力します。

   * **Name this reports** - 認定中にプレーヤーを簡単に追跡し、ブランドとプラットフォームを分けておくことができるようにプレーヤー名と日付を入力します。
   * **Adobe Analytics**

      * [!UICONTROL User Name ]および[!UICONTROL  Shared Secret] - これらのフィールドはオプションですが、Adobe Debug に Web サービス API の資格情報を追加すると、レポートスイートの変数名と変数設定を表示できます。

         次のいずれかの方法でアクセスできます。

         * [!UICONTROL Analytics／管理者／カンパニー設定／Web サービス]
         * [!UICONTROL Analytics／管理者／ユーザー管理／ユーザー／個々のユーザーの設定]新しいユーザーの Web サービス API の資格情報を作成するには、[!UICONTROL ユーザー管理]でユーザーを **Web サービスアクセス**&#x200B;ユーザーグループに追加します。
      * [!UICONTROL Default Endpoint] - このフィールドのデータはアドビが提供します。変更することはできません。
      * [!UICONTROL Extra Endpoint] - CNAME を使用している場合に、`metrics.companyname.com` などのトラッキングサーバーの `CNAMES` を追加します。
   * **ビデオハートビート（Media Analytics）**

      * [!UICONTROL Default Endpoint] - このフィールドのデータはアドビが提供します。変更することはできません。
      * [!UICONTROL Extra Endpoint] - CNAME を使用している場合に、`metrics.companyname.com` などのトラッキングサーバーの `CNAMES` を追加します。



