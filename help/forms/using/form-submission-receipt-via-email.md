---
title: 電子メールによるフォーム送信確認の送信
seo-title: 電子メールによるフォーム送信確認の送信
description: AEM Forms では、フォームの送信時に確認をユーザーに送信する電子メール送信アクションを設定できます。
seo-description: AEM Forms では、フォームの送信時に確認をユーザーに送信する電子メール送信アクションを設定できます。
uuid: c80b1ef4-8fe3-48e0-8fc6-3032dc022a38
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 574de3d5-69ba-4e2f-a8ab-c59f357e4386
docset: aem65
translation-type: tm+mt
source-git-commit: acc2a3977353386d7e1dfd1344a61d78812fe3fc
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 44%

---


# 電子メールによるフォーム送信確認の送信  {#sending-a-form-submission-acknowledgement-via-email}

## アクティビティフォームデータ送信 {#adaptive-form-data-submission}

アクティビティフォームでは、あらかじめ用意されたいくつかの[送信アクション](../../forms/using/configuring-submit-actions.md)が使用でき、フォームデータを複数のエンドポイントに送信できます。

例えば、**[!UICONTROL 電子メール]**&#x200B;送信アクションでは、アダプティブフォームの送信が成功した場合に電子メールが送信されます。 これは、フォームデータと PDF を電子メールで送信するように設定することもできます。

この記事では、アダプティブフォームで電子メールアクションを有効にする手順や、さまざまな設定について詳しく説明します。

>[!NOTE]
>
>「**[!UICONTROL PDFを電子メールで送信]**」オプションを使用して、完成したフォームをPDF添付ファイルとして電子メールで送信することもできます。 このアクションで使用できる設定オプションは、**[!UICONTROL 電子メール]**&#x200B;を送信アクションで使用できるオプションと同じです。 PDF のメール送信アクションは、XFA ベースのアダプティブフォームに対してのみ使用できます。

## メール送信アクション{#email-action}

「電子メールを送信」アクションを使用すると、アダプティブフォームの送信が成功した場合に、1人または複数の受信者に電子メールを自動的に送信できます。

>[!NOTE]
>
>「電子メールを送信」アクションを使用するには、[メールサービスの設定](/help/sites-administering/notification.md#configuring-the-mail-service)の説明に従ってAEMメールサービスを設定する必要があります。

### アダプティブフォームでの電子メール送信アクションの有効化{#enabling-email-action-on-an-adaptive-form}

1. アダプティブフォームを&#x200B;**[!UICONTROL 編集]**&#x200B;モードで開きます。

1. 「**[!UICONTROL コンテンツ]**」タブで、**[!UICONTROL フォームコンテナ]**&#x200B;をタップし、![設定](assets/configure-icon.svg)をタップして、アダプティブフォームのプロパティを表示します。

1. 「**[!UICONTROL 送信]**」セクションで、「**[!UICONTROL 送信リスト]**」ドロップダウンアクションから「**[!UICONTROL 電子メール]**&#x200B;を送信」を選択します。

   ![送信アクション](assets/submission-actions.png)

1. 「**[!UICONTROL 宛先]**」、「**[!UICONTROL CC]**」、「**[!UICONTROL BCC]**」の各フィールドに、有効な電子メールIDを指定します。

   「**[!UICONTROL 件名]**」と「**[!UICONTROL 電子メールテンプレート]**」の各フィールドに、それぞれ件名と電子メール本文を指定します。

   フィールドに変数プレースホルダーを指定することもできます。この場合、フィールドの値は、フォームがエンドユーザーによって正しく送信されたときに処理されます。詳細については、「[アダプティブフォームのフィールド名を使用した電子メールコンテンツの動的作成](../../forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p)」を参照してください。

   フォームに添付ファイルが含まれ、これらのファイルを電子メールに添付する場合は、「添付ファイルを含める」**[!UICONTROL を選択します。]**

   >[!NOTE]
   >
   >「**[!UICONTROL 電子メールでPDFを送信]**」オプションを選択する場合は、「添付ファイルを含める」オプションを選択する必要があります。

1. ![save](assets/save_icon.svg)をクリックして変更を保存します。

### アダプティブフォームのフィールド名を使用した電子メールコンテンツの動的作成 {#using-adaptive-form-field-names-to-dynamically-create-email-content}

アダプティブフォームのフィールド名はプレースホルダーと呼ばれ、ユーザーがフォームを送信した後にそのフィールドの値によって置き換えられます。

「**[!UICONTROL 電子メール]**&#x200B;を送信」アクションでは、アクションの実行時に処理されるプレースホルダーを使用できます。 これは、ユーザーがフォームを送信したときに電子メールのヘッダー（**[!UICONTROL 宛先]**、**[!UICONTROL CC]**、**[!UICONTROL BCC]**、**[!UICONTROL 件名]**&#x200B;など）が生成されることを意味します。

プレースホルダーを定義するには、送信アクションとして「**[!UICONTROL 電子メールを送信]**」を選択した後、フィールドに`${<field name>}`を指定します。

例えば、フォームに`email_addr`という名前の&#x200B;**[!UICONTROL 電子メールアドレス]**&#x200B;フィールドが含まれている場合、**[!UICONTROL 宛先]**、**[!UICONTROL CC]**&#x200B;または&#x200B;**[!UICONTROL BCC]**&#x200B;フィールドに次の内容を指定できます。

`${email_addr}`

ユーザーがフォームを送信すると、フォームの `email_addr` フィールドに入力された電子メール ID に電子メールが送信されます。

>[!NOTE]
>
>フィールドの&#x200B;**[!UICONTROL 編集]**&#x200B;ダイアログにフィールドの名前があります。

変数プレースホルダーは、**[!UICONTROL 件名]**&#x200B;フィールドと&#x200B;**[!UICONTROL 電子メールテンプレート]**&#x200B;フィールドでも使用できます。

次に例を示します。

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>繰り返し可能パネル内のフィールドは、変数プレースホルダーとして使用することはできません。

