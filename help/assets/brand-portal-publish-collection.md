---
title: Brand Portal へのコレクションの公開
description: コレクションをBrand Portalに公開および非公開にする方法を説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
docset: aem65
feature: Brand Portal
role: User
exl-id: 8f426012-d9ec-418e-8ab6-78e4aeff7538
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 80%

---

# Brand Portal へのコレクションの公開 {#publish-collections-to-brand-portal}

Adobe Experience Manager(AEM)Assets 管理者は、組織のAEM Assets Brand Portalインスタンスにコレクションを公開できます。 ただし、最初に AEM Assets を Brand Portal と統合する必要があります。詳しくは [AEM Assets と Brand Portal の連携の設定](/help/assets/configure-aem-assets-with-brand-portal.md)を参照してください。

その後、AEM Assets でオリジナルのコレクションに変更を加えても、そのコレクションを再び公開しない限り変更内容は Brand Portal に反映されません。このため、作業中の変更が Brand Portal に提供されることがありません。管理者が公開した承認済みの変更のみが Brand Portal で提供されます。

>[!NOTE]
>
>コンテンツフラグメントは Brand Portal に公開できません。したがって、AEM オーサー上でコンテンツフラグメントを選択している場合は、「**Brand Portal に公開**」アクションを使用できません。
>
>コンテンツフラグメントを含むコレクションをAEMオーサーからBrand Portalに公開した場合、コンテンツフラグメントを除くフォルダー内のすべてのコンテンツがBrand Portalインターフェイスにレプリケートされます。

## Brand Portal へのコレクションの公開 {#publish-a-collection-to-brand-portal}

1. AEM Assets の UI で AEM のロゴをクリックします。
1. **ナビゲーション**&#x200B;ページで、**アセット／コレクション**&#x200B;に移動します。
1. コレクションコンソールで Brand Portal に公開するコレクションを選択します。

   ![select_collection](assets/select_collection.png)

1. ツールバーで「**Brand Portal に公開**」をクリックします。
1. 確認ダイアログで「**公開**」をクリックします。
1. 確認メッセージを閉じます。
1. 管理者として Brand Portal にログインします。公開したコレクションがコレクションインターフェイスで利用できます。

   ![公開コレクション](assets/published_collection.png)

## コレクションを非公開にする {#unpublish-collections}

AEM Assets から Brand Portal へ公開したコレクションを非公開にすることができます。元のコレクションを非公開にすると、Brand Portal のユーザーはそのコピーを使用できなくなります。

1. AEM Assets インスタンスのコレクションコンソールから、非公開にするコレクションを選択します。

   ![select_collection-1](assets/select_collection-1.png)

1. ツールバーで「**Brand Portal から削除**」アイコンをクリックします。
1. 確認ダイアログで「**非公開**」をクリックします。
1. 確認メッセージを閉じます。コレクションが Brand Portal インターフェイスから削除されます。
