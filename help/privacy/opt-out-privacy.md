---
title: オプトアウトおよびプライバシーの説明
description: オプトイン、オプトアウトおよびプライバシーを処理する方法について説明します。
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
exl-id: 64f5ef2b-7850-43d8-8f32-3d008ea4f156
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 96%

---

# オプトアウトおよびプライバシー{#opt-out-and-privacy}

## オプトアウトとオプトイン {#opt-out-opt-in}

特定のデバイスでトラッキングアクティビティを許可するかどうかを制御できます。

* **モバイルアプリ** - VA ライブラリは、`AdobeMobile` ライブラリのプライバシーおよびオプトアウト設定に従います。トラッキングをオプトアウトするには、`AdobeMobile` ライブラリを使用する必要があります。`AdobeMobile` ライブラリのオプトアウトおよびプライバシー設定について詳しくは、[オプトアウトおよびプライバシー設定](https://experienceleague.adobe.com/docs/mobile-services/android/gdpr-privacy-android/privacy.html?lang=ja)を参照してください。
* **JavaScript およびブラウザーアプリ** - VA ライブラリは、`VisitorAPI` のプライバシーおよびオプトアウト設定に従います。トラッキングをオプトアウトするには、Visitor API サービスからオプトアウトする必要があります。オプトアウトおよびプライバシーについて詳しくは、[Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=ja) を参照してください。
* **OTT アプリ（Chromecast、Roku）-** OTT SDK は、EU 一般データ保護規則（GDPR）対応の API を提供します。これらの API を使用して、データ収集および送信の `opt` ステータスフラグを設定し、ローカルに保存されている ID を取得できます。

   >[!NOTE]
   >
   >プライバシーのステータスがオプトアウトに設定されている場合、メディアハートビートトラッキングコールも無効になります。

   次の設定を使用することで、Analytics データが特定のデバイスに送信されるかどうかを制御できます。

   * `ADBMobile.json` 設定ファイル内の `privacyDefault` 設定。この設定は、コード内で変更されるまで保持される初期設定を制御します。

   * `ADBMobile().setPrivacyStatus()` メソッド。

      * **オプトアウト：**

         * **Chromecast：**

            ```
            ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_OUT)
            ```

         * **Roku：**

            ```
            ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_OUT)
            ```
         >[!IMPORTANT]
         >
         >ユーザーがトラッキングをオプトアウトすると、再度オプトインするまで、永続化されたデバイスデータと ID がすべて消去されます。

      * **再度オプトインする：**

         * **Chromecast：**

            ```
            ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_IN)
            ```

         * **Roku：**

            ```
            ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)
            ```
      * **現在の設定を返す：**

         * **Chromecast：**

            ```
            ADBMobile.config.getPrivacyStatus()
            ```

         * **Roku：**

            ```
            ADBMobile().getPrivacyStatus()
            ```
   `setPrivacyStatus` を使用してプライバシー設定を変更した後は、同じメソッドを使用して再度変更されるまで、またはアプリを完全にアンインストールして再度インストールするまで、変更が保持されます。

## 保存されている ID の取得（OTT アプリ）  {#retrieving-stored-identifiers-ott-apps}

この情報は、ローカルに保存されているユーザー ID を Roku アプリケーションから取得する場合に役立ちます。

>[!IMPORTANT]
>
>すべての ID を取得するこのメソッドは、既知のユーザー ID、および SDK によって保持されているユーザー ID をすべて取得します。このメソッドは、ユーザーがオプトアウトする&#x200B;**前**&#x200B;に呼び出す必要があります。

ローカルに保存された ID は JSON 文字列で返されます。この文字列には次の情報が含まれている可能性があります。

* 会社コンテキスト - IMS 組織 ID
* ユーザー ID
* Experience Cloud ID（MCID）
* データソース ID（DPID、DPUUID）
* Analytics ID（AVID、AID、VID、関連する RSID）
* Audience Manager ID（UUID）

次に例を示します。

* **Chromecast：**

   ```
   ADBMobile.config.getAllIdentifiersAsync(callback)
   ```

* **Roku：**

   ```
   vids = ADBMobile().getAllIdentifiers()
   ```
