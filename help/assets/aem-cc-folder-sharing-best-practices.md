---
title: '[!DNLAdobe Experience Manager] [!DNL Adobe Creative Cloud] フォルダ共有のベストプラクティスに従います。'
description: Adobe Creative Cloud(CC)ユーザーとフォルダーを交換するように [!DNL Adobe Experience Manager] to allow users in [!DNL Experience Manager Assets] 設定します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 18%

---


# [!DNL Adobe Experience Manager] フォルダーの [!DNL Adobe Creative Cloud] 共有 {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>The [!DNL Experience Manager] to [!DNL Creative Cloud] Folder Sharing feature is deprecated. Adobeでは、 [Adobeアセットリンク](https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link.html) 、 [Experience Managerデスクトップアプリなど、新しい機能を使用することを強くお勧めします](https://docs.adobe.com/content/help/ja-JP/experience-manager-desktop-app/using/using.html)。 Learn more in [Experience Manager and Creative Cloud integration best practices](/help/assets/aem-cc-integration-best-practices.md).

[!DNL Adobe Experience Manager] のユーザーがアプリのユーザー [!DNL Assets] とフォルダーを共有できるように設定できます。これにより、ア [!DNL Adobe Creative Cloud] セットサービスでフォルダーを共有フォルダーとして使用できるようにな [!DNL Adobe Creative Cloud] ります。 The feature can be used to exchange files between creative teams and [!DNL Assets] users, especially when the creative users do not have access to the [!DNL Assets] deployment (they are not on the enterprise network).

This type of integration can be used in the following use cases, especially when working with users who do not have direct access to [!DNL Assets]:

* [!DNL Assets] ユーザーは、特定のデジタルアセットのセットを [!DNL Adobe Creative Cloud] ファイルのユーザーと共有します(例えば、新しいマーケティングアクティビティ向けのデザイン作業用のクリエイティブな概要と承認済みアセットのセット)。
* [!DNL Assets] ユーザーは、 [!DNL Adobe Creative Cloud] アプリユーザーが作成した新しいファイルを受け取ります。

>[!NOTE]
>
>Before reading this document, you can review the overall [Experience Manager and Creative Cloud integration best practices](/help/assets/aem-cc-integration-best-practices.md) for an overview of the integration.

## 概要 {#overview}

[!DNL Experience Manager] との [!DNL Creative Cloud] フォルダー共有は、とのアカウント間でのフォルダーとファイルのサーバー側の共有 [!DNL Assets][!DNL Creative Cloud] に依存します。 Creative professionals, who use the [!DNL Creative Cloud] desktop app on their desktops, can additionally make the shared folders available directly on their disks using [!DNL Adobe CreativeSync] technology.

以下の図は統合の概要を示しています。

![chlimage_1-179](assets/chlimage_1-406.png)

この統合の主要な要素は以下のとおりです。

* **[!DNL Experience Manager Assets]** エンタープライズネットワーク（マネージドサービスまたはオンプレミス）に導入： ここでフォルダの共有を開始します。
* **[!DNL Adobe Marketing Cloud Assets]コアサービス&#x200B;**: ストレージサービスとの間の仲介[!DNL Experience Manager]を行い[!DNL Creative Cloud]ます。 統合を使用する組織の管理者は、Marketing Cloud組織と[!DNL Assets]展開の間に信頼関係を確立する必要があります。 また、管理者は、 ユーザーがフォルダーも共有してセキュリティを強化できるように、[承認済みの Creative Cloud 共同作業者のリストを定義](https://docs.adobe.com/content/help/en/core-services/interface/assets/t-admin-add-cc-user.html)します。[!DNL Assets]

* **[!DNL Creative Cloud]アセットWebサービス&#x200B;**(ストレージと[!DNL Creative Cloud]ファイルWeb UI): ここでは、Creative Cloudーが共有された特定のCreative Cloudアプリユーザーが、招待を受諾して、ーアカウントストレージのフォルダーを表示できます。[!DNL Assets]
* **Creative Cloudデスクトップアプリ**: （オプション）クリエイティブユーザーのデスクトップから、ア [!DNL Creative Cloud] セットストレージーと同期して、共有フォルダーや共有ファイルに直接アクセスできます。

## 特徴と制限事項 {#characteristics-and-limitations}

