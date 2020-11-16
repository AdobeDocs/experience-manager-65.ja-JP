---
title: グラフィックレンダリング用のフォントの追加
seo-title: グラフィックレンダリング用のフォントの追加
description: AEM では、コンテンツから動的に取得したテキストを取り込んだグラフィックを生成できます
seo-description: AEM では、コンテンツから動的に取得したテキストを取り込んだグラフィックを生成できます
uuid: 67d9b10f-e986-4d29-bde2-10e08075fe17
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6af48ef5-75e6-4b66-bc0d-ecf254b1c4ef
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 64%

---


# グラフィックレンダリング用のフォントの追加{#adding-fonts-for-graphic-rendering}

AEM では、コンテンツから動的に取得したテキストを取り込んだグラフィックを生成できます.

その際に、独自のフォントを読み込んで使用することもできます。

現時点で、Java プラットフォームのすべての実装で [TrueType](https://en.wikipedia.org/wiki/Truetype) フォントがサポートされています。

1. CRXDE Liteを開き、プロジェクトアプリケーションフォルダーに移動します。

   `/apps/<your-project>/`

1. Under `/apps/<your-project>/` create a new node:

   * **名前**：`fonts`
   * **型**：`sling:Folder`

   すべての変更を保存します。

1. WebDAV などを使用して、フォントファイルをこのフォルダー内にコピーします。

   >[!NOTE]
   >
   >Font files in the repository must have the suffix `*.ttf` or `*.TTF`.

1. [Day Commons GFX Font Helperの](/help/sites-deploying/configuring-osgi.md) OSGi設定 [を更新します](/help/sites-deploying/osgi-configuration-settings.md)。フォ追加ントフォルダーのパス例えば `/apps/<your-project>/fonts`.

1. CRXDE Lite に戻ります。You should now see a `.fontlist` node in your folder containing the name of the imported fonts.

   これらのフォントは、今後 Java API で使用できます。

Java API でのフォントの使用方法について詳しくは、[Java API の Font クラスに関するドキュメント](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html)を参照してください。

