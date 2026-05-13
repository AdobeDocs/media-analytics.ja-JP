---
title: ハートビート測定について
description: ハートビートを使用してビデオ指標を収集する方法について説明します。
feature: Streaming Media
role: User, Admin, Developer
exl-id: 180dd9b1-877a-4ec1-8e81-c293800069c0
TQID: https://experienceleague.adobe.com/t6Y8Nj7WaEP76UOj8cCp40zSc3mHMfZuC9j5CifVIOg
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: b3f03848-ae12-48b2-8aab-cad18567eb32id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: eb9732ab-8232-4b21-bc4c-89de86dbe4d7id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: e6c28e30-8689-4bf4-8fa8-561343d308a9id: e7d92df1-c5ba-4e93-85df-f83171b889beid: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 316
ht-degree: 31%

---

# ハートビート測定について

Adobeのストリーミングメディアサービスでは、「ハートビート」を使用してビデオ指標を収集します。 ビデオ再生中、ハートビートはハートビートトラッキングサーバーに送信され、再生時間を測定します。 ハートビート呼び出しは、10 秒ごとに送信されます。 ハートビートにより、きめ細かいビデオエンゲージメント指標やより正確なビデオフォールアウトレポートが可能になります。 ストリーミングメディアサービスは、Media Analytics拡張機能のAdobe Launch、Media SDK、Media Collection APIを使用して、ハートビートを測定します。 `AppMeasurement` および `VisitorID` コンポーネントは、ビデオデータの受信に使用されます。

ストリーミングメディアサービスでハートビートを使用すると、次のメリットが得られます。

| 機能 | 説明 |
|---|---|
| メディアイベント | 詳細およびカスタムイベントは、メインコンテンツに対して 10 秒おき、広告に対して 1 秒おきに送信されます |
| 指標およびディメンション | ベンダーをまたいで標準化された指標、ディメンション、ベンチマークを明確化。 あらゆるプラットフォームをまたいで標準化されたソリューションを利用すれば、あらゆるメディアとプラットフォームで一貫性のある標準化された変数を使用して、より効率的なクロスキャンペーン、デバイス、ベンダー比較を可能にします。 |
| 統合 | Experience Cloud IDはAdobe Experience Cloudにリンクされているため、より簡単に相互分析できます。 Adobe Experience Cloudの自動化機能との連携により、メディアオーディエンスのセグメンテーション、ターゲティング、ユーザーの好みにもとづいたメディアレコメンデーションなどが可能です。 |
| 価格 | メディアストリームごとの透明性の高い追跡（シングル） |
| 実装およびサポート | 継続的なアップデートと改善により構成を合理化。 合理化された実装プロセスにより、Player APIを通じて変数をすばやくマッピングし、Adobe Debug Toolを使用して実装を検証して、必要なすべての変数を正確に追跡できます。 |
| パートナー共有 | Federated Media and Certified Metrics. Federated Mediaを通じてデータを共有することで、業界初のメディア共有機能を活用し、オペレーター、プログラマー、ディストリビューターなどのメディア配信パートナー全体でデータを包括的に評価できます。 |
| 高度な追跡 | ダウンロードされたコンテンツの追跡、エラー復旧の追跡および同時閲覧者。 接続に関係なく、デバイスでダウンロードおよび再生されるストリーミングメディアコンテンツを追跡できます。 |
