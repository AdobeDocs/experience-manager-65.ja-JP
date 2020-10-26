---
title: デジタルアセットを整理します
description: Experience Managerを使用して、デジタルアセット、画像、ファイル、フォルダーなどを整理します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 8%

---


# デジタルアセットを整理します {#organize-digital-assets}

Microsoft Office および PDF ドキュメントのすべてのデジタルアセット、メタデータおよびコンテンツが抽出され、検索可能になります。検索することでアセットの高度なフィルター処理が可能になり、適切な権限をフルに活用できます。メタデータは、Digital Asset Managementのメタデータで詳しく説明されています。

[!DNL Experience Manager Assets] は、コンテンツを複数の方法で整理する場合に使用できます。 フォルダーを使用して階層的に整理したり、タグなどを使用して順不同でアドホックな方法で整理したりできます。 ユーザーは DAM アセットエディターでタグを編集できます。このエディターでは、サブアセット、レンディションおよびメタデータが表示されます。

## フォルダ内のアセットの整理 {#organize-using-folders}

アセットを整理する最も基本的な方法は、アセットをフォルダに保存することです。 これは、ローカルファイルシステム内のフォルダにファイルを整理するのと似ています。 フォルダーの作成および管理方法について詳しくは、「アセットの [管理](manage-assets.md)」を参照してください。 ファイルやフォルダーの命名、サブフォルダーの配置、これらのフォルダー内のファイルの処理方法は、アセットの処理方法に大きな影響を与える可能性があります。 一貫した適切なファイルおよびフォルダーの命名方法を使用し、メタデータを十分に活用することで、デジタルアセットリポジトリを最大限に活用できます。

* ほとんどの場合、デジタルアセットリポジトリは常に増加しています。 したがって、コンテンツ作成サイクルの初期の段階で、メタデータの使用、フォルダー構造、ファイル名を形式化することが重要です。
* フォルダーは、デジタルアセットに対して一貫性のあるストレージ構造を適用する目的のみで使用します。この一貫性により、プロセスとアセットの管理が向上します。 例えば、次のタイプのフォルダーに配置されたアセットは、アセットの処理に適した [プロファイルを使用するのに役立ちます](processing-profiles.md)。

   * **開発フォルダー**:現在操作中のデジタルアセットが含まれます。
   * **クライアントフォルダー**:クライアントまたはプロジェクト名に基づくデジタルアセットが含まれます。
   * **プライマリフォルダー**:元のソースデジタルアセットが含まれます。
   * **レンダリングフォルダ**:元のソースデジタルアセットのレンディションとコピーが含まれます。
   * **File Size folders**:小、中、大のファイルサイズに基づくデジタルアセットが含まれます。
   * **ステージングフォルダー**:webサイト上でライブに公開する準備ができているデジタルアセットが含まれます。
   * **MIMEタイプフォルダ**:画像、ドキュメント、マルチメディアなど、MIMEタイプに固有のデジタルアセットが含まれます。
   * **Archive folders**:は、廃止されたデジタルアセットを含みます。
   * **日付ベースのフォルダ**:作成日または最終変更日に基づくデジタルアセットが含まれます。

* カスタマイズや自動化が引き続き機能するように、変更されない可能性の高いフォルダのディレクトリを作成します。 例えば、割り当てられた処理プロファイルは引き続き機能します。
* If an asset is already published, then you use [!DNL Experience Manager] to move the asset to another folder, and re-publish from its new location, the original published asset location is still available, along with the newly re-published asset. The original published asset, however, is *lost* to [!DNL Experience Manager] and cannot be unpublished. したがって、ベストプラクティスとして、最初にアセットの公開を取り消し、次に別のフォルダーに移動します。

## タグを使用したアセットの整理 {#use-tags-to-organize-assets}

タグをメタデータとして使用すると、アセットの検索、検索結果を使用したコレクションの作成、一部のアセットの検索ランクの向上、アセットの検索にAdobe SenseiのAIアルゴリズムの活用を簡単に行うことができます。

[!DNL Adobe Experience Manager Assets] は、自己学習アルゴリズムを使用して、非常にわかりやすいタグを作成し、数回クリックするだけで適切なアセットを見つけることができます。 スマートタグ付けは、Adobe Senseiを使用します。人工知能と機械学習フレームワークでは、標準的なタグと業務用のタグの両方を画像に認識し、適用するように学習できます。 また、スマートタグでは、コンテンツ、個々の単語またはフレーズを識別して、アセットに説明タグを自動的に適用できます

詳しくは、次の記事を参照してください。

* [Experience Managerのタグについて](/help/sites-authoring/tags.md)
* [アセットメタデータの編集](metadata.md)
* [アセットのスマートタグの強化](enhanced-smart-tags.md)

## コレクションとして整理 {#organize-as-collections}

のアセットコレクションを使用す [!DNL Experience Manager Assets]ると、複数のユーザ間でアセットを作成、編集、共有する機能を合理化できます。 アセット、フォルダー、コレクションの静的な参照リストを含むコレクションや、検索条件に基づいてアセットを取り込むコレクションなど、使用方法に基づいて複数のタイプのコレクションを作成します。  また、様々な場所のアセットを使用してコレクションを作成し、様々なアクセスレベル、表示レベル、編集権限を持つ複数のユーザーと共有することもできます。

For more information, see [manage collections](manage-collections.md)

<!-- TBD items: add screenshots where applicable
Any hints/recommendations of when to use what method of organizing? Some examples of how organizing helps towards a better taxonomy and improved content velocity.
Add back links to blog posts by marketing?
-->

## プロファイルを使用するようにアセットを整理する {#organize-to-use-profiles}

処理プロファイルには、定義済みのフォルダにアップロードされるアセットに適用される [!DNL Assets] 処理コマンドが含まれます。 プロファイルは、フォルダーまたは新たにアップロードされたアセットのコンテンツの処理を自動化するために使用します。 プロファイルを利用して、アセットをより適切に整理できます。

メタデータの使用、ファイル名、フォルダー構造を標準化することで、デジタルアセットのプールが大きくなるに従って、フォルダーに処理プロファイルをより正確で一貫性のある方法で適用できます。

>[!MORELIKETHIS]
>
>* [メタデータ、画像およびビデオを処理するプロファイル](processing-profiles.md)。
>* [メタデータプロファイル](/help/assets/metadata-config.md#metadata-profiles).
>* [ビデオプロファイル](video-profiles.md).
>* [ダイナミックメディアイメージプロファイル](image-profiles.md)。

