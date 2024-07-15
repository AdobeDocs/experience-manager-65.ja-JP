---
title: シングルサインオンとタイムアウトハンドラー
description: AEM Forms Workspace のセッションのタイムアウト値を設定する方法。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 4f824d80-f3f8-4010-9583-5a9ab1151a7b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 100%

---

# シングルサインオンとタイムアウトハンドラー {#single-sign-on-and-timeout-handlers}

AAEM Forms Workspace は SSO 対応です。ユーザーが Forms Manager、PDF Generator ユーザーインターフェイスなどの AEM Forms アプリケーションにログインして同じブラウザーセッションの AEM Forms Workspace にアクセスすると、ユーザーは AEM Forms Workspace にもログインしたことになります（また、その逆の場合も同じです）。

## AEM Forms Workspace でのサーバータイムアウトの処理 {#handling-server-timeout-in-nbsp-aem-forms-workspace}

ユーザーに対するセッションタイムアウトは、管理コンソールで設定できます。

タイムアウトを設定するには、`https://'[server]:[port]'/adminui` にログインし、**設定／User Management／設定／詳細なシステム属性の設定**&#x200B;に移動して必要な設定を行います。

AEM Forms Workspace で、タイムアウトは次のように処理されます。

* ユーザーのセッション時間は、ユーザーセッションを初期設定する `initialize` コールに応答して得られます。
* ポップアップダイアログが表示され、セッションが期限切れになる 15 秒前に、そのことがユーザーに通知されます。

このポップアップダイアログで、以下のようにします。

* 「OK」をクリックすると、ユーザーセッションが終了します。
* 「キャンセル」をクリックすると、ユーザーセッションが再初期設定されます。

>[!NOTE]
>
>何もしなかった場合は、セッション期限切れの 3 秒前に、ユーザーは AEM Forms Workspace から自動的にログアウトされます。
