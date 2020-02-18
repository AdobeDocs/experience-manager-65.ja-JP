---
title: PreferencesNodesのプログラムによる管理
seo-title: PreferencesNodesのプログラムによる管理
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

---


# 環境設定ノードのプログラム管理 {#programmatically-managing-the-preferencesnodes}

このトピックでは、Preferences Manager Service API(Java)を使用して、環境設定ノードをプログラムで管理する方法について説明します。

設定は、管理者UIから手動で変更できます。 オプションを変更するには、に移動しま `Home>Settings>User Management> Configuration>Manual Configuration`す。 変更を `config.xml` 行った後でインポートを行うと、ノードで行われた変更を除くすべての変更が失われるこ `/Adobe/Adobe Experience Manager Forms/Config/UM persist` とがあります。 User Managementのインポートとエクスポートのプレビューでは、他のコンポーネントの構成設定の変更はサポートされていません。 現在は、APIを使用してこれらの変更を行うことがで `PreferencesManagerServiceClient` きます。

**手順の概要環境**&#x200B;設定ノードをプログラムで管理するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. PreferencesManagerServiceクライアントの作成
1. 適切なロール操作または権限操作を呼び出します

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**PreferencesManagerServiceクライアントの作成**

User Management PreferencesManagerService操作をプログラムで実行する前に、PreferencesManagerServiceクライアントを作成する必要があります。 Java APIを使用すると、PreferencesManagerServiceClientオブジェクトを作成することで実現できます。

**適切なロール操作または権限操作を呼び出します**

サービスクライアントを作成したら、Preferences Manager操作を呼び出すことができます。 サービスクライアントでは、権限の読み取りと設定が可能です。
