---
title: 資格情報の使用に関する情報の確認
description: 秘密鍵証明書の使用情報を確認する方法を説明します。 秘密鍵証明書の使用に関する情報は、Acrobat Reader拡張機能を通じてアクセスできます。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: a8e16cf8-f3c8-48ce-87da-2f0de0b10a6e
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 9%

---

# 資格情報の使用に関する情報の確認 {#review-credential-use-information}

秘密鍵証明書には、Acrobat Reader DC Extensions エンドユーザー Web アプリケーションを通じてアクセスできる、使用目的を説明する情報が含まれています。 この情報を使用して、インストールされる秘密鍵証明書の種類（評価または実稼動）と有効期限を判断できます。

1. Web ブラウザーを開き、次の URL を入力します。

   http://localhost:[port]/ReaderExtensions （*port* は、アプリケーションサーバーのポート番号です）

1. デフォルトのユーザー名とパスワードを使用してログインします。

   ユーザー名： administrator

   パスワード：password

   >[!NOTE]
   >
   >デフォルトのユーザー名とパスワードを使用してログインするには、管理者またはスーパーユーザーの権限が必要です。 他のユーザーがAcrobat Reader DC拡張機能にアクセスできるようにするには、ユーザー管理でユーザーアカウントを作成し、そのユーザーにAcrobat Reader DC拡張機能 Web アプリケーションの役割を付与します。

1. 「秘密鍵証明書を選択」リストから秘密鍵証明書のエイリアスを選択し、「有効期限」と「使用目的の通知」に記載されている情報を確認します。

>[!NOTE]
>
>秘密鍵証明書の有効期限は、管理コンソールの設定/Trust Store の管理/ローカル秘密鍵証明書ページの「有効期限」でも確認できます。
