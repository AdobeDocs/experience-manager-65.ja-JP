---
title: インストール [!DNL Workfront for Experience Manager enhanced connector]
description: インストール [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 087bc811-e8f8-4db5-b066-627a9b082f57
source-git-commit: a589836c77fd919838dce60a1eaf676683c165c0
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 45%

---

# [!DNL Workfront for Experience Manager enhanced connector] のインストール {#assets-integration-overview}

で管理者アクセス権を持つユーザー [!DNL Adobe Experience Manager] 拡張コネクタをインストールします。 インストールする前に、プラットフォームのサポートとコネクタのその他の [前提条件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience) を確認してください。

>[!TIP]
>
>次を検索していますか： [!DNL Workfront for Experience Manager enhanced connector] AEMas a Cloud Serviceのドキュメント クリック [ここ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-install.html?lang=en).

>[!IMPORTANT]
>
>アドビでは、[!DNL Adobe Workfront for Experience Manager enhanced connector] のデプロイメントと設定を、認定パートナーまたは [!DNL Adobe Professional Services] を通じてのみ行うことを求めています。認定パートナーまたは [!DNL Adobe Professional Services] 以外がデプロイと設定を行った場合は、アドビのサポート対象外となります。
>
>アドビは、このコネクターを冗長にする[!DNL Adobe Workfront] および [!DNL Adobe Experience Manager] の更新をリリースする可能性があります。この場合、お客様はこのコネクターの使用から移行する必要が生じることがあります。

コネクタをインストールするには、次の手順に従います。

1. コネクタのダウンロード元 [[!DNL Software Distribution] リンク](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).

1. [ファイアウォールの設定](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html?lang=ja)。

1. Dispatcher で、`authorization`、`username` および `apikey` という名前の HTTP ヘッダーを許可します。`GET`、`POST` および `PUT` リクエストを `/bin/workfront-tools` に許可します。

1. 次のパスが [!DNL Experience Manager] リポジトリに存在しないことを確認します。

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. 次を使用してパッケージをインストール [!UICONTROL パッケージマネージャー]. パッケージのインストール方法については、 [パッケージマネージャーのドキュメント](/help/sites-administering/package-manager.md).

1. 作成 `wf-workfront-users` in [!DNL Experience Manager] ユーザーグループと権限の割り当て `jcr:all` から `/content/dam`.

システムユーザー `workfront-tools` が自動的に作成され、必要な権限が自動的に管理されます。からのすべてのユーザー [!DNL Workfront] コネクタを使用するユーザーは、このグループの一部として自動的に追加されます。

## 次の間の接続を設定 [!DNL Experience Manager] および [!DNL Workfront] {#configure-connection}

Workfrontとの接続を作成するには、次の手順に従います。

1. [!DNL Experience Manager] で、**[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL Workfront ツール設定]** を選択します。 

1. 左側のパネルで `workfront-tools` を選択し、ページの右上の領域で **[!UICONTROL 作成]** オプションを選択します。

1. **[!UICONTROL Workfront 接続]** ダイアログで、[!DNL Workfront] デプロイメントに必要な詳細を入力し、 **[!UICONTROL Workfront への接続]** オプションを選択します。正常に接続すると、[!DNL Workfront] ドキュメントのカスタム統合が [!DNL Workfront] 環境に自動作成されます。

   ![[!DNL Experience Manager] と [!DNL Workfront]](/help/assets/assets/wf-connection-config.png) の接続

1. 接続を確認するには、でアクセスします。 [!DNL Workfront] API キーが同じで、接続が **[!UICONTROL 有効]**. それには、「 **[!UICONTROL 設定]** > **[!UICONTROL ドキュメント]** > **[!UICONTROL カスタム統合]** in [!DNL Workfront].

## 更新 [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

Experience Manager Assetsでは、 [!DNL Workfront for Experience Manager enhanced connector] 以前のバージョンから最新のバージョンに移行する場合。

次の手順で [!DNL Workfront for Experience Manager enhanced connector] を最新バージョンに変更するには：

1. 拡張コネクタの最新バージョンをからダウンロードします。 [[!DNL Software Distribution] リンク](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).

1. 次を使用してパッケージをインストール [!UICONTROL パッケージマネージャー]. パッケージのインストール方法については、 [パッケージマネージャーのドキュメント](/help/sites-administering/package-manager.md).


