---
title: アセットインサイトにデモパッケージを使用する
description: デモパッケージを使用して、アセットインサイトで Web ページからデータを取得し、Web ページのインサイトを生成できるようにします。
contentOwner: AG
translation-type: tm+mt
source-git-commit: c1362c2c1f32d02d36d2067e0e74d927ddbc1554
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 78%

---


# アセットインサイトにデモパッケージを使用{#using-demo-package-for-asset-insights}

デモパッケージを使用して、アセットインサイトでサンプル Web ページからデータを取得し、サンプル Web ページのインサイトを生成できるようにします。

## [!DNL Use Experience Manager Assets] サンプルWebページを使用したインサイト   {#using-aem-assets-insights-with-sample-web-page}

1. [アセットインサイトの設定](configure-asset-insights.md)の手順に従って、アセットインサイトを設定します。
1. 次に示すサンプル Assets パッケージをダウンロードして、CRXDE パッケージマネージャーでインストールします。

   [ファイルを入手](assets/insightsdemo.zip)

1. 次に示すサンプル Web ページを含む ZIP ファイルをダウンロードして、ローカルファイルシステムに抽出します。

   [ファイルを入手](assets/demosite.zip)

1. Web ページをクリックして Web ブラウザーで開きます。

   >[!CAUTION]
   >
   >Web ページは localhost のサーバーからアセットを読み込むように設定されます。サーバーが別の場所で実行している場合は、localhost のサーバーアドレスを Web ページの HTML コンテンツのサーバーアドレスに変更してください。

   >[!NOTE]
   >
   >外部Webページは[!DNL Experience Manager]自体に含めることができます。
