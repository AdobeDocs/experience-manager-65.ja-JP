---
title: エンドポイントの追加、有効化、変更または削除
seo-title: Adding, enabling, modifying, or removing endpoints
description: エンドポイントを追加、有効化、変更、削除する方法について説明します。
seo-description: Learn how to add, enable, modify and remove endpoints.
uuid: c53f225b-3d55-42f6-8982-0cd7dde0c4f5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7d0d4f96-fc72-4e2b-a2cc-5741b0a30f74
exl-id: b7461d5c-95d1-4da2-9d2a-f54c410a87f9
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 10%

---

# エンドポイントの追加、有効化、変更または削除 {#adding-enabling-modifying-or-removing-endpoints}

## エンドポイントをサービスに追加する {#add-an-endpoint-to-a-service}

エンドポイントは、サービスにのみ追加できます。 エンドポイントは単独では存在できません。サービスに関連付ける必要があります。

>[!NOTE]
>
>エンドポイントを追加する際には、一意の名前を使用することをお勧めします。

1. 管理コンソールで、サービス／アプリケーションおよびサービス／サービスの管理をクリックします。
1. サービスの管理ページで、設定するサービスをクリックします。
1. 「エンドポイント」タブのリストで、追加するエンドポイントのタイプを選択し、「追加」をクリックします。
1. エンドポイントのタイプに応じて、追加のエンドポイント設定を指定します。

[監視フォルダーエンドポイントの設定](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)

[メールエンドポイントの設定](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)

[タスクマネージャーエンドポイントの設定](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)

[リモートエンドポイントの設定](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)

1. 「追加」をクリックします。

## エンドポイントの有効化または無効化 {#enable-or-disable-an-endpoint}

デフォルトでは、新しいエンドポイントは自動的に有効になります。 ただし、エンドポイントを無効にした場合、エンドポイントが動作可能になるように、有効にする必要があります。

サービスで問題が発生した場合は、関連するエンドポイントを無効にして、問題のトラブルシューティングを改善します。 また、通常のシステムメンテナンス中や、サービスのアップグレード時に、エンドポイントを無効にすることもできます。

1. 管理コンソールで、サービス/アプリケーションおよびサービス/エンドポイントの管理をクリックします。
1. エンドポイントの管理ページで、有効または無効にするエンドポイントのチェックボックスを選択し、「有効」または「無効」をクリックします。

## エンドポイントの変更 {#modify-an-endpoint}

>[!NOTE]
>
>管理コンソールを使用してエンドポイント設定に加えた変更は、アプリケーションのデザイン時コピーには反映されません。 アプリケーションを再デプロイすると、管理コンソールを使用してエンドポイントに加えた変更は失われます。

1. 管理コンソールで、サービス/アプリケーションおよびサービス/エンドポイントの管理をクリックします。
1. エンドポイントの管理ページで、変更するエンドポイントをクリックします。
1. エンドポイントを更新ページで、エンドポイントの名前、説明、設定を変更します。

   >[!NOTE]
   >
   >名前や説明には &lt; を含めないでください。含めると、Workspace に表示される名前や説明の一部が省略されます。

1. 変更を保存するには、「更新」をクリックします。

このタスクは、サービスの管理ページから、サービスを選択して「エンドポイント」タブをクリックすることで実行することもできます。

## エンドポイントの削除 {#remove-an-endpoint}

1. 管理コンソールで、サービス/アプリケーションおよびサービス/エンドポイントの管理をクリックします。
1. エンドポイントの管理ページで、削除するエンドポイントのチェックボックスを選択し、「削除」をクリックします。 エンドポイントが表示されなくなりました。
