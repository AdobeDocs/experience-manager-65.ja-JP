---
title: コレクション、スニペット、スニペット、スニペットテンプレートのマルチテナンシー
description: マルチテナンシー機能を使用して、お客様の組織に基づいてCRXリポジトリ内のコンテンツを分類し、不正アクセスを防ぐ方法を説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 2%

---


# Multi-tenancy for Collections, snippets, and snippet templates {#multi-tenancy-for-collections-snippets-and-snippet-templates}

マルチテナンシー機能を使用すると、組織のプレフィックスと組織IDに基づいてCRX内のコンテンツを分類し、他の組織のユーザーによる不正アクセスからコンテンツを保護できます。

[!DNL Adobe Experience Manager Assets] 各組織のデータを異なるパスに保存します。 各組織固有のパスは、異なるタイプのアセットがCRXに保存される従来の場所に含まれる組織のプレフィックスと組織IDで識別されます。

例えば、という名前のフォルダーを作成した場合 `Demo`、 [!DNL Experience Manager] アセットは従来、このフォルダーをに保存してい `../content/dam/Demo`ました。 マルチテナンシーを有効にした場合、 `../content/dam/<organization prefix>/<organization id>Demo`

For example, if for [!DNL Adobe Marketing Cloud] users of [!DNL Assets] (on demand) that are assigned to the `aodpremium` organization, you can use the multi-tenancy feature to configure `../content/dam/<mac>/<aodpremium>Demo` path to segregate their content. この例で、は組織のプレフィックス `mac` で、 `aodpremium` は組織IDです。

Based on the user&#39;s organization and ID, this qualified path is displayed in the [!DNL Assets] interface and various wizards, including the Move and Snippet creation wizards to enforce segregation.

マルチテナンシー機能を使用すると、次のタイプのアセットとコンポーネントを分類できます。

* コレクション
* 公開コレクション
* カタログ(追加ページの選択ウィザードを含む)
* テンプレート
* スニペットテンプレート
* Lightbox
