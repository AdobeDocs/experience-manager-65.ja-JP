---
title: ' [!DNL Adobe Creative Cloud] ベストプラクティスへのフォルダ共有'
description: ' [!DNL Adobe Experience Manager] to allow users in [!DNL Experience Manager Assets] を設定して、Adobe Creative Cloud(CC)ユーザーとフォルダーを交換します。'
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 17%

---


# [!DNL Adobe Experience Manager] フォル [!DNL Adobe Creative Cloud] ダー共有に  {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>[!DNL Experience Manager] ～ [!DNL Creative Cloud]フォルダー共有機能は廃止されました。 Adobeでは、[Adobeアセットリンク](https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link.html)や[Experience Managerデスクトップアプリ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)など、新しい機能を使用することを強くお勧めします。 詳細については、[Experience ManagerとCreative Cloudの統合に関するベストプラクティス](/help/assets/aem-cc-integration-best-practices.md)を参照してください。

[!DNL Adobe Experience Manager] を設定して、ユーザーがアプリのユーザー [!DNL Assets] とフォルダーを共有できるようにし [!DNL Adobe Creative Cloud] ます。これにより、ユーザーは、 [!DNL Adobe Creative Cloud] assetsサービスの共有フォルダーとして使用できます。この機能は、クリエイティブチームと[!DNL Assets]ユーザー間でファイルを交換する場合に使用できます。特に、クリエイティブユーザーが[!DNL Assets]デプロイメントにアクセスできない場合（エンタープライズネットワーク上に存在しない場合）に使用できます。

このタイプの統合は、特に[!DNL Assets]に直接アクセスできないユーザーを扱う場合に、次のような使用例で使用できます。

* [!DNL Assets] ユーザーは、特定のデジタルアセットのセットを [!DNL Adobe Creative Cloud] ファイルのユーザーと共有します(例えば、新しいマーケティングアクティビティ向けのデザイン作業用に、クリエイティブな概要と承認されたアセットのセット)。
* [!DNL Assets] ユーザーは、 [!DNL Adobe Creative Cloud] アプリユーザーが作成した新しいファイルを受け取ります。

