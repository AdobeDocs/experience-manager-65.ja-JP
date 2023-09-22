---
title: アセットインサイトにデモパッケージを使用
description: デモパッケージを使用して、アセットインサイトで web ページからデータを取得し、web ページのインサイトを生成できるようにします。
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
exl-id: 13947513-da76-43e1-ae01-abd24a59752a
source-git-commit: f7b24617dec77c6907798b1615debdc2329c9d80
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 61%

---

# アセットインサイトにデモパッケージを使用 {#using-demo-package-for-asset-insights}

デモパッケージを使用して、アセットインサイトでサンプル web ページからデータを取得し、サンプル web ページのインサイトを生成できるようにします。

## [!DNL Use Experience Manager Assets] サンプル web ページを使用したインサイト  {#using-aem-assets-insights-with-sample-web-page}

1. [アセットインサイトの設定](configure-asset-insights.md)の手順を使用してアセットインサイトを設定します。
1. 以下からサンプルのアセットパッケージをダウンロードし、CRXDE パッケージマネージャーからパッケージをインストールします。

[ファイルを入手](assets/insightsdemo.zip)

1. 次に示すサンプル web ページを含む ZIP ファイルをダウンロードして、ローカルファイルシステムに抽出します。

[ファイルを入手](assets/demosite.zip)

1. Web ブラウザーで開いた Web ページをクリックします。

   >[!CAUTION]
   >
   >Web ページは、localhost サーバーからアセットを読み込むように設定されます。 サーバーが別の場所で実行されている場合は、サーバーアドレスを localhost から Web ページのHTMLコンテンツにあるサーバーアドレスに変更します。

   >[!NOTE]
   >
   >外部の web ページは、[!DNL Experience Manager] 自体でホストされたものでもかまいません。
