---
title: テスト1標準再生
description: このトピックでは、検証で使用される標準再生テストについて説明します。
uuid: c4b3fead-1b27-484b-ab6a-39f1ae0f03f2
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# テスト 1：標準の再生{#test-standard-playback}

このテストケースでは、一般的な再生と順序付けを検証します。 これは、証明書要求の必須要素です。

## 証明書の要請フォーム

**次のURLから証明書申請フォームをダウンロードします。==&gt;**[Certification Request Form.](cert_req_form.docx)

## 認定テスト1の概要

Media Analyticsの導入には、2種類のトラッキングコールが含まれます。
* Adobe Analytics(AppMeasurement)サーバーに直接呼び出し — これらの呼び出しは、「Media Start」イベントと「Ad Start」イベントで発生します。
* Media Analytics（ハートビート）サーバーに対する呼び出し — 帯域内呼び出しと帯域外呼び出しが含まれます。
   * 帯域内 — SDKは、コンテンツの再生中に10秒間隔で、広告中に1秒間隔で、時間指定再生呼び出しまたは「ping」を送信します。
   * アウトオブバンド — これらの呼び出しは、いつでも発生する可能性があり、一時停止、バッファリング、エラー、コンテンツ完了、広告完了などが含まれます。

>[!NOTE]
>メディアトラッキングは、すべてのプラットフォームで同じ動作をします。

## テスト手順

次の操作を順に実行し、記録します。

1. **ページまたはアプリを読み込む**

   **トラッキングサーバー**（すべての Web サイトおよびモバイルアプリ）：

   * **Adobe Analytics(AppMeasurement)サーバー —** Experience cloud訪問者IDサービスには、RDCトラッキングサーバーに解決されるRDCトラッキングサーバーまたはCNAMEが必要です。 The Adobe Analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

   * **Media Analytics（ハートビート）サーバー —** このサーバーは常に「`[namespace].hb.omtrdc.net`」という形式で、会 `[namespace]` 社名を指定します。 この名前はアドビが提供します。
   すべてのトラッキングコールでユニバーサルな特定のキー変数を検証する必要があります。

   **`mid`Adobe訪問者ID (**):この変 `mid` 数は、AMCV cookieに設定された値を取り込むために使用されます。 The `mid` variable is the primary identification value for both websites and mobile apps, and also indicates that the Experience Cloud Visitor ID service is set up properly. これは、Adobe Analytics(AppMeasurement)呼び出しとMedia Analytics（ハートビート）呼び出しの両方で見つかります。

   * **Adobe Analytics start呼び出し**

      | パラメーター | 値（サンプル） |
      |---|---|
      | `pev2` | ms_s |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Webサイトページ呼び出し**

      | パラメーター | 値（サンプル） |
      |---|---|
      | `mid` | 30250035503789876473484580554595324209 |

   * **ライフサイクル呼び出し**

      | パラメーター | 値（サンプル） |
      |---|---|
      | `pev2` | ADBINTERNAL:Lifecycle |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Media Analyticsの開始呼び出し**

      | パラメーター | 値（サンプル） |
      |---|---|
      | `s:event:type` | start |

      >[!NOTE]
      >
      >Media Analytics start呼び出し(`s:event:type=start`)では、値 `mid` が存在しない場合があります。 これは問題ありません。Media Analytics playが呼び出される( `s:event:type=play`)まで表示されない場合があります。

   * **Media Analytics play呼び出し**

      | パラメーター | 値（サンプル） |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |


