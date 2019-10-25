---
seo-title: オプトアウトおよびプライバシー
title: オプトアウトおよびプライバシー
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
translation-type: tm+mt
source-git-commit: ffb97a0162e0bb609ea427afab81e4d8b532f20b

---


# オプトアウトおよびプライバシー{#opt-out-and-privacy}

## オプトアウトとオプトイン {#opt-out-opt-in}

特定のデバイスでトラッキングアクティビティを許可するかどうかを制御できます。

* **モバイルアプリ** - VA ライブラリは、`AdobeMobile` ライブラリのプライバシーおよびオプトアウト設定に従います。トラッキングをオプトアウトするには、`AdobeMobile` ライブラリを使用する必要があります。`AdobeMobile` ライブラリのオプトアウトおよびプライバシー設定について詳しくは、[オプトアウトおよびプライバシー設定](https://docs.adobe.com/content/help/en/mobile-services/android/gdpr-privacy-android/privacy.html)を参照してください。
* **JavaScript およびブラウザーアプリ** - VA ライブラリは、`VisitorAPI` のプライバシーおよびオプトアウト設定に従います。トラッキングをオプトアウトするには、Visitor API サービスからオプトアウトする必要があります。For further information on opt­out and privacy, see [Adobe Experience Platform Identity Service.](https://marketing.adobe.com/resources/help/en_US/mcvid/).
* **OTTアプリ(Chromecast、Roku)**`opt` - OTT SDKは、データ収集と送信のステータスフラグを設定し、ローカルに保存されたIDを取得できる、General Data Protection Regulation(GDPR)対応のAPIを提供します。

   >[!NOTE]
   >
   >また、プライバシーステータスがオプトアウトに設定されている場合、メディアハートビートトラッキング呼び出しも無効になります。

   次の設定を使用することで、Analytics データが特定のデバイスに送信されるかどうかを制御できます。

   * The `privacyDefault` setting in the `ADBMobile.json` config file. この設定は、コード内で変更されるまで保持される初期設定を制御します。

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
         >ユーザーが追跡をオプトアウトすると、ユーザーが再びオプトインするまで、持続的なすべてのデバイスデータとIDが削除されます。

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

## Retrieving Stored Identifiers (OTT Apps) {#retrieving-stored-identifiers-ott-apps}

この情報は、ローカルに保存されているユーザー ID を Roku アプリケーションから取得する場合に役立ちます。

>[!IMPORTANT]
>
>すべての識別子を取得する方法は、SDKが認識し、保持するすべてのユーザーIDを取得します。 このメソッドは、ユーザーがオプトアウトする&#x200B;**前**&#x200B;に呼び出す必要があります。

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