* **変更の一方向伝播：** ファイルの変更は、1方向(アセットが最初に作成（アップロード）されたシステム[!DNL Experience Manager] (または [!DNL Creative Cloud Assets])からのみ反映されます。 この統合では、2 つのシステム間で完全に自動化された双方向の同期はおこなわれません。
* **バージョン管理:**

   * [!DNL Experience Manager] では、 で作成および更新されたファイルについて、更新があった場合のみ、アセットのバージョンを作成します。[!DNL Experience Manager]
   * [!DNL Creative Cloud] Assets には、作業中（WIP）のファイルが更新された場合に実行される独自の[バージョン管理機能](https://helpx.adobe.com/jp/creative-cloud/help/versioning-faq.html)が用意されています（原則として最大 10 日間更新が保存されます）。

* **スペースの制限：** 交換するファイルのサイズと量は、クリエイティブユーザー向けの [Creative Cloudアセットの割り当て](https://helpx.adobe.com/jp/creative-cloud/kb/file-storage-quota.html) (購読レベルによって異なります)と、最大5 GBのファイルサイズによって制限されます。 また、容量は、Adobe Marketing Cloud Assets コアサービスで組織が保有しているアセット割り当てによっても制限されます。

* **必要な領域：** 共有フォルダー内のファイルも、コアサー [!DNL Experience Manager] ビスでキャッシュされたコピーと共に、に物理的に格納し、 [!DNL Creative Cloud][!DNL Marketing Cloud Assets] アカウントに格納する必要があります。
* **ネットワークと帯域幅：** 共有フォルダー内のファイルとすべての更新を、システム間でネットワーク経由で転送する必要があります。 共有する対象は、関連するファイルおよび更新のみに限るようにしてください。
* **フォルダの種類**: この種類の [!DNL Assets] フォルダーの共有は、での共有のコンテキストではサポートされていません `sling:OrderedFolder`[!DNL Adobe Marketing Cloud]。 If you want to share a folder, when creating it in [!DNL Assets], do not select the [!UICONTROL Ordered] option.

## ベストプラクティス {#best-practices}

Best practices for leveraging the [!DNL Experience Manager] to [!DNL Creative Cloud] folder sharing include:

* **ボリュームの考慮事項：** [!DNL Experience Manager] フォルダー共有は、特定の [!DNL Creative Cloud] キャンペーンやアクティビティに関連するなど、少数のファイルを共有する場合に使用します。 To share larger sets of assets, like all approved assets in the organization, use other distribution methods (for example, [!DNL Assets Brand Portal]) or [!DNL Experience Manager] desktop app.
* **階層の深い共有を避ける：** 共有は再帰的に機能し、選択的な非共有は許可されません。 通常、サブフォルダーを持たないフォルダー、または1つのサブフォルダーレベルなど非常に浅い階層を持つフォルダーのみを共有の対象とします。
* **一方向の共有用に別々のフォルダーを作成する：** 最終アセットをファイル間で共有する場合、およびクリエイティブに対応したアセット [!DNL Assets] をファイル間で再び共有する場合は、個別のフォルダ [!DNL Creative Cloud] ーを使用する必要があり [!DNL Creative Cloud][!DNL Assets]ます。 Together with a good naming convention for these folders, it creates an easier-to-understand working environment for [!DNL Assets] and [!DNL Creative Cloud] users alike.
* **共有フォルダーでのWIPの回避：** 共有フォルダーは作業中には使用しないでください。ファイルに頻繁に変更を加える必要がある作業を行うには、Creative Cloudファイル内の別のフォルダーを使用します。
* **共有フォルダー外での開始の新しい作業：** 新しいデザイン（クリエイティブファイル）は、Creative Cloudファイル内の別のWIPフォルダーで開始する必要があります。ユーザーと共有する準備が整ったら、共有フォルダーに移動または保存する必要があり [!DNL Assets] ます。
* **構造の共有の簡素化：** より管理しやすいオペレーティング設定を行うには、共有構造の簡素化を検討してください。 Instead of sharing with all creative users, [!DNL Assets] folders should be shared with team representative(s) only, like a creative director or team manager. クリエイティブサイドのマネージャーが最終アセットを受け取って作業割り当てを決定し、デザイナーは自身の Creative Cloud アカウントで WIP アセットの作業をするようにします。They can use Creative Cloud collaboration features to coordinate the work, and finally select and put assets that are ready to share back to [!DNL Assets] into their creative-ready shared folder.

The following diagram illustrates an example configuration for creating new designs based on existing final assets from [!DNL Assets].

![chlimage_1-180](assets/chlimage_1-407.png)
