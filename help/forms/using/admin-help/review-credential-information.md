---
title: 秘密鍵証明書の使用に関する情報の確認
seo-title: Review credential use information
description: 秘密鍵証明書の使用に関する情報の確認方法について説明します。
seo-description: Learn how to review credential use information.
uuid: 02af75f9-c235-470d-a98b-a2102aa31381
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cdf61cff-768b-49f7-9926-400bc96b0708
exl-id: a8e16cf8-f3c8-48ce-87da-2f0de0b10a6e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '180'
ht-degree: 100%

---

# 秘密鍵証明書の使用に関する情報の確認 {#review-credential-use-information}

証明書には、使用目的を示す情報が格納されており、Acrobat Reader DC Extensions エンドユーザー Web アプリケーションからアクセスできます。この情報から、インストールされる証明書の種類（評価用または実稼働環境用）と有効期限日を判別できます。

1. Web ブラウザーを開き、次の URL を入力します。

   http://localhost:[port]/ReaderExtensions （*port* は、アプリケーションサーバーのポート番号です）

1. 次のデフォルトのユーザー名とパスワードを使用してログインします。

   ユーザー名：administrator

   パスワード：password

   >[!NOTE]
   >
   >デフォルトのユーザー名とパスワードを使用してログインするには、管理者またはスーパーユーザーの権限が必要です。他のユーザーが Acrobat Reader DC Extensions にアクセスできるようにするには、User Management でユーザーアカウントを作成し、そのユーザーに Acrobat Reader DC Extensions Web アプリケーションロールを付与します。

1. 「秘密鍵証明書を選択」リストで証明書のエイリアスを選択し、「有効期限」および「使用目的の通知」に示されている情報を確認します。

>[!NOTE]
>
>証明書の有効期限は、設定／Trust Store の管理を選択し、管理コンソールのローカル秘密鍵証明書ページの「有効期限」で確認することもできます。
