---
title: 共有キューの設定
seo-title: Configuring Shared Queues
description: 共有キューでは、ユーザーキューを効率的に設定および管理できます。共有キューの設定方法について説明します。
seo-description: Shared Queues allow you to configure and manage user queues effectively. Learn how to configure shared queues.
uuid: 69ab611d-334b-40a5-bd2d-533d4cb25eda
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fc403a60-b635-4334-9bf8-2f3d2036b2f3
exl-id: 5f4467c1-0f3f-4dc6-9bd5-98259f327295
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 100%

---

# 共有キューの設定{#configuring-shared-queues}

共有キューでは、ユーザーキューを効率的に設定および管理できます。ユーザーキューは 1 人のユーザーに割り当てられたすべてのタスクです。詳しくは、[タスクリスト](https://help.adobe.com/ja_JP/livecycle/11.0/WorkspaceHelp/WS92d06802c76abadb-2b6ab502126beb6ba2f-7ffc.2.html)を参照してください。組織のニーズに従って、ユーザーキューを割り当て、割り当て解除、再割り当てすることができます。共有キューは次の 2 つの方法で管理できます。

**ユーザーへのアクセスを管理**

このオプションを使用すると、選択したユーザーキューへのアクセスを管理できます。

**ユーザーによるアクセスを管理**

このオプションを使用すると、選択したユーザーに割り当てられている共有キューを管理できます。

## 選択したユーザーキューへのアクセスの管理 {#managing-access-to-a-selected-user-queue}

ユーザーへのアクセスを管理機能により、選択したユーザーキューへのアクセスを管理できます。選択したユーザーキューを組織内の他のユーザーに与えたり取り消したりできます。例えば、Kara Bowman は社内にいません。ユーザーへのアクセスを管理機能を使用すると、Kara Bowman のキューを Akira Tanama および John Jacobs と共有してジョブを完了できます。後で Kara Bowman が社内に戻ったときに、Kara Bowman のキューへのアクセスを Akira Tanaka および John Jacobs から取り消すことができます。

ひとたび共有されると、これらのタスクは、ワークスペースを使用して、このキューへのアクセスを持つユーザーによって完了できます。

>[!NOTE]
>
>AEM Forms のリリースでは Flex Workspace は廃止されています。

### 選択したユーザーキューへのアクセスの設定 {#configuring-access-to-a-selected-user-queue}

1. 管理者アカウントを使用して管理コンソールにログインします。
1. **サービス**／**forms ワークフロー**／**共有キュー**&#x200B;を選択します。

1. 「ユーザーへのアクセスを管理」タブで、共有するキューのユーザーを探して選択します。いつでも右下のウィンドウには、選択したユーザーキューへのアクセスを持つユーザーのリストが表示されます。
1. 左下のウィンドウで、ユーザーを検索し選択します。「共有」をクリックします。
1. 「保存」をクリックして完了します。

### 選択したユーザーキューへのアクセスの取り消し {#revoking-access-to-a-selected-user-queue}

1. 管理者アカウントを使用して管理コンソールにログインします。
1. **サービス**／**forms ワークフロー**／**共有キュー**&#x200B;を選択します。

1. 「ユーザーへのアクセスを管理」タブで、管理するキューのユーザーを探して選択します。
1. 右下のウィンドウには、選択したユーザーキューへのアクセスを持つユーザーのリストが表示されます。ユーザーを選択し、「失効」をクリックします。
1. 「保存」をクリックして完了します。

## ユーザーに割り当てたキューの管理 {#managing-queues-assigned-to-a-user}

ユーザーによるアクセスを管理機能では、選択したユーザーに割り当てられているキューを管理できます。選択したユーザーに対して、ユーザーキューへのアクセスを個別に与えたり取り消したりできます。例えば、Akira Tanaka と John Jacobs のユーザーキューを Kara Bowman に割り当てることができます。ユーザーによるアクセスを管理機能を使用して、Kara Bowman を検索し、Akira Tanaka および John Jacobs に割り当てられているタスクへのアクセスを与えることができます。後で、Kara Bowman に与えられたこれらのユーザーキューへのアクセスを取り消すことができます。

割り当てられたこれらのタスクは、ユーザーがワークスペースを使用して完了できます。

>[!NOTE]
>
>AEM Forms のリリースでは Flex Workspace は廃止されています。

### 選択したユーザーキューへのアクセスの付与 {#granting-access-to-a-selected-user-queue}

1. 管理者アカウントを使用して管理コンソールにログインします。
1. **サービス**／**forms ワークフロー**／**共有キュー**&#x200B;を選択します。

1. 「ユーザーへのアクセスを管理」タブで、共有するキューのユーザーを探して選択します。いつでも右下のウィンドウには、選択したユーザーキューへのアクセスを持つユーザーのリストが表示されます。
1. 左下ウィンドウで、選択したユーザーと共有するユーザーキューを検索し選択します。「共有」をクリックします。
1. 「保存」をクリックして完了します。

### 選択したユーザーキューへのアクセスの取り消し {#revoking_access_to_a_selected_user_queue-1}

1. 管理者アカウントを使用して管理コンソールにログインします。
1. **サービス**／**forms ワークフロー**／**共有キュー**&#x200B;を選択します。

1. 「ユーザーによるアクセスを管理」タブで、管理するキューのユーザーを探して選択します。
1. 右下のウィンドウには、選択したユーザーに割り当てられているユーザーキューのリストが表示されます。ユーザーキューを選択し、「失効」をクリックします。
1. 「保存」をクリックして完了します。
