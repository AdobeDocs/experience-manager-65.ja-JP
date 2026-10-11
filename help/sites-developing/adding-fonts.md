---
title: グラフィックレンダリング用のフォントの追加
description: AEM では、コンテンツから動的に取得したテキストを組み込んだグラフィックを生成できます
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 725c81d0-0258-4118-8b01-29fd7bcaf9b3
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 100%
---
# グラフィックレンダリング用のフォントの追加{#adding-fonts-for-graphic-rendering}

AEM では、コンテンツから動的に取得したテキストを組み込んだグラフィックを生成できます

その際に、独自のフォントを読み込んで使用することもできます。

現時点で、Java プラットフォームのすべての実装で [TrueType](https://ja.wikipedia.org/wiki/TrueType) フォントがサポートされています。

1. CRXDE Lite を開き、次の場所にあるプロジェクトアプリケーションフォルダーに移動します。

   `/apps/<your-project>/`

1. `/apps/<your-project>/` の下に、新しいノードを作成します。

   * **名前**：`fonts`
   * **型**：`sling:Folder`

   すべての変更を保存します。

1. WebDAV などを使用して、フォントファイルをこのフォルダー内にコピーします。

   >[!NOTE]
   >
   >リポジトリ内のフォントファイルのサフィックスは、`*.ttf` または `*.TTF` である必要があります。

1. [Day Commons GFX Font Helper](/help/sites-deploying/osgi-configuration-settings.md) の [OSGi 設定](/help/sites-deploying/configuring-osgi.md)を更新します。 フォントフォルダーへのパスを追加します（例：`/apps/<your-project>/fonts`）。

1. CRXDE Lite に戻ります。 読み込んだフォントの名前を含むフォルダー内に、`.fontlist`ノードが表示されます。

   これらのフォントは、今後 Java API で使用できます。

Java API でのフォントの使用方法について詳しくは、[Java API の Font クラスに関するドキュメント](https://docs.oracle.com/javase/6/docs/api/java/awt/Font.html)を参照してください。
