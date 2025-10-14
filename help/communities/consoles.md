---
title: コミュニティコンソール
description: グローバルナビゲーションパネルから、オーサー環境で使用できるAdobe Experience Manager コミュニティコンソールについて説明します。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 36f2e3d2-46c7-48a8-a1e9-213f581bd9f3
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 2%

---

# コミュニティコンソール {#communities-consoles}

AEM Communitiesのコンソールは、オーサー環境でグローバルナビゲーションパネルから使用でき、次のような管理タスクにアクセスできます。

* [コミュニティサイトの作成](sites-console.md)
* サイト内にネストされた [&#x200B; グループ &#x200B;](groups.md) の追加
* 管理 [&#x200B; コミュニティサイトテンプレート &#x200B;](sites.md)
* [&#x200B; コミュニティメンバー &#x200B;](members.md) の管理
* [&#x200B; モデレート &#x200B;](moderate-ugc.md) ユーザー作成コンテンツ（UGC）
* 作成 [&#x200B; カスタムバッジ &#x200B;](badges.md)
* [UGC のデフォルトストレージ &#x200B;](srp-config.md) の設定

[UGC ストレージ &#x200B;](working-with-srp.md) が、オーサー環境とPublish環境で共有される共通ストアとして設定されている場合、オーサー環境とPublish環境の両方から使用できる [&#x200B; モデレートコンソール &#x200B;](moderation.md) は、UGC の 1 つのインスタンスで動作します。

オーサー環境では、管理者権限でログインした後、ナビゲーションコンソールとツールコンソールから `Communities` コンソールを使用できます。

>[!NOTE]
>
>Publish環境では、ログインしたメンバーが適切な権限を持っている場合、[&#x200B; コミュニティサイト &#x200B;](sites-console.md) に「`Administration`」メニュー項目が表示されます。

## グローバルナビゲーションパネル {#global-navigation-panel}

左上隅の `Adobe Experience Manager` アイコンを選択して、グローバルナビゲーションパネルを開き、次の 2 つのアイコンにアクセスします。

* [ナビゲーションコンソール](#navigation-console)
* [ツールコンソール](tools.md)

## ナビゲーションコンソール {#navigation-console}

様々な Communities コンソールにアクセスするには、グローバルナビゲーションから **ナビゲーション、Communities** を選択します。

![communities](assets/communities.png)

* [Sites](sites-console.md)

  Sites コンソールには、オーサー環境でアクセスして、コミュニティサイトとその [&#x200B; グループ &#x200B;](groups.md) を作成および管理できます。

* [モデレート](moderation.md)

  モデレートコンソールは、UGC およびオーサー環境の一括モデレート用です。 1 つ以上のコミュニティサイトに対して [&#x200B; コミュニティモデレーター &#x200B;](users.md#publishenvironmentusersandgroups) のロールが割り当てられたコミュニティメンバーは、Publish環境で同様の一括モデレートコンソールにアクセスできます。

* [メンバー、グループ](members.md)

  メンバーコンソールおよびグループコンソールは、Publish環境に存在するコミュニティメンバーおよびメンバーグループをオーサー環境から管理するためのものです。

* [レポート](reports.md)

  コミュニティサイトで [Adobe Analyticsを有効 &#x200B;](sites-console.md#analytics) にしている場合、レポートコンソールで、割り当て、ページビュー、投稿コンテンツ（UGC）に関するレポートが生成されます。 コンソールは、オーサー環境でのみ使用できます。

## ツールコンソール {#tools-console}

グローバルナビゲーションから [Communities ツール &#x200B;](tools.md) （旧称：管理コンソール）にアクセスするには、**[!UICONTROL ツール]**/**[!UICONTROL Communities]** を選択します。
