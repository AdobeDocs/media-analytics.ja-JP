---
title: アプリのアクションの追跡
description: アプリのアクションは、測定したいアプリ内で発生するイベントです。
uuid: 9cdc048a-419a-4725-bd61-6ca6d909cf10
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# アプリのアクションの追跡 {#track-app-actions}

アクションは、測定したいアプリ内で発生するイベントです。

各アクションは、イベントが発生するたびに増分される、1 つ以上の対応する指標を持ちます。例えば、新規サブスクリプションごとに、コンテンツがレーティングされるたびに、またはレベルが完了するたびに、`trackAction` 呼び出しを送信します。

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

