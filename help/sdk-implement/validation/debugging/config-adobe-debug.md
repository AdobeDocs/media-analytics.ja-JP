---
seo-title: Adobe Debug の設定
title: Adobe Debug の設定
uuid: e416458d- f23c-41ce-8d99- fa5076c455f0
translation-type: tm+mt
source-git-commit: 5ff3566fae2c1df559341057fafdd289774e4b2f

---


# Adobe Debug の設定{#configure-adobe-debug}

## Adobe Debug へのアクセス {#section_AF81E7AD331E41FFA371AB9DA924BFBB}

Adobe Debug にアクセスするには：

1. [Experience Cloud](https://www.marketing.adobe.com) に移動し、新しいAdobe Experience Cloudユーザーを作成します。

   >[!TIP]
   >
   >このログインは、Adobe Analyticsへのログインに使用するユーザー名とパスワードとは異なります。

1. Experience Cloud アカウントを作成したら、アドビの担当者に連絡して、Adobe Debug へのアクセス権をリクエストします。
1. After access has been granted, go to [https://debug.adobe.com](https://debug.adobe.com) and use your Experience Cloud credentials to log in.

   ![](assets/adobe-debug-login.png)

   このツールでサポートされるブラウザーは次のとおりです。
   * Google Chrome
   * Mozilla Firefox
   * Apple Safari
   * Microsoft Internet Explorer バージョン 9 ～ 11

推奨されるブラウザーは、Chrome および Firefox の最新バージョンです。

## Debug Proxy {#section_8D3493B8426B46DEB9CD7E2ABD785D66}

Debug Proxyをダウンロードして設定します。

1. Download the Debug Proxy app at [App Downloads.](https://debug.adobe.com/#/downloads)

   サポートされるオペレーティングシステムは次のとおりです。
   * OS X 10.7（64 bit）以降
   * Windows 7.1（64 bit）以降
   ![](assets/debug-proxy-app.png)

1. Debug Proxy サーバーは、ローカルマシン上で稼働し、ポート 33284 を使用し、システムプロキシとして設定されます。

   OS とブラウザーに応じて、ブラウザー設定を調整する必要がある場合があります。

## デスクトップまたはアプリでの SSL 証明書のダウンロードおよびインストール {#section_2F9547E301CB413299A67BD59AFBEE0D}

Adobe Debug を初めて実行すると、一意の SSL 証明書が生成されます。デスクトップまたはアプリで HTTPS トラフィックをサポートする場合は、アドビの SSL 証明書をダウンロードしてインストールする必要があります。

SSL証明書をダウンロードしてインストールします。

1. After Adobe Debug has been installed and started, go to [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl) and download the certification.
1. 証明書の読み込み

   **Mac OS**
   1. ルート CA 証明書をダブルクリックして、キーチェーンアクセスで開きます。
   1. ルート CA 証明書がログインに表示されます。
   1. ルート CA 証明書を「システム」に移動（ドラッグ）します。
   1. すべてのユーザーおよびローカルシステムプロセスによって確実に信頼されるために、証明書を「システム」にコピーする必要があります。
   1. ルート CA 証明書を開き、「信頼」を展開し、「常に信頼」を選択し、変更内容を保存します。
   **Windows**
   1. 次のどちらかの手順を実行します。

      * [ローカルコンピューターの信頼されたルート証明機関ストアへの証明書の追加](https://technet.microsoft.com/en-us/library/cc754841.aspx#BKMK_addlocal)
<!--        * [How To Import a Trusted Root Certification Authority In Windows 7/Vista/XP](https://www.sqlservermart.com/HowTo/Windows_Import_Certificate.aspx) You might need to quit and reopen your browser to see the change.
-->

    1. Firefoxの場合は、[Mozilla Firefoxでのルート証明書のインストール]の手順を実行します。](https://wiki.wmtransfer.com/projects/webmoney/wiki/Installing_root_certificate_in_Mozilla_Firefox)
    
    You might need to quit and reopen Firefox to see the change.
    
    ** iOSデバイス**
    1."**[!UACROL Settings app]****&gt;****[!UACROL WiFi settings]**.
    
    1. Safariで[Debug]に移動します。](https://proxy.debug.adobe.com/ssl)
    
    Safari will prompt you to install the SSL certificate.

## モバイルデバイスへの SSL 証明書のインストール {#section_F2A3336F482C43E2ABEA742AD5CCACCA}

Adobe Debug で HTTPS 呼び出しが見つからない場合は、モバイルデバイスに Adobe Debug の SSL 証明書をインストールする必要があります。

### iOS  

iOS デバイスに SSL 証明書をインストールするには：

1. On your laptop, turn on the Debug Proxy, and go to [Adobe Debug.](https://debug.adobe.com)
1. iOS デバイスで次の手順を実行します。
   1. デバイスを機内モードに切り替えます。
   1. ラップトップで使用しているのと同じ Wi-Fi 信号を選択します。
   1. ラップトップで、Debug Proxy アプリに表示されている IP とポートを手動で設定します。
   1. Apple Safari ブラウザーウィンドウを開きます。
   1. [https://proxy.debug.adobe.com/sslに移動します。](https://proxy.debug.adobe.com/ssl)
   1. SSL 証明書をダウンロードしてインストールします。

1. ラップトップで、Adobe Debug セッションを開始します。
1. iOS デバイスでテストを開始します。

### Android

Android デバイスに SSL 証明書をインストールするには：

1. On your laptop turn on the Debug Proxy and go to [Adobe Debug.](https://debug.adobe.com)
1. Android デバイスで次の手順を実行します。
   1. デバイスを機内モードに切り替えます。
   1. ラップトップで使用しているのと同じ Wi-Fi 信号を選択します。
   1. ラップトップで、Debug Proxy アプリに表示されている IP とポートを手動で設定します。
   1. ブラウザーウィンドウを開きます。
   1. [https://proxy.debug.adobe.com/sslに移動します。](https://proxy.debug.adobe.com/ssl)
   1. SSL 証明書をダウンロードしてインストールします。

1. ラップトップで、Adobe Debug セッションを開始します。
1. Android デバイスでテストを開始します。

