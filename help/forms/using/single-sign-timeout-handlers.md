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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# シングルサインオンとタイムアウトハンドラー {#single-sign-on-and-timeout-handlers}

AEM Forms Workspace は SSO 対応です。ユーザーがForms ManagerやPDF GeneratorユーザーインターフェイスなどのAEM Formsアプリケーションにログインし、同じブラウザーセッションでAEM Forms Workspaceにアクセスした場合、そのユーザーはAEM Forms Workspaceにログインします。逆の場合も同様です。

## AEM Forms Workspace でのサーバータイムアウトの処理 {#handling-server-timeout-in-nbsp-aem-forms-workspace}

ユーザーに対するセッションタイムアウトは、 管理コンソールで設定できます。

To set the timeout, login to `https://[server]:[port]/adminui`, navigate to **Settings > User Management > Configuration > Configure Advanced System Attributes**, and make the desired settings.

AEM Forms Workspaceでは、タイムアウトは次のように処理されます。

* ユーザーのセッション時間長は、ユーザーセッションを初期設定する `initialize` コールに応答して得られます。
* ポップアップダイアログが表示され、セッションが期限切れになる 15 秒前に、そのことがユーザーに通知されます。

このポップアップダイアログで、以下のようにします。

* 「OK」をクリックすると、ユーザーセッションが終了します。
* 「キャンセル」をクリックすると、ユーザーセッションが再初期設定されます。

>[!NOTE]
>
>何も行われない場合、ユーザーはセッション有効期限が切れる3秒前にAEM Forms Workspaceから自動的にログアウトされます。

**[サポートへのお問い合わせ](https://www.adobe.com/account/sign-in.supportportal.html)**
