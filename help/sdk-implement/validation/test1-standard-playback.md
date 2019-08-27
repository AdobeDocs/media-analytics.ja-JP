---
seo-title: テスト1標準再生
title: テスト1標準再生
uuid: c4b3fad-1b27-484b- ab6a-39f1ae0f03f2
translation-type: tm+mt
source-git-commit: f2b08663a928e27625a9ff63f783c510f41e7a8c

---


# テスト 1：標準の再生{#test-standard-playback}

このテストケースでは、一般的な再生と優先順位を検証します。証明書リクエストの必須要素です。

## Certification Request Form

**証明書リクエストフォームを以下からダウンロードします。==&gt;**  [Certification Request Form.](cert_req_form.docx)

## 認定テスト1の概要

Media Analyticsの導入には、2種類のトラッキングコールが含まれます。
* Adobe Analytics（AppMeasurement）サーバーに直接呼び出した呼び出し-これらの呼び出しは、"Media Start"イベントと"Ad Start"イベントで発生します。
* Media Analytics（ハートビート）サーバーへの呼び出し-これらのサーバーには、帯域内または帯域外呼び出しが含まれます。
   * バンド内- SDKは、コンテンツ再生中に時間間隔を10秒間隔で送信し、広告中の1秒間隔で"ping"を送信します。
   * 帯域外-これらの呼び出しは、任意の時点で発生する可能性があります。一時停止、バッファリング、エラー、コンテンツ完了、広告完了などがあります。

>[!NOTE]
>メディアトラッキングは、すべてのプラットフォームで同じ動作をします。

## テスト手順

次のアクションを完了して記録します。

1. **ページまたはアプリを読み込む**

   **トラッキングサーバー**（すべての Web サイトおよびモバイルアプリ）：

   * **Adobe Analytics（AppMeasurement）サーバー-** Experience Cloud訪問者IDサービスには、RDCトラッキングサーバーに解決するRDCトラッキングサーバーまたはCNAMEが必要です。The Adobe Analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

   * **Media Analytics（ハートビート）サーバー-** このサーバーには常に「」という形式が`[namespace].hb.omtrdc.net`あり、ここでは会社名を `[namespace]` 指定します。この名前はアドビによって提供されます。
   すべてのトラッキングコールにわたって普遍的な特定のキー変数を検証する必要があります。

   **Adobe訪問者ID（`mid`）:** 変数は `mid` 、AMCV cookieに設定された値を取り込むために使用されます。The `mid` variable is the primary identification value for both websites and mobile apps, and also indicates that the Experience Cloud Visitor ID service is set up properly. これは、Adobe Analytics（AppMeasurement）呼び出しとMedia Analytics（ハートビート）呼び出しの両方にあります。

   * **Adobe Analytics Start呼び出し**

      | パラメーター | 値（サンプル） |
      |---|---|
      | `pev2` | ms_s |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Webサイトのページ呼び出し**

      | パラメーター | 値（サンプル） |
      |---|---|
      | `mid` | 30250035503789876473484580554595324209 |

   * **ライフサイクル呼び出し**

      | パラメーター | 値（サンプル） |
      |---|---|
      | `pev2` | ADBINTERNAL:Lifecycle |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Media Analytics Start呼び出し**

      | パラメーター | 値（サンプル） |
      |---|---|
      | `s:event:type` | start |

      >[!NOTE]
      >
      >Media Analyticsの開始呼び出し時に`s:event:type=start``mid` 、値が存在しない可能性があります。これは問題ありません。これらは、Media Analytics Play（ `s:event:type=play`）が呼び出されるまで表示されません。

   * **Media Analytics Play呼び出し**

      | パラメーター | 値（サンプル） |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |


