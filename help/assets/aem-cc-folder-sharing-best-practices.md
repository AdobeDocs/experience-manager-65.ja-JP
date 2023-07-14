---
title: ' [!DNL Adobe Creative Cloud]  へのフォルダー共有時のベストプラクティス'
description: ' [!DNL Experience Manager Assets]  のユーザーが Adobe Creative Cloud ユーザーとフォルダーを交換できるように  [!DNL Adobe Experience Manager]  を設定します。'
contentOwner: AG
role: User, Admin
feature: Collaboration
exl-id: 130cec6d-1cdd-4304-94bb-65e6bb573e55
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 64%

---

# [!DNL Adobe Experience Manager] から [!DNL Adobe Creative Cloud] へのフォルダー共有 {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>[!DNL Experience Manager] から [!DNL Creative Cloud] へのフォルダー共有機能は廃止されました。Adobeは、次のような新しい機能を使用することをお勧めします。 [Adobeアセットリンク](https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link.html) または [Experience Managerデスクトップアプリ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja). 詳しくは、[Experience Manager と Creative Cloud の統合のベストプラクティス](/help/assets/aem-cc-integration-best-practices.md)を参照してください。

[!DNL Adobe Experience Manager] は、[!DNL Assets] のユーザーに [!DNL Adobe Creative Cloud] アプリのユーザーとのフォルダー共有を許可するように設定できます。これにより、[!DNL Adobe Creative Cloud] アセットサービスの共有フォルダーとして利用が可能になります。この機能を使用すると、クリエイティブチームと [!DNL Assets] ユーザーの間でファイルをやり取りすることができます。特に、クリエイティブユーザーが [!DNL Assets] デプロイメントへのアクセス権を持っていない（エンタープライズネットワーク上にいない）場合に有用です。

このタイプの統合は、以下のユースケースに使用できます。特に、[!DNL Assets] への直接アクセス権を持っていないユーザーと作業する場合に便利です。

* [!DNL Assets] ユーザーが [!DNL Adobe Creative Cloud] ファイルのユーザーと特定のデジタルアセット群を共有する場合（例えば、新しいマーケティング活動のデザイン作業に使用するクリエイティブブリーフや一連の承認済みアセットなど）
* [!DNL Assets] ユーザーが [!DNL Adobe Creative Cloud] アプリユーザーの作成した新規ファイルを受け取る場合

>[!NOTE]
>
>このドキュメントを読む前に、[Experience Manager と Creative Cloud の統合のベストプラクティス](/help/assets/aem-cc-integration-best-practices.md)全体を確認すると、統合の概要を把握することができます。

## 概要 {#overview}

