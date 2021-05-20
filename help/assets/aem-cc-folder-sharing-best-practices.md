---
title: ' [!DNL Adobe Creative Cloud] ベストプラクティスへのフォルダー共有'
description: ' [!DNL Adobe Experience Manager] to allow users in [!DNL Experience Manager Assets] を設定して、Adobe Creative Cloud(CC)ユーザーとフォルダーを交換します。'
contentOwner: AG
role: Business Practitioner, Administrator
feature: コラボレーション
exl-id: 130cec6d-1cdd-4304-94bb-65e6bb573e55
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 18%

---

# [!DNL Adobe Experience Manager] フォルダ [!DNL Adobe Creative Cloud] ー共有へ  {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>[!DNL Experience Manager]から[!DNL Creative Cloud]へのフォルダー共有機能は非推奨（廃止予定）となりました。 Adobeでは、[AdobeExperience Managerリンク](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html)や[アセットデスクトップアプリケーション](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja)など、新しい機能を使用することを強くお勧めします。 詳しくは、[Experience ManagerとCreative Cloudの統合に関するベストプラクティス](/help/assets/aem-cc-integration-best-practices.md)を参照してください。

[!DNL Adobe Experience Manager] は、のユーザーがアプリのユ [!DNL Assets] ーザーとフォルダーを共有できるように設定で [!DNL Adobe Creative Cloud] き、アセットサービスで共有フォルダーとして使 [!DNL Adobe Creative Cloud] 用できます。この機能は、クリエイティブチームと[!DNL Assets]ユーザーの間でファイルを交換する場合に使用できます。特に、クリエイティブユーザーが[!DNL Assets]デプロイメントにアクセスできない場合（エンタープライズネットワーク上にない場合）に使用できます。

このタイプの統合は、特に[!DNL Assets]に直接アクセスできないユーザーを扱う場合に、次の使用例で使用できます。

* [!DNL Assets] ユーザーは、特定のデジタルアセットのセットをファイルのユーザーと共有しま [!DNL Adobe Creative Cloud] す（新しいマーケティングアクティビティのデザイン作業用に、クリエイティブブリーフや承認済みアセットのセットなど）。
* [!DNL Assets] ユーザーは、アプリユーザーによって作成された新しいフ [!DNL Adobe Creative Cloud] ァイルを受け取ります。

>[!NOTE]
>
>このドキュメントを読む前に、[Experience ManagerとCreative Cloudの統合に関するベストプラクティス](/help/assets/aem-cc-integration-best-practices.md)で、統合の概要を確認してください。

## 概要 {#overview}

[!DNL Experience Manager] フォルダー [!DNL Creative Cloud] 共有は、とアカウント間でのフォルダーおよびファイルのサーバー側共有に [!DNL Assets] 依存 [!DNL Creative Cloud] します。デスクトップで[!DNL Creative Cloud]デスクトップアプリケーションを使用するクリエイティブプロフェッショナルは、[!DNL Adobe CreativeSync]テクノロジーを使用して、共有フォルダーを直接ディスク上で使用できるようにすることもできます。

以下の図は統合の概要を示しています。

![chlimage_1-179](assets/chlimage_1-406.png)

この統合の主要な要素は以下のとおりです。

