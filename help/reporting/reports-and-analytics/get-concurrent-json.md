---
title: 同時ビューア JSON レポートデータの取得
description: 同時ビューア JSON レポートデータの取得
uuid: 9168f114-2459-4951-a06c-57b735d09dc0
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 84%

---


# 同時ビューア JSON レポートデータの取得{#get-concurrent-viewers-json-report-data}

Analytics API の&#x200B;_*バージョン 1.4*_ を使用して、同時ビューアレポートデータを取得できます。
* [Analytics API](https://github.com/AdobeDocs/analytics-1.4-apis)
* [Swagger](https://adobedocs.github.io/analytics-1.4-apis/swagger-docs.html#/Report/Report.Get)

1. UI に組み込まれた任意のセグメントを使用してデータをフィルタリングします。 特定のコンテンツ ID でフィルタリングするには、新しいセグメントを作成します。
1. リクエスト本文の `elements` -> `id` を `videoconcurrentviewers` に設定します。
1. 十分な量のデータをリクエストします。 アドビでは、データにギャップがないようにするために、3200 データポイントをお勧めします。

   * レポートで指定したデータ範囲は、ビデオセッションが終了した時点ですべての同時視聴者データ _を収集します。_
そのため、1日に開始し、午前0時（つまり、翌日）に終了するセッションを考慮する必要があります。

   * 1 日以上のデータをリクエストしますが、分析では&#x200B;_*最初の日のデータのみ*_&#x200B;を使用します。

次に、このシナリオでのリクエストペイロードの例を示します。

```
{
  "reportDescription":{
    "reportSuiteID":"[YOUR_RSID]",
    "dateFrom":"2018-07-01",
    "dateTo":"2018-07-02",
    "metrics":[
      {
        "id":"instances"
      }
    ],
    "elements":[
      {
        "id":"videoconcurrentviewers",
        "top":"3200"
      }
    ],
    "segments":[
      {
        "id":"s1234_58ca4fc7e4b0abc238707bb9"                                         
      }
    ],
    "sortBy":"instances",
    "locale":"en_US"
  }
}
```

<!--
You can extract the concurrent viewers report data using the API Explorer as follows. 

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

   The concurrent viewers report data, in JSON format, is presented in the Response field.
   
   For example:
   
   ![](assets/api_helper_2.png) 

   ![](assets/api_helper_1.png)

-->
