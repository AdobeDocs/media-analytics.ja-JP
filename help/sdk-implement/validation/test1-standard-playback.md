---
seo-title: テスト1標準再生
title: テスト1標準再生
uuid: c4b3fad-1b27-484b- ab6a-39f1ae0f03f2
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# テスト 1：標準の再生{#test-standard-playback}

このテストケースでは、一般的な再生と順序を検証し、証明書リクエストフォームの一部として必要になります。Download the certification request form here: [Certification Request Form.](cert_req_form_nielsen.docx)

ビデオ実装は次のタイプのトラッキングコールで構成されています。
* ビデオ開始および広告開始の呼び出しは AppMeasurement サーバーに直接送信されます。
* Media Analytics（MA）ハートビート呼び出しは、開始時および10秒ごとにAdobe VAトラッキングサーバーに送信されます。

>[!NOTE]
>ビデオトラッキングはあらゆるプラットフォーム、デスクトップ、モバイルで同じように動作します。

次の順序でアクションを実行して記録する必要があります。

1. **ページまたはアプリを読み込む**

   **トラッキングサーバー**（すべての Web サイトおよびモバイルアプリ）：

   * **AppMeasurement（Adobe Analytics）**- Experience Cloud 訪問者 ID サービスを使用するには、RDC トラッキングサーバー、または RDC サーバーに解決される CNAME が必要です。The analytics tracking server should end in `.sc.omtrdc.net` or be a CNAME.

   * **Media Analytics（ハートビート）-** このサーバーは常にフォーマットを持ちます。ここ `[namespace].hb.omtrdc.net``[namespace]` では、ログイン会社によって定義され、アドビが提供します。
   すべてのトラッキングコールにわたる特定のキー、ユニバーサル変数を検証する必要があります。

   **Adobe訪問者ID（`mid`）:** 変数は `mid` 、AMCV cookieに設定された値を取り込むために使用されます。The `mid` variable is the primary identification value for both websites and mobile apps, and also indicates that the Experience Cloud Visitor ID service is set up properly. これは、AppMeasurementおよびMedia Analytics（MA）呼び出しの両方にあります。

   * **Heartbeat Play 呼び出し**

      | パラメーター | 値（サンプル） |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |

   * **Media Analyticsの開始呼び出し**

      | パラメーター | 値（サンプル） |
      |---|---|
      | `pev2` | ms_s |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Web サイトページ呼び出し**

      | パラメーター | 値（サンプル） |
      |---|---|
      | `mid` | 30250035503789876473484580554595324209 |

   * **ライフサイクル呼び出し**

      | パラメーター | 値（サンプル） |
      |---|---|
      | `pev2` | ADBINTERNAL:Lifecycle |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Heartbeat Start 呼び出し**

      | パラメーター | 値（サンプル） |
      |---|---|
      | `s:event:type` | start |

   * **VA Start 呼び出し**

      >[!NOTE]
      >
      >On VA Start Calls ( `s:event:type=start`) the `mid` values may not be present. これは問題ありません。They may not appear until the VA Play Calls ( `s:event:type=play`).

      | パラメーター | 値（サンプル） |
      |---|---|
      | `pev2` | ms_s |


1. **ビデオプレーヤーの起動**

   ビデオプレーヤーが起動すると、次の順番で重要な呼び出しが送信されます。

   1. ビデオ分析の開始
   1. ハートビートの開始
   1. ハートビート分析開始
   上記の最初の2回の呼び出しには、追加のメタデータと変数が含まれています。For call parameters and metadata, see [Test call details.](/help/sdk-implement/validation/test-call-details.md)

1. **広告ブレークを視聴する（可能な場合）**

   * **広告開始**
   ビデオ広告の開始時には、次の順番で重要な呼び出しが送信されます。

   1. ビデオ広告分析開始
   1. ハートビート広告開始
   1. ハートビート広告分析開始
   最初の2つの呼び出しには、追加のメタデータと変数が含まれています。For call parameters and metadata, see [Test call details.](/help/sdk-implement/validation/test-call-details.md#section_wz3_yff_f2b)

   * **広告再生**

      広告の再生中には、ハートビート呼び出しが 1 秒間隔でハートビートサーバーに送信されます。

   * **広告完了**

      ビデオ広告がすべて再生されると、ハートビート完了呼び出しが送信されます。



1. **広告再生を 30 秒間一時停止します（可能な場合）。**  **広告一時停止**

   広告の一時停止中には、ハートビート呼び出しが 1 秒間隔でハートビートサーバーに送信されます。

   >[!NOTE]
   >
   >再生ヘッドの値は、一時停止中に一定のままにしておく必要があります。

1. **メインコンテンツビデオを中断せずに 10 分間再生します。** **コンテンツの再生 **

   通常のメインコンテンツ再生中には、ハートビート呼び出しが 10 秒間隔でハートビートサーバーに送信されます。

   注意：

   * 再生ヘッドの位置は、1 回の再生呼び出しにつき 10 ずつ増やす必要があります。
   * `l:event:duration` の値は、前回のトラッキングコールからのミリ秒数を表し、10 秒の呼び出しのたびにほぼ同じ値である必要があります。

      For call parameters and metadata, see [Test call details](/help/sdk-implement/validation/test-call-details.md#section_u1l_1gf_f2b) in *Test Call Details*

1. **再生中に 30 秒以上一時停止します。**&#x200B;ビデオプレーヤーの一時停止中には、一時停止イベントの呼び出しが 10 秒間隔で送信されます。一時停止が終わったら、再生イベントが再開される必要があります。

1. **ビデオをシーク／スクラビングします。**&#x200B;ビデオ再生ヘッドのスクラビング時には、特別なトラッキングコールが送信されることはありません。ただし、スクラビング後にビデオ再生が再開されたときに、メインコンテンツ内の新しい位置が再生ヘッドの値に反映される必要があります。

1. **ビデオをもう一度再生します（VOD のみ）。**&#x200B;ビデオをもう一度再生したときに、新しいビデオ視聴の場合と同じように、一連のビデオ開始呼び出しが新たに送信される必要があります。

1. **プレイリスト内の次のビデオを視聴します。**&#x200B;プレイリスト内の次のビデオのビデオ開始時に、一連のビデオ開始呼び出しが新たに送信される必要があります。

1. **ビデオまたはストリームを切り替えます。**&#x200B;ライブストリームを切り替えるときに、最初のストリームのハートビート完了呼び出しが送信されてはいけません。ビデオ開始呼び出しとビデオ再生呼び出しは、新しい番組とストリームの名前、新しい番組の適切な再生ヘッドと期間の値を使用して開始される必要があります。

