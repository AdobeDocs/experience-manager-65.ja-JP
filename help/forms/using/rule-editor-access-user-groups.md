---
title: 選択したユーザーグループにルールエディターへのアクセスを許可する
seo-title: Grant rule editor access to select user groups
description: 選択したユーザーグループに対して、ルールエディターへのアクセス制限を付与します。
seo-description: Grant restricted access to rule editor to select user groups.
uuid: efa2570a-20ac-4b43-8a0e-38247f84d02f
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ab694a93-00d2-44d7-8ded-68ab2ad50693
docset: aem65
feature: Adaptive Forms
exl-id: a1a2b277-3133-404b-a7fc-337cedddb12c
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 70%

---

# 選択したユーザーグループにルールエディターへのアクセスを許可する{#grant-rule-editor-access-to-select-user-groups}

<span class="preview"> Adobeでは、最新の拡張可能なデータキャプチャを使用することをお勧めします [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja) 対象： [新しいアダプティブFormsの作成](/help/forms/using/create-an-adaptive-form-core-components.md) または [AEM SitesページへのアダプティブFormsの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). これらのコンポーネントは、アダプティブFormsの作成における大幅な進歩を表し、印象的なユーザーエクスペリエンスを実現します。 この記事では、基盤コンポーネントを使用してアダプティブFormsを作成する古い方法について説明します。 </span>

## 概要 {#overview}

アダプティブFormsでは、様々なスキルを持つ様々なタイプのユーザーが作業をおこなうことができます。 正しい知識を使用してスクリプトや複雑なルールを操作できる上級ユーザーもいれば、アダプティブフォームのレイアウトや基本的なプロパティ以外の操作はできない初心者レベルのユーザーもいます。

AEM Formsを使用すると、ユーザーの役割や機能に基づいて、ルールエディターへのアクセスを制限できます。 アダプティブフォームの設定サービスを使用して、ルールエディターを表示してアクセスできる[ユーザーグループ](/help/sites-administering/security.md)を指定することができます。

## ルールエディターにアクセスできるユーザーグループの指定 {#specify-user-groups-that-can-access-rule-editor}

1. 管理者として AEM Forms にログインします。
1. オーサーインスタンスで、![adobeexperiencemanager](assets/adobeexperiencemanager.png)Adobe Experience Manager／ツール![ハンマー](assets/hammer.png)／操作／Web コンソール をクリックしてください。新しいウィンドウに Web コンソールが表示されます。

   ![1-2](assets/1-2.png)

1. Web コンソールウィンドウで、**[!UICONTROL アダプティブフォームとインタラクティブ通信の web チャネル設定]**&#x200B;を探してクリックします。**[!UICONTROL アダプティブフォームおよびインタラクティブ通信 web チャネルの設定]**&#x200B;ダイアログが表示されます。値を変更せずに、「**保存**」をクリックします。

   CRX-repository に/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config ファイルが作成されます。

1. 管理者として CRXDE にログインします。/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config ファイルを開いて編集します。
1. 次のプロパティを使用して、ルールエディターにアクセスできるグループの名前（例えば RuleEditorsUserGroup）を指定し、「**すべて保存**」をクリックします。

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   複数のグループにアクセスを有効にするには、コンマ区切りの値のリストを指定します。

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![ユーザーを作成](assets/create_user_new.png)

   これで、指定されたユーザーグループ（ここでは RuleEditorsUserGroup）に属していないユーザーがフィールドをタップした場合、コンポーネントのツールバーに「ルールを編集」アイコン（![edit-rules1](assets/edit-rules1.png)）が表示されなくなります。

   ![componentstoolbarwither](assets/componentstoolbarwithre.png)

   ルールエディターへのアクセス権を持つユーザーに表示されるコンポーネントツールバー

   ![componentstoolbarwithouter](assets/componentstoolbarwithoutre.png)

   ルールエディターへのアクセス権を持たないユーザーに表示されるコンポーネントツールバー

   ユーザーをグループに追加する方法については、[ユーザーの管理とセキュリティ](/help/sites-administering/security.md)を参照してください。
