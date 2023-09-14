---
title: 選択したユーザーグループにルールエディターへのアクセスを許可する
description: 選択したユーザーグループに対して、ルールエディターへのアクセス制限を付与します。
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Adaptive Forms
exl-id: a1a2b277-3133-404b-a7fc-337cedddb12c
source-git-commit: fd8bb7d3d9040e0a7a6b2f65751445f41aeab73e
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 45%

---

# 選択したユーザーグループにルールエディターへのアクセスを許可する{#grant-rule-editor-access-to-select-user-groups}

<span class="preview"> Adobeでは、最新の拡張可能なデータキャプチャを使用することをお勧めします [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja) 対象： [新しいアダプティブFormsの作成](/help/forms/using/create-an-adaptive-form-core-components.md) または [AEM SitesページへのアダプティブFormsの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). これらのコンポーネントは、アダプティブFormsの作成における大幅な進歩を表し、印象的なユーザーエクスペリエンスを実現します。 この記事では、基盤コンポーネントを使用したアダプティブFormsのオーサリングに関する古いアプローチについて説明します。 </span>

## 概要 {#overview}

アダプティブFormsでは、様々なスキルを持つ様々なタイプのユーザーが作業をおこなうことができます。 正しい知識を使用してスクリプトや複雑なルールを操作できる上級ユーザーもいれば、アダプティブフォームのレイアウトや基本的なプロパティ以外の操作はできない初心者レベルのユーザーもいます。

AEM Formsを使用すると、ユーザーの役割や機能に基づいて、ルールエディターへのアクセスを制限できます。 Adaptive Forms Configuration Service の設定で、 [ユーザーグループ](/help/sites-administering/security.md) ルールエディターを表示してアクセスできる

## ルールエディターにアクセスできるユーザーグループの指定 {#specify-user-groups-that-can-access-rule-editor}

1. 管理者として AEM Forms にログインします。
1. オーサーインスタンスで、![adobeexperiencemanager](assets/adobeexperiencemanager.png)Adobe Experience Manager／ツール![ハンマー](assets/hammer.png)／操作／Web コンソール をクリックしてください。新しいウィンドウに Web コンソールが表示されます。

   ![1-2](assets/1-2.png)

1. Web コンソールウィンドウで、を探して「 **[!UICONTROL アダプティブフォームとインタラクティブ通信の Web チャネル設定]**. **[!UICONTROL アダプティブフォームとインタラクティブ通信の Web チャネル設定]** ダイアログボックスが表示されます。 値を変更せずに、「**保存**」をクリックします。

   これにより、CRX-repository に/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config ファイルが作成されます。

1. 管理者として CRXDE にログインします。/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config ファイルを開いて編集します。
1. 次のプロパティを使用して、ルールエディターにアクセスできるグループの名前（例えば RuleEditorsUserGroup）を指定し、「**すべて保存**」をクリックします。

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   複数のグループに対するアクセスを有効にするには、コンマ区切り値のリストを指定します。

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![ユーザーを作成](assets/create_user_new.png)

   これで、指定したユーザーグループ（ここでは RuleEditorsUserGroup）に属していないユーザーがフィールドをタップしたときに、ルールを編集アイコン ( ![edit-rules1](assets/edit-rules1.png)) は、コンポーネントツールバーでは使用できません。

   ![componentstoolbarwither](assets/componentstoolbarwithre.png)

   ルールエディターへのアクセス権を持つユーザーに表示されるコンポーネントツールバー

   ![componentstoolbarwithouter](assets/componentstoolbarwithoutre.png)

   ルールエディターへのアクセス権を持たないユーザーに表示されるコンポーネントツールバー

   ユーザーをグループに追加する方法については、[ユーザーの管理とセキュリティ](/help/sites-administering/security.md)を参照してください。
