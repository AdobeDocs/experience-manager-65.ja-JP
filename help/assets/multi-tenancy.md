---
title: コレクション、スニペット、スニペットテンプレートのマルチテナント
description: マルチテナント機能を使用して、お客様の組織に基づいて CRX リポジトリのコンテンツを隔離して、未承認のアクセスを防止する方法を説明します。
contentOwner: AG
role: Developer, Admin, Leader
feature: Collections
exl-id: f95560c9-f1b9-4e86-94a7-70347d268d8f
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: ac365bec-0634-4744-9473-c42f47320593
    internal-label: Asset management and governance
subfeature_v2:
  - id: c73531c3-4c05-471e-beff-cefb35857910
    internal-label: Collections
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 87%
---
# コレクション、スニペット、スニペットテンプレートのマルチテナント {#multi-tenancy-for-collections-snippets-and-snippet-templates}

マルチテナント機能を使用すると、組織接頭辞と組織 ID に基づいて CRX のコンテンツを隔離し、他の組織のユーザーによるコンテンツへの未承認のアクセスを防止できます。

[!DNL Adobe Experience Manager Assets] は、各組織のデータを別々のパスに保存します。 各組織固有のパスは、組織のプレフィックスと組織IDで識別されます
これは、さまざまな種類のアセットがCRXに保存されている従来の場所に含まれています。

例えば、`Demo` というフォルダーを作成すると、[!DNL Experience Manager] アセットは、習慣的にこのフォルダーを `../content/dam/Demo` に保存します。 マルチテナント機能を有効にすると、`../content/dam/<organization prefix>/<organization id>Demo` にデータを保存できるようになります。

例えば、[!DNL Adobe Marketing Cloud] で [!DNL Assets]（オンデマンド）の ユーザーが `aodpremium` 組織に割り当てられている場合、マルチテナント機能を使用して `../content/dam/<mac>/<aodpremium>Demo` パスを設定して、そのコンテンツを隔離できます。 この例では、`mac` は組織の接頭辞で、`aodpremium` は組織 ID です。

ユーザーの組織と ID に基づいて、この修飾パスは、[!DNL Assets] インターフェイスおよび様々なウィザード（隔離を強制するための移動およびスニペットの作成ウィザードなど）に表示されます。

マルチテナント機能を使用すると、次のタイプのアセットとコンポーネントを隔離できます。

* コレクション
* 公開コレクション
* カタログ（ページの追加／選択ウィザードを含む）
* テンプレート
* スニペットテンプレート
* ライトボックス
