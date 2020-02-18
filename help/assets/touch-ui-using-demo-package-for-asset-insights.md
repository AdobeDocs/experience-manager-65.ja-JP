---
title: アセットインサイトにデモパッケージを使用する
description: デモパッケージを使用して、アセットインサイトで Web ページからデータを取得し、Web ページのインサイトを生成できるようにします。
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Use demo package for Asset Insights {#using-demo-package-for-asset-insights}

デモパッケージを使用して、アセットインサイトでサンプル Web ページからデータを取得し、サンプル Web ページのインサイトを生成できるようにします。

## Use AEM Assets Insights with sample web page  {#using-aem-assets-insights-with-sample-web-page}

1. Configure Asset Insights using the instructions in [Configuring Asset Insights](touch-ui-configuring-asset-insights.md).
1. 次に示すサンプル AEM Assets パッケージをダウンロードして、CRXDE パッケージマネージャーでインストールします。

   [ファイルを入手](assets/insightsdemo.zip)

1. 次に示すサンプル Web ページを含む ZIP ファイルをダウンロードして、ローカルファイルシステムに抽出します。

   [ファイルを入手](assets/demosite.zip)

1. Web ページをクリックして Web ブラウザーで開きます。

   >[!CAUTION]
   >
   >Web ページは localhost のサーバーからアセットを読み込むように設定されます。サーバーが別の場所で実行している場合は、localhost のサーバーアドレスを Web ページの HTML コンテンツのサーバーアドレスに変更してください。

   >[!NOTE]
   >
   >外部の Web ページは、AEM 自体でホストされたものでもかまいません。
