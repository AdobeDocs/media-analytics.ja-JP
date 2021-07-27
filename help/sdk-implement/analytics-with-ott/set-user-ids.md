---
title: ユーザー ID の設定
description: 一意の顧客識別子として提供されるユーザー ID を設定するための API。
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
exl-id: 6b451082-47f3-4e65-9fe0-cecb2d20dc2d
feature: Media Analytics、API
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: ht
source-wordcount: '56'
ht-degree: 100%

---

# ユーザー ID の設定 {#set-user-ids}

ユーザー ID はアプリケーションがユーザーに対して定義する一意のカスタム訪問者識別子です。

ADBMobile SDK で一意のユーザー ID を設定および取得する手順は次のとおりです。

* **設定:**

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
