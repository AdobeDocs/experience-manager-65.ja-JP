---
title: アセットインサイトにデモパッケージを使用する
description: デモパッケージを使用して、AdobeアセットインサイトでWebページのデータをキャプチャし、インサイトを生成できるようにします。
contentOwner: AG
role: User, Admin
feature: アセットインサイト、アセットレポート
exl-id: 13947513-da76-43e1-ae01-abd24a59752a
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 53%

---

# アセットインサイトにデモパッケージを使用する {#using-demo-package-for-asset-insights}

デモパッケージを使用して、AdobeアセットインサイトでサンプルWebページのデータをキャプチャし、インサイトを生成できます。

## [!DNL Use Experience Manager Assets] サンプルWebページを使用したインサイト  {#using-aem-assets-insights-with-sample-web-page}

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
   >外部Webページは、[!DNL Experience Manager]自体に含めることができます。
