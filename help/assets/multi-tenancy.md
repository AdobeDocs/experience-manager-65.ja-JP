---
title: コレクション、スニペット、スニペットテンプレートのマルチテナンシー
description: マルチテナンシー機能を使用して、お客様の組織に基づいてCRXリポジトリ内のコンテンツを分離し、不正アクセスを防ぐ方法を説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Multi-tenancy for Collections, snippets, and snippet templates {#multi-tenancy-for-collections-snippets-and-snippet-templates}

マルチテナンシー機能を使用すると、組織のプレフィックスと組織IDに基づいてCRX内のコンテンツを分類し、他の組織のユーザーによる不正アクセスからコンテンツを保護できます。

Adobe Experience Manager（AEM）Assets では、組織のデータは、組織ごとに異なるパスに保存されます。各組織固有のパスは、異なるタイプのアセットがCRXに保存される従来の場所に含まれる組織のプレフィックスと組織IDで識別されます。

例えば、という名前のフォルダーを作成した場合、AEMア `Demo`セットは従来、このフォルダーをに保存していま `../content/dam/Demo`す。 マルチテナンシーを有効にした場合、 `../content/dam/<organization prefix>/<organization id>Demo`

For example, if for [!DNL Adobe Marketing Cloud] users of AEM Assets (on demand) that are assigned to the `aodpremium` organization, you can use the multi-tenancy feature to configure `../content/dam/<mac>/<aodpremium>Demo` path to segregate their content. この例では、は組 `mac` 織のプレフィックスで、 `aodpremium` は組織IDです。

ユーザーの組織とIDに基づいて、この修飾パスはAEM Assetsインターフェイスと、移動およびスニペット作成ウィザードを含む、分離を強制する様々なウィザードに表示されます。

マルチテナンシー機能を使用すると、次のタイプのアセットとコンポーネントを区別できます。

* コレクション
* 公開コレクション
* カタログ（ページの追加/選択ウィザードを含む）
* テンプレート
* スニペットテンプレート
* Lightbox
