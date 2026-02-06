---
title: ユーザー ID の設定
description: 一意の顧客識別子として提供されるユーザー ID を設定するための API。
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
exl-id: 6b451082-47f3-4e65-9fe0-cecb2d20dc2d
feature: "Streaming Media, API"
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 45%

---

# ユーザー ID の設定 {#set-user-ids}

ユーザー ID は、アプリケーションでユーザーに対して定義される一意のカスタム訪問者識別子です。

ADBMobile SDKに一意のユーザー ID を次のように設定して取得します。

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
