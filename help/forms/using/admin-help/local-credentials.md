---
title: ローカル秘密鍵証明書の管理
seo-title: ローカル秘密鍵証明書の管理
description: ローカル秘密鍵証明書を管理する方法について説明します。
seo-description: ローカル秘密鍵証明書を管理する方法について説明します。
uuid: 3c4358e0-aaff-4e94-a6b2-04b463fca260
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 598a9a03-3773-4620-8867-1f754d8ca031
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 98%

---


# ローカル秘密鍵証明書の管理 {#managing-local-credentials}

ローカル秘密鍵証明書は、Trust Store の管理でホストされる秘密鍵証明書です。*ローカル秘密鍵証明書*&#x200B;は、ユーザーの DES 秘密鍵証明書が保存されている場所を特定するものです。Trust Store の管理では、ローカル秘密鍵証明書の読み込み、編集、削除ができるように、例えば既存の PFX ファイルを使用して、ローカル秘密鍵証明書の読み込みと管理を行うことができます。

AEM Forms は、標準の PKCS12 形式（.pfx ファイルおよび .p12 ファイル）の、最大 4,096 ビットの RSA 秘密鍵証明書および DSA 秘密鍵証明書をサポートします。

秘密鍵証明書はいくつでも読み込みと書き出しを行うことができます。同じエイリアスを使用して期限切れの秘密鍵証明書を置き換えるには、秘密鍵証明書を削除してから、同じエイリアスで新しい秘密鍵証明書を読み込みます。

Acrobat Reader DC Extensions に関連する情報および手順については、[証明書を Acrobat Reader DC Extensions で使用するための設定](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions)を参照してください。

## 秘密鍵証明書の読み込み {#import-a-credential}

1. 管理コンソールで、設定／Trust Store の管理／ローカル秘密鍵証明書をクリックします。
1. 「読み込み」をクリックし、「Trust Store の種類」で次のいずれかのオプションを選択します。

   * **ドキュメント署名証明書：**&#x200B;ドキュメントの電子署名の発行に使用する秘密鍵証明書です。
   * **Acrobat Reader DC Extensions 証明書：** Acrobat Reader DC Extensions に固有の電子証明書です。これにより、生成された PDF ドキュメントで Adobe Reader の使用権限をアクティブにすることができます。
   * **デフォルト：** Acrobat Reader DC Extensions で使用するデフォルトの証明書であることを示します。

   証明書の取得について詳しくは、「[AEM Forms のインストールの準備](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)」を参照してください。

1. 「エイリアス」ボックスに、秘密鍵証明書の ID を入力します。この ID は、Acrobat Reader DC Extensions および Signature サービスで証明書の表示名として使用されます。このエイリアスは、AEM Forms SDK を使用してプログラムから秘密鍵証明書にアクセスするときにも使用されます。

   >[!NOTE]
   >
   >エイリアス名は、見やすいように大文字に自動的に変換されます。エイリアス名をプロセスで参照するときは、大文字と小文字は区別されません。

1. 「参照」をクリックして秘密鍵証明書を見つけ、秘密鍵証明書のパスワードを入力して「OK」をクリックします。

   「形式が正しくないか、パスワードが正しくないため、秘密鍵証明書を読み込めませんでした」というエラーメッセージが表示される場合は、パスワードが有効であることを確認してください。

## 秘密鍵証明書の書き出し {#export-a-credential}

秘密鍵証明書は、PKCS#12 形式で P12 ファイルとして書き出されます。

1. 管理コンソールで、設定／Trust Store の管理／ローカル秘密鍵証明書をクリックします。
1. 書き出す秘密鍵証明書のエイリアス名をクリックし、「書き出し」をクリックします。
1. 「パスワード」ボックスにパスワードを入力します。このパスワードは新規で、書き出した秘密鍵証明書の暗号化に使用します。
1. 「書き出し」をクリックし、指示に従って秘密鍵証明書を書き出して、「OK」をクリックします。

## 秘密鍵証明書のエイリアスまたは Trust Store の種類の編集 {#edit-a-credential-s-alias-or-trust-store-type}

秘密鍵証明書が読み込まれたら、エイリアス名および Trust Store の種類を編集できます。

1. 管理コンソールで、設定／Trust Store の管理／ローカル秘密鍵証明書をクリックします。
1. 編集する秘密鍵証明書のエイリアス名をクリックします。
1. 「秘密鍵証明書を更新」をクリックします。
1. 必要に応じて、エイリアス名と Trust Store の種類を編集し、「OK」をクリックします。

## 秘密鍵証明書の削除 {#delete-a-credential}

1. 管理コンソールで、設定／Trust Store の管理／ローカル秘密鍵証明書をクリックします。
1. 削除する秘密鍵証明書のチェックボックスを選択します。
1. 「削除」をクリックし、「OK」をクリックします。

