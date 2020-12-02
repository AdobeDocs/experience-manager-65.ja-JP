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


# コレクション、スニペット、スニペットテンプレートのマルチテナンシー{#multi-tenancy-for-collections-snippets-and-snippet-templates}

マルチテナンシー機能を使用すると、組織のプレフィックスと組織IDに基づいてCRX内のコンテンツを分類し、他の組織のユーザーによる不正アクセスからコンテンツを保護できます。

[!DNL Adobe Experience Manager Assets] 各組織のデータを異なるパスに保存します。組織固有の各パスは、組織のプレフィックスと組織IDによって識別されます
の値は、様々なタイプのアセットがCRXに保存される従来の場所に含まれています。

例えば、`Demo`という名前のフォルダーを作成した場合、[!DNL Experience Manager]アセットは従来、`../content/dam/Demo`にフォルダーを保存していました。 マルチテナンシーを有効にすると、`../content/dam/<organization prefix>/<organization id>Demo`にデータを格納できるようになります。

例えば、`aodpremium`組織に割り当てられている[!DNL Assets]の[!DNL Adobe Marketing Cloud]ユーザー（オンデマンド）の場合、マルチテナンシー機能を使用して、コンテンツを分離する`../content/dam/<mac>/<aodpremium>Demo`パスを設定できます。 この例では、`mac`が組織のプレフィックス、`aodpremium`が組織IDです。

ユーザーの組織とIDに基づいて、この修飾パスは[!DNL Assets]インターフェイスや、分離を強制する移動およびスニペット作成ウィザードなどの様々なウィザードに表示されます。

マルチテナンシー機能を使用すると、次のタイプのアセットとコンポーネントを分類できます。

* コレクション
* 公開コレクション
* カタログ(追加ページの選択ウィザードを含む)
* テンプレート
* スニペットテンプレート
* Lightbox
