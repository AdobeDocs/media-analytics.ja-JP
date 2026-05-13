---
title: アプリのアクションの追跡
description: アプリのアクションは、測定したいアプリ内で発生するイベントです。
uuid: 9cdc048a-419a-4725-bd61-6ca6d909cf10
exl-id: 88b7d540-67b7-4ec1-8273-02e34853bf60
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/ahqWp2yjs-zkd9dTRWTkE7b6KE-WpwVR0OH9vCqTPjI
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 132
ht-degree: 100%

---

# アプリのアクションの追跡{#track-app-actions}

アクションは、アプリ内で発生し、測定対象となるイベントです。

各アクションには、イベントが発生するたびに増分される、1 つ以上の対応する指標があります。 例えば、新規サブスクリプションごとに、コンテンツがレーティングされるたびに、またはレベルが完了するたびに、`trackAction` 呼び出しを送信します。

アクションは自動的には追跡されないので、追跡するイベントが発生したときに `trackAction` を呼び出し、アクションをカスタムイベントにマップします。

1. 追跡するイベントが発生したら、`trackAction` を呼び出します。

   * **Roku：**

     ```js
     ADBMobile().trackAction("myapp.ActionName", {})
     ```

   * **Chromecast：**

     ```js
     ADBMobile.analytics.trackAction("myapp.ActionName", {});
     ```

1. アクションをカスタムイベントにマップします。

   * **Roku：**

     ```js
     dictionary = {} 
     dictionary["myapp.social.SocialSource"] = "Twitter"  
     ADBMobile().trackAction("myapp.SocialShare", dictionary)
     ```

   * **Chromecast：**

     ```js
     var dictionary = {}; 
     dictionary["myapp.social.SocialSource"] = "Twitter"; 
     ADBMobile.analytics.trackAction("myapp.SocialShare", dictionary);
     ```

各アクション追跡呼び出しで追加のコンテキストデータを送信することもできます。
