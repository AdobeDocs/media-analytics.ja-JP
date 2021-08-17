---
title: Adobe Debug の設定
description: Media SDK 実装のトラブルシューティングに使用できる Adobe Debug の設定方法について説明します。
uuid: e416458d-f23c-41ce-8d99-fa5076c455f0
exl-id: 48ad3f23-f36d-44f3-b8d9-b0b3a2ee06bc
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 41023be25308092a1b3e7c40bad2d8085429a0bc
workflow-type: ht
source-wordcount: '653'
ht-degree: 100%

---

# Adobe Debug の設定 {#configure-adobe-debug}

## Adobe Debug へのアクセス {#accessing-adobe-debug}

Adobe Debug にアクセスするには：

1. [Experience Cloud](https://www.marketing.adobe.com/) に移動し、新しい Adobe Experience Cloud ユーザーを作成します。

   >[!TIP]
   >
   >このログインは、Adobe Analytics へのログインに使用するユーザー名／パスワードとは異なります。

1. Experience Cloud アカウントを作成したら、アドビの担当者に連絡して、Adobe Debug へのアクセス権をリクエストします。
1. アクセス権が付与されたら、[https://debug.adobe.com](https://debug.adobe.com) にアクセスし、Experience Cloud の資格情報を使用してログインします。

   ![](assets/adobe-debug-login.png)

   このツールでサポートされるブラウザーは次のとおりです。
   * Google Chrome
   * Mozilla Firefox
   * Apple Safari
   * Microsoft Internet Explorer バージョン9 ～ 11

推奨ブラウザーは、Chrome と Firefox の最新バージョンです。

## Debug Proxy {#debug-proxy}

Debug Proxy のダウンロードおよび設定：

1. [アプリダウンロード](https://debug.adobe.com/#/downloads)から Debug Proxy アプリをダウンロードします。

   次のオペレーティングシステムがサポートされています。
   * OS X 10.7 64 ビット以上
   * Windows 7.1 64 ビット以上

   ![](assets/debug-proxy-app.png)

1. Debug Proxy サーバーは、ローカルマシンのポート 33284 で実行され、システムプロキシとして設定されます。

   OS とブラウザーに基づいてブラウザーの調整が必要になる場合があります。

## デスクトップまたはアプリでの SSL 証明書のダウンロードおよびインストール {#download-and-install-sSL-desktop}

Adobe Debug を初めて実行すると、一意の SSL 証明書が生成されます。デスクトップやアプリで HTTPS トラフィックをサポートする場合は、SSL 証明書をダウンロードしてインストールする必要があります。

SSL 証明書をダウンロードしてインストールします。

1. Adobe Debug がインストールされ、起動したら、[https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl) に移動し、証明書をダウンロードします。
1. 証明書をインポートします。

   **Mac OS**
   1. ルート CA 証明書をダブルクリックして、キーチェーンアクセスで開きます。
   1. ルート CA 証明書がログインに表示されます。
   1. ルート CA 証明書を「システム」に移動（ドラッグ）します。
   1. すべてのユーザーおよびローカルシステムプロセスによって確実に信頼されるために、証明書を「システム」にコピーする必要があります。
   1. ルート CA 証明書を開き、「信頼」を展開し、「常に信頼」を選択し、変更内容を保存します。

   **Windows**
   1. 次のどちらかの手順を実行します。

      * [ローカルコンピューターの信頼されたルート証明機関ストアへの証明書の追加](https://technet.microsoft.com/ja-jp/library/cc754841.aspx#BKMK_addlocal)
   1. Firefox の場合は、[Mozilla Firefox でのルート証明書のインストール](https://wiki.wmtransfer.com/projects/webmoney/wiki/Installing_root_certificate_in_Mozilla_Firefox)に記載されている手順を実行します。

      変更を確認するには、Firefox を終了して再度開く必要がある場合があります。
   **iOS デバイス**
   1. Adobe Debug を HTTP プロキシとして使用するように iOS デバイスを設定するには、**[!UICONTROL 設定アプリ]****／****[!UICONTROL Wifi 設定]**&#x200B;をクリックします。

   1. Safari では、[デバッグ](https://proxy.debug.adobe.com/ssl)に移動します。

      Safari に、SSL 証明書のインストールを求めるメッセージが表示されます。




## モバイルデバイスへの SSL 証明書のインストール {#install-sSL-for-mobile-device}

Adobe Debug で HTTPS 呼び出しが見つからない場合は、モバイルデバイスに Adobe Debug の SSL 証明書をインストールする必要があります。

### iOS

iOS デバイスに SSL 証明書をインストールするには：

1. ラップトップで、Debug Proxy を有効にし、[Adobe Debug](https://debug.adobe.com) に移動します。
1. iOS デバイスで次の手順を実行します。
   1. デバイスを機内モードに切り替えます。
   1. ノートパソコンと同じ Wi-Fi 信号を選択します。
   1. ラップトップで、Debug Proxy アプリに表示される IP とポートを手動で設定します。
   1. Apple Safari ブラウザーウィンドウを開きます。
   1. [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl) に移動します。
   1. SSL 証明書をダウンロードしてインストールします。

1. ラップトップで、Adobe Debug セッションを開始します。
1. iOS デバイスでテストを開始します。

### Android

Android デバイスに SSL 証明書をインストールするには：

1. ラップトップで、Debug Proxy を有効にし、[Adobe Debug](https://debug.adobe.com) に移動します。
1. ご使用の Android デバイスで、次の手順を実行します。
   1. デバイスを機内モードに設定します。
   1. ノートパソコンと同じ Wi-Fi 信号を選択します。
   1. ラップトップで、Debug Proxy アプリに表示される IP とポートを手動で設定します。
   1. ブラウザーウィンドウを開きます。
   1. [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl) に移動します。
   1. SSL 証明書をダウンロードしてインストールします。

1. ラップトップで、Adobe Debug セッションを開始します。
1. Android デバイスでテストを開始します。
