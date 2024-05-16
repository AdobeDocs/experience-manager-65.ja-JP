---
title: Analytics と外部プロバイダー
description: 汎用分析スニペットの独自のインスタンスを設定して、新しいサービス設定を定義する方法を説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 9bf818f9-6e33-4557-b2e4-b0d4900f2a05
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: ht
source-wordcount: '445'
ht-degree: 100%

---


# Analytics と外部プロバイダー {#analytics-with-external-providers}

Analytics は、Web サイトがどのように使用されているかに関する、重要で興味深い情報を提供できます。

様々な標準提供の設定が、次のような適切なサービスとの統合で利用できます。

* [Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* [Adobe Target](/help/sites-administering/target.md)

また、**汎用分析スニペット**&#x200B;の独自のインスタンスを設定して、新しいサービス設定を定義できます。

情報は、web ページに追加されるコードの小さなスニペットを使用して収集されます。例：

>[!CAUTION]
>
>`script` タグでスクリプトを囲まないでください。

```
var _gaq = _gaq || [];
_gaq.push(['_setAccount', 'UA-XXXXX-X']);
_gaq.push(['_trackPageview']);

(function() {
    var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
    ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'https://www') + '.google-analytics.com/ga.js';
    var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
})();
```

このようなスニペットを使用して、データを収集しレポートを生成できます。収集される実際のデータは、プロバイダーおよび実際に使用されるスニペットによって異なります。統計の例には次が含まれます。

* 経時的な訪問者数
* 訪問ページ数
* 使用された検索語句
* ランディングページ

>[!CAUTION]
>
>Geometrixx-Outdoors デモサイトは、ページプロパティで提供した属性が、対応する `js` スクリプトの HTML ソースコード（`</html>` 終了タグのすぐ上）に追加されるように設定されています。
>
>独自の `/apps` がデフォルトページコンポーネント（`/libs/foundation/components/page`）から継承しない場合、ユーザー（またはその開発者）が対応する `js` スクリプトが含まれていること（例えば、`cq/cloudserviceconfigs/components/servicescomponents` が含まれていること、同様のメカニズムが使用されていること）を確認する必要があります。
>
>これをしないと、どのサービス（汎用、Analytics、Target など）も機能しません。

## 汎用スニペットを使用したサービスの作成 {#creating-a-new-service-with-a-generic-snippet}

基本設定の場合：

1. **ツール**&#x200B;コンソールを開きます。
1. 左側のパネルから、**クラウドサービス設定**&#x200B;を展開します。
1. 「**汎用分析スニペット**」をダブルクリックしてページを開きます。

   ![汎用分析スニペット](assets/analytics_genericoverview.png)

1. 「+」をクリックして、ダイアログボックスを使用して新しい設定を追加します。少なくとも名前（例：Google Analytics）を割り当てます。

   ![設定の作成](assets/analytics_addconfig.png)

1. 「**作成**」をクリックすると、スニペットダイアログがすぐに開くので、適切な JavaScript スニペットをフィールドに貼り付けます。

   ![コンポーネントの編集](assets/analytics_snippet.png)

1. 「**OK**」をクリックして保存します。

## ページでの新しいサービスの使用 {#using-your-new-service-on-pages}

今作成したサービス設定は、必要なページで使用するように設定する必要があります。

1. ページに移動します。
1. サイドキックから&#x200B;**ページプロパティ**&#x200B;を開き、「**クラウドサービス**」タブを選択します。
1. 「**サービスを追加**」をクリックし、必要なサービスを選択します。例：**汎用分析スニペット**。

   ![クラウドサービスの追加](assets/analytics_selectservice.png)

1. 「**OK**」をクリックして保存します。
1. 「**クラウドサービス**」タブに戻ります。**汎用分析スニペット**&#x200B;が、`Configuration reference missing` のメッセージと共に表示されます。ドロップダウンリストを使用して、具体的なサービスインスタンスを選択します。例：google-analytics。

   ![クラウドサービス設定の追加](assets/analytics_selectspecificservice.png)

1. 「**OK**」をクリックして保存します。

   ページのページソースを表示すると、スニペットが表示されるようになります。

   一定の時間が経過すると、収集された統計を表示できます。

   >[!NOTE]
   >
   >設定が子ページを持つページに添付されている場合、サービスはそれらにも継承されます。
