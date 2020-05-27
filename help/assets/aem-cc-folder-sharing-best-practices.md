---
title: Adobe Experience ManagerとAdobe Creative Cloudのフォルダー共有のベストプラクティス
description: Experience Manager AssetsのユーザーがAdobe Creative Cloud(CC)ユーザーとフォルダーを交換できるようにAdobe Experience Managerを設定します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 35%

---


# Adobe Experience ManagerからAdobe Creative Cloudへのフォルダー共有 {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>Experience ManagerからCreative Cloudへのフォルダー共有機能は廃止されました。 アドビでは、 [Adobe Asset Link](https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link.html) 、 [Experience Managerデスクトップアプリケーションなど、新しい機能を使用することを強くお勧めします](https://helpx.adobe.com/jp/experience-manager/desktop-app/aem-desktop-app.html)。 Learn more in [Experience Manager and Creative Cloud integration best practices](/help/assets/aem-cc-integration-best-practices.md).

Adobe Experience Managerは、アセット内のユーザーがAdobe Creative Cloudアプリのユーザーとフォルダーを共有できるように設定できるので、Adobe Creative Cloud Assetsサービスで共有フォルダーとして使用できます。 この機能を使用すると、クリエイティブチームと Assets ユーザーの間でファイルをやり取りすることができます。特に、クリエイティブユーザーが Assets インスタンスへのアクセス権を持っていない（エンタープライズネットワーク上にいない）場合に便利です。

このタイプの統合は、以下の場合に使用できます。特に、 Assets への直接アクセス権を持っていないユーザーと作業する場合に便利です。

*  Assets ユーザーが Adobe Creative Cloud Files のユーザーと一連の特定アセットを共有する場合（新しいマーケティング活動のデザイン作業に使用するクリエイティブブリーフや承認済みアセットのセットなど）。
* Adobe Creative Cloud アプリユーザーが作成した新しいファイルを、 Assets ユーザーが受け取る場合。

>[!NOTE]
>
>Before reading this document, you can review the overall [Experience Manager and Creative Cloud integration best practices](/help/assets/aem-cc-integration-best-practices.md) for a higher-level overview of the topic.

## 概要 {#overview}

Experience ManagerからCreative Cloudへのフォルダー共有は、アセットとCreative Cloudアカウント間でのフォルダーとファイルのサーバー側での共有に依存します。 また、デスクトップで Creative Cloud デスクトップアプリケーションを使用しているクリエイティブプロフェッショナルは、Adobe CreativeSync テクノロジーを使用して、共有フォルダーを直接ディスク上で使用するように設定できます。

以下の図は統合の概要を示しています。

![chlimage_1-179](assets/chlimage_1-406.png)

この統合の主要な要素は以下のとおりです。

