---
title: アセットのワークフローオフローダー
seo-title: アセットのワークフローオフローダー
description: アセットのワークフローオフローダーについて説明します。
seo-description: アセットのワークフローオフローダーについて説明します。
uuid: d1c93ef9-a0e1-43c7-b591-f59d1ee4f88b
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 91f0fd7d-4b49-4599-8f0e-fc367d51aeba
translation-type: tm+mt
source-git-commit: f24142064b15606a5706fe78bf56866f7f9a40ae

---


# アセットのワークフローオフローダー{#assets-workflow-offloader}

Assets ワークフローオフローダーを使用すると、Adobe Experience Manager（AEM）Assets の複数のインスタンスを有効にして、プライマリ（リーダー）インスタンスでの処理の負荷を軽減できます。処理の負荷は、リーダーインスタンスとそれに追加する各種オフローダー（ワーカー）インスタンスの間で分散されます。アセットの処理の負荷を分散すると、AEM Assets でのアセット処理の効率と速度が上がります。さらに、特定の MIME タイプのアセットの処理に専用リソースを割り当てやすくなります。例えば、トポロジの特定のノードを InDesign アセットの処理専用として割り当てることができます。

## オフローダートポロジの設定 {#configure-offloader-topology}

Configuration Managerを使用して、リーダーインスタンスのURLと、リーダーインスタンス上の接続要求のオフローダーインスタンスのホスト名を追加します。

1. Tap/click the AEM logo, and choose **Tools** > **Operations** > **Web Console** to open Configuration Manager.
1. From the Web Console, select **Sling** >  **Topology Management**.

   ![chlimage_1-44](assets/chlimage_1-44a.png)

1. In the Topology Management page, tap/click the **Configure Discovery.Oak Service** link.

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. In the Discovery Service Configuration page, specify the connector URL for the leader instance in the **Topology Connector URLs** field.

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. In the **Topology Connector Whitelist** field, specify IP address or host names of offloader instances that are allowed to connect with the leader instance. 「**Save**」をタップまたはクリックします。

   ![chlimage_1-47](assets/chlimage_1-47a.png)

1. リーダーインスタンスに接続されているオフローダーインスタンスを確認するには、**ツール**／**導入**／**トポロジ**&#x200B;で、クラスタービューをタップまたはクリックします。

## オフロードの無効化 {#disable-offloading}

1. Tap/click the AEM logo, and choose **Tools** > **Deployment** > **Offloading**. The **Offloading Browser** page displays topics and the server instances that can consume the topics.

   ![chlimage_1-48](assets/chlimage_1-48a.png)

1. Disable the *com/adobe/granite/workflow/offloading* topic on the leader instances with which users interact to upload or change AEM assets.

   ![chlimage_1-49](assets/chlimage_1-49a.png)

## リーダーインスタンスでのワークフローランチャーの設定 {#configure-workflow-launchers-on-the-leader-instance}

Configure workflow launchers to use the [!UICONTROL DAM Update Asset Offloading] workflow on the leader instance instead of the **Dam Update Asset** workflow.

1. Tap/click the AEM logo, and choose, **Tools** > **Workflow** > **Launchers** to open the **Workflow Launchers** console.

   ![chlimage_1-50](assets/chlimage_1-50a.png)

1. Locate the two Launcher configurations with event type **Node Created** and **Node Modified** respectively, which run the **DAM Update Asset** workflow.
1. For each configuration, select the checkbox before it and tap/click the **View Properties** icon from the toolbar to display the **Launcher Properties** dialog.

   ![chlimage_1-51](assets/chlimage_1-51a.png)

1. From the **Workflow** list, choose [!UICONTROL DAM Update Asset Offloading] and tap/click **Save**.

   ![chlimage_1-52](assets/chlimage_1-52a.png)

1. Tap/click the AEM logo, and choose, **Tools** > **Workflow** > **Models** to open the **Workflow Models** page.
1. Select the [!UICONTROL DAM Update Asset Offloading] workflow, and tap/click **Edit** from the toolbar to display its details.

   ![chlimage_1-53](assets/chlimage_1-53a.png)

1. Display the context menu for the **DAM Workflow Offloading** step, and choose **Edit**. 設定ダイアログの「**汎用引数**」タブで「**ジョブトピック**」フィールドのエントリを確認します。

   ![chlimage_1-54](assets/chlimage_1-54a.png)

## オフローダーインスタンスのワークフローランチャーの無効化 {#disable-the-workflow-launchers-on-the-offloader-instances}

Disable the workflow launchers that run the **DAM Update Asset** workflow on the leader instance.

1. Tap/click the AEM logo, and choose, **Tools** > **Workflow** > **Launchers** to open the **Workflow Launchers** console.

   ![chlimage_1-55](assets/chlimage_1-55a.png)

1. Locate the two Launcher configurations with event type **Node Created** and **Node Modified** respectively, which run the **DAM Update Asset** workflow.
1. For each configuration, select the checkbox before it and tap/click the **View Properties** icon from the toolbar to display the **Launcher Properties** dialog.

   ![chlimage_1-56](assets/chlimage_1-56a.png)

1. In the **Activate** section, drag the slider to disable the workflow launcher and tap/click **Save** to disable it.

   ![chlimage_1-57](assets/chlimage_1-57a.png)

1. リーダーインスタンスで画像タイプのアセットをアップロードします。 オフロードされたインスタンスによって、アセットに対して生成され、移植されたサムネールを確認します。

