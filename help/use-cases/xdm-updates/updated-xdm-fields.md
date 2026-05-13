---
title: Analytics ソースコネクタの実装を、ストリーミングメディアサービス用の新しいXDM フィールドに更新する
description: Analytics ソースコネクタ実装を更新されたXDM ストリーミングメディアフィールドに移行する方法について説明します
feature: Streaming Media
role: User, Admin, Developer
exl-id: d239b203-71ce-4307-884f-9d11cc623d04
TQID: https://experienceleague.adobe.com/cEIBTufYRaIusKjm-CszVvsFmZNfMS-RAvOm3wbbBgc
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 886
ht-degree: 1%

---

# Analytics ソースコネクタの実装を、ストリーミングメディアサービス用の新しいXDM フィールドに更新する

>[!NOTE]
>
>この情報は、[Analytics ソースコネクタ &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/sources/connectors/adobe-applications/analytics)を使用して、Adobe AnalyticsからAdobe Experience Platformにストリーミングメディアデータを取り込み、Customer Journey Analytics レポートやその他のPlatform サービスで使用する企業向けです。
>
>この変更は、データの収集、処理、レポートなど、Adobe Analytics as a スタンドアロンアプリケーションには影響しません。 データフィードや処理ルールなどのツールは影響を受けないため、Analyticsの実装を更新する必要はありません。

ストリーミングメディアサービス用の新しいAdobe Data Collection （Analytics ソースコネクタ）実装が利用可能になり、XDM フィールドのセットから別のフィールドに移行できるようになりました。

## 新しいXDM フィールドパス

この移行の一環として、Adobe Data Collection （Analytics ソースコネクタ）フローで使用されるXDM スキーマに`mediaReporting` XDM フィールドパスが追加されました。 既存および新しく生成されたAdobe データ収集スキーマには、この新しいフィールドが自動的に含まれます。

## 古いXDM フィールドパスの置き換え

Adobe AnalyticsからAdobe Experience Platformにストリーミングメディアデータを転送するすべてのAdobe Data Collection （Analytics ソースコネクタ）フローは、現在、新しい`mediaReporting` XDM フィールドパスと古い`media.mediaTimed` XDM フィールドパスの両方でデータを送信しています。 どちらのフィールドパスも、2025年10月末までの3か月間ご利用いただけます。 10月以降、`media.mediaTimed` フィールドは完全に非推奨となり、10月以降に取り込まれるデータには`mediaReporting`のみが含まれます。 非推奨化後、`media.mediaTimed` フィールドはAdobe Experience Platform スキーマ UIに表示されなくなり、これらのフィールドでのデータ取り込みは停止します。 その結果、これらのフィールドは、Adobe Experience Platform サービスで使用できなくなります。

この日付より前に取り込まれたデータは、レポートで引き続き使用できます。

## 新しいXDM フィールドパスとの追加の違い

ストリーミングメディア用の新しいAdobe ソースコネクタの実装により、Adobe Analyticsからのキープアライブ呼び出しがAdobe Experience Platformに取り込まれるようになりました。

以前は、これらの呼び出しは、Customer Journey AnalyticsなどのPlatform アプリケーションには反映されていませんでした。 その結果、レポートに次の違いが見られる場合があります。

* **正確なセッション数**：場合によっては、keep-alive呼び出しは、ダイレクトメディアのインタラクションがない場合でもアクティブユーザーセッションを維持するのに役立つため、セッション数のデフレーションを意味する場合があります。 これらのキープアライブ呼び出しは、最後のイベントから20分ごとに、メディア再生ごとに生成され、訪問をオープンに保つことを目的としています。 Customer Journey Analyticsで最適なセッショントラッキングを確実に実行するには、データビューで訪問の有効期限を30分に設定することをお勧めします。

* **イベント数の増加**：キープアライブ呼び出しはCustomer Journey Analytics イベント指標でカウントされるようになったため。 キープアライブ呼び出しをレポートから除外する場合は、イベントタイプが`media.keepalive`のイベントを除外するフィルターを作成できます。

この変更により、AnalyticsとCJA レポートの間の整合性が強化されます。

## 既存の設定の移行

移行をスムーズに行うには、2025年10月末までに、すべての顧客が既存の設定を`media.mediaTimed` フィールドから`mediaReporting` フィールドに移行する必要があります。 影響を受ける領域は、`media.mediaTimed`の使用に依存する領域です。次の節で説明するように移行する必要があります。

### Customer Journey Analytics**

CJA レポートを移行するには、次の2つの方法があります。

>[!NOTE]
>
>次のいずれかのオプションを選択した後、Customer Journey Analytics レポートで使用されている各`media.mediaTimed` フィールドを、対応する派生フィールドまたはレポート XDM フィールドパスに手動で置き換える必要があります。

* **履歴データを保持するため**: Adobe チームは、古いXDM フィールドと新しいXDM フィールドを1つのフィールドに組み合わせた派生フィールドのセットを導入する、事前定義されたCustomer Journey Analytics テンプレートを開発しました。 このテンプレートは、リクエストに応じてCustomer Journey Analytics接続ごとに有効にできます。 新しいフィールドを有効にする方法については、Adobe サポートチームにお問い合わせください。 これらの派生フィールドは、組織の派生フィールド制限にカウントされません。

  マッピングのリストを表示するには、[Adobe Experience PlatformとCustomer Journey AnalyticsのMedia Analytics パラメーターのマッピング &#x200B;](/help/use-cases/xdm-updates/parameters-mapping.md)を参照してください。

* **履歴データが不要な場合**: レポート時にレポート XDM フィールドのパスを使用するだけで十分です。 詳しくは、[新しいストリーミングメディアフィールドを使用するようにCustomer Journey Analyticsを移行する](/help/use-cases/xdm-updates/migrate-cja-setup.md)を参照してください。

### Real-Time CDP

すべてのオーディエンスとプロファイルは`mediaReporting`に基づいている必要があります。 詳しくは、[新しいストリーミングメディアフィールドへのプロファイルの移行](/help/use-cases/xdm-updates/migrate-profiles.md)を参照してください。

### データストリームとデータ収集

動的設定とデータ マッピングでは、`mediaReporting`を使用する必要があります。 詳しくは、[&#x200B; カスタムフィールドのデータ準備を新しいストリーミングメディアフィールドに移行](/help/use-cases/xdm-updates/migrate-dataprep.md)を参照してください。

### 移行する必要があるその他のサービス

* Adobe Journey Optimizer: キャンペーンとジャーニーの設定には、`mediaReporting`を組み込む必要があります。

* イベント転送：設定には`mediaReporting` フィールドのみを含める必要があります。

* クエリサービス：クエリは`mediaReporting` フィールドを参照する必要があります。

* タグ設定：すべてのタグ設定は`mediaReporting` フィールドを参照する必要があります。

* 接続と宛先：データ フローのインポートとエクスポートは、`mediaReporting` フィールドを中心に構造化する必要があります。

`media.mediaTimed` フィールドに依存するその他のフローは影響を受け、ロジックの更新が必要です。

## 次のステップとサポート

ストリーミングメディア用Adobe データ収集を使用しているすべてのお客様は、指定された移行期間内に移行を完了する必要があります。

ご質問やサポートが必要な場合は、Adobeサポートチームまでお気軽にお問い合わせください。