[!DNL Experience Manager] と [!DNL Creative Cloud] のフォルダー共有は、サーバー側で [!DNL Assets] と [!DNL Creative Cloud] のアカウント間でフォルダーとファイルが共有されているかに依存します。クリエイティブプロフェッショナル ( [!DNL Creative Cloud] デスクトップアプリケーションをデスクトップ上に置くと、を使用して、共有フォルダーをディスク上で直接使用できるようになります。 [!DNL Adobe CreativeSync] 技術。

以下の図は統合の概要を示しています。

![chlimage_1-179](assets/chlimage_1-406.png)

この統合の主要な要素は以下のとおりです。

* **[!DNL Experience Manager Assets]** エンタープライズネットワーク (Managed Servicesまたはオンプレミス ) にデプロイされる場合：フォルダーの共有はここで開始されます。
* **[!DNL Adobe Experience Cloud Assets]コアサービス**：[!DNL Experience Manager] と [!DNL Creative Cloud] のストレージサービス間で仲介を行います。統合を使用する組織の管理者は、組織組織と [!DNL Assets] デプロイメント。 また、管理者は、 ユーザーがフォルダーも共有してセキュリティを強化できるように、[承認済みの Creative Cloud 共同作業者のリストを定義](https://experienceleague.adobe.com/docs/core-services/interface/services/assets/t-admin-add-cc-user.html)します。[!DNL Assets]

* **[!DNL Creative Cloud]Assets の web サービス**（ストレージおよび [!DNL Creative Cloud] ファイルの web UI）：[!DNL Assets] フォルダーを共有している特定の Creative Cloud アプリユーザーが招待を受け入れ、自身の Creative Cloud アカウントのストレージにあるフォルダーを参照できる場所です。
* **Creative Cloudデスクトップアプリ**:（オプション）との同期を通じて、クリエイティブユーザーのデスクトップから共有フォルダー/ファイルに直接アクセスできるようにします。 [!DNL Creative Cloud] アセットストレージ。

## 特徴と制限事項 {#characteristics-and-limitations}

* **変更の一方向の伝播：**&#x200B;ファイルの変更は、アセットが最初に作成（アップロード）されたシステム（[!DNL Experience Manager] または [!DNL Creative Cloud Assets]）から一方向にのみ伝播します。この統合では、2 つのシステム間で完全に自動化された双方向同期は実行されません。
* **バージョン管理:**

   * [!DNL Experience Manager] では、 で作成および更新されたファイルについて、更新があった場合のみ、アセットのバージョンを作成します。[!DNL Experience Manager]
   * [!DNL Creative Cloud] Assets は独自の [バージョン管理機能](https://helpx.adobe.com/jp/creative-cloud/help/versioning-faq.html) Work in Progress の更新を対象としている（基本的には、更新が最大 10 日間保存されます）

* **スペースの制限：** 交換するファイルのサイズとボリュームは、特定の [Creative Cloud資産の割当](https://helpx.adobe.com/jp/creative-cloud/kb/file-storage-quota.html) クリエイティブユーザーの場合（サブスクリプションレベルに応じて異なります）と最大ファイルサイズは 5 GB に制限されます。 また、容量は、組織がAdobe Experience Cloud Assets コアサービスに保有するアセットの割り当てによって制限されます。

* **容量要件：** 共有フォルダー内のファイルも、 [!DNL Experience Manager] そしてその後 [!DNL Creative Cloud] アカウント、キャッシュされたコピーを [!DNL Experience Cloud Assets] コアサービス。
* **ネットワークと帯域幅：** 共有フォルダー内のファイルとすべての更新は、システム間のネットワークを介して転送する必要があります。 関連するファイルと更新のみが共有されていることを確認します。
* **フォルダータイプ**：`sling:OrderedFolder` タイプの [!DNL Assets] フォルダーの共有は、[!DNL Adobe Experience Cloud] での共有ではサポートされません。フォルダーの共有が必要な場合は、[!DNL Assets] でフォルダーを作成するときに「[!UICONTROL 並べ替え]」オプションを選択しないでください。

## ベストプラクティス {#best-practices}

を使用する際のベストプラクティス [!DNL Experience Manager] から [!DNL Creative Cloud] フォルダー共有の対象：

* **ボリュームを考慮する：** [!DNL Experience Manager] と [!DNL Creative Cloud] のフォルダー共有は、例えば、具体的なキャンペーンやアクティビティに関連した少数のファイルを共有する場合に使用します。組織で承認されたすべてのアセットなど、多数のアセットのセットを共有する場合は、他の配信方法（例えば [!DNL Assets Brand Portal] や [!DNL Experience Manager] デスクトップアプリなど）を使用します。
* **深い階層を共有しない：** 共有は再帰的に機能し、選択的な共有解除は許可されません。 通常は、サブフォルダーを持たないフォルダー、または 1 つのサブフォルダーレベルのように浅い階層を持つフォルダーのみを共有の対象とします。
* **一方向共有のためにフォルダーを分離する：**&#x200B;最終アセットを [!DNL Assets] から [!DNL Creative Cloud] ファイルへ送って共有したり、クリエイティブレディアセットを [!DNL Creative Cloud] ファイル から [!DNL Assets] へ戻して共有したりするには、フォルダーを分離する必要があります。これらのフォルダーの命名に十分な注意を払うことで、[!DNL Assets] と [!DNL Creative Cloud] の双方のユーザーが理解しやすい作業環境を構築することができます。
* **WIP 作業のために共有フォルダーを使用しない：**&#x200B;共有フォルダーは、処理中の作業（WIP）で使用しないでください。ファイルを頻繁に変更する必要がある作業を行うには、Creative Cloud Files の別のフォルダーを使用します。
* **新しい作業は共有フォルダー以外で開始する：**&#x200B;新しいデザイン（クリエイティブファイル）は、Creative Cloud Files の WIP 専用フォルダーで開始してください。新しいデザインを [!DNL Assets] ユーザーと共有する準備ができたら、共有フォルダーに移動または保存してください。
* **共有構造の簡素化：** より扱いやすいオペレーティングセットアップのために、共有構造の簡素化について検討してください。 すべてのクリエイティブユーザーと共有する代わりに、 [!DNL Assets] フォルダは、クリエイティブディレクターやチームマネージャーなど、チーム担当者とのみ共有する必要があります。 クリエイティブサイドのマネージャーが最終アセットを受け取って作業割り当てを決定し、デザイナーは自身の Creative Cloud アカウントで WIP アセットの作業をするようにします。デザイナーは Creative Cloud のコラボレーション機能を使用して共同作業を行います。最後に、準備ができたアセットを選択し、[!DNL Assets] のクリエイティブレディ用共有フォルダーに戻して共有します。

次の図は、からの既存の最終アセットに基づいてデザインを作成するための設定例を示しています。 [!DNL Assets].

![chlimage_1-180](assets/chlimage_1-407.png)
