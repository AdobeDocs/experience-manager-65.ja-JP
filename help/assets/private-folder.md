---
title: AEMでのプライベートフォルダーの作成と共有
description: Adobe Experience Manager（AEM）Assets でプライベートフォルダーを作成して、他のユーザーと共有し、様々な権限をユーザーに割り当てる方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# プライベートフォルダーの共有 {#private-folder-sharing}

Adobe Experience Manager（AEM） Assets のユーザーインターフェイスに、自分だけが使用できるプライベートフォルダーを作成できます。このプライベートフォルダーを他のユーザーと共有して、他のユーザーに様々な権限を割り当てることもできます。ユーザーはフォルダーに対して、割り当てられた権限のレベルに応じた様々なタスク（フォルダー内のアセットの表示、アセットの編集など）を実行できます。

1. In the Assets console, tap/click **[!UICONTROL Create]** from the toolbar and then choose **[!UICONTROL Folder]** from the menu.

   ![アセットフォルダの作成](assets/Create-folder.png)

1. In the **[!UICONTROL Create Folder]** dialog, enter a title and name (optional) for the folder, and select **[!UICONTROL Private]**.

   ![「非公開」チェックボックスを選択して、フォルダーを非公開にします](assets/private-folder.png)

1. 「**[!UICONTROL 作成]**」をタップまたはクリックします。UI 内にプライベートフォルダーが作成されます。

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. フォルダーを他のユーザーと共有し、権限を割り当てるには、フォルダーを選択し、ツールバーの「**[!UICONTROL プロパティ]**」アイコンをクリックまたはタップします。

   ![chlimage_1-414](assets/chlimage_1-414.png)

   >[!NOTE]
   >
   >フォルダーは、共有するまで他のユーザーに表示されません。

1. In the **[!UICONTROL Folder Properties]** page, select a user from the **[!UICONTROL Add User]** list, assign a role to the user on your private folder, and click **[!UICONTROL Add]**.

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >フォルダーを共有するユーザーに、各種役割（編集者、所有者、閲覧者など）を割り当てることができます。ユーザーに所有者の役割を割り当てると、ユーザーにフォルダーにエディター権限が付与されます。さらに、フォルダーを他のユーザーと共有できるようになります。編集者の役割を割り当てると、ユーザーがプライベートフォルダーのアセットを編集できるようになります。閲覧者の役割を割り当てると、ユーザーがプライベートフォルダーのアセットを表示できるようになります。

1. 「**[!UICONTROL 保存]**」をクリックします。割り当てた役割に応じて、ユーザーが AEM Assets にログインしたときに、プライベートフォルダーに対する一連の権限が割り当てられます。
1. 「**[!UICONTROL OK]**」をクリックして、確認メッセージを閉じます。
1. フォルダーを共有するユーザーに対して、共有に関する通知が送信されます。通知を確認するには、そのユーザーの資格情報で AEM Assets にログインします。

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. 通知アイコンをタップまたはクリックすると、通知のリストが開きます。

   ![通知のリスト](assets/Assets-Notification.png)

1. 管理者によって共有されたプライベートフォルダーのエントリをクリックまたはタップして、フォルダーを開きます。

>[!NOTE]
>
>プライベートフォルダーを作成するには、プライベートフォルダーを作成する親フォルダーに対する ACL の読み取りおよび編集権限が必要です。If you are not an administrator, these permissions are not enabled for you by default on `/content/dam`. この場合、プライベートフォルダーを作成またはフォルダー設定を表示する前に、ユーザー ID またはグループ用にそれらの権限を取得します。
