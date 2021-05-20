---
title: Brand Portal へのコレクションの公開
seo-title: Brand Portal へのコレクションの公開
description: Brand Portal を対象としたコレクションの公開および非公開の方法を学びます。
seo-description: Brand Portal を対象としたコレクションの公開および非公開の方法を学びます。
uuid: 7de58548-4cfa-4a94-bac7-9e914dee9042
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 90e3fd0e-9bc3-4aff-8c7b-7408f5b940e8
docset: aem65
feature: Brand Portal
role: Business Practitioner
exl-id: 8f426012-d9ec-418e-8ab6-78e4aeff7538
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 69%

---

# Brand Portal へのコレクションの公開 {#publish-collections-to-brand-portal}

Adobe Experience Manager（AEM）Assets の管理者は、組織の AEM Assets Brand Portal のインスタンスにコレクションを公開できます。ただし、最初に AEM Assets を Brand Portal と統合する必要があります。詳しくは [AEM Assets と Brand Portal の連携の設定](/help/assets/configure-aem-assets-with-brand-portal.md)を参照してください。

その後、AEM Assetsで元のコレクションに変更を加えても、そのコレクションを再度公開するまで、変更はBrand Portalに反映されません。 この特性により、作業中の変更がBrand Portalでは利用できなくなります。 管理者が公開した承認済みの変更のみが Brand Portal で提供されます。

>[!NOTE]
>
>コンテンツフラグメントは Brand Portal に公開できません。したがって、AEMオーサー上でコンテンツフラグメントを選択した場合、「**Brand Portalに公開**」アクションは使用できません。
>
>コンテンツフラグメントを含むコレクションを AEM オーサーインスタンスから Brand Portal へ公開した場合は、そのフォルダー内のコンテンツフラグメントを除く全コンテンツが Brand Portal インターフェイスにレプリケートされます。

## Brand Portal へのコレクションの公開 {#publish-a-collection-to-brand-portal}

1. AEM Assets の UI で AEM のロゴをクリックします。
1. **ナビゲーション**&#x200B;ページで、**アセット／コレクション**&#x200B;に移動します。
1. コレクションコンソールで、Brand Portalに公開するコレクションを選択します。

   ![select_collection](assets/select_collection.png)

1. ツールバーで「**Brand Portal に公開**」をクリックします。
1. 確認ダイアログで「**公開**」をクリックします。
1. 確認メッセージを閉じます。
1. 管理者として Brand Portal にログインします。公開したコレクションがコレクションインターフェイスで利用できます。

   ![公開コレクション](assets/published_collection.png)

## コレクションを非公開にする {#unpublish-collections}

AEM AssetsからBrand Portalに公開したコレクションを非公開にできます。 元のコレクションを非公開にすると、そのコレクションのコピーはBrand Portalユーザーには使用できなくなります。

1. AEM Assets インスタンスのコレクションコンソールから、非公開にしたいコレクションを選択します。

   ![select_collection-1](assets/select_collection-1.png)

1. ツールバーで「**Brand Portal から削除**」アイコンをクリックします。
1. 確認ダイアログで「**非公開**」をクリックします。
1. 確認メッセージを閉じます。コレクションが Brand Portal インターフェイスから削除されます。