* **[!DNL Experience Manager Assets]** エンタープライズネットワーク（マネージドサービスまたはオンプレミス）にデプロイされる場合：フォルダーの共有はここで開始されます。
* **[!DNL Adobe Marketing Cloud Assets]コアサービス**:とストレージサービスの間の [!DNL Experience Manager] 仲介 [!DNL Creative Cloud] として機能します。統合を使用する組織の管理者は、Marketing Cloud組織と[!DNL Assets]デプロイメントの間に信頼関係を確立する必要があります。 また、管理者は、 ユーザーがフォルダーも共有してセキュリティを強化できるように、[承認済みの Creative Cloud 共同作業者のリストを定義](https://experienceleague.adobe.com/docs/core-services/interface/assets/t-admin-add-cc-user.html)します。[!DNL Assets]

* **[!DNL Creative Cloud]アセットWebサービス** (ストレージおよび [!DNL Creative Cloud] ファイルWeb UI):ここでは、特定のCreative Cloudアプリユーザー（フォルダーの共有相手）が招待を受け入 [!DNL Assets] れ、自分のCreative Cloudアカウントストレージにそのフォルダーを表示できます。
* **Creative Cloudデスクトップアプリケーション**:（オプション）クリエイティブユーザーのデスクトップから、アセットストレージと同期を介して共有フォルダー/ファイルに直接ア [!DNL Creative Cloud] クセスできます。

## 特徴と制限事項 {#characteristics-and-limitations}

* **変更の一方向伝播：** ファイルの変更は、アセットが最初に作成（アップロード）されたシステム([!DNL Experience Manager] または [!DNL Creative Cloud Assets])から、一方向にのみ伝播されます。この統合では、2 つのシステム間で完全に自動化された双方向の同期はおこなわれません。
* **バージョン管理:**

   * [!DNL Experience Manager] では、 で作成および更新されたファイルについて、更新があった場合のみ、アセットのバージョンを作成します。[!DNL Experience Manager]
   * [!DNL Creative Cloud] Assets には、作業中（WIP）のファイルが更新された場合に実行される独自の[バージョン管理機能](https://helpx.adobe.com/jp/creative-cloud/help/versioning-faq.html)が用意されています（原則として最大 10 日間更新が保存されます）。

* **容量の制限：** 交換するファイルのサイズとボリュームは、クリエイティブユーザー向けの特定の [Creative Cloudアセットの割合(購読レベルに応じ](https://helpx.adobe.com/jp/creative-cloud/kb/file-storage-quota.html) る)と、最大5 GBのファイルサイズの制限によって制限されます。また、容量は、Adobe Marketing Cloud Assets コアサービスで組織が保有しているアセット割り当てによっても制限されます。

* **容量の要件：** 共有フォルダー内のファイルは、コアサービスにキャッシュされたコピーと共に、物理的ににに保存 [!DNL Experience Manager] し、アカウン [!DNL Creative Cloud] トに保存する必 [!DNL Marketing Cloud Assets] 要もあります。
* **ネットワークと帯域幅：** 共有フォルダー内のファイルとすべての更新は、システム間のネットワークを介して転送する必要があります。共有する対象は、関連するファイルおよび更新のみに限るようにしてください。
* **フォルダーの種類**:タイプのフ [!DNL Assets] ォルダーの共有 `sling:OrderedFolder`は、での共有のコンテキストではサポートされま [!DNL Adobe Marketing Cloud]せん。フォルダーを共有する場合は、[!DNL Assets]でフォルダーを作成する際に、「[!UICONTROL 並べ替え]」オプションを選択しないでください。

## ベストプラクティス {#best-practices}

[!DNL Experience Manager]と[!DNL Creative Cloud]のフォルダー共有を活用するためのベストプラクティスは次のとおりです。

* **ボリュームに関する考慮事項：** [!DNL Experience Manager] および [!DNL Creative Cloud] フォルダー共有は、特定のキャンペーンやアクティビティなどに関連した、より少数のファイルを共有する場合に使用します。組織内の承認済みアセットすべてと同様に、大量のアセットセットを共有するには、他の配布方法（例：[!DNL Assets Brand Portal]）や[!DNL Experience Manager]デスクトップアプリを使用します。
* **深い階層の共有を避ける：** 共有は再帰的に機能し、選択的な共有解除はできません。通常、共有の対象となるのは、サブフォルダーがないフォルダーか、1つのサブフォルダーレベルなど、非常に浅い階層のフォルダーのみです。
* **一方向共有用にフォルダーを分離する：** 最終アセットをからファイルに共有する場合、およびクリエイティブレディアセットをファイルからに共有する場合に、個別のフォルダーを使用 [!DNL Assets] する必要があ [!DNL Creative Cloud] りま [!DNL Creative Cloud] す [!DNL Assets]。これらのフォルダーに適切な命名規則を付けると、[!DNL Assets]と[!DNL Creative Cloud]のユーザーを同じように、わかりやすい作業環境が作成されます。
* **共有Creative Cloudー内でWIPを避ける：** 共有フォルダーは作業中には使用しないでください。ファイルに頻繁に変更を加える必要のある作業を実行するには、共有フォルダーを作業中に別のフォルダーを使用します。
* **共有Creative Cloudー以外で新しい作業を開始：** 新しいデザイン（クリエイティブファイル）は、フォルダーファイル内の別のWIPフォルダーで開始する必要がありま [!DNL Assets] す。ユーザーと共有する準備が整ったら、共有フォルダーに移動または保存します。
* **共有構造の簡素化：** より管理しやすいオペレーティングセットアップをおこなうには、共有構造を簡素化することを検討してください。[!DNL Assets]フォルダーは、クリエイティブユーザー全員と共有する代わりに、クリエイティブディレクターやチームマネージャーと同様に、チーム担当者とのみ共有する必要があります。 クリエイティブサイドのマネージャーが最終アセットを受け取って作業割り当てを決定し、デザイナーは自身の Creative Cloud アカウントで WIP アセットの作業をするようにします。Creative Cloudのコラボレーション機能を使用して作業を調整し、最後に[!DNL Assets]と共有する準備が整ったアセットを選択して、クリエイティブレディの共有フォルダーに戻すことができます。

次の図は、[!DNL Assets]の既存の最終アセットに基づいて新しいデザインを作成するための設定例を示しています。

![chlimage_1-180](assets/chlimage_1-407.png)
