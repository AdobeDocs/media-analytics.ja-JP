---
title: Adobe Audience Manager有効化とは何ですか。
description: 追加の処理ルールやカスタム変数を使用せずに、アプリケーションアクションをメディアトラッキングデータにリンクする方法を説明します。
translation-type: tm+mt
source-git-commit: 901539a2095b23f9108a934eb61d182b14ccd9e8
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 93%

---


# Audience Manager の有効化 {#audience-manager-enablement}

データ管理プラットフォーム（DMP）である Adobe Audience Manager（AAM）は、オーディエンスデータアセットを 1 つにまとめるのに役立ちます。それにより、サイト訪問者について商業的に関連性のある情報の収集や、マーケティング用のセグメントの作成および適切なオーディエンスをターゲットにした広告やコンテンツの提供が容易になります。

AAM を利用すれば、データ販売者、exchange、デマンド側のプラットフォームに縛られることがありません。さらに、AAM は、パートナーのデータアセットについては、完全に無関係です。複数のデータソースにアクセスできるので、デジタルパブリッシャーは、AAM によって幅広い種類のサードパーティデータやアドビのプライベートデータコープを利用できるようになります。AAM について詳しくは、AAM ドキュメントの [Audience Manager 製品ドキュメント](https://docs.adobe.com/content/help/ja-JP/audience-manager/user-guide/aam-home.html)を参照してください。

**VA から AAM へのデータ転送 -** ビデオコンテンツとビデオ広告の両方で、ソリューション（予約）変数を使用して収集された指標とメタデータを AAM へと自動的に送信できます。データ転送は、デスクトップ、モバイル、OTT を含むすべてのプラットフォームで使用できます。このサーバーサイドデータ転送を有効にするには、Adobe Client Care に連絡して、このフィードを有効にするよう依頼する必要があります。

>[!IMPORTANT]
>
>データを AAM に円滑に転送するには、最新バージョンのメディア SDK ライブラリが必要です。

フェデレーテッドデータは、AAM へのデータ共有を完全にサポートします。フェデレーテッドデータの設定を確認するには、アドビのチームにご相談ください。

## OTT／AAM メソッド {#ott-aam-methods}

これらのメソッドを利用して、Audience Manager からシグナルを送信し、訪問者セグメントを取得できます。

### Chromecast {#am-chromecast}

* `getVisitorProfile() -`

   取得された最も直近の訪問者プロファイルを返します。シグナルがまだ送信されていない場合は、空のオブジェクトを返します。

   ```js
   ADBMobile.audienceManager.getVisitorProfile();
   ```

* `getDpid() -`

   取得された最も直近の訪問者プロファイルを返します。シグナルがまだ送信されていない場合は、空のオブジェクトを返します。

   ```js
   ADBMobile.audienceManager.getDpid();
   ```

* `getDpuuid() -`

   現在の DPUUID を返します。

   ```js
   ADBMobile.audienceManager.getDpuuid();
   ```

* `setDpidAndDpuuid() -`

   DPID および DPUUID を設定します。DPID と DPUUID が設定されている場合は、各シグナルと共に送信されます。

   ```js
   ADBMobile.audienceManager.SetDpidAndDpuuid("myDpid", "myDpuuid");
   ```

* `submitSignal() -`

   特性を含むシグナルを Audience Management に送信します。

   ```js
   ADBMobile.audienceManager.SubmitSignal();
   ```

### Roku {#am-roku}

* `audienceVisitorProfile -`

   取得された最も直近の訪問者プロファイルを返します。シグナルがまだ送信されていない場合は、空のオブジェクトを返します。

   ```js
   ADBMobile().audienceVisitorProfile()
   ```

* `audienceDpid -`

   取得された最も直近の訪問者プロファイルを返します。シグナルがまだ送信されていない場合は、空のオブジェクトを返します。

   ```js
   ADBMobile().audienceDpid()
   ```

* `audienceDpuuid -`

   現在の DPUUID を返します。

   ```js
   ADBMobile().audienceDpuuid()
   ```

* `audienceSetDpidAndDpuuid -`

   DPID および DPUUID を設定します。DPID と DPUUID が設定されている場合は、各シグナルと共に送信されます。

   ```js
   ADBMobile().audienceSetDpidAndDpuuid("myDpid", "myDpuuid")
   ```

* `audienceSubmitSignal -`

   特性を含むシグナルを Audience Management に送信します。

   ```js
   ADBMobile().audienceSubmitSignal()
   ```
