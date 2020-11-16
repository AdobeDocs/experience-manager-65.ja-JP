---
title: 証明書の管理
seo-title: 証明書の管理
description: 証明書の取り込みおよび書き出し方法とその信頼設定を編集する方法について説明します。
seo-description: 証明書の取り込みおよび書き出し方法とその信頼設定を編集する方法について説明します。
uuid: 46b1dbe5-517c-4294-bb52-cc6700a768e8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9fd531c0-5206-4be0-a450-13e0dc806068
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 83%

---


# 証明書の管理 {#managing-certificates}

Trust Store の管理では、電子署名の検証および証明書認証のために、サーバーで信頼される証明書の読み込み、編集および削除を行うことができます。証明書はいくつでも読み込みと書き出しを行うことができます。証明書が読み込まれたら、信頼設定および Trust Store の種類を編集できます。Trust Store の種類を組み合わせる場合は、次のオプションを考慮してください。

* **Trust for Certificate Authentication with CA：** CRL の検証では、「ID で信頼」も選択します。
* **Trust for Certificate Authentication with ICA：**「ID で信頼」だけを選択します。ICA は証明書認証では信頼しないでください。ICA を証明書認証で信頼する場合、ICA はパス構築のための CA になります。ICA が証明書認証と ID の両方で信頼された場合、ICA が CA となるので、CA ベンダー証明書は無視されます。
* **Trust for OCSP Server with HTTPs：** OCSP 応答側サーバーが HTTPS の場所に存在する場合は、「SSL 接続で信頼」も選択する必要があります。OCSP 応答側で CRL の検証を必要とする場合は、必ず「ID で信頼」も選択します。
* **Adobe Root：**「SSL Connections」または「OCSP Server」の Trust Store の種類は選択しないでください。「Adobe Root」は「SSL Connections」および「OCSP Server」では信頼されません。Adobe では OCSP および SSL の証明書は発行されません。「Adobe Root」はエイリアス名 =&quot;ADOBEROOT&quot; によって暗黙的に信頼されます。

サポートされるのは、X509v3 証明書のみです。この証明書タイプは、DER でエンコードされたバイナリファイル（.cer ファイル）または同じ DER でエンコードされた証明書の Base64 でエンコードされたバージョンを含むテキストファイル（Privacy Enhanced Mail（PEM）形式の X509 証明書など）で提供されます。

署名の検証を完了するために必要となる証明書は、同じストア（HSM またはデータベース）にある必要があります。

Trust Manager API を使用して証明書の読み込みおよび削除を行うこともできます。詳しくは、「[AEM Forms によるプログラミング](https://www.adobe.com/go/learn_aemforms_programming_63)」の「Trust Manager API を使用した証明書の読み込み」および「Trust Manager API を使用した証明書の削除」を参照してください。

## 証明書の読み込み {#import-a-certificate}

1. In administration console, click **[!UICONTROL Settings > Trust Store Management > Certificates]**.
1. 「読み込み」をクリックし、「Trust Store の種類」で次のいずれかのオプションを選択します。

   * **SSL 接続で信頼：** SSL 経由で外部システムに接続するために AEM Forms で証明書を使用できることを指定します。
   * **署名の認証で信頼：**&#x200B;作成者の電子署名の認証のために、ドキュメントの署名処理で証明書を信頼することを指定します。
   * **署名で信頼：**&#x200B;作成者以外の電子署名について、ドキュメントの署名処理で証明書を信頼することを指定します。
   * **証明書認証で信頼：**&#x200B;証明書またはスマートカードによるユーザー認証を行うために、AEM Forms で証明書を使用することを指定します。
   * **OCSP サーバーで信頼：**&#x200B;外部の OCSP レスポンダーに接続するために AEM Forms で証明書を使用できることを指定します。
   * **ID で信頼：**&#x200B;上記の種類以外の情報を信頼するために証明書を使用できることを指定します。

   >[!NOTE]
   >
   >Trust Store ではアドビのルート証明書の証明書認証、署名、署名の認証および ID が暗黙的に信頼されます。

1. 「エイリアス」ボックスに、この証明書の ID を入力します。
1. Click **[!UICONTROL Browse]** to locate the certificate and then click **[!UICONTROL OK]**.

## 証明書の書き出し {#export-a-certificate}

1. In administration console, click **[!UICONTROL Settings > Trust Store Management > Certificates]**.
1. 書き出す証明書のエイリアス名をクリックします。The **[!UICONTROL Certificate Details]** page is displayed.
1. Click **[!UICONTROL Export]**, follow the directions to export the certificate, and then click **[!UICONTROL OK]**.

## 証明書の信頼設定と Trust Store の種類の編集 {#edit-a-certificate-s-trust-settings-and-trust-store-type}

1. In administration console, click **[!UICONTROL Settings > Trust Store Management > Certificates]**.
1. 編集する証明書のエイリアス名をクリックします。
1. Click **[!UICONTROL Update Certificate]**.
1. 証明書のエイリアス名を変更するには、「エイリアス」ボックスに新しい名前を入力します。
1. 証明書の Trust Store の種類を更新するには、適切な Trust Store の種類を選択します。
1. To update the policy restrictions, in the Certificate Policies box, type the policy information, and then click **[!UICONTROL OK]**.

## 証明書の削除 {#delete-a-certificate}

1. In administration console, click **[!UICONTROL Settings > Trust Store Management > Certificates]**.
1. Select the check boxes for the certificates to delete, click **[!UICONTROL Delete]**, and then click **[!UICONTROL OK]**.

