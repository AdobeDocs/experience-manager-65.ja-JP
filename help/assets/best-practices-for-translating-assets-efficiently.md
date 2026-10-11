---
title: アセットの翻訳のベストプラクティス
description: 翻訳された各バージョンを同期し、翻訳ワークフローを合理化するための、アセットの効率的な管理に関するベストプラクティス。
contentOwner: AG
role: Admin
feature: Asset Management
exl-id: e632dcdb-b2b9-45bc-89e7-337b44b6fc61
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 100%
---
# アセットの翻訳のベストプラクティス {#best-practices-for-translating-assets-efficiently}

[!DNL Adobe Experience Manager Assets] の多言語ワークフローで、デジタルアセットのバイナリ、メタデータおよびタグを複数のロケール用に翻訳し、翻訳されたアセットを管理します。 詳しくは、[多言語のアセット](multilingual-assets.md)を参照してください。

アセットの管理を効率化して、様々な翻訳バージョンを確実に同期するには、翻訳ワークフローを実行する前にアセットの[言語コピー](preparing-assets-for-translation.md)を作成します。

アセットやアセットのグループの言語コピーは、類似のコンテンツ階層を持つ言語の兄弟（または同族言語のアセットのバージョン）です。

それぞれの言語コピーは独立したアセットです。 このため、アセットを複数のロケールに翻訳すると、CRX リポジトリのサイズが大幅に増加する可能性があります。 例えば、合計サイズ 10 GB のアセットを 2 つの言語に翻訳すると、リポジトリのサイズが約 20 GB（1 つの言語につき 10 GB）増加する可能性があります。

アセットバイナリは、メタデータやタグに比べて、はるかに大きなストレージエリアを占有します。 このため、メタデータとタグの翻訳のみが目的である場合、バイナリの翻訳は省略してください。 バイナリの元のコピーをリポジトリに保持して、別のロケールに翻訳されたメタデータやタグと関連付けることができます。 複数の翻訳バージョンではなく、バイナリの単一コピーを維持すると、リポジトリサイズへの影響が最小限に抑えられます。

ファイルデータストアや Amazon S3 データストアは、これらのシナリオに最適なストレージインフラストラクチャを提供します。 これらのストレージリポジトリには、複数のロケールのメタデータやタグで共有できるアセットバイナリの単一のコピー（レンディションを含む）が保存されます。 このため、アセットの言語コピーを作成してメタデータやタグを翻訳しても、リポジトリのサイズには影響しません。

いくつかのワークフローや翻訳統合フレームワークの設定を少し変更して、プロセスをさらに合理化することもできます。

1. 次のいずれかの操作を行います。

   * [ファイルデータストアの設定](/help/sites-deploying/data-store-config.md)
   * [Amazon S3 データストアの設定](/help/sites-deploying/data-store-config.md)

<!--
1. Disable the [DAM MetaData Write-back](/help/sites-administering/workflow-offloader.md#disable-offloading) workflow.

   As the name suggests, the [!UICONTROL DAM Metadata Writeback] workflow rewrites the metadata to the binary file. Because the metadata changes after translation, writing it back to the binary file generates a different binary for a language copy.

   >[!NOTE]
   >
   >Disabling the [!UICONTROL DAM MetaData Writeback] workflow turns off XMP metadata write-back on asset binaries. Consequently, future metadata changes are no longer be saved within the assets. Evaluate the consequences before disabling this workflow.
-->

1. 「[!UICONTROL 最終変更日を設定]」ワークフローを有効化します。

   アセットの最終変更日は、「[!UICONTROL DAM メタデータの書き戻し]」ワークフローが設定します。 このワークフローは手順 2 で無効にするので、[!DNL Assets] は今後アセットの最終変更日を最新の状態に保つことができなくなります。 このため、「*最終変更日を設定*」ワークフローを有効化して、アセットの最終変更日が最新の状態に保たれるようにします。 最終変更日が古いアセットは、エラーの原因となる場合があります。

1. アセットのバイナリを翻訳しないように、[翻訳統合フレームワークを設定](/help/sites-administering/tc-tic.md)します。 「[!UICONTROL アセット]」タブの「**[!UICONTROL アセットを翻訳]**」オプションの選択を解除して、アセットのバイナリの翻訳を停止します。
1. [多言語アセットのワークフロー](multilingual-assets.md)を使用して、アセットのメタデータやタグを翻訳します。
