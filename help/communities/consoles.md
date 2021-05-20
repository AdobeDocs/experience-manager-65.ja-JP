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
role: Administrator
exl-id: 36f2e3d2-46c7-48a8-a1e9-213f581bd9f3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 13%

---

# コミュニティコンソール {#communities-consoles}

AEM Communitiesコンソールは、オーサー環境のグローバルナビゲーションパネルから使用でき、次のような管理タスクにアクセスできます。

* [コミュニティサイトの作成](sites-console.md)
* サイト内にネストされた[グループ](groups.md)を追加
* [コミュニティサイトテンプレート](sites.md)の管理
* [コミュニティメンバー](members.md)の管理
* [](moderate-ugc.md) ユーザー生成コンテンツ(UGC)のモデレート
* [カスタムバッジ](badges.md)を作成します。
* UGC](srp-config.md)の[デフォルトストレージの設定

[UGCストレージ](working-with-srp.md)をオーサー環境とパブリッシュ環境で共有される共通ストアに設定すると、オーサー環境とパブリッシュ環境の両方から使用できる[モデレートコンソール](moderation.md)は、UGCの単一のインスタンス上で動作します。

オーサー環境では、管理者権限でサインインした後、ナビゲーションコンソールとツールコンソールから`Communities`コンソールを使用できます。

>[!NOTE]
>
>パブリッシュ環境では、サインインしたメンバーが適切な権限を持つ場合、[コミュニティサイト](sites-console.md)に`Administration`メニュー項目が表示されます。

## グローバルナビゲーションパネル {#global-navigation-panel}

`Adobe Experience Manager` のアイコンを選択し、グローバルナビゲーションパネルを開いて次の 2 つのアイコンにアクセスします。

* [ナビゲーションコンソール](#navigation-console)
* [ツールコンソール](tools.md)

## ナビゲーションコンソール {#navigation-console}

様々なコミュニティコンソールにアクセスするには、グローバルナビゲーションから&#x200B;**ナビゲーション/コミュニティ**&#x200B;を選択します。

![コミュニティ](assets/communities.png)

* [Sites](sites-console.md)

   サイトコンソールには、オーサー環境でコミュニティサイトとその[グループ](groups.md)を作成および管理する目的でアクセスできます。

* [モデレート](moderation.md)

   モデレートコンソールは、オーサー環境でのUGCの一括モデレート用です。 同様の一括モデレートコンソールは、パブリッシュ環境で、1つ以上のコミュニティサイトに対して[コミュニティモデレーター](users.md#publishenvironmentusersandgroups)の役割を割り当てられたコミュニティメンバーにアクセスできます。

* [メンバー、グループ](members.md)

   メンバーコンソールとグループコンソールは、パブリッシュ環境に存在するコミュニティメンバーとメンバーグループをオーサー環境から管理するためのものです。

* [レポート](reports.md)

   レポートコンソールでは、コミュニティサイトでAdobe Analytics[が有効になっている場合に、割り当て、ページビュー、投稿されたコンテンツ(UGC)に関するレポートを生成できます。 ](sites-console.md#analytics)コンソールは、オーサー環境でのみ使用できます。

* [リソース](resources.md)

   リソースコンソールでは、[イネーブルメントマネージャー](enablement.md#communitymanagers)が、[イネーブルメントコミュニティサイト](overview.md#enablement-community)のメンバーに対してリソースを作成、管理、割り当てます。 コンソールは、オーサー環境でのみ使用できます。

## ツールコンソール {#tools-console}

[コミュニティツール](tools.md)（以前の管理コンソール）にアクセスするには、グローバルナビゲーションから次の手順を実行します。**[!UICONTROL ツール]** / **[!UICONTROL コミュニティ]**
