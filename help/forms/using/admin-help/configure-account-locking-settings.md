---
title: アカウントロックの設定
seo-title: アカウントロックの設定
description: 「アカウントロックを有効にする」オプションを使用して、連続する認証エラーが指定の回数発生した後で、ユーザーアカウントをロックします。
seo-description: 「アカウントロックを有効にする」オプションを使用して、連続する認証エラーが指定の回数発生した後で、ユーザーアカウントをロックします。
uuid: 5ff3fb76-8b11-4818-9a75-40ed8e121da5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d4409c6b-f4ef-499c-8daa-e93a163ff8ab
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 95%

---


# アカウントロックの設定 {#configure-account-locking-settings}

新しいドメインを追加する場合、アカウントロックを有効にするかどうかを指定します。「アカウントロックを有効にする」オプションを選択すると、連続する認証エラーが指定の回数発生した後で、ユーザーアカウントがロックされます。指定した時間が経過した後、ユーザーは認証をもう一度試行することができます。この機能により、ユーザーが様々な秘密鍵証明書の組み合わせを使用してシステムにアクセスしようとすることを防ぎます。

ドメインの管理ページの設定を使用して、認証エラーの最大数およびアカウントがロックされている時間を指定できます。これらの設定は、アカウントロックが有効になっているすべてのドメインに適用されます。

1. In administration console, click **[!UICONTROL Settings > User Management > Domain Management]**.
1. 「連続する認証エラーの最大回数」ボックスに、アカウントがロックされるまで連続して何回ログインの失敗が許可されるか、その回数を入力します。デフォルト値は 20 です。
1. 「アカウントのロック解除までの時間（分）」ボックスに、ユーザーアカウントがロックされている時間（分）を入力します。指定した時間（分）が経過すると、ユーザーはもう一度ログインを試行できます。デフォルト値は 30 です。
1. 「**[!UICONTROL 保存]**」をクリックします。

