---
title: アプリの状態の追跡
description: 'アプリの状態は、アプリ内の様々な画面またはビューで、表示されるとtrackState呼び出しが発生します。 '
uuid: 2f98fb43-c362-4a9b-8732-fa7e963da729
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# アプリの状態の追跡{#track-app-states}

状態とは、アプリケーションの様々な画面またはビューのことです。アプリケーションに新しい状態が表示されるたびに、呼び出しを送信する必要があ `trackState` ります。 例えば、ユーザーがホームページからビデオの詳細画面に移動した場合は、呼び出しを送信し `trackState` ます。 通常、状態はパスレポートを使用して表示されるので、ユーザーがアプリ内をどのように移動しているか、どの状態が最も多く閲覧されているかを確認できます。

## trackState呼び出し

通常、アプリが新し `trackState` い画面を読み込むたびに呼び出します。

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Chromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

The state name is reported in the "View State" variable in Adobe Mobile services, and a view is recorded for each `trackState` call. 他のAnalyticsインターフェイスでは、「View State」は「Page Name」としてレポートされます。「状態ビュー」は、「ページビュー数」としてレポートされます。

## コンテキストデータの送信

「状態名」に加えて、トラック状態呼び出しのたびに追加のコンテキストデータを送信できます。

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
>コンテキストデータ値は、Adobe Mobile Servicesのカスタム変数にマップする必要があります。

