---
title: コミュニティコンソール
seo-title: コミュニティコンソール
description: コミュニティコンソールについて説明しています
seo-description: コミュニティコンソールについて説明しています
uuid: 1c5b2600-9059-4b44-9741-f1b627423d3c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 5fa9ee8b-5893-4ae9-a986-bfdbb00f355f
translation-type: tm+mt
source-git-commit: d6c8bbb9aa763a2eb6660b6b6755aba75241e394

---


# コミュニティコンソール {#communities-consoles}

AEM Communitiesコンソールは、グローバルナビゲーションパネルから作成者環境で使用でき、次のような管理タスクにアクセスできます。

* [コミュニティサイトの作成](sites-console.md)
* Adding [groups](groups.md) nested within the site
* Managing [community site templates](sites.md)
* Managing [community members](members.md)
* [ユーザー生成](moderate-ugc.md) (UGC)コンテンツのモデレート
* Create [custom badges](badges.md)
* Configuring the [default storage for UGC](srp-config.md)

When [UGC storage](working-with-srp.md) is configured to be a common store shared by author and publish environments, the [moderation console](moderation.md), available from both author and publish environments, operates on a solitary instance of UGC.

In the author environment, after signing in with administrator privileges, the `Communities` consoles are available from the navigation and tools consoles.

>[!NOTE]
>
>In the publish environment, a [community site](sites-console.md) will display an `Administration` menu item when the signed in member has appropriate privileges.

## グローバルナビゲーションパネル {#global-navigation-panel}

![chlimage_1-91](assets/chlimage_1-91.png)

`Adobe Experience Manager` のアイコンを選択し、グローバルナビゲーションパネルを開いて次の 2 つのアイコンにアクセスします。

* [ナビゲーションコンソール](#navigation-console)
* [ツールコンソール](tools.md)

## ナビゲーションコンソール {#navigation-console}

To access the various Communities consoles, from global navigation select **navigation, Communities**.

![chlimage_1-92](assets/chlimage_1-92.png)

* [Sites](sites-console.md)

   The Sites console is accessible in the author environment for the purpose of creating and managing community sites and its [groups](groups.md).

* [モデレート](moderation.md)

   モデレートコンソールは、UGCの一括モデレートおよび作成者環境用です。 A similar bulk moderation console is accessible in the publish environment to community members assigned the role of [community moderator](users.md#publishenvironmentusersandgroups) for one or more community sites.

* [メンバー、グループ](members.md)

   [メンバ]コンソールと[グループ]コンソールは、コミュニティメンバと、発行環境に存在するメンバグループを作成者環境から管理するためのものです。

* [レポート](reports.md)

   The Reports console is where reports on assignments, page views, and posted content (UGC) may be generated when a community site has [enabled Adobe Analytics](sites-console.md#analytics). コンソールは、作成者環境でのみ使用できます。

* [リソース](resources.md)

   The Resources console is where [enablement managers](enablement.md#communitymanagers) create, manage and assign resources to members of an [enablement community site](overview.md#enablement-community). コンソールは、作成者環境でのみ使用できます。

## ツールコンソール {#tools-console}

To access [Communities Tools](tools.md) (formerly the administration console), from global navigation: **[!UICONTROL Tools > Communities]**
