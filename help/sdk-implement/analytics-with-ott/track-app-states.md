---
title: アプリの状態の追跡
description: 'アプリの状態は、アプリケーション内の別の画面または表示で、表示されると、trackState 呼び出しをおこなう必要があります。 '
uuid: 2f98fb43-c362-4a9b-8732-fa7e963da729
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# アプリの状態の追跡 {#track-app-states}

状態とは、アプリケーションの様々な画面またはビューのことです。アプリケーションに新しい状態が表示されるたびに、`trackState` 呼び出しを送信する必要があります。例えば、ユーザーがホームページからビデオの詳細画面に移動する際に、`trackState` 呼び出しを送信します。通常、状態はパスレポートを使用して表示されるので、ユーザーがアプリ内をどのように移動しているか、どの状態が最も多く閲覧されているかを確認できます。

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

状態名は、Adobe Mobile Services の「View State」変数でレポートされます。また、ビューは、`trackState` 呼び出しごとに記録されます。その他の Analytics インターフェイスでは、「画面遷移」は「ページ名」としてレポートされます。「状態ビュー数」は、「ページビュー数」としてレポートされます。

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

