---
title: PreferencesNodesをプログラムで管理する
seo-title: PreferencesNodesをプログラムで管理する
description: 環境設定マネージャーサービスAPI(Java)を使用して、環境設定ノードをプログラムで管理します。
seo-description: 環境設定マネージャーサービスAPI(Java)を使用して、環境設定ノードをプログラムで管理します。
uuid: f0cb117a-a6cc-4ca5-8511-b3bc9f6738e9
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9d4dba7f-49d8-4112-bc8a-04dafc99a936
role: Developer
exl-id: 108eb249-879b-4e4f-b431-8118b8656e62
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---

# 環境設定ノード{#programmatically-managing-the-preferencesnodes}をプログラムで管理する

**このドキュメントのサンプルと例は、JEE上のAEM Forms環境に限られています。**

このトピックでは、環境設定マネージャーサービスAPI(Java)を使用して、プログラムで環境設定ノードを管理する方法について説明します。

設定は、Administrator UIから手動で変更できます。 オプションを変更するには、`Home>Settings>User Management> Configuration>Manual Configuration`に移動します。 `config.xml`を読み込むと、ノード`/Adobe/Adobe Experience Manager Forms/Config/UM persist`で行われた変更を除くすべての変更が失われます。 User Managementの読み込みと書き出しのプレビューでは、他のコンポーネントの構成設定の変更はサポートされていません。 これらの変更は、`PreferencesManagerServiceClient` APIを使用して行うことができます。

**手順の概要プ**&#x200B;ログラムで環境設定ノードを管理するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. PreferencesManagerServiceクライアントの作成
1. 適切なロールまたは権限操作を呼び出す

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

**PreferencesManagerServiceクライアントの作成**

User Management PreferencesManagerService操作をプログラムで実行する前に、PreferencesManagerServiceクライアントを作成する必要があります。 Java APIを使用すると、PreferencesManagerServiceClientオブジェクトを作成してこれを実現できます。

**適切なロールまたは権限操作を呼び出す**

サービスクライアントを作成したら、Preferences Manager操作を呼び出すことができます。 サービスクライアントを使用すると、権限の読み取りと設定が可能です。
