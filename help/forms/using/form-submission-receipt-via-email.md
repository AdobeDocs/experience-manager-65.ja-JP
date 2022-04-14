---
title: 電子メールによるフォーム送信確認の送信
seo-title: Sending a form submission acknowledgement via email
description: AEM Forms では、フォームの送信時に確認をユーザーに送信する電子メール送信アクションを設定できます。
seo-description: AEM Forms allows you to configure the email submit action that sends an acknowledgement to a user on submitting the form.
uuid: c80b1ef4-8fe3-48e0-8fc6-3032dc022a38
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 574de3d5-69ba-4e2f-a8ab-c59f357e4386
docset: aem65
exl-id: bca4044a-18a9-4b97-92de-eff1e9a840f9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '546'
ht-degree: 100%

---

# 電子メールによるフォーム送信確認の送信 {#sending-a-form-submission-acknowledgement-via-email}

## アダプティブフォームのデータ送信 {#adaptive-form-data-submission}

アクティビティフォームでは、あらかじめ用意されたいくつかの[送信アクション](../../forms/using/configuring-submit-actions.md)が使用でき、フォームデータを複数のエンドポイントに送信できます。

例えば、**[!UICONTROL 電子メールを送信]**&#x200B;アクションは、アクティビティフォームの送信に成功したときに、電子メールを送信します。これは、フォームデータと PDF を電子メールで送信するように設定することもできます。

この記事では、アダプティブフォームで電子メールアクションを有効にする手順や、さまざまな設定について詳しく説明します。

>[!NOTE]
>
>「**[!UICONTROL 電子メールで PDF を送信]**」オプションを使用すると、完了したフォームを PDF 添付ファイルとして電子メールで送信することもできます。このアクションで使用できる設定オプションは、**[!UICONTROL 電子メールを送信]**&#x200B;アクションで使用できるオプションと同じです。PDF のメール送信アクションは、XFA ベースのアダプティブフォームに対してのみ使用できます。

## 電子メールを送信アクション {#email-action}

電子メールを送信アクションを使用すると、作成者は、アダプティブフォームの送信に成功したときに、1 人または複数の受信者に自動的に電子メールを送信できます。

>[!NOTE]
>
>電子メールアクションを使用するには、[電子メールサービスの設定](/help/sites-administering/notification.md#configuring-the-mail-service)で説明されているように AEM メールサービスを設定する必要があります。

### アダプティブフォームでの電子メールアクションの有効化 {#enabling-email-action-on-an-adaptive-form}

1. アダプティブフォームを&#x200B;**[!UICONTROL 編集]**&#x200B;モードで開きます。

1. 「**[!UICONTROL コンテンツ]**」タブで、**[!UICONTROL フォームコンテナ]**&#x200B;をタップし、![設定](assets/configure-icon.svg)をタップして、アダプティブフォームのプロパティを表示します。

1. 「**[!UICONTROL 送信]**」セクションで、**[!UICONTROL 送信アクション]**&#x200B;ドロップダウンリストから「**[!UICONTROL 電子メールを送信]**」を選択します。

   ![送信アクション](assets/submission-actions.png)

1. **[!UICONTROL 宛先]**、**[!UICONTROL CC]** および **[!UICONTROL BCC]** フィールドに有効な電子メール ID を指定します。

   **[!UICONTROL 件名]**&#x200B;および&#x200B;**[!UICONTROL 電子メールテンプレート]**&#x200B;フィールドに、それぞれ件名と電子メール本文を指定します。

   フィールドに変数プレースホルダーを指定することもできます。この場合、フィールドの値は、フォームがエンドユーザーによって正しく送信されたときに処理されます。詳細については、「[アダプティブフォームのフィールド名を使用した電子メールコンテンツの動的作成](../../forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p)」を参照してください。

   フォームに添付ファイルがあり、それを電子メールに添付する場合は、**[!UICONTROL 添付ファイルを含める]**&#x200B;を選択してください。

   >[!NOTE]
   >
   >「**[!UICONTROL 電子メールで PDF を送信]**」オプションを選択した場合は、「添付ファイルを含める」オプションを選択する必要があります。

1. 「![保存](assets/save_icon.svg)」をクリックして、変更を保存します。

### アダプティブフォームのフィールド名を使用した電子メールコンテンツの動的作成 {#using-adaptive-form-field-names-to-dynamically-create-email-content}

アダプティブフォームのフィールド名はプレースホルダーと呼ばれ、ユーザーがフォームを送信した後にそのフィールドの値によって置き換えられます。

**[!UICONTROL 電子メールを送信]**&#x200B;アクションでは、アクションを実行する際に処理されるプレースホルダーを使用できます。これは、ユーザーがフォームを送信する際に、電子メールのヘッダー（**[!UICONTROL 宛先]**、**[!UICONTROL CC]**、**[!UICONTROL BCC]**、**[!UICONTROL 件名]**&#x200B;など）が生成されることを意味します。

プレースホルダーを定義するには、送信アクションとして「**[!UICONTROL 電子メールを送信]**」を選択してから、フィールドに `${<field name>}` を指定します。

例えば、フォームに `email_addr` という名前の「**[!UICONTROL 電子メールアドレス]**」フィールドが含まれる場合、ユーザーの電子メール ID を取得するために、「**[!UICONTROL 宛先]**」、「**[!UICONTROL CC]**」または「**[!UICONTROL BCC]**」フィールドに以下を指定できます。

`${email_addr}`

ユーザーがフォームを送信すると、フォームの `email_addr` フィールドに入力された電子メール ID に電子メールが送信されます。

>[!NOTE]
>
>フィールドの&#x200B;**[!UICONTROL 編集]**&#x200B;ダイアログにフィールドの名前があります。

また、変数プレースホルダーは、「**[!UICONTROL 件名]**」および「**[!UICONTROL 電子メールテンプレート]**」フィールドにも使用できます。

以下に例を示します。

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>繰り返し可能なパネル内のフィールドは、変数プレースホルダーとして使用することはできません。
