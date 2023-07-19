---
title: シングルサインオンとタイムアウトハンドラー
seo-title: Single Sign On and timeout handlers
description: AEM Forms Workspace のセッションタイムアウト値の設定方法。
seo-description: How-to set the session timeout value for AEM Forms workspace.
uuid: 17583fd5-6453-41d3-bb63-a639983fbea9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 698990a2-dd3f-480f-9d15-d87563860297
exl-id: 4f824d80-f3f8-4010-9583-5a9ab1151a7b
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 40%

---

# シングルサインオンとタイムアウトハンドラー {#single-sign-on-and-timeout-handlers}

AEM Forms workspace は SSO 有効です。 ユーザーがForms Manager やPDF GeneratorユーザーインターフェイスなどのAEM Formsアプリケーションにログインし、同じブラウザーセッションでAEM Forms Workspace にアクセスした場合、そのユーザーはAEM Forms Workspace にログインし、逆にログインします。

## AEM Forms Workspace でのサーバータイムアウトの処理 {#handling-server-timeout-in-nbsp-aem-forms-workspace}

ユーザーのセッションタイムアウトは、管理コンソールで設定できます。

タイムアウトを設定するには、`https://'[server]:[port]'/adminui` にログインし、**設定／User Management／設定／詳細なシステム属性の設定**&#x200B;に移動して必要な設定を行います。

AEM Forms Workspace で、タイムアウトは次のように処理されます。

* ユーザーのセッション時間は、ユーザーセッションを初期設定する `initialize` コールに応答して得られます。
* ポップアップダイアログが表示され、セッションの有効期限が 15 秒前にセッションの有効期限が切れようとしていることがユーザーに通知されます。

このポップアップダイアログで、次の操作を実行します。

* 「 OK 」をクリックして、ユーザーセッションを終了します。
* 「キャンセル」をクリックして、ユーザーセッションを再初期化します。

>[!NOTE]
>
>何もしなかった場合は、セッション期限切れの 3 秒前に、ユーザーは AEM Forms Workspace から自動的にログアウトされます。
