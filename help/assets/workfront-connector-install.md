---
title: インストール [!DNL Workfront for Experience Manager enhanced connector]
description: インストール [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
source-git-commit: 8d39e1c86e5185a181400f10b7822a57c9d3aeae
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---


# インストール [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

で管理者アクセス権を持つユーザー [!DNL Adobe Experience Manager] 拡張コネクタをインストールします。 インストールする前に、プラットフォームのサポートとその他を確認してください [コネクタの前提条件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>Adobeには、 [!DNL Adobe Workfront for Experience Manager enhanced connector] 認定パートナーまたは [!DNL Adobe Professional Services]. 認定パートナーなしでデプロイおよび設定した場合、または [!DNL Adobe Professional Services]の場合、Adobeではサポートされません。
>
>Adobeが次の更新をリリースする可能性がある： [!DNL Adobe Workfront] および [!DNL Adobe Experience Manager] このコネクタを冗長にするこの場合、お客様はこのコネクタの使用から移行する必要が生じる場合があります。

コネクタをインストールするには、次の手順に従います。

1. コネクタのダウンロード元 [[!DNL Software Distribution] リンク](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).

1. [ファイアウォールの設定](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html).

1. Dispatcher で、という名前の HTTP ヘッダーを許可します。 `authorization`, `username`、および `apikey`. 許可 `GET`, `POST`、および `PUT` リクエスト： `/bin/workfront-tools`.

1. 次のパスがに存在しないことを確認してください。 [!DNL Experience Manager] リポジトリ：

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. 次を使用してパッケージをインストール [!UICONTROL パッケージマネージャー]. パッケージのインストール方法については、 [パッケージマネージャーのドキュメント](/help/sites-administering/package-manager.md).

1. 作成 `wf-workfront-users` in [!DNL Experience Manager] ユーザーグループと権限の割り当て `jcr:all` から `/content/dam`.

システムユーザー `workfront-tools` が自動的に作成され、必要な権限が自動的に管理されます。 からのすべてのユーザー [!DNL Workfront] コネクタを使用するユーザーは、このグループの一部として自動的に追加されます。

## 次の間の接続を設定 [!DNL Experience Manager] および [!DNL Workfront] {#configure-connection}

Workfrontとの接続を作成するには、次の手順に従います。

1. In [!DNL Experience Manager]を選択します。 **[!UICONTROL ツール]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront Tools Configuration]**.

1. 選択 `workfront-tools` を選択し、 **[!UICONTROL 作成]** 」オプションを使用して、ページの右上に表示されます。

1. 内 **[!UICONTROL Workfront Connection]** ダイアログで、 [!DNL Workfront] 配置、選択 **[!UICONTROL Workfrontに接続]** オプション。 正常に接続されると、 [!DNL Workfront] ドキュメントのカスタム統合が [!DNL Workfront] 環境。

   ![接続 [!DNL Experience Manager] および [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. 接続を確認するには、でアクセスします。 [!DNL Workfront] API キーが同じで、接続が **[!UICONTROL 有効]**. それには、「 **[!UICONTROL 設定]** > **[!UICONTROL ドキュメント]** > **[!UICONTROL カスタム統合]** in [!DNL Workfront].
