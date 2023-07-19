---
title: アセットの翻訳のベストプラクティス
description: 翻訳された各バージョンを同期し、翻訳ワークフローを合理化するための、アセットの効率的な管理に関するベストプラクティス。
contentOwner: AG
role: Admin
feature: Asset Management
exl-id: e632dcdb-b2b9-45bc-89e7-337b44b6fc61
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 38%

---

# アセットの翻訳のベストプラクティス {#best-practices-for-translating-assets-efficiently}

[!DNL Adobe Experience Manager Assets] の多言語ワークフローで、デジタルアセットのバイナリ、メタデータおよびタグを複数のロケール用に翻訳し、翻訳されたアセットを管理します。詳しくは、[多言語のアセット](multilingual-assets.md)を参照してください。

アセットを効率的に管理し、翻訳された複数のバージョンを確実に同期させるには、 [言語コピー](preparing-assets-for-translation.md) 翻訳ワークフローを実行する前のアセットの数です。

アセットまたはアセットのグループの言語コピーは、類似したコンテンツ階層を持つ言語の兄弟（または同じ言語のアセットのバージョン）です。

各言語コピーは独立したアセットです。 したがって、アセットを複数のロケールに翻訳すると、CRX リポジトリのサイズが大幅に大きくなる可能性があります。 例えば、組み合わせサイズが 10 GB のアセットを 2 つの言語に翻訳すると、リポジトリのサイズが約 20 GB（各言語に 10 GB）増える場合があります。

アセットバイナリは、メタデータやタグに比べて、はるかに大きなストレージ領域を占有します。 したがって、メタデータやタグの翻訳が目的のみになる場合は、バイナリを翻訳する場合は省略します。 バイナリの元のコピーをリポジトリに保持して、異なるロケールに翻訳されたメタデータやタグと関連付けることができます。 複数の翻訳バージョンではなく、バイナリの単一コピーを保持することで、リポジトリサイズへの影響を最小限に抑えます。

ファイルデータストアとAmazon S3 データストアは、これらのシナリオに最適なストレージインフラストラクチャを提供します。 これらのストレージリポジトリには、複数のロケールのメタデータおよびタグで共有できるアセットバイナリ（レンディションを含む）の単一のコピーが格納されます。 したがって、アセット言語コピーの作成とメタデータおよびタグの翻訳は、リポジトリサイズに影響しません。

また、いくつかのワークフローと翻訳統合フレームワークに対して設定をいくつか変更し、プロセスをさらに合理化することもできます。

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

   アセットの最終変更日は、「[!UICONTROL DAM メタデータの書き戻し]」ワークフローが設定します。このワークフローは手順 2 で無効にするので、[!DNL Assets] は今後アセットの最終変更日を最新の状態に保つことができなくなります。このため、「*最終変更日を設定*」ワークフローを有効化して、アセットの最終変更日が最新の状態に保たれるようにします。最終変更日が古いアセットは、エラーの原因となる場合があります。

1. アセットのバイナリを翻訳しないように、[翻訳統合フレームワークを設定](/help/sites-administering/tc-tic.md)します。「[!UICONTROL アセット]」タブの「**[!UICONTROL アセットを翻訳]**」オプションの選択を解除して、アセットのバイナリの翻訳を停止します。
1. [多言語アセットのワークフロー](multilingual-assets.md)を使用して、アセットのメタデータやタグを翻訳します。
