---
title: ローカル資格情報の管理
description: Trust Store 管理を使用してローカル秘密鍵証明書を管理する方法を説明します。 AEM Forms は、標準の PKCS12 形式の RSA および DSA 資格情報をサポートします。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: c5905272-7d09-47e4-8b35-4cc25a148477
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 50158d81-1c06-57f7-8bd7-e8ff76a93f85
    internal-label: Document Security
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 98%
---
# ローカル資格情報の管理 {#managing-local-credentials}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

ローカル秘密鍵証明書は、Trust Store 管理でホストされる秘密鍵証明書です。 *ローカル秘密鍵証明書*&#x200B;は、ユーザーの DES 秘密鍵証明書が保存される場所を特定するものです。 Trust Store 管理を使用すると、既存の PFX ファイルなどを使用してローカル秘密鍵証明書の読み込みと管理を行い、ローカル秘密鍵証明書の読み込み、編集および削除を行うことができます。

AEM Forms は、標準の PKCS12 形式（.pfx および .p12 ファイル）の最大 4096 ビットの RSA および DSA 資格情報をサポートします。

任意の数の資格情報を読み込みおよび書き出しできます。 同じエイリアスを使用して期限切れの資格情報を置き換える場合は、資格情報を削除してから、同じエイリアスで新しい資格情報を読み込みます。

Acrobat Reader DC Extensions に関する情報と手順について詳しくは、[証明書を Acrobat Reader DC Extensions で使用するための設定](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions)を参照してください。

## 秘密鍵証明書を読み込み {#import-a-credential}

1. 管理コンソールで、設定／Trust Store の管理／ローカル資格情報をクリックします。
1. 「インポート」をクリックします。 「Trust Store Type」で、次のいずれかのオプションを選択します。

   * **ドキュメント署名証明書：**&#x200B;ドキュメントの電子署名の発行に使用する資格情報です。
   * **Acrobat Reader DC Extensions 証明書：** Acrobat Reader DC Extensions に固有の電子証明書です。これにより、生成された PDF ドキュメントで Adobe Reader の使用権限をアクティブにすることができます。
   * **デフォルト：** Acrobat Reader DC Extensions で使用するデフォルトの証明書であることを示します。

   証明書の取得について詳しくは、[AEM Forms のインストールの準備](https://helpx.adobe.com/jp/pdf/aem-forms/6-3/prepare-install-single-server.pdf)を参照してください。

1. 「エイリアス」ボックスに、資格情報の識別子を入力します。 この ID は、Acrobat Reader DC Extensions および Signature サービスで証明書の表示名として使用されます。 このエイリアスは、AEM Forms SDK を使用してプログラムから証明書にアクセスする場合にも使用されます。

   >[!NOTE]
   >
   >エイリアス名は、表示用に自動的に大文字に変換されます。 エイリアス名をプロセスで参照する際、大文字と小文字は区別されません。

1. 「参照」をクリックして資格情報を探し、資格情報のパスワードを入力して「OK」をクリックします。

   「ファイル形式が正しくないか、パスワードが正しくないため、証明書を読み込めませんでした」というエラーメッセージが表示される場合は、パスワードが有効であることを確認してください。

## 秘密鍵証明書を書き出し {#export-a-credential}

資格情報は、PKCS#12 形式で P12 ファイルとして書き出されます。

1. 管理コンソールで、設定／Trust Store の管理／ローカル資格情報をクリックします。
1. 書き出す資格情報のエイリアス名をクリックし、「書き出し」をクリックします。
1. 「パスワード」ボックスに、パスワードを入力します。 このパスワードは新規に入力し、書き出した秘密鍵証明書の暗号化に使用します。
1. 「書き出し」をクリックし、指示に従って秘密鍵証明書を書き出し、「OK」をクリックします。

## 資格情報のエイリアスまたは Trust Store のタイプの編集 {#edit-a-credential-s-alias-or-trust-store-type}

資格情報が読み込まれたら、そのエイリアス名と Trust Store のタイプを編集できます。

1. 管理コンソールで、設定／Trust Store の管理／ローカル資格情報をクリックします。
1. 編集する資格情報のエイリアス名をクリックします。
1. 「秘密鍵証明書を更新」をクリックします。
1. 必要に応じてエイリアス名と Trust Store のタイプを編集し、「OK」をクリックします。

## 秘密鍵証明書を削除 {#delete-a-credential}

1. 管理コンソールで、設定／Trust Store の管理／ローカル資格情報をクリックします。
1. 削除する資格情報のチェックボックスをオンにします。
1. 「削除」をクリックして、「OK」をクリックします。
