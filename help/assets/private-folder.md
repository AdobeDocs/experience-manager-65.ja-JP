---
title: AEMでのプライベートフォルダーの作成と共有
description: Adobe Experience Manager (AEM) Assets でプライベートフォルダーを作成して、他のユーザーと共有し、様々な特権をユーザーに割り当てる方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 979d5074fcf94ca999fd941c77038ab6305cc67d
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 71%

---


# プライベートフォルダーの共有 {#private-folder-sharing}

Adobe Experience Manager (AEM) Assets のユーザーインターフェイスに、自分だけが使用できるプライベートフォルダーを作成できます。このプライベートフォルダーを他のユーザーと共有し、他のユーザーに様々な権限を割り当てることができます。 ユーザーはフォルダーに対して、割り当てられた特権のレベルに応じた様々なタスク（フォルダー内のアセットの表示、アセットの編集など）を実行できます。

>[!NOTE]
>
> プライベートフォルダーには常に、所有者の役割を持つ1つ以上のメンバーが含まれます。


1. アセットコンソールのツールバーの「**[!UICONTROL 作成]**」をタップまたはクリックし、メニューの「**[!UICONTROL フォルダー]**」を選択します。

   ![アセットフォルダーの作成](assets/Create-folder.png)

1. In the **[!UICONTROL Create Folder]** dialog, enter a title and name (optional) for the folder, and select **[!UICONTROL Private]**.

   ![「非公開」チェックボックスを選択して、フォルダーを非公開にします](assets/private-folder.png)

1. 「**[!UICONTROL 作成]**」をタップまたはクリックします。UI 内にプライベートフォルダーが作成されます。

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. フォルダーを他のユーザーと共有し、特権を割り当てるには、フォルダーを選択し、ツールバーの「**[!UICONTROL プロパティ]**」アイコンをクリックまたはタップします。

   ![chlimage_1-414](assets/chlimage_1-414.png)

   >[!NOTE]
   >
   >フォルダーを共有するまで、他のユーザーにはフォルダーが表示されません。

1. In the **[!UICONTROL Folder Properties]** page, select a user from the **[!UICONTROL Add User]** list, assign a role to the user on your private folder, and click **[!UICONTROL Add]**.

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >フォルダーを共有するユーザーに、各種役割（編集者、所有者、閲覧者など）を割り当てることができます。ユーザーに所有者の役割を割り当てると、ユーザーにフォルダーにエディター特権が付与されます。さらに、フォルダーを他のユーザーと共有できるようになります。編集者の役割を割り当てると、ユーザーがプライベートフォルダーのアセットを編集できるようになります。閲覧者の役割を割り当てると、ユーザーがプライベートフォルダーのアセットを表示できるようになります。

   >[!NOTE]
   >
   > プライベートフォルダーには常に、所有者の役割を持つ1つ以上のメンバーが含まれます。 したがって、管理者はすべての所有者メンバーをプライベートフォルダーから削除することはできません。 ただし、既存の所有者をプライベートフォルダー管理者から削除するには、他のユーザーを所有者として追加する必要があります。

1. 「**[!UICONTROL 保存]**」をクリックします。割り当てた役割に応じて、ユーザーが AEM Assets にログインしたときに、プライベートフォルダーに対する一連の特権が割り当てられます。
1. 「**[!UICONTROL OK]**」をクリックして、確認メッセージを閉じます。
1. フォルダーを共有するユーザーに対して、共有に関する通知が送信されます。通知を確認するには、そのユーザーの資格情報で AEM Assets にログインします。

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. 通知アイコンをタップまたはクリックすると、通知のリストが開きます。

   ![通知のリスト](assets/Assets-Notification.png)

1. 管理者によって共有されたプライベートフォルダーのエントリをクリックまたはタップして、フォルダーを開きます。

>[!NOTE]
>
>プライベートフォルダーを作成するには、プライベートフォルダーを作成する親フォルダーに対する ACL の読み取りおよび編集権限が必要です。If you are not an administrator, these permissions are not enabled for you by default on `/content/dam`. この場合、プライベートフォルダーを作成またはフォルダー設定を表示する前に、ユーザー ID またはグループ用にそれらの権限を取得します。
