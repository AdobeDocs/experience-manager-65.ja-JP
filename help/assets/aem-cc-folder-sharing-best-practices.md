---
title: ' [!DNL Adobe Creative Cloud]  へのフォルダー共有時のベストプラクティス'
description: ' [!DNL Experience Manager Assets]  のユーザーが Adobe Creative Cloud ユーザーとフォルダーを交換できるように  [!DNL Adobe Experience Manager]  を設定します。'
contentOwner: AG
role: User, Admin
feature: Collaboration
exl-id: 130cec6d-1cdd-4304-94bb-65e6bb573e55
source-git-commit: a76772b8761e35a828814ffe0ac3b019266ff008
workflow-type: ht
source-wordcount: '958'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager] から [!DNL Adobe Creative Cloud] へのフォルダー共有 {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>[!DNL Experience Manager] から [!DNL Creative Cloud] へのフォルダー共有機能は廃止されました。[Adobe Asset Link](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html) または [Experience Manager デスクトップアプリ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja)などの新しい機能を使用することを強くお勧めします。詳しくは、[Experience Manager と Creative Cloud の統合のベストプラクティス](/help/assets/aem-cc-integration-best-practices.md)を参照してください。

[!DNL Adobe Experience Manager] は、[!DNL Assets] のユーザーに [!DNL Adobe Creative Cloud] アプリのユーザーとのフォルダー共有を許可するように設定できます。これにより、[!DNL Adobe Creative Cloud] アセットサービスの共有フォルダーとして利用が可能になります。この機能を使用すると、クリエイティブチームと [!DNL Assets] ユーザーの間でファイルをやり取りすることができます。特に、クリエイティブユーザーが [!DNL Assets] デプロイメントへのアクセス権を持っていない（エンタープライズネットワーク上にいない）場合に有用です。

このタイプの統合は、以下のユースケースに使用できます。特に、[!DNL Assets] への直接アクセス権を持っていないユーザーと作業する場合に便利です。

* [!DNL Assets] ユーザーが [!DNL Adobe Creative Cloud] ファイルのユーザーと特定のデジタルアセット群を共有する場合（例えば、新しいマーケティング活動のデザイン作業に使用するクリエイティブブリーフや一連の承認済みアセットなど）
* [!DNL Assets] ユーザーが [!DNL Adobe Creative Cloud] アプリユーザーの作成した新規ファイルを受け取る場合

>[!NOTE]
>
>このドキュメントを読む前に、[Experience Manager と Creative Cloud の統合のベストプラクティス](/help/assets/aem-cc-integration-best-practices.md)全体を確認すると、統合の概要を把握することができます。

## 概要 {#overview}

[!DNL Experience Manager] と [!DNL Creative Cloud] のフォルダー共有は、サーバー側で [!DNL Assets] と [!DNL Creative Cloud] のアカウント間でフォルダーとファイルが共有されているかに依存します。また、デスクトップで [!DNL Creative Cloud] デスクトップアプリケーションを使用しているクリエイティブプロフェッショナルは、[!DNL Adobe CreativeSync] テクノロジーを使用して、共有フォルダーを直接ディスク上でも使用するように設定できます。

以下の図は統合の概要を示しています。

![chlimage_1-179](assets/chlimage_1-406.png)

この統合の主要な要素は以下のとおりです。

* エンタープライズネットワーク（Managed Services またはオンプレミス）にデプロイされた **[!DNL Experience Manager Assets]**：フォルダー共有はここから開始されます。
* **[!DNL Adobe Marketing Cloud Assets]コアサービス**：[!DNL Experience Manager] と [!DNL Creative Cloud] のストレージサービス間で仲介を行います。統合を使用する組織の管理者は、Marketing Cloud 組織と [!DNL Assets] デプロイメントの間に信頼関係を確立する必要があります。また、管理者は、 ユーザーがフォルダーも共有してセキュリティを強化できるように、[承認済みの Creative Cloud 共同作業者のリストを定義](https://experienceleague.adobe.com/docs/core-services/interface/assets/t-admin-add-cc-user.html?lang=ja)します。[!DNL Assets]

* **[!DNL Creative Cloud]Assets の web サービス**（ストレージおよび [!DNL Creative Cloud] ファイルの web UI）：[!DNL Assets] フォルダーを共有している特定の Creative Cloud アプリユーザーが招待を受け入れ、自身の Creative Cloud アカウントのストレージにあるフォルダーを参照できる場所です。
* **Creative Cloud デスクトップアプリ**：（オプション）[!DNL Creative Cloud] Assets ストレージと同期することで、クリエイティブユーザーのデスクトップから共有のフォルダーやファイルに直接アクセスすることができます。

## 特徴と制限事項 {#characteristics-and-limitations}

* **変更の一方向の伝播：**&#x200B;ファイルの変更は、アセットが最初に作成（アップロード）されたシステム（[!DNL Experience Manager] または [!DNL Creative Cloud Assets]）から一方向にのみ伝播します。この統合では、2 つのシステム間で完全に自動化された双方向の同期はおこなわれません。
* **バージョン管理:**

   * [!DNL Experience Manager] では、 で作成および更新されたファイルについて、更新があった場合のみ、アセットのバージョンを作成します。[!DNL Experience Manager]
   * [!DNL Creative Cloud] Assets には、作業中（WIP）のファイルが更新された場合に実行される独自の[バージョン管理機能](https://helpx.adobe.com/jp/creative-cloud/help/versioning-faq.html)が用意されています（原則として最大 10 日間更新が保存されます）。

* **容量制限：**&#x200B;交換するファイルのサイズおよびボリュームは、クリエイティブユーザーに適用される特定の [Creative Cloud Assets 割り当て](https://helpx.adobe.com/jp/creative-cloud/kb/file-storage-quota.html)（サブスクリプションレベルに依存します）とファイルサイズの上限（5 GB）によって制限されます。また、容量は、Adobe Marketing Cloud Assets コアサービスで組織が保有しているアセット割り当てによっても制限されます。

* **容量要件：**&#x200B;共有フォルダーのファイルは、[!DNL Experience Manager] と [!DNL Creative Cloud] アカウントで物理的に保存する必要があります。キャッシュコピーは [!DNL Marketing Cloud Assets] コアサービスに保持されます。
* **ネットワークと帯域幅：**&#x200B;共有フォルダーのファイルとその更新はすべて、システム間のネットワーク経由で転送する必要があります。共有する対象は、関連するファイルおよび更新のみに限るようにしてください。
* **フォルダータイプ**：`sling:OrderedFolder` タイプの [!DNL Assets] フォルダーの共有は、[!DNL Adobe Marketing Cloud] での共有ではサポートされません。フォルダーの共有が必要な場合は、[!DNL Assets] でフォルダーを作成するときに「[!UICONTROL 並べ替え]」オプションを選択しないでください。

## ベストプラクティス {#best-practices}

[!DNL Experience Manager] を利用して [!DNL Creative Cloud] フォルダーを共有する場合、次のようなベストプラクティスが考えられます。

* **ボリュームを考慮する：** [!DNL Experience Manager] と [!DNL Creative Cloud] のフォルダー共有は、例えば、具体的なキャンペーンやアクティビティに関連した少数のファイルを共有する場合に使用します。組織で承認されたすべてのアセットなど、多数のアセットのセットを共有する場合は、他の配信方法（例えば [!DNL Assets Brand Portal] や [!DNL Experience Manager] デスクトップアプリなど）を使用します。
* **深い階層の共有を避ける：**&#x200B;共有は再帰的に適用されます。また、一部だけ共有を解除することはできません。通常、フォルダーの共有には、サブフォルダーのないフォルダー、または階層の浅いフォルダー（サブフォルダーが 1 レベルなど）を使用します。
* **一方向共有のためにフォルダーを分離する：**&#x200B;最終アセットを [!DNL Assets] から [!DNL Creative Cloud] ファイルへ送って共有したり、クリエイティブレディアセットを [!DNL Creative Cloud] ファイル から [!DNL Assets] へ戻して共有したりするには、フォルダーを分離する必要があります。これらのフォルダーの命名に十分な注意を払うことで、[!DNL Assets] と [!DNL Creative Cloud] の双方のユーザーが理解しやすい作業環境を構築することができます。
* **WIP 作業のために共有フォルダーを使用しない：**&#x200B;共有フォルダーは、処理中の作業（WIP）で使用しないでください。ファイルを頻繁に変更する必要がある作業を行うには、Creative Cloud Files の別のフォルダーを使用します。
* **新しい作業は共有フォルダー以外で開始する：**&#x200B;新しいデザイン（クリエイティブファイル）は、Creative Cloud Files の WIP 専用フォルダーで開始してください。新しいデザインを [!DNL Assets] ユーザーと共有する準備ができたら、共有フォルダーに移動または保存してください。
* **共有の構造を簡素化する：**&#x200B;操作の設定管理を向上させるには、共有の構造を簡素化する必要があります。[!DNL Assets] フォルダーを共有する相手は、クリエイティブユーザー全員ではなく、クリエイティブディレクターやチームマネージャーなどチームの代表者のみに制限してください。クリエイティブサイドのマネージャーが最終アセットを受け取って作業割り当てを決定し、デザイナーは自身の Creative Cloud アカウントで WIP アセットの作業をするようにします。デザイナーは Creative Cloud のコラボレーション機能を使用して共同作業を行います。最後に、準備ができたアセットを選択し、[!DNL Assets] のクリエイティブレディ用共有フォルダーに戻して共有します。

以下の図は、[!DNL Assets] の既存の最終アセットに基づいて新しいデザインを作成するための設定例を示しています。

![chlimage_1-180](assets/chlimage_1-407.png)
