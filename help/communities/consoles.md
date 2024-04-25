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
* 追加中 [グループ](groups.md) サイト内にネスト
* 管理 [コミュニティサイトテンプレート](sites.md)
* 管理 [コミュニティメンバー](members.md)
* [モデレート](moderate-ugc.md) ユーザー生成コンテンツ（UGC）
* 作成 [カスタムバッジ](badges.md)
* の設定 [ugc のデフォルトストレージ](srp-config.md)

条件 [UGC ストレージ](working-with-srp.md) オーサー環境とパブリッシュ環境で共有される共通ストアとして設定される [モデレートコンソール](moderation.md)は、オーサー環境とパブリッシュ環境の両方から利用でき、UGC の単一のインスタンスで動作します。

オーサー環境で、管理者権限でログインした後、 `Communities` コンソールは、ナビゲーションコンソールとツールコンソールから使用できます。

>[!NOTE]
>
>パブリッシュ環境では、 [コミュニティサイト](sites-console.md) を表示 `Administration` サインイン メンバーが適切な特権を持っているときのメニュー項目です。

## グローバルナビゲーションパネル {#global-navigation-panel}

「」を選択します `Adobe Experience Manager` 左上隅のアイコンを使用してグローバルナビゲーションパネルを開き、次の 2 つのアイコンにアクセスします。

* [ナビゲーションコンソール](#navigation-console)
* [ツールコンソール](tools.md)

## ナビゲーションコンソール {#navigation-console}

グローバルナビゲーションから様々な Communities コンソールにアクセスするには、を選択します。 **ナビゲーション、コミュニティ**.

![コミュニティ](assets/communities.png)

* [Sites](sites-console.md)

  Sites コンソールには、オーサー環境でアクセスして、コミュニティサイトとそのサイトを作成および管理できます [グループ](groups.md).

* [モデレート](moderation.md)

  モデレートコンソールは、UGC およびオーサー環境の一括モデレート用です。 次の役割が割り当てられたコミュニティメンバーは、パブリッシュ環境で同様の一括モデレートコンソールにアクセスできます [コミュニティ調整者](users.md#publishenvironmentusersandgroups) （1 つ以上のコミュニティサイトの場合）。

* [メンバー、グループ](members.md)

  メンバーコンソールとグループコンソールは、パブリッシュ環境に存在するコミュニティメンバーとメンバーグループをオーサー環境から管理するためのものです。

* [レポート](reports.md)

  コミュニティサイトに次の機能がある場合、レポートコンソールで、割り当て、ページビュー、投稿コンテンツ（UGC）に関するレポートが生成されます [がAdobe Analyticsを有効にしました](sites-console.md#analytics). コンソールは、オーサー環境でのみ使用できます。

## ツールコンソール {#tools-console}

アクセス対象 [コミュニティツール](tools.md) （旧称は管理コンソール）グローバルナビゲーションから： **[!UICONTROL ツール]** > **[!UICONTROL コミュニティ]**
