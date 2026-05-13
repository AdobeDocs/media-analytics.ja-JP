---
title: Adobe Audience Manager のイネーブルメントとは何ですか。
description: 追加の処理ルールおよびカスタム変数を使用せずに、アプリケーションアクションをメディアトラッキングデータにリンクする方法を説明します。
exl-id: c0d73bc2-4713-498a-8882-ff66c7f3dd50
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/oInE3GwgI1k5-UbqMUm9yvjXfIF0SsRXPrnUWmWT9Ww
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 408
ht-degree: 100%

---

# Audience Manager の有効化{#audience-manager-enablement}

データ管理プラットフォーム（DMP）である Adobe Audience Manager（AAM）は、オーディエンスデータアセットを 1 つにまとめるのに役立ちます。それにより、サイト訪問者について商業的に関連性のある情報の収集や、マーケティング用のセグメントの作成および適切なオーディエンスをターゲットにした広告やコンテンツの提供が容易になります。

AAM を利用すれば、データ販売者、exchange、デマンド側のプラットフォームに縛られることがありません。 さらに、AAM は、パートナーのデータアセットについては、完全に無関係です。 複数のデータソースにアクセスできる AAM を使用すれば、デジタルパブリッシャーは、幅広い種類のサードパーティデータを利用できるようになります。 AAM について詳しくは、AAM ドキュメントの [Audience Manager 製品ドキュメント](https://docs.adobe.com/content/help/ja-JP/experience-cloud/user-guides/home.html)を参照してください。

**VA から AAM へのデータ転送 -** ビデオコンテンツとビデオ広告の両方で、ソリューション（予約）変数を使用して収集された指標とメタデータを AAM へと自動的に送信できます。 データ転送は、デスクトップ、モバイル、OTT を含むすべてのプラットフォームで使用できます。 このサーバーサイドデータ転送を有効にするには、Adobe Client Care に連絡して、このフィードを有効にするよう依頼する必要があります。

>[!IMPORTANT]
>
>データを AAM に円滑に転送するには、最新バージョンのメディア SDK ライブラリが必要です。

フェデレーテッドデータは、AAM へのデータ共有を完全にサポートします。 フェデレーテッドデータの設定を確認するには、アドビのチームにご相談ください。

## OTT／AAM メソッド {#ott-aam-methods}

これらのメソッドを利用して、Audience Manager からシグナルを送信し、訪問者セグメントを取得できます。

### Chromecast {#am-chromecast}

* `getVisitorProfile() -`

  取得された最も直近の訪問者プロファイルを返します。 シグナルがまだ送信されていない場合は、空のオブジェクトを返します。

  ```js
  ADBMobile.audienceManager.getVisitorProfile();
  ```

* `getDpid() -`

  取得された最も直近の訪問者プロファイルを返します。 シグナルがまだ送信されていない場合は、空のオブジェクトを返します。

  ```js
  ADBMobile.audienceManager.getDpid();
  ```

* `getDpuuid() -`

  現在の DPUUID を返します。

  ```js
  ADBMobile.audienceManager.getDpuuid();
  ```

* `setDpidAndDpuuid() -`

  DPID および DPUUID を設定します。 DPID と DPUUID が設定されている場合は、各シグナルと共に送信されます。

  ```js
  ADBMobile.audienceManager.setDpidAndDpuuid("myDpid", "myDpuuid");
  ```

* `submitSignal() -`

  特性を含むシグナルを Audience Management に送信します。

  ```js
  ADBMobile.audienceManager.submitSignal({"sampleTrait":"sampleValue"});
  ```

### Roku {#am-roku}

* `audienceVisitorProfile -`

  取得された最も直近の訪問者プロファイルを返します。 シグナルがまだ送信されていない場合は、空のオブジェクトを返します。

  ```js
  ADBMobile().audienceVisitorProfile()
  ```

* `audienceDpid -`

  取得された最も直近の訪問者プロファイルを返します。 シグナルがまだ送信されていない場合は、空のオブジェクトを返します。

  ```js
  ADBMobile().audienceDpid()
  ```

* `audienceDpuuid -`

  現在の DPUUID を返します。

  ```js
  ADBMobile().audienceDpuuid()
  ```

* `audienceSetDpidAndDpuuid -`

  DPID および DPUUID を設定します。 DPID と DPUUID が設定されている場合は、各シグナルと共に送信されます。

  ```js
  ADBMobile().audienceSetDpidAndDpuuid("myDpid", "myDpuuid")
  ```

* `audienceSubmitSignal -`

  特性を含むシグナルを Audience Management に送信します。

  ```js
  traitData = {}
  traitData["sampleTrait"] = "sampleValue"
  ADBMobile().audienceSubmitSignal(traitData)
  ```
