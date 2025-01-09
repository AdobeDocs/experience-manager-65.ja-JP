---
title: 証明書の管理
description: 証明書の取り込みおよび書き出し方法とその信頼設定を編集する方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1fe0e7b4-6109-4f7a-8858-8237a1c5c93b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '646'
ht-degree: 100%

---

# 証明書の管理 {#managing-certificates}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

Trust Store 管理を使用すると、電子署名の検証および証明書認証のために、サーバー上で信頼する証明書の読み込み、編集、削除ができます。証明書はいくつでも読み込みと書き出しを行うことができます。証明書が読み込まれたら、信頼設定および Trust Store のタイプを編集できます。Trust Store の種類を組み合わせる場合は、次のオプションを考慮してください。

* **Trust for Certificate Authentication with CA：** CRL の検証では、「ID で信頼」も選択します。
* **Trust for Certificate Authentication with ICA：**「ID で信頼」だけを選択します。ICA は証明書認証では信頼しないでください。ICA を証明書認証で信頼する場合、ICA はパス構築のための CA になります。ICA が証明書認証と ID の両方で信頼された場合、ICA が CA となるので、CA ベンダー証明書は無視されます。
* **Trust for OCSP Server with HTTPs：** OCSP 応答側サーバーが HTTPS の場所に存在する場合は、「SSL 接続で信頼」も選択する必要があります。OCSP 応答側で CRL の検証を必要とする場合は、必ず「ID で信頼」も選択します。
* **Adobe Root：**「SSL Connections」または「OCSP Server」の Trust Store の種類は選択しないでください。「Adobe Root」は「SSL Connections」および「OCSP Server」では信頼されません。Adobe では OCSP および SSL の証明書は発行されません。「Adobe Root」はエイリアス名 =&quot;ADOBEROOT&quot; によって暗黙的に信頼されます。

サポートされるのは、X509v3 証明書のみです。この証明書タイプは、DER でエンコードされたバイナリファイル（.cer ファイル）または同じ DER でエンコードされた証明書の Base64 でエンコードされたバージョンを含むテキストファイル（Privacy Enhanced Mail（PEM）形式の X509 証明書など）で提供されます。

署名の検証を完了するために必要となる証明書は、同じストア（HSM またはデータベース）にある必要があります。

Trust Manager API を使用して証明書の読み込みおよび削除を行うこともできます。詳しくは、[AEM Forms によるプログラミング](https://www.adobe.com/go/learn_aemforms_programming_63_jp)の「Trust Manager API を使用した証明書の読み込み」および「Trust Manager API を使用した証明書の削除」を参照してください。

## 証明書の読み込み {#import-a-certificate}

1. 管理コンソールで、**[!UICONTROL 設定／Trust Store の管理／証明書]**&#x200B;をクリックします。
1. 「インポート」をクリックし、「Trust Store の種類」で次のいずれかのオプションを選択します。

   * **SSL 接続で信頼：** SSL 経由で外部システムに接続するために AEM Forms で証明書を使用できることを指定します。
   * **署名の認証で信頼：**&#x200B;作成者のデジタル署名の認証のために、ドキュメントの署名処理で証明書を信頼することを指定します。
   * **署名で信頼：**&#x200B;作成者以外のデジタル署名について、ドキュメントの署名処理で証明書を信頼することを指定します。
   * **証明書認証で信頼：**&#x200B;証明書またはスマートカードによるユーザー認証を行うために、AEM Forms で証明書を使用することを指定します。
   * **OCSP サーバーで信頼：**&#x200B;外部の OCSP レスポンダーに接続するために AEM Forms で証明書を使用できることを指定します。
   * **ID で信頼：**&#x200B;上記の種類以外の情報を信頼するために証明書を使用できることを指定します。

   >[!NOTE]
   >
   >Trust Store ではアドビのルート証明書の証明書認証、署名、署名の認証および ID が暗黙的に信頼されます。

1. 「エイリアス」ボックスに、この証明書の ID を入力します。
1. 「**[!UICONTROL 参照]**」をクリックして証明書を探し、「**[!UICONTROL OK]**」をクリックします。

## 証明書のエクスポート {#export-a-certificate}

1. 管理コンソールで、**[!UICONTROL 設定／Trust Store の管理／証明書]**&#x200B;をクリックします。
1. エクスポートする証明書のエイリアス名をクリックします。**[!UICONTROL 証明書の詳細]**&#x200B;ページが表示されます。
1. 「**[!UICONTROL エクスポート]**」をクリックし、指示に従って証明書をエクスポートして、「**[!UICONTROL OK]**」をクリックします。

## 証明書の信頼設定と Trust Store の種類の編集 {#edit-a-certificate-s-trust-settings-and-trust-store-type}

1. 管理コンソールで、**[!UICONTROL 設定／Trust Store の管理／証明書]**&#x200B;をクリックします。
1. 編集する証明書のエイリアス名をクリックします。
1. 「**[!UICONTROL 証明書を更新]**」をクリックします。
1. 証明書のエイリアス名を変更するには、「エイリアス」ボックスに新しい名前を入力します。
1. 証明書の Trust Store の種類を更新するには、適切な Trust Store の種類を選択します。
1. ポリシーに関する制限を更新するには、「証明書のポリシー」ボックスにポリシー情報を入力し、「**[!UICONTROL OK]**」をクリックします。

## 証明書の削除 {#delete-a-certificate}

1. 管理コンソールで、**[!UICONTROL 設定／Trust Store の管理／証明書]**&#x200B;をクリックします。
1. 削除する証明書のチェックボックスを選択して「**[!UICONTROL 削除]**」をクリックし、「**[!UICONTROL OK]**」をクリックします。
