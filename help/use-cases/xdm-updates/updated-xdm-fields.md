---
title: Analytics ソースコネクタ実装の、更新された XDM ストリーミングメディアフィールドへの移行
description: 更新された XDM ストリーミングメディアフィールドへの Analytics ソースコネクタ実装の移行について説明します
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a0a357c3fe7e958b0b6491c84f17f26a806ea205
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 0%

---

# Analytics ソースコネクタ実装のストリーミングメディア用の新しい XDM フィールドへの更新

>[!NOTE]
>
>この情報は、[Analytics ソースコネクタ ](https://experienceleague.adobe.com/ja/docs/experience-platform/sources/connectors/adobe-applications/analytics) を使用して、Customer Journey Analytics レポートまたはその他の Platform サービスで使用するために、Adobe AnalyticsからAdobe Experience Platformにストリーミングメディアデータを取り込む組織を対象としています。
>
>変更内容は、データ収集、処理、レポートを含む、Adobe Analytics as a スタンドアロンアプリケーションには影響しません。 データフィードや処理ルールなどのツールは影響を受けないため、Analytics 実装を更新する必要はありません。

Streaming Media サービスの新しいAdobe データ収集（Analytics ソースコネクタ）実装が、XDM フィールドセット間で移行できるようになりました。

## 新しい XDM フィールドパス

この移行の一環として、Adobe データ収集（Analytics ソースコネクタ）フローで使用される XDM スキーマに `mediaReporting` XDM フィールドパスが追加されました。 既存のAdobe データ収集スキーマと新しく生成されたデータ収集スキーマには、この新しいフィールドが自動的に含まれます。

## 古い XDM フィールドパスの置き換え

Adobe AnalyticsからAdobeにストリーミングメディアデータを転送するすべてのAdobe Experience Platform データ収集（Analytics ソースコネクタ）フローは、現在、新しい `mediaReporting` XDM フィールドパスと古い `media.mediaTimed` XDM フィールドパスの両方でデータを送信しています。 これらのフィールドパスは両方とも、2025 年 10 月末まで、3 か月間使用できます。 10 月以降、`media.mediaTimed` のフィールドは完全に非推奨になり、10 月以降に取り込んだデータには `mediaReporting` のみが含まれます。 廃止後、`media.mediaTimed` のフィールドはAdobe Experience Platform スキーマ UI に表示されなくなり、これらのフィールドへのデータの取り込みは停止されます。 その結果、これらのフィールドは、どのAdobe Experience Platform サービスでも使用できなくなります。

この日付より前に取り込まれたデータは、レポートできます。

## 新しい XDM フィールドパスとの追加の違い

Streaming Media 用の新しいAdobe ソースコネクタの実装により、Adobe Analyticsからのキープアライブ呼び出しがAdobe Experience Platformに取り込まれるようになりました。

以前は、これらの呼び出しは、Customer Journey Analyticsなどの Platform アプリには反映されていませんでした。 その結果、組織ではレポートで次のような違いが生じる場合があります。

* **正確なセッション数**：場合によっては、セッション数にデフレが生じることを意味する可能性があります。キープアライブ呼び出しは、直接のメディアインタラクションがない場合でもアクティブなユーザーセッションを維持するのに役立つからです。 これらのキープアライブ呼び出しは、訪問を開いたままにする目的で、メディア再生ごとに、最後のイベントの後 20 分ごとに生成されます。 Customer Journey Analyticsでの最適なセッショントラッキングを確保するには、データビューで訪問の有効期限を 30 分に設定することをお勧めします。

* **イベント数の増加**：キープアライブ呼び出しがCustomer Journey Analytics イベント指標でカウントされるようになりました。 レポートからキープアライブ呼び出しを除外する場合は、イベントタイプが `media.keepalive` のイベントを除外するフィルターを作成できます。

この変更により、Analytics とCJAのレポートの整合性が向上します。

## 既存の設定を移行

スムーズな移行を確実に行うために、すべてのお客様は、2025 年 10 月末までに既存の設定を `media.mediaTimed` フィールドから `mediaReporting` フィールドに移行する必要があります。 影響を受ける領域は、`media.mediaTimed` の使用に依存する領域であり、次の節で説明するように移行する必要があります。

### Customer Journey Analytics**

CJA レポートを移行する方法は 2 つあります。

>[!NOTE]
>
>次のいずれかのオプションを選択した後、Customer Journey Analytics レポートで使用される各 `media.mediaTimed` フィールドを、対応する派生フィールドまたはレポート XDM フィールドパスに手動で置き換える必要があります。

* **履歴データを保持するため**:Adobe チームは、事前定義済みのCustomer Journey Analytics テンプレートを開発して、古い XDM フィールドと新しい XDM フィールドを 1 つのフィールドに組み合わせた一連の派生フィールドを導入しました。 このテンプレートは、リクエストに応じて、Customer Journey Analytics接続ごとに有効にすることができます。 新しいフィールドを有効にする方法については、Adobe サポートチームにお問い合わせください。 これらの派生フィールドは、組織の派生フィールド制限にはカウントされません。

  マッピングのリストを表示するには、[Adobe Experience PlatformとCustomer Journey Analytics用の Media Analytics パラメーターマッピング ](/help/use-cases/xdm-updates/parameters-mapping.md) を参照してください。

* **履歴データが不要な場合**：レポート時にレポート XDM フィールドパスを使用すれば十分です。 詳しくは、[ 新しいストリーミングメディアフィールドを使用するためのCustomer Journey Analyticsの移行 ](/help/use-cases/xdm-updates/migrate-cja-setup.md) を参照してください。

### Real-Time CDP

すべてのオーディエンスとプロファイルは、`mediaReporting` に基づいている必要があります。 詳しくは、[ 新しいストリーミングメディアフィールドへのプロファイルの移行 ](/help/use-cases/xdm-updates/migrate-profiles.md) を参照してください。

### データストリームとデータ収集

動的設定とデータマッピングでは、`mediaReporting` を使用する必要があります。 詳しくは、[ カスタムフィールドのデータ準備を新しいストリーミングメディアフィールドに移行する ](/help/use-cases/xdm-updates/migrate-dataprep.md) を参照してください。

### 移行が必要なその他のサービス

* Adobe Journey Optimizer：キャンペーンとジャーニーの設定には `mediaReporting` を組み込む必要があります。

* イベント転送：設定には、`mediaReporting` フィールドのみを含める必要があります。

* クエリサービス：クエリは、`mediaReporting` のフィールドを参照する必要があります。

* タグ設定：タグを設定する場合は、すべてのフィールド `mediaReporting` 参照する必要があります。

* 接続と宛先：読み込みと書き出しのデータフローは、`mediaReporting` のフィールドを中心に構造化する必要があります。

`media.mediaTimed` のフィールドに依存するその他のフローは影響を受け、ロジックの更新が必要となることに注意してください。

## 次のステップとサポート

Adobe Data Collection for Streaming Media を使用しているすべてのユーザーは、指定された移行期間内に移行を完了する必要があります。

ご質問やサポートのニーズについては、遠慮なくAdobe サポートチームにお問い合わせください。

