---
seo-title: アプリの状態の追跡
title: アプリの状態の追跡
uuid: 2f98fb43- c362-4a9b-8732- fa7e963da729
translation-type: tm+mt
source-git-commit: 9cdf69e30fa727aeb974213769a7ab61fb05b756

---


# アプリの状態の追跡{#track-app-states}

状態とは、アプリケーションの様々な画面またはビューのことです。Each time a new state is displayed in your application, you should send a `trackState` call. For example, when a user navigates from the home page to the video details screen, send a `trackState` call. 通常、状態はパスレポートを使用して表示されるので、ユーザーがアプリ内をどのように移動しているか、どの状態が最も多く閲覧されているかを確認できます。

## trackState呼び出し

You typically call `trackState` each time the app loads a new screen.

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Chromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

The state name is reported in the "View State" variable in Adobe Mobile services, and a view is recorded for each `trackState` call. 他のAnalyticsインターフェイスでは、"View State"は"Page Name"としてレポートされます。「状態ビュー」は「ページビュー数」としてレポートされます。

## コンテキストデータの送信

"State Name"に加えて、各トラック状態呼び出しで追加のコンテキストデータを送信できます。

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
>コンテキストデータ値は、Adobe Mobileサービスのカスタム変数にマップする必要があります。