1. **メディアプレイヤーの起動**

   メディアプレイヤーが起動すると、Media SDKは次の順序でキー呼び出しを2つのサーバーに送信します。

   1. Adobe Analyticsサーバー-呼び出しの開始
   1. Media Analyticsサーバー-呼び出しの開始
   1. Media Analyticsサーバー-"Adobe Analytics Start呼び出し要求」
   上記の最初の2回の呼び出しには、追加のメタデータと変数が含まれています。パラメーターとメタデータの呼び出しについては、テストの呼び出しの詳細を参照 [してください。](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   上記の3回目の呼び出しは、Media SDKがAdobe AnalyticsのStart呼び出し（`pev2=ms_s`）をAdobe Analyticsサーバーに送信することを要求したMedia Analyticsサーバーに通知します。

1. **広告ブレークを視聴する（可能な場合）**

   * **広告開始**
   広告が開始すると、次のキー呼び出しが次の順序で送信されます。

   1. Adobe Analyticsサーバー-広告開始呼び出し
   1. Media Analyticsサーバー-広告開始呼び出し
   1. Media Analyticsサーバー-"Adobe Analytics広告開始呼び出し要求」
   最初の2つの呼び出しには、追加のメタデータと変数が含まれています。パラメーターとメタデータの呼び出しについては、テストの呼び出しの詳細を参照 [してください。](/help/sdk-implement/validation/test-call-details.md#view-ad-playback)

   3回目の呼び出しでは、Media SDKがMedia SDKサーバーに、Adobe Analytics広告開始呼び出し（`pev2=msa_s`）がAdobe Analyticsサーバーに送信されるように指示しています。

   * **広告再生**

      広告の再生中、Media Analytics SDKは、「広告」タイプのplayイベントを毎秒Media Analyticsサーバーに送信します。

   * **広告完了**

      広告の100%ポイントでは、Media Analytics Complete呼び出しを送信する必要があります。



1. **広告再生を 30 秒間一時停止します（可能な場合）。**  **広告一時停止**

   広告一時停止中、Media Analyticsのハートビートまたは"ping"の呼び出しは、SDKから1秒ごとにMedia Analyticsサーバーに送信されます。

   >[!NOTE]
   >
   >再生ヘッドの値は、一時停止中に一定のままにしておく必要があります。

   パラメーターとメタデータの呼び出しについては、テストの呼び出しの詳細を参照 [してください。](/help/sdk-implement/validation/test-call-details.md#ma-ad-pause-call)

1. **10分間連続してメインコンテンツを再生します。**  **コンテンツの再生**

   メインコンテンツ再生中、Media SDKは、ハートビート（Play呼び出し）を10秒ごとにMedia Analyticsサーバーに送信します。

   注意：

   * 再生ヘッド位置は、すべてのPlay呼び出しで10増分します。
   * `l:event:duration` の値は、前回のトラッキングコールからのミリ秒数を表し、10 秒の呼び出しのたびにほぼ同じ値である必要があります。

      パラメーターとメタデータの呼び出しについては、テストの呼び出しの詳細を参照 [してください。](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **再生中に 30 秒以上一時停止します。** メディアプレーヤーの一時停止時、イベントの呼び出しは、SDKによって10秒ごとにMedia Analyticsサーバーに送信されます。一時停止が終わったら、再生イベントを再開する必要があります。

   パラメーターとメタデータの呼び出しについては、テストの呼び出しの詳細を参照 [してください。](/help/sdk-implement/validation/test-call-details.md#pause-main-content)

1. **メディアをシーク/スクラブします。** メディア再生ヘッドのスクラブ時に、特別なトラッキングコールは送信されません。ただし、スクラブ後にメディア再生が再開されると、再生ヘッドの値はメインコンテンツ内の新しい位置を反映する必要があります。

1. **メディアを再生（VODのみ）** メディアが再生されると、新しいメディア開始呼び出しのセット（新規起動の場合と同様）が送信されます。

1. **プレイリストの次のメディアを表示します。** プレイリストの次のメディアのメディア開始時に、新しいメディア開始呼び出しのセットを送信する必要があります。

1. **メディアまたはストリームを切り替えます。** ライブストリームを切り替える場合、最初のストリームに対してMedia Analytics完全呼び出しを送信しないでください。メディア開始呼び出しおよび再生の呼び出しは、新しい表示とストリーム名で始まり、新しい番組の再生ヘッドと継続時間の値を使用して開始する必要があります。

