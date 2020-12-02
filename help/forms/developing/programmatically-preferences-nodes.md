---
title: PreferencesNodesのプログラム管理
seo-title: PreferencesNodesのプログラム管理
description: 'null'
seo-description: 'null'
uuid: f0cb117a-a6cc-4ca5-8511-b3bc9f6738e9
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9d4dba7f-49d8-4112-bc8a-04dafc99a936
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---


# 環境設定ノードのプログラム管理{#programmatically-managing-the-preferencesnodes}

このトピックでは、Preferences Manager Service API(Java)を使用して、環境設定ノードをプログラムで管理する方法について説明します。

設定は、管理者UIから手動で変更できます。 オプションを変更するには、`Home>Settings>User Management> Configuration>Manual Configuration`に移動します。 変更を行った後で`config.xml`を読み込むと、ノード`/Adobe/Adobe Experience Manager Forms/Config/UM persist`で行われた変更以外の変更はすべて失われます。 User Managementのインポートとエクスポートのプレビューでは、他のコンポーネントの構成設定の変更はサポートされていません。 現在は、`PreferencesManagerServiceClient` APIを使用してこれらの変更を行うことができます。

**手**&#x200B;順の概要環境設定ノードをプログラムで管理するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. PreferencesManagerServiceクライアントの作成
1. 適切なロールまたは権限操作を呼び出します

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

**PreferencesManagerServiceクライアントの作成**

User Management PreferencesManagerService操作をプログラムで実行する前に、PreferencesManagerServiceクライアントを作成する必要があります。 Java APIを使用すると、PreferencesManagerServiceClientオブジェクトを作成することで実現できます。

**適切なロールまたは権限操作を呼び出します**

サービスクライアントを作成したら、環境設定マネージャーの操作を呼び出すことができます。 サービスクライアントでは、権限の読み取りと設定が可能です。
