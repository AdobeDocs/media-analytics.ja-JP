---
title: Analytics 2.0 API を使用したメディア再生滞在時間の JSON レポートデータの取得
description: Analytics 2.0 API を使用してメディア再生滞在時間のレポートデータを取得する方法を説明します。 リクエストと応答のサンプルを表示します。
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
exl-id: 65e5b67a-26fc-433e-b99b-0ebbc24428ac
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 100%

---

# Analytics 2.0 API を使用したメディア再生滞在時間の JSON レポートデータの取得{#get-media-playback-time-spent-json-report-data}

[_*Analytics 2.0 API*_](https://www.adobe.io/apis/experiencecloud/analytics/docs.html) を使用して、メディア再生滞在時間のレポートデータを取得できます。

1. UI に組み込まれた任意のセグメントを使用してデータをフィルタリングします。特定のコンテンツ ID でフィルタリングするには、新しいセグメントを作成します。
1. リクエスト本文の `elements` -> `id` を、秒単位と分単位のどちらで出力するかに応じて `metrics/playback_time_spent_seconds` または `metrics/playback_time_spent_minutes` に設定します。
1. 十分な量のデータをリクエストします。

   * レポートで指定したデータ範囲で、ビデオセッション終了時に、すべての同時ビューアデータを取得します&#x200B;_。_&#x200B;ある日に開始し、真夜中以降（つまり翌日）に終了するセッションを考慮する必要があります。

   * 分析で、リクエストで意図した期間より 1 日分多いデータをリクエストしますが、 _*意図したデータのみを使用します。*_

1 日分のデータに対するリクエストペイロードの例は、次のようになります。リクエストは 2 日間連続でおこなわれますが、レポートでは、最初の日のみを使用します。

## リクエストのサンプル

```json
{
    "rsid": "[YOUR_RSID]",
    "locale": "en_US",
    "dimension": "variables/daterangeminute",
    "globalFilters": [
        {
            "dateRange": "2021-09-02T00:00/2021-09-03T00:00",
            "type": "dateRange"
        }
    ],
    "metricContainer": {
        "metrics": [
            {
                "columnId": "column1",
                "id": "metrics/playback_time_spent_minutes"
            }
        ]
    },
    "settings": {
        "dimensionSort": "asc",
        "limit": "2000",
        "page": 0
  }
}
```

## 応答のサンプル

```JSON
{
   "totalPages":1,
   "firstPage":true,
   "lastPage":true,
   "numberOfElements":1440,
   "number":0,
   "totalElements":1440,
   "columns":{
      "dimension":{
         "id":"variables/daterangeminute",
         "type":"time"
      },
      "columnIds":[
         "column1"
      ]
   },
   "rows":[
      {
         "itemId":"12008020000",
         "value":"00:00 2021-09-02",
         "data":[
            123.0
         ]
      },
      {
         "itemId":"12008020001",
         "value":"00:01 2021-09-02",
         "data":[
            143.0
         ]
      },
      {
         "itemId":"12008020002",
         "value":"00:02 2021-09-02",
         "data":[
            167.0
         ]
      },

      ...
      {
         "itemId":"12008022359",
         "value":"23:59 2021-09-02",
         "data":[
            768.0
         ]
      }
   ],
   "summaryData":{
      "filteredTotals":[
         17124.0
      ],
      "totals":[
         18453.0
      ]
   }
}
```


<!--
You can extract the Media Playback Time Spent report data using the Experience Cloud API Explorer as follows.

1. Navigate to: [https://www.adobe.io.](https://www.adobe.io)
1. Select and enter the following information in the API Explorer form:

    * **API -** Select "Report".
    * **Method -** Select "Queue".
    * **Environment -** Select your data center.
    * Request JSON - Specify the following:

        * `reportSuiteID` - For info on reports suites: [Report Suites](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/report-suites-admin.html)

        * `dateTo` - End date of the report.         

          >[!NOTE]
          >
          >The maximum time period supported is two days.

        * `dateFrom` - Start date of the report.
        * `elements : id` - Set to `"videoconcurrentviewers"`

        * `elements : top` - Specify the number of entries to be returned.

      Sample request body:

      ```    
      {
          "reportDescription": {
              "reportSuiteID": "[Your Report Suite ID]",
              "dateTo": "2017-09-07",
              "dateFrom": "2017-09-07"
              "metrics": [
                  {
                      "id": "instances"
                  }
              ],
              "elements": [
                  {
                      "id": "videoconcurrentviewers",
                      "top": 2880
                  }
              ]
              "locale": "en_US"
          }
      }

      ```

      >[!TIP]
      >
      >Some sessions are ended on the next day, and at that point the data will be available for reporting. In that case the best approach is to select 2 days (2880 minutes) of data, and use only the data for the first day (1440 minutes).

1. Click **Get Response**.

   In the Response field, you should get a `reportID`.
1. In the form, change **Method** to "Get".
1. Enter the value of the `reportID` you received in Step 3, and click **Get Response**.

   The Media Playback Time Spent report data, in JSON format, is presented in the Response field.

   For example:

   ![](assets/api_helper_2.png)

   ![](assets/api_helper_1.png)

-->
