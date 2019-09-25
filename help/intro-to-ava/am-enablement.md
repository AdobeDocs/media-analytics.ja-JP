---
seo-title: Audience Manager の有効化
title: Audience Manager の有効化
uuid: 8a7f9343-ebc3-4087-9d7e-5972640d2455
translation-type: tm+mt
source-git-commit: 8ae15f1e14731a97d212ab66816a777b4dcc897e

---


# Audience Manager の有効化{#audience-manager-enablement}

データ管理プラットフォーム（DMP）である Adobe Audience Manager（AAM）は、オーディエンスデータアセットを 1 つにまとめるのに役立ちます。それにより、サイト訪問者について商業的に関連性のある情報の収集や、マーケティング用のセグメントの作成および適切なオーディエンスをターゲットにした広告やコンテンツの提供が容易になります。

AAM を利用すると、データ販売者、exchange、デマンド側のプラットフォームに縛られることがありません。また、AAM はお客様の提携先のデータアセットにまったくとらわれません。複数のデータソースにアクセスできるので、デジタルパブリッシャーは、AAM によって幅広い種類のサードパーティデータやアドビのプライベートデータコープを利用できるようになります。AAMについて詳しくは、AAMドキュメントの [Audience Manager製品ドキュメントを参照してください。](https://docs-author.corp.adobe.com/content/help/en/audience-manager/user-guide/aam-home.html)

**VA から AAM へのデータ転送** - ビデオコンテンツおよびビデオ広告については、ソリューション（予約）変数を使用して収集された指標およびメタデータが自動的に AAM に送信されます。デスクトップ、モバイル、OTT など、あらゆるプラットフォーム間でデータを転送できます。このサーバー側のデータ転送を有効にするには、Adobe Client Care に連絡し、このフィードを有効にするよう依頼する必要があります。

>[!IMPORTANT]
>
>AAMへのデータのスムーズな転送を確保するには、最新バージョンのMedia SDKライブラリを使用する必要があります。

フェデレーテッドデータは AAM とのデータ共有を完全にサポートしています。担当のアドビチームと連携してフェデレーテッドデータ設定を確認してください。

## OTT／AAM メソッド {#section_yqq_5br_v2b}

これらのメソッドを利用して、Audience Manager からシグナルを送信し、訪問者セグメントを取得できます。

### Chromecast {#am-chromecast}

* `getVisitorProfile() -`

   取得された最も直近の訪問者プロファイルを返します。まだシグナルが送信されていない場合は空のオブジェクトを返します。

   ```js
   ADBMobile.audienceManager.getVisitorProfile();
   ```

* `getDpid() -`

   取得された最も直近の訪問者プロファイルを返します。まだシグナルが送信されていない場合は空のオブジェクトを返します。

   ```js
   ADBMobile.audienceManager.getDpid();
   ```

* `getDpuuid() -`

   現在の DPUUID を返します。

   ```js
   ADBMobile.audienceManager.getDpuuid();
   ```

* `setDpidAndDpuuid() -`

   DPID および DPUUID を設定します。DPID および DPUUID が設定されている場合、各シグナルと共に送信されます。

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

   取得された最も直近の訪問者プロファイルを返します。まだシグナルが送信されていない場合は空のオブジェクトを返します。

   ```js
   ADBMobile().audienceVisitorProfile()
   ```

* `audienceDpid -`

   取得された最も直近の訪問者プロファイルを返します。まだシグナルが送信されていない場合は空のオブジェクトを返します。

   ```js
   ADBMobile().audienceDpid()
   ```

* `audienceDpuuid -`

   現在の DPUUID を返します。

   ```js
   ADBMobile().audienceDpuuid()
   ```

* `audienceSetDpidAndDpuuid -`

   DPID および DPUUID を設定します。DPID および DPUUID が設定されている場合、各シグナルと共に送信されます。

   ```js
   ADBMobile().audienceSetDpidAndDpuuid("myDpid", "myDpuuid")
   ```

* `audienceSubmitSignal -`

   特性を含むシグナルを Audience Management に送信します。

   ```js
   ADBMobile().audienceSubmitSignal()
   ```

