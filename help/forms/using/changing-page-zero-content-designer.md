---
title: Designer の Page Zero コンテンツの変更
seo-title: Designer の Page Zero コンテンツの変更
description: XFA PDF を Adobe 以外の PDF ビューアで表示するとき、Page Zero に表示されるメッセージを変更する方法をご存知ですか。
seo-description: XFA PDF を Adobe 以外の PDF ビューアで表示するとき、Page Zero に表示されるメッセージを変更する方法をご存知ですか。
uuid: ac23fb21-3f15-48ea-aeeb-4ecc12b771ac
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 56b6a573-8aba-43e7-acb7-c2da45869d95
docset: aem65
translation-type: tm+mt
source-git-commit: 3cbcd23254e16231a199276aa2f9e70d6ff39b34
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 72%

---


# Designer での Page Zero コンテンツの変更 {#changing-page-zero-content-in-designer}

Page Zero content is displayed by default when a non-Adobe PDF viewer, such as the default PDF viewer in [!DNL Chrome] or [!DNL Firefox], cannot read the content of the PDF/XFA form. デフォルトの Page Zero メッセージは、次のとおりです。

![defaultpage0message](assets/defaultpage0message.png)

[!DNL AEM Forms] バージョンのDesignerでは、Page Zeroに表示されるメッセージを変更できます。 Page Zero メッセージを変更するには、次の手順を実行します。

1. Ensure that you have the [!DNL AEM Forms] version of Designer installed. Designer の「バージョン情報」画面で、バージョンを確認することができます。

1. Page Zero コンテンツを変更するフォームを開きます。

1. Click **[!UICONTROL File]** > **[!UICONTROL Form Properties]**.

1. In the [!UICONTROL Form Properties] dialog, click ![plus](assets/plus.png) (Plus icon) to add a custom property.

1. プロパティの名前として **_pagezerocontent** を指定します。
1. 新しい Page Zero メッセージを、リッチテキスト形式で値として追加します。次に例を示します。


   `<body xmlns="https://www.w3.org/1999/xhtml" xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/"><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">You are seeing this message maybe because you are using a non Adobe PDF Viewer or an Old version of Adobe Reader. You can upgrade to the latest version of Adobe Reader for Windows, Mac, or Linux by visiting <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/reader_download.</p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">For more assistance with Adobe Reader visit <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/acrreader.</p></body>`

1. フォームを PDF として保存します。

1. PDF フォームをブラウザーで表示して、メッセージが更新されたことを確認します。上述の例は、次のように表示されます。

   ![changedmessage](assets/changedmessage.png)

>[!NOTE]
>
>フォームを再度開いたときに、作成したカスタムプロパティがフォームプロパティダイアログに正しく表示されない場合があります。その場合でも、動作には問題ありません。フォームには、更新後の Page Zero メッセージが表示されます。
