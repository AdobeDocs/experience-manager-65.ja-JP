---
title: アセットの翻訳のベストプラクティス
description: 翻訳された各バージョンを同期し、翻訳ワークフローを合理化するための、アセットの効率的な管理に関するベストプラクティス。
contentOwner: AG
role: Administrator
feature: アセット管理
exl-id: e632dcdb-b2b9-45bc-89e7-337b44b6fc61
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 81%

---

# アセットの翻訳のベストプラクティス{#best-practices-for-translating-assets-efficiently}

[!DNL Adobe Experience Manager Assets] は、デジタルアセットのバイナリ、メタデータ、タグを複数のロケールに翻訳し、翻訳済みアセットを管理するための多言語ワークフローをサポートしています。詳しくは、[多言語のアセット](multilingual-assets.md)を参照してください。

アセットの管理を効率化して、翻訳された各バージョンが確実に同期されるようにするには、翻訳ワークフローを実行する前にアセットの[言語コピー](preparing-assets-for-translation.md)を作成します。

アセットやアセットのグループの言語コピーは、類似のコンテンツ階層を持つ言語の兄弟（または同系言語のアセットのバージョン）です。

各言語コピーは独立したアセットです。このため、アセットを複数のロケールに翻訳すると、CRX リポジトリのサイズが大幅に大きくなります。例えば、合計サイズが 10 GB のアセットを 2 言語に翻訳すると、リポジトリのサイズが約 20 GB（各言語 10 GB）大きくなります。

アセットのバイナリはメタデータやタグと比較して、大量のストレージ領域を占有します。このため、メタデータやタグを翻訳するだけで済む場合は、バイナリの翻訳は省略してください。別のロケールに翻訳されたメタデータとタグとの関連付けのために、バイナリの元のコピーをリポジトリで保持することができます。バイナリは、複数の翻訳されたバージョンではなく単一のコピーを管理することで、リポジトリのサイズへの影響を最小限に抑えることができます。

ファイルデータストアや Amazon S3 データストアはこれらのシナリオに最適なストレージインフラストラクチャを提供します。これらのストレージリポジトリは、複数のロケールのメタデータやタグで共有できる、アセットバイナリの単一のコピー（レンディションを含む）を保存します。このため、アセットの言語コピーを作成してメタデータやタグを翻訳しても、リポジトリのサイズには影響を及ぼしません。

いくつかのワークフローや翻訳統合フレームワークの設定を少し変更して、処理の効率を上げることもできます。

1. 以下のいずれかの操作を行います。

   * [ファイルデータストアの設定](/help/sites-deploying/data-store-config.md)
   * [Amazon S3 データストアの設定](/help/sites-deploying/data-store-config.md)

<!--
1. Disable the [DAM MetaData Write-back](/help/sites-administering/workflow-offloader.md#disable-offloading) workflow.

   As the name suggests, the [!UICONTROL DAM Metadata Writeback] workflow rewrites the metadata to the binary file. Because the metadata changes after translation, writing it back to the binary file generates a different binary for a language copy.

   >[!NOTE]
   >
   >Disabling the [!UICONTROL DAM MetaData Writeback] workflow turns off XMP metadata write-back on asset binaries. Consequently, future metadata changes are no longer be saved within the assets. Evaluate the consequences before disabling this workflow.
-->

1. 「最終変更日を設定」ワークフローを有効化します。

   アセットの最終変更日は、「DAM メタデータの書き戻し」ワークフローが設定します。手順2でこのワークフローを無効にしたので、[!DNL Assets]では、アセットの最終変更日を最新の状態に保つことができなくなります。 このため、「最終変更日を設定」**&#x200B;ワークフローを有効化して、アセットの最終変更日が最新の状態に保たれるようにします。最終変更日が最新でないアセットはエラーの原因となる場合があります。

1. アセットのバイナリを翻訳しないように、[翻訳統合フレームワークを設定](/help/sites-administering/tc-tic.md)します。「[!UICONTROL アセット]」タブの「**[!UICONTROL アセットを翻訳]**」オプションの選択を解除して、アセットバイナリの翻訳を停止します。
1. [多言語のアセットワークフロー](multilingual-assets.md)を使用して、アセットのメタデータ/タグを翻訳します。
