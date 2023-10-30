---
title: ローカル資格情報の管理
description: Trust Store 管理を使用してローカル秘密鍵証明書を管理する方法を説明します。 AEM forms は、標準の PKCS12 形式の RSA 秘密鍵証明書と DSA 秘密鍵証明書をサポートします。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: c5905272-7d09-47e4-8b35-4cc25a148477
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 3%

---

# ローカル資格情報の管理 {#managing-local-credentials}

ローカル秘密鍵証明書は、Trust Store 管理でホストされる秘密鍵資格情報です。 A *ローカル秘密鍵証明書* は、ユーザーの DES 秘密鍵証明書が保存される場所を示します。 Trust Store の管理では、既存の PFX ファイルなどを使用してローカル秘密鍵証明書の読み込みと管理を行い、ローカル秘密鍵証明書の読み込み、編集、削除を行うことができます。

AEM forms は、標準の PKCS12 形式（.pfx および.p12 ファイル）の最大 4096 ビットの RSA および DSA 秘密鍵証明書をサポートします。

任意の数の資格情報を読み込み、書き出しできます。 同じエイリアスを使用して期限切れの秘密鍵証明書を置き換える場合は、秘密鍵証明書を削除し、同じエイリアスで新しい秘密鍵証明書を読み込みます。

Acrobat Reader DC Extensions に関する情報と手順については、 [資格情報をAcrobat Reader DC Extensions で使用するための設定](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions).

## 秘密鍵証明書の読み込み {#import-a-credential}

1. 管理コンソールで、設定/Trust Store の管理/ローカル秘密鍵証明書をクリックします。
1. 「読み込み」をクリックします。「Trust Store の種類」で、次のいずれかのオプションを選択します。

   * **ドキュメント署名証明書：**&#x200B;ドキュメントの電子署名の発行に使用する資格情報です。
   * **Acrobat Reader DC Extensions 資格情報：** Adobe Readerの使用権限を生成するPDFドキュメントで有効にする、Acrobat Reader DC Extensions に固有の電子証明書。
   * **デフォルト：** これが、Acrobat Reader DC Extensions で使用するデフォルトの資格情報であることを示します。

   秘密鍵証明書の取得について詳しくは、 [AEM forms のインストールの準備](https://helpx.adobe.com/pdf/aem-forms/6-3/prepare-install-single-server.pdf).

1. 「エイリアス」ボックスに、秘密鍵証明書の識別子を入力します。 この識別子は、Acrobat Reader DC Extensions と Signature サービスで証明書の表示名として使用されます。 このエイリアスは、AEM forms SDK を使用してプログラムで秘密鍵証明書にアクセスする場合にも使用されます。

   >[!NOTE]
   >
   >エイリアス名は、表示用に自動的に大文字に変換されます。 エイリアス名をプロセスで参照する際、大文字と小文字は区別されません。

1. 「参照」をクリックして秘密鍵証明書を探し、秘密鍵証明書のパスワードを入力して、「OK」をクリックします。

   「ファイル形式が正しくないか、パスワードが正しくないため、秘密鍵証明書を読み込めませんでした」というエラーメッセージが表示される場合は、パスワードが有効であることを確認します。

## 秘密鍵証明書の書き出し {#export-a-credential}

秘密鍵証明書は、PKCS#12 形式で P12 ファイルとして書き出されます。

1. 管理コンソールで、設定/Trust Store の管理/ローカル秘密鍵証明書をクリックします。
1. 書き出す秘密鍵証明書のエイリアス名をクリックし、「書き出し」をクリックします。
1. 「パスワード」ボックスに、パスワードを入力します。 このパスワードは新規で、書き出した秘密鍵証明書の暗号化に使用されます。
1. 「書き出し」をクリックし、指示に従って資格情報を書き出し、「OK」をクリックします。

## 秘密鍵証明書のエイリアスまたは Trust Store の種類の編集 {#edit-a-credential-s-alias-or-trust-store-type}

秘密鍵証明書が読み込まれたら、そのエイリアス名と Trust Store の種類を編集できます。

1. 管理コンソールで、設定/Trust Store の管理/ローカル秘密鍵証明書をクリックします。
1. 編集する秘密鍵証明書のエイリアス名をクリックします。
1. 「秘密鍵証明書を更新」をクリックします。
1. 必要に応じてエイリアス名と Trust Store の種類を編集し、「OK」をクリックします。

## 秘密鍵証明書の削除 {#delete-a-credential}

1. 管理コンソールで、設定/Trust Store の管理/ローカル秘密鍵証明書をクリックします。
1. 削除する秘密鍵証明書のチェックボックスをオンにします。
1. 「削除」をクリックし、「OK」をクリックします。
