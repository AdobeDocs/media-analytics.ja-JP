---
seo-title: 同時ビューア JSON レポートデータの取得
title: 同時ビューア JSON レポートデータの取得
uuid: 9168f114-2459-4951-a06c-57b735d09dc0
translation-type: tm+mt
source-git-commit: 82317dfd0e6eaef20890d03c32fe088a7574ead2

---


# 同時ビューア JSON レポートデータの取得{#get-concurrent-viewers-json-report-data}

同時ビューアのレポートデータは、 _* 1.4バージョンのAnalytics APIを使用して&#x200B;*_ 、次のように取得できます。
* [Analytics API](https://github.com/AdobeDocs/analytics-1.4-apis)
* [スワガー](https://adobedocs.github.io/analytics-1.4-apis/swagger-docs.html#/Report/Report.Get)

1. UI上に構築された任意のセグメントを使用して、データをフィルタリングします。 特定のコンテンツIDでフィルターするには、新しいセグメントを作成します。
1. リクエスト本 `elements` 文の `id` -&gt;をに設定します `videoconcurrentviewers`。
1. 十分な量のデータをリクエストします。 データに隙間がないように、3200のデータポイントを使用することをお勧めします。

   * レポートで指定するデータ範囲は、ビデオセッション終了時に同時に _収集されるすべてのビューアデータです。_
したがって、1日に開始し、真夜中過ぎに終了するセッション（翌日）を考慮する必要があります。

   * 1日以上のデータをリクエストするが、分析ではデ _*&#x200B;ータの最初の日のみを使用する。*_

このシナリオのサンプルリクエストペイロードは、次のようになります。

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
You can extract the concurrent viewers report data using the Experience Cloud API Explorer as follows. 

1. Navigate to: [https://marketing.adobe.com/developer/api-explorer.](https://marketing.adobe.com/developer/api-explorer)
1. Select and enter the following information in the API Explorer form:

    * **API -** Select "Report".
    * **Method -** Select "Queue".
    * **Environment -** Select your data center.
    * Request JSON - Specify the following:

        * `reportSuiteID` - For info on reports suites: [Report Suites](https://marketing.adobe.com/resources/help/en_US/sc/implement/ref-reports-report-suites.html)
        
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
