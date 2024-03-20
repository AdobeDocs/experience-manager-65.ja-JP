---
title: メールによるフォーム送信確認の送信
description: AEM Forms では、フォームの送信時に確認をユーザーに送信するメール送信アクションを設定できます。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: bca4044a-18a9-4b97-92de-eff1e9a840f9
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 100%

---

# メールによるフォーム送信確認の送信 {#sending-a-form-submission-acknowledgement-via-email}

## アダプティブフォームデータの送信 {#adaptive-form-data-submission}

アダプティブフォームには、いくつかのすぐに使用できる[送信アクション](../../forms/using/configuring-submit-actions.md)ワークフローが用意されており、フォームデータを複数のエンドポイントに送信できます。

例えば、**[!UICONTROL メールを送信]**&#x200B;アクションは、アクティビティフォームの送信に成功したときに、メールを送信します。これは、フォームデータと PDF をメールで送信するように設定することもできます。

この記事では、アダプティブフォームでメールアクションを有効にする手順や、様々な設定について詳しく説明します。

>[!NOTE]
>
>「**[!UICONTROL メールで PDF を送信]**」オプションを使用すると、完了したフォームを PDF 添付ファイルとしてメールで送信することもできます。このアクションで使用できる設定オプションは、**[!UICONTROL メールを送信]**&#x200B;アクションで使用できるオプションと同じです。PDF のメール送信アクションは、XFA ベースのアダプティブフォームに対してのみ使用できます。

## メールを送信アクション {#email-action}

メールを送信アクションを使用すると、作成者は、アダプティブフォームの送信に成功したときに、1 人または複数の受信者に自動的にメールを送信できます。

>[!NOTE]
>
>メールアクションを使用するには、[メールサービスの設定](/help/sites-administering/notification.md#configuring-the-mail-service)で説明されているように AEM メールサービスを設定する必要があります。

### アダプティブフォームでのメールアクションの有効化 {#enabling-email-action-on-an-adaptive-form}

1. アダプティブフォームを&#x200B;**[!UICONTROL 編集]**&#x200B;モードで開きます。

1. 「**[!UICONTROL コンテンツ]**」タブで、**[!UICONTROL フォームコンテナ]**&#x200B;を選択し、![設定](assets/configure-icon.svg)を選択して、アダプティブフォームのプロパティを表示します。

1. 「**[!UICONTROL 送信]**」セクションで、**[!UICONTROL 送信アクション]**&#x200B;ドロップダウンリストから「**[!UICONTROL メールを送信]**」を選択します。

   ![送信アクション](assets/submission-actions.png)

1. **[!UICONTROL 宛先]**、**[!UICONTROL CC]** および **[!UICONTROL BCC]** フィールドに有効なメール ID を指定します。

   **[!UICONTROL 件名]**&#x200B;および&#x200B;**[!UICONTROL メールテンプレート]**&#x200B;フィールドに、それぞれ件名とメール本文を指定します。

   フィールドに変数プレースホルダーを指定することもできます。この場合、フィールドの値は、フォームがエンドユーザーによって正しく送信されたときに処理されます。詳しくは、[アダプティブフォームのフィールド名を使用したメールコンテンツの動的作成](../../forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p)を参照してください。

   フォームに添付ファイルがあり、それをメールに添付する場合は、**[!UICONTROL 添付ファイルを含める]**&#x200B;を選択してください。

   >[!NOTE]
   >
   >「**[!UICONTROL メールで PDF を送信]**」オプションを選択した場合は、「添付ファイルを含める」オプションを選択する必要があります。

1. 「![保存](assets/save_icon.svg)」をクリックして、変更を保存します。

### アダプティブフォームのフィールド名を使用したメールコンテンツの動的作成 {#using-adaptive-form-field-names-to-dynamically-create-email-content}

アダプティブフォームのフィールド名はプレースホルダーと呼ばれ、ユーザーがフォームを送信した後にそのフィールドの値によって置き換えられます。

**[!UICONTROL メールを送信]**&#x200B;アクションでは、アクションを実行する際に処理されるプレースホルダーを使用できます。これは、ユーザーがフォームを送信する際に、メールのヘッダー（**[!UICONTROL 宛先]**、**[!UICONTROL CC]**、**[!UICONTROL BCC]**、**[!UICONTROL 件名]**&#x200B;など）が生成されることを意味します。

プレースホルダーを定義するには、送信アクションとして「**[!UICONTROL メールを送信]**」を選択してから、フィールドに `${<field name>}` を指定します。

例えば、フォームに `email_addr` という名前の「**[!UICONTROL メールアドレス]**」フィールドが含まれる場合、ユーザーのメール ID を取得するために、「**[!UICONTROL 宛先]**」、「**[!UICONTROL CC]**」または「**[!UICONTROL BCC]**」フィールドに以下を指定できます。

`${email_addr}`

ユーザーがフォームを送信すると、フォームの `email_addr` フィールドに入力されたメール ID にメールが送信されます。

>[!NOTE]
>
>フィールドの&#x200B;**[!UICONTROL 編集]**&#x200B;ダイアログにフィールドの名前があります。

また、変数プレースホルダーは、「**[!UICONTROL 件名]**」および「**[!UICONTROL メールテンプレート]**」フィールドにも使用できます。

例：

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>繰り返し可能なパネル内のフィールドは、変数プレースホルダーとして使用することはできません。
