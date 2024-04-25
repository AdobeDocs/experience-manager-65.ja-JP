---
title: バッジコンソール
description: コミュニティバッジコンソールを使用すると、メンバーが獲得（授与）した場合や、コミュニティで特定の役割を担った（割り当てられた）場合に表示できるカスタムバッジを追加できます
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 50ed9ec4-ff04-4f9d-aefb-0837542a9455
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 6%

---

# バッジコンソール {#badges-console}

## バッジについて {#about-badges}

コミュニティバッジコンソールを使用すると、メンバーが獲得（授与）した場合や、コミュニティで特定の役割を担った（割り当てられた）場合に表示できるカスタムバッジを追加できます。

### バッジの表示 {#badge-visibility}

現在、コミュニティメンバーが獲得または割り当てられているバッジは、名前とアバターと共に次の場所に表示されます。

* プロファイル
* [フォーラム](/help/communities/forum.md)
* [Q&amp;A](/help/communities/working-with-qna.md)
* [リーダーボード](/help/communities/enabling-leaderboard.md)
* [アイディエーション](/help/communities/ideation-feature.md)

オーサー環境でバッジコンソールに移動します。

* グローバルナビゲーションから： **[!UICONTROL ツール]** > **[!UICONTROL コミュニティ]** > **[!UICONTROL バッジ]**

このコンソールには、現在使用可能なバッジと、新しいバッジを追加できるバッジが表示されます。

![badges-homepage](assets/badges-homepage.png)

## バッジを作成 {#create-badge}

バッジは、適切な小さい画像（高さが 26～32 ピクセルの 72 dpi）をアップロードし、名前を付けることで作成されます。 バッジ画像は、次の場所にあるリポジトリに保存されます。 `/libs/settings/community/badging/images` とは、パブリッシュ環境に自動的にレプリケートされます。

パブリッシュ環境がパブリッシャーのファームの場合は、を設定する必要があります [ユーザー同期](/help/communities/sync.md).

![create-badge](assets/create-badge.png)

* **画像をアップロード**

  （*必須*） JPEG形式または PNG 形式で、推奨サイズが 32 x 32 ピクセル、72 dpi のバッジ画像。

* **名前**

  （*必須*） バッジ名。 これがデフォルトです `Display Name` とリポジトリノード名。 次の場合 `Name` は有効なリポジトリノード名ではありません。変更されています。

* **表示名**

  （*オプション*） ユーザーインターフェイスでバッジに表示する名前。 デフォルトは、に対して入力された変更されていないテキストです `Name`.

* **説明**

  （*オプション*） バッジの説明。

## 追加情報 {#additional-information}

スコアおよびバッジルールの設定について詳しくは、を参照してください [スコアおよびバッジ](/help/communities/implementing-scoring.md).

メンバーのバッジの管理については、を参照してください [メンバーコンソール](/help/communities/members.md).
