---
title: バッジコンソール
description: コミュニティのバッジコンソールを使用すると、獲得（授与）時またはコミュニティで特定の役割を担う（割り当てられた）時に、メンバーに対して表示できるカスタムバッジを追加できます
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 50ed9ec4-ff04-4f9d-aefb-0837542a9455
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 6%

---

# バッジコンソール {#badges-console}

## バッジについて {#about-badges}

コミュニティバッジコンソールを使用すると、獲得（与えられる）時やコミュニティで特定の役割を担う（割り当てられる）時に、メンバーに対して表示できるカスタムバッジを追加できます。

### バッジの表示 {#badge-visibility}

現在、コミュニティメンバーが獲得または割り当てられたバッジは、その名前とアバターと共に以下の場所に表示されます。

* プロファイル
* [フォーラム](/help/communities/forum.md)
* [Q&amp;A](/help/communities/working-with-qna.md)
* [リーダーボード](/help/communities/enabling-leaderboard.md)
* [アイディエーション](/help/communities/ideation-feature.md)

オーサー環境で、バッジコンソールに移動します。

* グローバルナビゲーションから： **[!UICONTROL ツール]** > **[!UICONTROL Communities]** > **[!UICONTROL バッジ]**

このコンソールには、現在使用可能なバッジと、新しいバッジを追加できるバッジが表示されます。

![badges-homepage](assets/badges-homepage.png)

## バッジを作成 {#create-badge}

バッジは、適切に小さい画像（72 dpi、高さが 26 ～ 32 ピクセルの範囲）をアップロードし、名前を指定することで作成されます。 バッジの画像は、リポジトリ ( ) の `/libs/settings/community/badging/images` とは、パブリッシュ環境に自動的にレプリケートされます。

パブリッシュ環境がパブリッシャーのファームの場合は、次の設定が必要です。 [ユーザー同期](/help/communities/sync.md).

![create-badge](assets/create-badge.png)

* **画像をアップロード**

  (*必須*)JPEGまたは PNG 形式の 72 dpi での推奨サイズが 32 x 32 ピクセルのバッジ画像。

* **名前**

  (*必須*) バッジ名。 これがデフォルトです `Display Name` リポジトリノード名。 次の場合、 `Name` は有効なリポジトリノード名ではないので、変更されています。

* **表示名**

  (*オプション*) ユーザーインターフェイスに表示されるバッジの名前。 デフォルトは、 `Name`.

* **説明**

  (*オプション*) バッジの説明。

## 追加情報 {#additional-information}

スコアルールとバッジルールの設定について詳しくは、 [スコアとバッジ](/help/communities/implementing-scoring.md).

メンバーのバッジの管理については、 [メンバーコンソール](/help/communities/members.md).
