---
title: バッジコンソール
seo-title: Badges Console
description: Communities のバッジコンソールを使用すると、バッジを獲得（授与された）したとき、またはコミュニティで特定の役割についた（割り当てられた）ときにメンバーに表示できるカスタムバッジを追加できます
seo-description: The Communities Badges console lets you add custom badges that can be displayed for members when earned (awarded) or when they take on a specific role in the community (assigned)
uuid: 7103b133-ef3f-47d6-a2dc-4e6ff92e8fed
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 135b3077-5343-4888-858d-de5e9b1d4b04
docset: aem65
role: Admin
exl-id: 50ed9ec4-ff04-4f9d-aefb-0837542a9455
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 57%

---

# バッジコンソール {#badges-console}

## バッジについて {#about-badges}

Communities のバッジコンソールでは、バッジを獲得（授与された）したとき、またはコミュニティで特定の役割についた（割り当てられた）ときにメンバーに表示できるカスタムバッジを追加できます

### バッジの表示 {#badge-visibility}

現在、コミュニティメンバーが獲得するバッジ、またはコミュニティメンバーに割り当てられるバッジは、次の場所にメンバーの名前とアバターとともに表示されます。

* プロファイル
* [フォーラム](/help/communities/forum.md)
* [Q&amp;A](/help/communities/working-with-qna.md)
* [リーダーボード](/help/communities/enabling-leaderboard.md)
* [アイディエーション](/help/communities/ideation-feature.md)

オーサー環境で、バッジコンソールに移動します。

* グローバルナビゲーションから： **[!UICONTROL ツール]** > **[!UICONTROL コミュニティ]** > **[!UICONTROL バッジ]**

このコンソールでは、現在利用可能なバッジが表示され、新しいバッジを追加できます。

![badges-homepage](assets/badges-homepage.png)

## バッジを作成 {#create-badge}

バッジを作成するには、適度に小さい画像（高さが 26 から 32 ピクセルの 72 dpi）をアップロードし、名前を入力します。バッジの画像は、リポジトリ ( ) の `/libs/settings/community/badging/images` とは、パブリッシュ環境に自動的にレプリケートされます。

パブリッシュ環境がパブリッシャーのファームである場合、[ユーザーの同期](/help/communities/sync.md)を設定する必要があります。

![create-badge](assets/create-badge.png)

* **画像をアップロード**

   (*必須*)JPEGまたは PNG 形式の 72dpi での推奨サイズが 32 x 32 ピクセルのバッジ画像。

* **名前**

   (*必須*) バッジ名。 これがデフォルトです `Display Name` リポジトリのノード名。 この `Name` は有効なリポジトリノード名ではありません。変更されます。

* **表示名**

   (*オプション*) UI でバッジに表示する名前です。 デフォルトは、 `Name`.

* **説明**

   (*オプション*) バッジの説明。

## 追加情報 {#additional-information}

スコアルールとバッジルールの設定について詳しくは、 [スコアとバッジ](/help/communities/implementing-scoring.md).

メンバーのバッジの管理については、[メンバーコンソール](/help/communities/members.md)を参照してください。
