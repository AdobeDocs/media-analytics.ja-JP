---
seo-title: ユーザー ID の設定
title: ユーザー ID の設定
uuid: fdd54fec-79cd-4bf8- b17e-4d61d84f6310
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# ユーザー ID の設定{#set-user-ids}

ユーザー ID はアプリケーションがユーザーに対して定義する一意のカスタム訪問者識別子です。

ADBMobile SDK で一意のユーザー ID を設定および取得する手順は次のとおりです。

* **設定：**

   * **Roku：**

      ```
      ADBMobile().setUserIdentifer("app-generated-unique-id")
      ```

   * **Chromecast：**

      ```
      ADBMobile().config.setUserIdentifer("app-generated-unique-id");
      ```

* **取得：**

   * **Roku：**

      ```
      vid = ADBMobile().userIdentifer()
      ```

   * **Chromecast：**

      ```
      vid = ADBMobile().config.getUserIdentifer();
      ```
