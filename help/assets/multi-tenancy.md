---
title: コレクション、スニペット、スニペットテンプレートのマルチテナント
description: マルチテナント機能を使用して、お客様の組織に基づいて CRX リポジトリのコンテンツを隔離して、未承認のアクセスを防止する方法を説明します。
contentOwner: AG
role: Architect, Admin, Leader
feature: Collections
exl-id: f95560c9-f1b9-4e86-94a7-70347d268d8f
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: ht
source-wordcount: '220'
ht-degree: 100%

---

# コレクション、スニペット、スニペットテンプレートのマルチテナント {#multi-tenancy-for-collections-snippets-and-snippet-templates}

マルチテナント機能を使用すると、組織プレフィックスと組織 ID に基づいて CRX のコンテンツを隔離し、他の組織のユーザーによるコンテンツへの未承認のアクセスを防止できます。

[!DNL Adobe Experience Manager Assets] は、各組織のデータを別々のパスに保存します。各組織に特有のパスは、CRX 内で様々なタイプのアセットを保存する従来の場所に含まれる、組織プレフィックスと組織 ID によって識別されます。


例えば、`Demo` というフォルダーを作成すると、[!DNL Experience Manager] アセットは、習慣的にこのフォルダーを `../content/dam/Demo` に保存します。マルチテナント機能を有効にすると、`../content/dam/<organization prefix>/<organization id>Demo` にデータを保存できるようになります。

例えば、[!DNL Adobe Marketing Cloud] で [!DNL Assets]（オンデマンド）の ユーザーが `aodpremium` 組織に割り当てられている場合、マルチテナント機能を使用して `../content/dam/<mac>/<aodpremium>Demo` パスを設定して、そのコンテンツを隔離できます。この例では、`mac` は組織のプレフィックスで、`aodpremium` は組織 ID です。

ユーザーの組織と ID に基づいて、この修飾パスは、[!DNL Assets] インターフェイスおよび様々なウィザード（隔離を強制するための移動およびスニペットの作成ウィザードなど）に表示されます。

マルチテナント機能を使用すると、次のタイプのアセットとコンポーネントを隔離できます。

* コレクション
* 公開コレクション
* カタログ（ページの追加／選択ウィザードを含む）
* テンプレート
* スニペットテンプレート
* ライトボックス
