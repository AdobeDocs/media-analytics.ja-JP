---
title: オプトアウトとプライバシーについて
description: オプトイン、オプトアウトおよびプライバシーの取り扱い方法を説明します。
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
exl-id: 64f5ef2b-7850-43d8-8f32-3d008ea4f156
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/eF09wxu2mIUoFph5EdHz5y0XtcpXHHLINqSGLQEMoHU
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 382
ht-degree: 92%

---

# オプトアウトおよびプライバシー{#opt-out-and-privacy}

## オプトアウトとオプトイン {#opt-out-opt-in}

特定のデバイスでトラッキングアクティビティを許可するかどうかを制御できます。

* **モバイルアプリ -** メディア拡張機能は、データ収集のプライバシー設定に従います。 トラッキングをオプトアウトするには、プライバシーを「[タグでオプトアウト](https://developer.adobe.com/client-sdks/documentation/getting-started/create-a-mobile-property/#create-a-mobile-property)」または「[Mobile SDK のプライバシーステータスを更新](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/#getprivacystatus)」に設定する必要があります。
* **JavaScript およびブラウザーアプリ** - VA ライブラリは、`VisitorAPI` のプライバシーおよびオプトアウト設定に従います。 トラッキングをオプトアウトするには、Visitor API サービスからオプトアウトする必要があります。 オプトアウトとプライバシーについて詳しくは、[Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=ja)を参照してください。
* **OTT アプリ（Chromecast、Roku）-** OTT SDK は、EU 一般データ保護規則（GDPR）対応の API を提供します。これらの API を使用して、データ収集および送信の `opt` ステータスフラグを設定し、ローカルに保存されている ID を取得できます。

  >[!NOTE]
  >
  >プライバシーのステータスがオプトアウトに設定されている場合、メディアハートビートトラッキングコールも無効になります。

  次の設定を使用することで、Analytics データが特定のデバイスに送信されるかどうかを制御できます。

   * `ADBMobile.json` 設定ファイル内の `privacyDefault` 設定。 この設定は、コード内で変更されるまで保持される初期設定を制御します。

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

## 保存されている ID の取得（OTT アプリ） {#retrieving-stored-identifiers-ott-apps}

この情報は、ローカルに保存されているユーザー ID を Roku アプリケーションから取得する場合に役立ちます。

>[!IMPORTANT]
>
>すべての ID を取得するこのメソッドは、既知のユーザー ID、および SDK によって保持されているユーザー ID をすべて取得します。 このメソッドは、ユーザーがオプトアウトする&#x200B;**前**&#x200B;に呼び出す必要があります。

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
