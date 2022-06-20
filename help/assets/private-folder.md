---
title: アセットを共有するプライベートフォルダー
description: ' [!DNL Adobe Experience Manager Assets]  でプライベートフォルダーを作成して、他のユーザーと共有し、様々な特権をユーザーに割り当てる方法について説明します。'
contentOwner: AG
role: User
feature: Collaboration
exl-id: c1aece06-7c1c-43a0-bea0-6f11ecda7e68
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 96%

---

# [!DNL Adobe Experience Manager Assets] のプライベートフォルダー {#private-folder}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/private-folder.html?lang=en) |
| AEM 6.5 | この記事 |
| AEM 6.4 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-64/assets/managing/private-folder.html?lang=en) |

[!DNL Adobe Experience Manager Assets] のユーザーインターフェイスに、自分だけが使用できるプライベートフォルダーを作成できます。このプライベートフォルダーを他のユーザーと共有して、他のユーザーに様々な権限を割り当てることができます。ユーザーはフォルダーに対して、割り当てられた特権のレベルに応じた様々なタスク（フォルダー内のアセットの表示、アセットの編集など）を実行できます。

>[!NOTE]
>
>プライベートフォルダーには、所有者の役割を持つメンバーが少なくとも 1 人含まれています。

## プライベートフォルダーの作成と共有 {#create-share-private-folder}

プライベートフォルダーを作成して共有するには：

1. [!DNL Assets] コンソールのツールバーの「**[!UICONTROL 作成]**」をクリックし、メニューの「**[!UICONTROL フォルダー]**」を選択します。

   ![アセットフォルダーを作成](assets/Create-folder.png)

1. **[!UICONTROL フォルダーを作成]**&#x200B;ダイアログで、フォルダーのタイトルと名前（オプション）を入力して、「**[!UICONTROL プライベート]**」を選択します。

1. **[!UICONTROL 作成]**&#x200B;をクリックすると、プライベートフォルダーが作成されます。

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. フォルダーを他のユーザーと共有し、特権を割り当てるには、フォルダーを選択し、ツールバーの「**[!UICONTROL プロパティ]**」をクリックします。

   ![情報オプション](assets/do-not-localize/info-circle-icon.png)

   >[!NOTE]
   >
   >フォルダーを共有するまで、他のユーザーにはフォルダーが表示されません。

1. **[!UICONTROL フォルダーのプロパティ]**&#x200B;ページで、**[!UICONTROL ユーザーを追加]**&#x200B;リストからユーザーを選択し、プライベートフォルダーでの役割をそのユーザーに割り当てて、「**[!UICONTROL 追加]**」をクリックします。

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >フォルダーを共有するユーザーには、`Editor`、`Owner`、`Viewer` など、様々な役割を割り当てることができます。ユーザーに `Owner` の役割を割り当てると、そのユーザーはフォルダー対して `Editor` 権限を持ちます。さらに、フォルダーを他のユーザーと共有できるようになります。`Editor` の役割を割り当てると、ユーザーがプライベートフォルダーのアセットを編集できるようになります。閲覧者の役割を割り当てると、ユーザーがプライベートフォルダーのアセットを表示できるようになります。

   >[!NOTE]
   >
   >プライベートフォルダーには、`Owner` の役割を持つメンバーが 1 人以上含まれています。したがって、管理者はすべての所有者メンバーをプライベートフォルダーから削除することはできません。ただし、プライベートフォルダーから既存の所有者（および管理者自体）を削除するには、管理者は別のユーザーを所有者として追加する必要があります。

1. 「**[!UICONTROL 保存]**」をクリックします。割り当てた役割に応じて、ユーザーが [!DNL Assets] にログインしたときに、プライベートフォルダーに対する一連の権限が割り当てられます。
1. 「**[!UICONTROL OK]**」をクリックして、確認メッセージを閉じます。
1. フォルダーを共有するユーザーに対して、共有に関する通知が送信されます。通知を確認するには、そのユーザーの資格情報で [!DNL Assets] にログインします。

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. 「[!UICONTROL 通知]」をクリックして、通知のリストを開きます。

   ![通知のリスト](assets/Assets-Notification.png)

1. 管理者によって共有されたプライベートフォルダーのエントリをクリックして、フォルダーを開きます。

>[!NOTE]
>
>プライベートフォルダーを作成するには、プライベートフォルダーを作成する親フォルダーに対する読み取りおよび修正の[アクセス制御権限](/help/sites-administering/security.md#permissions-in-aem)が必要です。管理者でない場合、これらの権限は `/content/dam` でデフォルトでは有効になっていません。この場合、プライベートフォルダーを作成する前に、ユーザー ID またはグループ用にそれらの権限を取得します。

## プライベートフォルダーの削除 {#delete-private-folder}

フォルダーを選択してトップメニューから「[!UICONTROL 削除]」オプションを選択するか、キーボードの Backspace キーを使用して、フォルダーを削除できます。

![トップメニューの削除オプション](assets/delete-option.png)

>[!CAUTION]
>
>CRXDE Lite からプライベートフォルダーを削除すると、リポジトリに冗長なユーザーグループが残ります。

>[!NOTE]
>
>上記の方法を使用してユーザーインターフェイスからフォルダーを削除すると、関連するユーザーグループも削除されます。
>
>ただし、既存の冗長ユーザーグループ、未使用のユーザーグループ、自動生成されたユーザーグループは、作成者インスタンス（`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`）の JMX で `clean` メソッドを使用してリポジトリから削除できます。
