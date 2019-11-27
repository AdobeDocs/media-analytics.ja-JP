---
title: ユーザー ID の設定
description: 一意の顧客識別子として提供されるユーザー ID を設定するための API。
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# ユーザー ID の設定 {#set-user-ids}

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
