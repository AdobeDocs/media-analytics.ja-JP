---
title: アプリの状態の追跡
description: アプリの状態とは、アプリケーションの様々な画面またはビューのことです。 trackState 呼び出しを使用してアプリケーションでアプリの状態をトラッキングする方法を説明します。
uuid: 2f98fb43-c362-4a9b-8732-fa7e963da729
exl-id: bb1e0eee-7c59-40b4-9359-a7441b9686b8
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/fVNQ4CIqXbSYyi32rBlB2B9S6YTsBwxJhD3XaeDcDIE
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 188
ht-degree: 100%

---

# アプリの状態の追跡{#track-app-states}

状態とは、アプリケーションの様々な画面またはビューのことです。 アプリケーションに新しい状態が表示されるたびに、`trackState` 呼び出しを送信する必要があります。 例えば、ユーザーがホームページからビデオの詳細画面に移動する際に、`trackState` 呼び出しを送信します。 通常、状態はパスレポートを使用して表示されるので、ユーザーがアプリ内をどのように移動しているか、どの状態が最も多く閲覧されているかを確認できます。

## trackState 呼び出し

通常、アプリが新しい画面を読み込むたびに、`trackState` を呼び出しします。

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Chromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

状態名は、Adobe Mobile Services の「View State」変数でレポートされます。また、ビューは、`trackState` 呼び出しごとに記録されます。 その他の Analytics インターフェイスでは、「画面遷移」は「ページ名」としてレポートされます。「状態ビュー数」は、「ページビュー数」としてレポートされます。

## コンテキストデータの送信

「State Name」に加えて、各アクション追跡呼び出しを使用して追加のコンテキストデータを送信できます。

### Roku

```js
dictionary = { } 
dictionary["myapp.login.LoginStatus"] = "logged in"  
ADBMobile().trackState("Home Screen", dictionary)
```

### Chromecast

```js
var dictionary = { }; 
dictionary["myapp.login.LoginStatus"] = "logged in"; 
ADBMobile.analytics.trackState("Home Screen", dictionary); 
```

>[!NOTE]
>
>コンテキストデータ値は、Adobe Mobile Services のカスタム変数にマッピングする必要があります。
