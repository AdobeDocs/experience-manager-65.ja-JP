---
title: グラフィックレンダリング用のフォントの追加
description: AEMを使用すると、コンテンツから動的に取得したテキストを組み込んだグラフィックを生成できます。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 725c81d0-0258-4118-8b01-29fd7bcaf9b3
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 72%

---

# グラフィックレンダリング用のフォントの追加{#adding-fonts-for-graphic-rendering}

AEMを使用すると、コンテンツから動的に取り込んだテキストを組み込んだグラフィックを生成できます。

その際に、独自のフォントを読み込んで使用することもできます。

現時点で、Java プラットフォームのすべての実装で [TrueType](https://ja.wikipedia.org/wiki/TrueType) フォントがサポートされています。

1. CRXDE Lite を開き、次の場所にあるプロジェクトアプリケーションフォルダーに移動します。

   `/apps/<your-project>/`

1. の下 `/apps/<your-project>/` ノードを作成します。

   * **名前**：`fonts`
   * **型**：`sling:Folder`

   すべての変更を保存します。

1. WebDAV などを使用して、フォントファイルをこのフォルダー内にコピーします。

   >[!NOTE]
   >
   >リポジトリ内のフォントファイルのサフィックスは、`*.ttf` または `*.TTF` である必要があります。

1. を更新します。 [OSGi 設定](/help/sites-deploying/configuring-osgi.md) / [Day Commons GFX Font Helper](/help/sites-deploying/osgi-configuration-settings.md). フォントフォルダーのパス ( `/apps/<your-project>/fonts`.

1. CRXDE Lite に戻ります。読み込んだフォントの名前を含むフォルダー内に、`.fontlist`ノードが表示されます。

   これらのフォントは、今後 Java API で使用できます。

Java API でのフォントの使用方法について詳しくは、[Java API の Font クラスに関するドキュメント](https://docs.oracle.com/javase/6/docs/api/java/awt/Font.html)を参照してください。
