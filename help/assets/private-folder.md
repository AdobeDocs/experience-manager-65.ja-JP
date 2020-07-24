---
title: Adobe Experience Manager内のプライベートフォルダーを作成して共有します。
description: Adobe Experience Managerアセット内にプライベートフォルダーを作成し、他のユーザーと共有し、それらに様々な権限を割り当てる方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 29cf202b2522b4e624960e8b911f77ec7f291e24
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 44%

---


# プライベートフォルダーの共有 {#private-folder-sharing}

専用に使用できるAdobe Experience Managerアセットユーザーインターフェイスで、プライベートフォルダーを作成できます。 このプライベートフォルダーを他のユーザーと共有し、他のユーザーに様々な権限を割り当てることができます。 ユーザーはフォルダーに対して、割り当てられた特権のレベルに応じた様々なタスク（フォルダー内のアセットの表示、アセットの編集など）を実行できます。

>[!NOTE]
>
>プライベートフォルダーには、所有者の役割を持つメンバが少なくとも1つ存在します。

1. In the Assets console, click **[!UICONTROL Create]** from the toolbar and then choose **[!UICONTROL Folder]** from the menu.

   ![アセットフォルダーの作成](assets/Create-folder.png)

1. In the **[!UICONTROL Create Folder]** dialog, enter a title and name (optional) for the folder, and select **[!UICONTROL Private]** option.

1. 「 **[!UICONTROL 作成]**」をクリックします。 プライベートフォルダーが作成されます。

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. To share the folder with other users and the assign privileges to them, select the folder, and click **[!UICONTROL Properties]** from the toolbar.

   ![情報オプション](assets/do-not-localize/info-circle-icon.png)

   >[!NOTE]
   >
   >フォルダーを共有するまで、他のユーザーにはフォルダーが表示されません。

1. In the **[!UICONTROL Folder Properties]** page, select a user from the **[!UICONTROL Add User]** list, assign a role to the user on your private folder, and click **[!UICONTROL Add]**.

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >フォルダーを共有するユーザーに、各種役割（編集者、所有者、閲覧者など）を割り当てることができます。ユーザーに所有者の役割を割り当てると、ユーザーにフォルダーにエディター特権が付与されます。さらに、フォルダーを他のユーザーと共有できるようになります。編集者の役割を割り当てると、ユーザーがプライベートフォルダーのアセットを編集できるようになります。ビューアの役割を割り当てた場合、ユーザはプライベートフォルダ内のアセットの表示のみが可能です。

   >[!NOTE]
   >
   >プライベートフォルダーには、所有者の役割を持つメンバが少なくとも1つ存在します。 したがって、管理者はすべての所有者メンバーをプライベートフォルダーから削除することはできません。 ただし、既存の所有者（および管理者自体）をプライベートフォルダーから削除するには、管理者は別のユーザーを所有者として追加する必要があります。

1. 「**[!UICONTROL 保存]**」をクリックします。割り当てた役割に応じて、ユーザーが Assets にログインしたときに、プライベートフォルダーに対する一連の特権が割り当てられます。
1. 「**[!UICONTROL OK]**」をクリックして、確認メッセージを閉じます。
1. フォルダーを共有するユーザーに対して、共有に関する通知が送信されます。通知を確認するには、そのユーザーの資格情報で Assets にログインします。

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. 「通知」をクリックして、通知のリストを開きます。

   ![通知のリスト](assets/Assets-Notification.png)

1. 管理者が共有するプライベートフォルダーのエントリをクリックして、フォルダーを開きます。

>[!NOTE]
>
>プライベートフォルダーを作成するには、プライベートフォルダーを作成する親フォルダーに対する ACL の読み取りおよび編集権限が必要です。If you are not an administrator, these permissions are not enabled for you by default on `/content/dam`. この場合、プライベートフォルダーを作成またはフォルダー設定を表示する前に、ユーザー ID またはグループ用にそれらの権限を取得します。
