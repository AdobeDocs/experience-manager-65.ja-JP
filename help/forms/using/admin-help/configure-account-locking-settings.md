---
title: アカウントロックの設定
description: 「アカウントロックを有効にする」オプションを使用して、認証エラーが連続して指定の回数発生した後で、ユーザーアカウントをロックします。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: eb8c748d-51d9-4684-97c5-e982ad84ba9f
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '196'
ht-degree: 100%

---

# アカウントロックの設定 {#configure-account-locking-settings}

ドメインを追加する場合、アカウントロックを有効にするかどうかを指定します。「アカウントロックを有効にする」オプションを選択すると、認証エラーが連続して指定の回数発生した後で、ユーザーアカウントがロックされます。指定した時間が経過した後、ユーザーは認証をもう一度試行することができます。この機能により、ユーザーが様々な秘密鍵証明書の組み合わせを使用してシステムにアクセスしようとすることを防ぎます。

ドメインの管理ページの設定を使用して、認証エラーの最大数およびアカウントがロックされている時間を指定できます。これらの設定は、アカウントロックが有効になっているすべてのドメインに適用されます。

1. 管理コンソールで、**[!UICONTROL 設定／User Management／ドメインの管理]**&#x200B;をクリックします。
1. 「連続する認証エラーの最大回数」ボックスに、アカウントがロックされるまで連続して何回ログインの失敗が許可されるか、その回数を入力します。デフォルト値は 20 です。
1. 「アカウントのロック解除までの時間（分）」ボックスに、ユーザーアカウントがロックされている時間（分）を入力します。指定した時間（分）が経過すると、ユーザーはもう一度ログインを試行できます。デフォルト値は 30 です。
1. 「**[!UICONTROL 保存]**」をクリックします。
