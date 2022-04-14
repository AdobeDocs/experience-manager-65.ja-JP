---
title: アカウントロックの設定
seo-title: Configure account-locking settings
description: 「アカウントロックを有効にする」オプションを使用して、連続する認証エラーが指定の回数発生した後で、ユーザーアカウントをロックします。
seo-description: Use the Enable Account Locking option to lock user accounts after a specified number of consecutive authentication failures.
uuid: 5ff3fb76-8b11-4818-9a75-40ed8e121da5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d4409c6b-f4ef-499c-8daa-e93a163ff8ab
exl-id: eb8c748d-51d9-4684-97c5-e982ad84ba9f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '194'
ht-degree: 100%

---

# アカウントロックの設定 {#configure-account-locking-settings}

新しいドメインを追加する場合、アカウントロックを有効にするかどうかを指定します。「アカウントロックを有効にする」オプションを選択すると、連続する認証エラーが指定の回数発生した後で、ユーザーアカウントがロックされます。指定した時間が経過した後、ユーザーは認証をもう一度試行することができます。この機能により、ユーザーが様々な秘密鍵証明書の組み合わせを使用してシステムにアクセスしようとすることを防ぎます。

ドメインの管理ページの設定を使用して、認証エラーの最大数およびアカウントがロックされている時間を指定できます。これらの設定は、アカウントロックが有効になっているすべてのドメインに適用されます。

1. 管理コンソールで、**[!UICONTROL 設定／User Management／ドメインの管理]**&#x200B;をクリックします。
1. 「連続する認証エラーの最大回数」ボックスに、アカウントがロックされるまで連続して何回ログインの失敗が許可されるか、その回数を入力します。デフォルト値は 20 です。
1. 「アカウントのロック解除までの時間（分）」ボックスに、ユーザーアカウントがロックされている時間（分）を入力します。指定した時間（分）が経過すると、ユーザーはもう一度ログインを試行できます。デフォルト値は 30 です。
1. 「**[!UICONTROL 保存]**」をクリックします。
