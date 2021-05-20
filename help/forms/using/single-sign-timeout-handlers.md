---
title: シングルサインオンとタイムアウトハンドラー
seo-title: シングルサインオンとタイムアウトハンドラー
description: AEM Forms Workspace のセッションのタイムアウト値を設定する方法。
seo-description: AEM Forms Workspace のセッションのタイムアウト値を設定する方法。
uuid: 17583fd5-6453-41d3-bb63-a639983fbea9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 698990a2-dd3f-480f-9d15-d87563860297
exl-id: 4f824d80-f3f8-4010-9583-5a9ab1151a7b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 55%

---

# シングルサインオンとタイムアウトハンドラー {#single-sign-on-and-timeout-handlers}

AEM Forms Workspace は SSO 対応です。ユーザーがForms ManagerやPDF GeneratorなどのAEM Formsアプリケーションにログインし、同じブラウザーセッションでAEM Forms Workspaceにアクセスした場合、ユーザーはAEM Forms Workspaceにログインし、その逆も同様です。

## AEM Forms Workspace でのサーバータイムアウトの処理 {#handling-server-timeout-in-nbsp-aem-forms-workspace}

ユーザーに対するセッションタイムアウトは、 管理コンソールで設定できます。

タイムアウトを設定するには、`https://'[server]:[port]'/adminui`にログインし、**設定/User Management/設定/詳細なシステム属性を設定**&#x200B;に移動して、必要な設定を行います。

AEM Forms Workspaceのタイムアウトは、次のように処理されます。

* ユーザーのセッション時間長は、ユーザーセッションを初期設定する `initialize` コールに応答して得られます。
* ポップアップダイアログが表示され、セッションが期限切れになる 15 秒前に、そのことがユーザーに通知されます。

このポップアップダイアログで、以下のようにします。

* 「OK」をクリックすると、ユーザーセッションが終了します。
* 「キャンセル」をクリックすると、ユーザーセッションが再初期設定されます。

>[!NOTE]
>
>何も実行されなかった場合、ユーザーはセッションの有効期限が切れる3秒前に、AEM Forms Workspaceから自動的にログアウトされます。