* **Experience Manager Assetsサーバー** ：エンタープライズネットワークにデプロイ（マネージドサービスまたはオンプレミス）されます。 ここでフォルダの共有を開始します。
* **Adobe Marketing Cloud Assetsコアサービス**: Experience ManagerとCreative Cloudストレージサービスの間に介在します。 この統合を使用する企業の管理者は、Marketing Cloud 組織と Assets インスタンスの間に信頼関係を確立する必要があります。また、管理者は、 Assets ユーザーがフォルダーも共有してセキュリティを強化できるように、[承認済みの Creative Cloud 共同作業者のリストを定義](https://marketing.adobe.com/resources/help/ja_JP/mcloud/t_admin_add_cc_user.html)します。

* **Creative Cloud Assets Webサービス** (ストレージおよびCreative Cloud Files Web UI): ここでは、アセットフォルダーが共有された特定のCreative Cloudアプリユーザーが、招待を受諾して、Creative Cloudアカウントストレージーのフォルダーを表示できます。
* **Creative Cloudデスクトップアプリケーション**: （オプション）Creative Cloud Assetsストレージーと同期することで、クリエイティブユーザーのデスクトップから共有フォルダーや共有ファイルに直接アクセスできます。

## 特徴と制限事項 {#characteristics-and-limitations}

* **変更の一方向伝播：** ファイルの変更は、1方向(アセットが最初に作成（アップロード）された（Experience ManagerまたはCreative Cloud Assets）システムからのみ反映されます。 この統合では、2 つのシステム間で完全に自動化された双方向の同期はおこなわれません。
* **バージョン管理:**

   * Experience Managerでは、ファイルがExperience Managerで作成され、そこで更新された場合にのみ、アセットのバージョンが更新時に作成されます。
   * Creative Cloud Assets には、作業中（WIP）のファイルが更新された場合に実行される独自の[バージョン管理機能](https://helpx.adobe.com/jp/creative-cloud/help/versioning-faq.html)が用意されています（原則として最大 10 日間更新が保存されます）。

* **スペースの制限：** 交換するファイルのサイズと量は、クリエイティブユーザー向けの [Creative Cloud Assetsの割り当て](https://helpx.adobe.com/jp/creative-cloud/kb/file-storage-quota.html) (購読レベルによって異なります)と、最大5 GBまでに制限されます。 また、容量は、Adobe Marketing Cloud Assets コアサービスで組織が保有しているアセット割り当てによっても制限されます。

* **必要な領域：** 共有フォルダー内のファイルも、Experience Managerに物理的に保存され、次にCreative Cloudアカウントに保存され、キャッシュされたコピーと共にMarketing Cloud Assetsコアサービスに保存される必要があります。
* **ネットワークと帯域幅：** 共有フォルダー内のファイルとすべての更新を、システム間でネットワーク経由で転送する必要があります。 共有する対象は、関連するファイルおよび更新のみに限るようにしてください。
* **フォルダータイプ**：`sling:OrderedFolder` タイプの Assets フォルダーの共有は、Adobe Marketing Cloud での共有の文脈ではサポートされません。フォルダーを共有したい場合は、 Assets でフォルダーを作成するときに「並べ替え」オプションを選択しないでください。

## ベストプラクティス {#best-practices}

Experience ManagerをCreative Cloudフォルダーと共有するためのベストプラクティスは次のとおりです。

* **ボリュームの考慮事項：** 特定のキャンペーンーやアクティビティーなど、少数のファイルを共有する場合は、Experience Manager/Creative Cloudのフォルダー共有を使用する必要があります。 組織内の承認済みアセットと同様に、より大きなアセットのセットを共有するには、他の配布方法（Assets Brand Portalなど）またはExperience Managerデスクトップアプリを使用します。

* **階層の深い共有を避ける：** 共有は再帰的に機能し、選択的な非共有は許可されません。 通常、サブフォルダーを持たないフォルダー、または1つのサブフォルダーレベルなど非常に浅い階層を持つフォルダーのみを共有の対象とします。
* **一方向の共有用に別々のフォルダーを作成する：** 最終アセットをCreative Cloudファイルに共有する場合と、Creative CloudファイルからAssetsに戻す場合には、個別のフォルダーを使用します。 これらのフォルダーに適切な命名規則を組み合わせると、アセットとCreative Cloudのユーザーに対して、より理解しやすい作業環境が作成されます。
* **共有フォルダーでのWIPの回避：** 共有フォルダーは作業中には使用しないでください。Creative Cloud Files内の別のフォルダーを使用して、ファイルに頻繁に変更を加える必要のある作業を行ってください。
* **共有フォルダー外での開始の新しい作業：** 新しいデザイン（クリエイティブファイル）は、Creative Cloud Files内の別のWIPフォルダーで開始する必要があります。Assetsユーザーと共有する準備が整ったら、共有フォルダーに移動または保存する必要があります。
* **構造の共有の簡素化：** より管理しやすいオペレーティング設定を行うには、共有構造の簡素化を検討してください。 すべてのクリエイティブユーザーと共有する代わりに、アセットフォルダーは、クリエイティブディレクターやチームマネージャーなど、チームの担当者とのみ共有する必要があります。 クリエイティブサイドのマネージャーが最終アセットを受け取って作業割り当てを決定し、デザイナーは自身の Creative Cloud アカウントで WIP アセットの作業をするようにします。Creative Cloudのコラボレーション機能を使用して作業を調整し、最後に、アセットと共有できるアセットを選択して、クリエイティブに対応した共有フォルダーに戻すことができます。

以下の図に、 Assets の既存の最終アセットに基づいて新しいデザインを作成するための設定例を示します。

![chlimage_1-180](assets/chlimage_1-407.png)
