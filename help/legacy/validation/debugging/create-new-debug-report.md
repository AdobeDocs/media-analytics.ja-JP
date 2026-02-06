---
title: 新しいデバッグレポートの作成
description: 新しいデバッグレポートの作成方法を説明します。
uuid: 438fde3d-98f9-46d1-9672-75d204361568
exl-id: 047acf35-8c1c-4493-9ee7-e2bad47c351e
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 44%

---

# 新しいデバッグレポートの作成{#create-a-new-debug-report}

新しいデバッグレポートを作成するには：

1. 「[!UICONTROL Create New Debug Report]」で、以下を選択します。

   ![](assets/create-new-debug-report.png)

1. フィールドに次の情報を入力します。

   * **レポートに名前を付ける** - プレーヤーの名前と日付を入力します。これにより、認定中にプレーヤーを簡単に追跡し、ブランドとプラットフォームを区別することができます。
   * **Adobe Analytics**

      * [!UICONTROL  ユーザー名 ] および [!UICONTROL  共有暗号鍵 ] – これらのフィールドはオプションですが、web サービス API 資格情報をAdobe デバッグに追加して、レポートスイートの変数名と変数設定を表示することができます。

        にアクセスするには、次のいずれかの方法を使用します。

         * [!UICONTROL Analytics/管理者/会社設定/web サービス ]
         * [!UICONTROL Analytics /管理者/ User Management / ユーザー/個々のユーザーの設定 ] 新しいユーザーの Web サービス API 資格情報を作成するには、[!UICONTROL User Management] で、ユーザーを **Web サービスアクセス** ユーザーグループに追加します。

      * [!UICONTROL Default Endpoint] - このフィールドのデータはアドビが提供します。変更することはできません。
      * [!UICONTROL Extra Endpoint] - CNAME を使用している場合に、`metrics.companyname.com` などのトラッキングサーバーの `CNAMES` を追加します。

   * **ビデオハートビート（Media Analytics）**

      * [!UICONTROL Default Endpoint] - このフィールドのデータはアドビが提供します。変更することはできません。
      * [!UICONTROL Extra Endpoint] - CNAME を使用している場合に、`metrics.companyname.com` などのトラッキングサーバーの `CNAMES` を追加します。
