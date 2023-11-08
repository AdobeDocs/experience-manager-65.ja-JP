---
title: Analytics と外部プロバイダー
description: 汎用分析スニペットの独自のインスタンスを設定して、新しいサービス設定を定義する方法を説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 9bf818f9-6e33-4557-b2e4-b0d4900f2a05
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 26%

---


# Analytics と外部プロバイダー {#analytics-with-external-providers}

Analytics は、Web サイトがどのように使用されているかに関する、重要で興味深い情報を提供できます。

様々な標準提供の設定が、次のような適切なサービスとの統合で利用できます。

* [Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* [Adobe Target](/help/sites-administering/target.md)

また、 **汎用 Analytics スニペット** をクリックして、新しいサービス設定を定義します。

その後、情報が収集され、Web ページに追加されるコードの小さなスニペットが使用されます。 次に例を示します。

>[!CAUTION]
>
>スクリプトをで囲まない `script` タグ。

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

このようなスニペットを使用すると、データを収集してレポートを生成できます。 収集される実際のデータは、プロバイダーと、使用する実際のコードスニペットによって異なります。 統計の例を次に示します。

* 長期間の訪問者数
* 訪問したページ数
* 使用された検索語句
* ランディングページ

>[!CAUTION]
>
>Geometrixxアウトドアデモサイトは、ページプロパティで指定された属性が HTML ソースコード ( `</html>` 終了タグ ) を、 `js` スクリプト。
>
>自分のものの場合 `/apps` デフォルトのページコンポーネント ( `/libs/foundation/components/page`) を使用する場合は、 `js` スクリプトは、例えば、 `cq/cloudserviceconfigs/components/servicescomponents`または同様のメカニズムを使用している必要があります。
>
>これがないと、どのサービス（汎用、Analytics、Target など）も機能しません。

## 汎用スニペットを使用したサービスの作成 {#creating-a-new-service-with-a-generic-snippet}

基本設定の場合：

1. **ツール**&#x200B;コンソールを開きます。
1. 左側のウィンドウで、を展開します。 **Cloud Service設定**.
1. ダブルクリック **汎用分析スニペット** ページを開くには：

   ![汎用分析スニペット](assets/analytics_genericoverview.png)

1. 「 + 」をクリックし、ダイアログボックスを使用して新しい設定を追加します。 少なくとも、名前 ( 例：Google Analytics) を割り当てます。

   ![設定の作成](assets/analytics_addconfig.png)

1. クリック **作成**&#x200B;スニペットダイアログがすぐに開き、適切な JavaScript スニペットをフィールドに貼り付けます。

   ![コンポーネントの編集](assets/analytics_snippet.png)

1. 「**OK**」をクリックして保存します。

## ページでの新しいサービスの使用 {#using-your-new-service-on-pages}

サービス設定を作成したら、必要なページを設定して使用する必要があります。

1. ページに移動します。
1. サイドキックから&#x200B;**ページプロパティ**&#x200B;を開き、「**クラウドサービス**」タブを選択します。
1. クリック **サービスを追加**「 」をクリックし、必要なサービスを選択します。例えば、 **汎用分析スニペット**:

   ![クラウドサービスの追加](assets/analytics_selectservice.png)

1. 「**OK**」をクリックして保存します。
1. 次の場所に戻ります。 **Cloud Service** タブをクリックします。 **汎用分析スニペット**&#x200B;が、`Configuration reference missing` のメッセージと共に表示されます。「 」ドロップダウンリストを使用して、特定のサービスインスタンスを選択します。 例えば、google-analytics の場合は次のようになります。

   ![クラウドサービス設定の追加](assets/analytics_selectspecificservice.png)

1. 「**OK**」をクリックして保存します。

   これで、ページのページソースを表示した場合に、スニペットを表示できます。

   一定時間が経過すると、収集した統計を表示できます。

   >[!NOTE]
   >
   >設定が子ページを持つページに添付されている場合、サービスはそれらにも継承されます。
