---
title: コレクション、スニペット、スニペット、スニペットテンプレートのマルチテナンシー
description: マルチテナンシー機能を使用して、お客様の組織に基づいてCRXリポジトリ内のコンテンツを分類し、不正アクセスを防ぐ方法を説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 2%

---


# Multi-tenancy for Collections, snippets, and snippet templates {#multi-tenancy-for-collections-snippets-and-snippet-templates}

マルチテナンシー機能を使用すると、組織のプレフィックスと組織IDに基づいてCRX内のコンテンツを分類し、他の組織のユーザーによる不正アクセスからコンテンツを保護できます。

Adobe Experience Manager Assetsは、組織ごとに異なるパスでデータを保存します。 各組織固有のパスは、異なるタイプのアセットがCRXに保存される従来の場所に含まれる組織のプレフィックスと組織IDで識別されます。

例えば、という名前のフォルダーを作成した場合、Experience Managerアセット `Demo`は従来、このフォルダーをに保存してい `../content/dam/Demo`ました。 マルチテナンシーを有効にした場合、 `../content/dam/<organization prefix>/<organization id>Demo`

For example, if for [!DNL Adobe Marketing Cloud] users of Assets (on demand) that are assigned to the `aodpremium` organization, you can use the multi-tenancy feature to configure `../content/dam/<mac>/<aodpremium>Demo` path to segregate their content. この例で、は組織のプレフィックス `mac` で、 `aodpremium` は組織IDです。

ユーザーの組織とIDに基づいて、この修飾パスがアセットインターフェイスと様々なウィザードに表示されます。このウィザードには、分離を強制する移動やスニペットの作成ウィザードが含まれます。

マルチテナンシー機能を使用すると、次のタイプのアセットとコンポーネントを分類できます。

* コレクション
* 公開コレクション
* カタログ(追加ページの選択ウィザードを含む)
* テンプレート
* スニペットテンプレート
* Lightbox