>[!NOTE]
>
>このドキュメントを読む前に、統合とCreative Cloud統合のベストプラクティス](/help/assets/aem-cc-integration-best-practices.md)の[全体を確認して、統合の概要を確認してください。

## 概要 {#overview}

[!DNL Experience Manager] を [!DNL Creative Cloud] フォルダー共有にすると、とのアカウント間でのフォルダーとファイルのサーバー側の共有 [!DNL Assets] に依存し [!DNL Creative Cloud] ます。クリエイティブプロフェッショナルは、デスクトップで[!DNL Creative Cloud]デスクトップアプリを使用し、[!DNL Adobe CreativeSync]テクノロジを使用して、共有フォルダーをディスク上で直接利用できるようにすることもできます。

以下の図は統合の概要を示しています。

![chlimage_1-179](assets/chlimage_1-406.png)

この統合の主要な要素は以下のとおりです。

* **[!DNL Experience Manager Assets]** エンタープライズネットワーク（マネージドサービスまたはオンプレミス）に導入：ここでフォルダの共有を開始します。
* **[!DNL Adobe Marketing Cloud Assets]コアサービス**: [!DNL Experience Manager] と [!DNL Creative Cloud] ストレージサービスの間に介在する役割を果たします。統合を使用する組織の管理者は、Marketing Cloud組織と[!DNL Assets]展開との間に信頼関係を確立する必要があります。 また、管理者は、 ユーザーがフォルダーも共有してセキュリティを強化できるように、[承認済みの Creative Cloud 共同作業者のリストを定義](https://experienceleague.adobe.com/docs/core-services/interface/assets/t-admin-add-cc-user.html)します。[!DNL Assets]

* **[!DNL Creative Cloud]アセットWebサービス** (ストレージと [!DNL Creative Cloud] ファイルWeb UI):ここでは、Creative Cloudーが共有された特定のCreative Cloudアプリユーザーが、招待を受諾して、ーアカウントストレージのフォルダーを表示できます。 [!DNL Assets] 
* **Creative Cloudデスクトップアプリ**:（オプション）クリエイティブユーザーのデスクトップから、 [!DNL Creative Cloud] アセットストレージーと同期して、共有フォルダーや共有ファイルに直接アクセスできます。

## 特徴と制限事項 {#characteristics-and-limitations}

* **変更の一方向の伝達：** ファイルの変更は、アセットが最初に作成（アップロード）された([!DNL Experience Manager] または [!DNL Creative Cloud Assets]最初に作成された)システムから、1方向にのみ伝達されます。この統合では、2 つのシステム間で完全に自動化された双方向の同期はおこなわれません。
* **バージョン管理:**

   * [!DNL Experience Manager] では、 で作成および更新されたファイルについて、更新があった場合のみ、アセットのバージョンを作成します。[!DNL Experience Manager]
   * [!DNL Creative Cloud] Assets には、作業中（WIP）のファイルが更新された場合に実行される独自の[バージョン管理機能](https://helpx.adobe.com/jp/creative-cloud/help/versioning-faq.html)が用意されています（原則として最大 10 日間更新が保存されます）。

* **スペースの制限：交換するファイルの** サイズと量は、クリエイティブなユーザー向けの [Creative Cloudアセットの](https://helpx.adobe.com/jp/creative-cloud/kb/file-storage-quota.html) クォータ(購読レベルによる)と最大5 GBの制限によって制限されます。また、容量は、Adobe Marketing Cloud Assets コアサービスで組織が保有しているアセット割り当てによっても制限されます。

* **容量の要件：共有フォルダ** ー内のファイルも物理的に格納し [!DNL Experience Manager] 、 [!DNL Creative Cloud] コアサービスにキャッシュされたコピーと共にアカウントに格納する必要があり [!DNL Marketing Cloud Assets] ます。
* **ネットワークと帯域幅：共有フォルダ** ー内のファイルとすべての更新を、システム間でネットワーク経由で転送する必要があります。共有する対象は、関連するファイルおよび更新のみに限るようにしてください。
* **フォルダの種類**:この種類の [!DNL Assets] フォルダーの共有は、での共有のコンテキストではサポートされていません `sling:OrderedFolder` [!DNL Adobe Marketing Cloud]。フォルダーを共有する場合、[!DNL Assets]で作成する際に、[!UICONTROL 順序付けられた]オプションを選択しないでください。

## ベストプラクティス {#best-practices}

[!DNL Experience Manager]と[!DNL Creative Cloud]のフォルダー共有を活用するためのベストプラクティスは次のとおりです。

* **ボリュームに関する考慮事項：** [!DNL Experience Manager] および [!DNL Creative Cloud] フォルダー共有は、特定のキャンペーンやアクティビティに関連するなど、少数のファイルを共有する場合に使用します。組織内の承認済みアセットと同様に、より大きなアセットセットを共有するには、他の配布方法（例：[!DNL Assets Brand Portal]）や[!DNL Experience Manager]デスクトップアプリを使用します。
* **深い階層の共有を避ける：共有** は再帰的に機能し、選択的な非共有は許可されません。通常、サブフォルダーを持たないフォルダー、または1つのサブフォルダーレベルなど非常に浅い階層を持つフォルダーのみを共有の対象とします。
* **一方向の共有用に個別のフォルダー：最終アセットをファイル間で共有する場合、およびクリエイティブに対応したアセットをフ** ァイル間で共有する場合は、 [!DNL Assets] 別のフォルダーを使用する必要があり [!DNL Creative Cloud]  [!DNL Creative Cloud]  [!DNL Assets]ます。これらのフォルダーに適切な命名規則を加えると、[!DNL Assets]と[!DNL Creative Cloud]の両方のユーザーに対して、わかりやすい作業環境が作成されます。
* **共有フォルダーでのWIPの回避：** 共有フォルダーは作業中には使用しないでください。ファイルに頻繁に変更を加える必要がある作業を実行するには、Creative Cloudファイルで別のフォルダーを使用します。
* **共有フォルダー以外での開始の新規作業：** 新しいデザイン（クリエイティブファイル）は、Creative Cloudファイル内の別のWIPフォルダーで開始する必要があります。ユー [!DNL Assets] ザーと共有する場合は、移動するか共有フォルダーに保存する必要があります。
* **構造の共有の簡素化：より管理しや** すいオペレーティングの設定を行うため、構造の共有を簡素化することを検討してください。すべてのクリエイティブユーザーと共有する代わりに、[!DNL Assets]フォルダーは、クリエイティブディレクターやチームマネージャーなど、チームの担当者とのみ共有する必要があります。 クリエイティブサイドのマネージャーが最終アセットを受け取って作業割り当てを決定し、デザイナーは自身の Creative Cloud アカウントで WIP アセットの作業をするようにします。Creative Cloudのコラボレーション機能を使用して作業を調整し、最後に[!DNL Assets]に共有するアセットを選択して、クリエイティブに対応した共有フォルダーに戻すことができます。

次の図は、[!DNL Assets]の既存の最終アセットに基づいて新しいデザインを作成するための設定例を示しています。

![chlimage_1-180](assets/chlimage_1-407.png)
