---
title: ストリーミングメディアサービスのタグを使用したモバイルSDKの設定方法
description: モバイルアプリにAdobeのストリーミングメディアサービスを導入する方法について説明します。
feature: Streaming Media
role: User, Admin, Developer
exl-id: b4944b5f-cbae-4efc-9ef7-962d3f342240
TQID: https://experienceleague.adobe.com/IfnXB76Qycsic-ezOzZX4X-5RakbTQ0tlt7va6q2fZ8
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 199
ht-degree: 70%

---

# Mobile SDK のインストール {#install-mobile-sdks}

AndroidまたはiOSにモバイルアプリ用のAdobe ストリーミングメディアサービスを実装するには、以下をインストールして設定します。

* **Adobe Experience Platform モバイル SDK**

  データを収集するには、次のいずれかを使用します。
   * Adobe Experience Platformのタグ。 Adobe Experience Platform のタグは、他のタグ要件と共に Analytics コードを導入できるタグ管理ソリューションです。
   * Adobe Experience Platform Edge

* **Android 用 Media SDK** または **iOS 用 Media SDK**

* **Adobe Media Analytics for Audio and Video 拡張機能**

SDK のダウンロード方法とその他のドキュメントリソースについては、[タグを使用した Media SDK、拡張機能、OTT SDK の取得](/help/getting-started/download-sdks.md)を参照してください

* **有効な設定パラメーターの取得**

  これらのパラメーターは、Analytics アカウントの設定後、アドビ担当者から取得できます。

* **メディアプレーヤーで以下の API を含める**

   * *プレーヤーイベントをサブスクライブするための API* - Media SDK では、プレーヤーでイベントが発生する際に、シンプルな API のセットを呼び出す必要があります。

   * *プレーヤー情報を提供する API* - これには、メディア名、再生ヘッドの位置、広告、チャプターなど、現在再生中の情報が含まれます。
