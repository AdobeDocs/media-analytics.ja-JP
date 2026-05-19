---
title: メディアストリーム属性とは何ですか。
description: 追加の処理ルールおよびカスタム変数を使用せずに、アプリケーションアクションをメディアトラッキングデータにリンクする方法を説明します。
exl-id: 75cc9088-776d-4b10-b358-9fff956a7eb7
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/G0RufpSDBB65tr4XJRvPU2keKgKxv1uDviyhqzxEVD4
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: e4f5f438-eabb-4c54-9133-b817e3d125f5
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 215
ht-degree: 87%

---

# メディアストリームのアトリビューション {#media-stream-attribution}

メディアストリームのアトリビューションを使用すると、追加の処理ルールやカスタム変数がなくても、アプリケーションアクションをメディアトラッキングデータにリンクできます。

## メディアトラッキング外部のメディアディメンション

メディアディメンションを、ページビューやカスタムリンクなどの Analytics 呼び出しに追加できます。 実装時に、メディアコンテキストデータパラメーターを Analytics トラッキングコールに追加する必要があります。

特定のレポートに対してこの機能を有効にするには、Admin Console からメディアトラッキング設定を再度有効にします。

>[!NOTE]
>
>メディア指標は、ハートビートイベントに基づいてストリーミングメディアサービスによって計算されるので、メディアトラッキング以外で使用できる&#x200B;_not_&#x200B;です。 また、メディア指標が異なる実装によって水増しされないことも重要です。

## メディアストリームのアトリビューションの使用

次の JavaScript の例は、名前が「ヒーローバナー」に設定されたカスタムリンクトラッキングコールを生成します。

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

Analytics レポートでは、`Show` eVar を使用してデータを分類したり、追跡リンクインスタンスをカウントしたりできます。 レポートは次のようになります。

![](/assets/myShow-rpt-1.png)

## ユースケース

以下の例は、次の項目のユースケースを示します。

* カテゴリ配置
* ヒーロー配置
* エンゲージメント
* 購読

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)
