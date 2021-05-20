---
title: 選択したユーザーグループにルールエディターへのアクセスを許可する
seo-title: 選択したユーザーグループにルールエディターへのアクセスを許可する
description: 選択したユーザーグループにルールエディターへの制限付きアクセスを許可します。
seo-description: 選択したユーザーグループにルールエディターへの制限付きアクセスを許可します。
uuid: efa2570a-20ac-4b43-8a0e-38247f84d02f
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ab694a93-00d2-44d7-8ded-68ab2ad50693
docset: aem65
feature: アダプティブフォーム
exl-id: a1a2b277-3133-404b-a7fc-337cedddb12c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 74%

---

# 選択したユーザーグループにルールエディターへのアクセスを許可する{#grant-rule-editor-access-to-select-user-groups}

## 概要 {#overview}

アダプティブフォームで作業を行うユーザーのタイプやスキルは、それぞれ異なっています。正しい知識を使用してスクリプトや複雑なルールを操作できる上級ユーザーもいれば、アダプティブフォームのレイアウトや基本的なプロパティ以外の操作はできない初心者レベルのユーザーもいます。

AEM Forms では、各ユーザーの役割や職務に応じて、ルールエディターへのアクセスを制限することができます。アダプティブフォームの設定サービスを使用して、ルールエディターを表示してアクセスできる[ユーザーグループ](/help/sites-administering/security.md)を指定することができます。

## ルールエディターにアクセスできるユーザーグループの指定 {#specify-user-groups-that-can-access-rule-editor}

1. 管理者として AEM Forms にログインします。
1. オーサーインスタンスで、![adobeexperiencemanager](assets/adobeexperiencemanager.png)Adobe Experience Manager/ツール![ハンマー](assets/hammer.png)/操作/Webコンソールをクリックします。 新しいウィンドウに Web コンソールが表示されます。

   ![1-2](assets/1-2.png)

1. Webコンソールウィンドウで、「 **[!UICONTROL アダプティブフォームとインタラクティブ通信Webチャネルの設定]** 」を探してクリックします。 **[!UICONTROL 「アダプティブフォーム」と「インタラクティブ通信Webチャネルの設定」]** ダイアログが表示されます。値を変更せずに、「**保存**」をクリックします。

   これにより、CRX リポジトリに /apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config ファイルが作成されます。

1. 管理者として CRXDE にログインします。編集のため、/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config ファイルを開きます。
1. 次のプロパティを使用して、ルールエディターにアクセスできるグループの名前（例えば RuleEditorsUserGroup）を指定し、「**すべて保存**」をクリックします。

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   複数のグループに対するアクセスを有効にするには、コンマで区切られた値のリストを指定します。

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![ユーザーを作成](assets/create_user_new.png)

   現在は、指定したユーザーグループ（ここではRuleEditorsUserGroup）に属していないユーザーがフィールドをタップした場合、コンポーネントツールバーでルールを編集アイコン( ![edit-rules1](assets/edit-rules1.png) )を使用できません。

   ![componentstoolbarwither](assets/componentstoolbarwithre.png)

   ルールエディターへのアクセス権を持つユーザーに表示されるコンポーネントツールバー

   ![componentstoolbarwithouter](assets/componentstoolbarwithoutre.png)

   ルールエディターへのアクセス権を持たないユーザーに表示されるコンポーネントツールバー

   ユーザーをグループに追加する方法については、[ユーザーの管理とセキュリティ](/help/sites-administering/security.md)を参照してください。