1. **メディアプレイヤーの起動**

   メディアプレイヤーが起動すると、Media SDKは、次の順序で2つのサーバーにキー呼び出しを送信します。

   1. Adobe Analyticsサーバー — 呼び出しの開始
   1. Media Analyticsサーバー — 呼び出しの開始
   1. メディア分析サーバー — 「Adobe Analytics start呼び出しのリクエスト」
   上記の最初の2つの呼び出しには、追加のメタデータと変数が含まれています。 呼び出しパラメーターとメタデータについては、テスト呼び出しの [詳細を参照してください。](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   上記の3回目の呼び出しは、Adobe Analytics start呼び出し(`pev2=ms_s`)のAdobe Analyticsサーバーへの送信をMedia SDKが要求したことをMedia Analyticsサーバーに通知します。

1. **広告ブレークを視聴する（可能な場合）**

   * **広告開始**
   広告が開始されると、次のキー呼び出しが次の順序で送信されます。

   1. Adobe Analyticsサーバー — Ad start呼び出し
   1. Media Analyticsサーバー — Ad start呼び出し
   1. メディア分析サーバー — 「Adobe Analytics Ad start呼び出しのリクエスト」
   最初の2つの呼び出しには、追加のメタデータと変数が含まれます。 呼び出しパラメーターとメタデータについては、テスト呼び出しの [詳細を参照してください。](/help/sdk-implement/validation/test-call-details.md#view-ad-playback)

   3回目の呼び出しは、Media SDKがAdobe Analytics Ad Start呼び出し(`pev2=msa_s`)のAdobe Analyticsサーバーへの送信を要求したことをMedia Analyticsサーバーに通知します。

   * **広告再生**

      広告の再生中、Media Analytics SDKは「ad」タイプの再生イベントを1秒ごとにMedia Analyticsサーバーに送信します。

   * **広告完了**

      広告の100%ポイントで、Media Analytics Complete呼び出しが送信されます。



1. **広告再生を 30 秒間一時停止します（可能な場合）。**  **広告一時停止**

   広告の一時停止中、Media Analyticsハートビートまたは「ping」呼び出しは、SDKによってMedia Analyticsサーバーに毎秒送信されます。

   >[!NOTE]
   >
   >再生ヘッドの値は、一時停止中は一定に保たれる必要があります。

   呼び出しパラメーターとメタデータについては、テスト呼び出しの [詳細を参照してください。](/help/sdk-implement/validation/test-call-details.md#ma-ad-pause-call)

1. **メインコンテンツを10分間中断せずに再生します。**  **コンテンツの再生**

   メインコンテンツの再生中、Media SDKはハートビート（Play呼び出し）を10秒ごとにMedia Analyticsサーバーに送信します。

   メモ:

   * 再生ヘッドの位置は、Play呼び出しのたびに10ずつ増加する必要があります。
   * `l:event:duration` の値は、前回のトラッキングコールからのミリ秒数を表し、10 秒の呼び出しのたびにほぼ同じ値である必要があります。

      呼び出しパラメーターとメタデータについては、テスト呼び出しの [詳細を参照してください。](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **再生中に 30 秒以上一時停止します。** メディアプレイヤーの一時停止時に、SDKが一時停止イベント呼び出しを10秒ごとにMedia Analyticsサーバーに送信します。 一時停止が終わったら、再生イベントを再開する必要があります。

   呼び出しパラメーターとメタデータについては、テスト呼び出しの [詳細を参照してください。](/help/sdk-implement/validation/test-call-details.md#pause-main-content)

1. **メディアをシーク/スクラブします。** メディア再生ヘッドのスクラブ時には、特別なトラッキングコールは送信されませんが、スクラブ後にメディア再生が再開される場合、再生ヘッドの値は、メインコンテンツ内の新しい位置を反映する必要があります。

1. **メディアの再生（VODのみ）。** メディアの再生時に、新しいMedia start呼び出しのセットが送信されます（新しい開始と同様）。

1. **プレイリストの次のメディアを表示します。** プレイリスト内の次のメディアのメディア開始時に、新しいMedia start呼び出しのセットが送信されます。

1. **メディアまたはストリームの切り替え** ライブストリームを切り替える場合、Media Analyticsの最初のストリームの完了呼び出しは送信されません。 Media start呼び出しとPlay呼び出しは、新しいshowとstream名で始まり、新しいshowの正しい再生ヘッドと継続時間の値で始まる必要があります。

