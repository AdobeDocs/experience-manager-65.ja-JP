---
title: バッジコンソール
seo-title: バッジコンソール
description: Communities のバッジコンソールを使用すると、バッジを獲得（授与された）したとき、またはコミュニティで特定の役割についた（割り当てられた）ときにメンバーに表示できるカスタムバッジを追加できます
seo-description: Communities のバッジコンソールを使用すると、バッジを獲得（授与された）したとき、またはコミュニティで特定の役割についた（割り当てられた）ときにメンバーに表示できるカスタムバッジを追加できます
uuid: 7103b133-ef3f-47d6-a2dc-4e6ff92e8fed
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 135b3077-5343-4888-858d-de5e9b1d4b04
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# バッジコンソール{#badges-console}

## バッジについて {#about-badges}

Communities のバッジコンソールでは、バッジを獲得（授与された）したとき、またはコミュニティで特定の役割についた（割り当てられた）ときにメンバーに表示できるカスタムバッジを追加できます

### バッジの表示 {#badge-visibility}

現在、コミュニティメンバーが獲得するバッジ、またはコミュニティメンバーに割り当てられるバッジは、次の場所にメンバーの名前とアバターとともに表示されます。

* プロファイル
* [フォーラム](/help/communities/forum.md)
* [Q&amp;A](/help/communities/working-with-qna.md)
* [リーダーボード](/help/communities/enabling-leaderboard.md)
* [アイディエーション](/help/communities/ideation-feature.md)

オーサー環境でバッジコンソールに接続するには

* グローバルナビゲーションから：**ツール／コミュニティ／バッジ**

このコンソールでは、現在利用可能なバッジが表示され、新しいバッジを追加できます。

![chlimage_1-123](assets/chlimage_1-123.png)

## バッジを作成 {#create-badge}

バッジを作成するには、適度に小さい画像（高さが 26 から 32 ピクセルの 72 dpi）をアップロードし、名前を入力します。The badge image is stored in the repository at `/etc/community/badging/images` and is automatically replicated to the publish environment.

パブリッシュ環境がパブリッシャーのファームである場合、[ユーザーの同期](/help/communities/sync.md)を設定する必要があります。

![chlimage_1-124](assets/chlimage_1-124.png)

* **画像をアップロ**&#x200B;ード(必須&#x200B;**)バッジの画像で、推奨サイズが32 x 32ピクセル、72 dpi、JPEGまたはPNG形式です。

* **名前**(必&#x200B;*須*)バッジの名前。 It is the default `Display Name` as well as the repository node name. If the `Name` is not a valid repository node name, it will be modified.

* **表示名**(オ&#x200B;*プション*) UIにバッジに表示する名前。 Default is the unaltered text entered for the `Name`.

* **説明**(オ&#x200B;*プション*)バッジの説明。

## 追加情報 {#additional-information}

For details on setting up scoring and badging rules, see [Scoring and Badges](/help/communities/implementing-scoring.md).

メンバーのバッジの管理については、[メンバーコンソール](/help/communities/members.md)を参照してください。
