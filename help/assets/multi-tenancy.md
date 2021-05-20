---
title: コレクション、スニペット、スニペットテンプレートのマルチテナント機能
description: マルチテナント機能を使用して、お客様の組織に基づいてCRXリポジトリ内のコンテンツを分離し、不正アクセスを防ぐ方法を説明します。
contentOwner: AG
role: Architect, Administrator, Leader
feature: コレクション
exl-id: f95560c9-f1b9-4e86-94a7-70347d268d8f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 2%

---

# コレクション、スニペット、スニペットの各テンプレートのマルチテナント化{#multi-tenancy-for-collections-snippets-and-snippet-templates}

マルチテナント機能を使用すると、組織のプレフィックスと組織IDに基づいてCRX内のコンテンツを区別し、他の組織のユーザーによるコンテンツへの不正アクセスを防ぐことができます。

[!DNL Adobe Experience Manager Assets] は、各組織のデータを異なるパスに格納します。各組織固有のパスは、組織のプレフィックスと組織IDで識別されます
異なるタイプのアセットがCRXに保存される従来の場所に含まれます。

例えば、`Demo`という名前のフォルダーを作成した場合、[!DNL Experience Manager]アセットは通常、`../content/dam/Demo`にフォルダーを保存します。 マルチテナント機能を有効にすると、`../content/dam/<organization prefix>/<organization id>Demo`にデータを保存できるようになりました。

例えば、[!DNL Assets]（オンデマンド）の[!DNL Adobe Marketing Cloud]ユーザーが`aodpremium`組織に割り当てられている場合は、マルチテナント機能を使用して`../content/dam/<mac>/<aodpremium>Demo`パスを設定し、そのコンテンツを区別できます。 この例では、 `mac`は組織のプレフィックス、 `aodpremium`は組織IDです。

ユーザーの組織とIDに基づいて、この修飾パスは[!DNL Assets]インターフェイスと、分離を強制する移動およびスニペット作成ウィザードを含む様々なウィザードに表示されます。

マルチテナント機能を使用すると、次のタイプのアセットとコンポーネントを区別できます。

* コレクション
* 公開コレクション
* カタログ（ページの追加/選択ウィザードを含む）
* テンプレート
* スニペットテンプレート
* Lightbox
