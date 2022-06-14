---
title: PreferencesNodes をプログラムで管理する
seo-title: Programmatically managing the PreferencesNodes
description: Preferences Manager サービス API (Java) を使用して、環境設定ノードをプログラムで管理してください。
seo-description: Use the Preferences Manager Service API (Java) to programmatically manage the Preferences Nodes.
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
source-wordcount: '245'
ht-degree: 100%

---

# 環境設定ノードをプログラムで管理する {#programmatically-managing-the-preferencesnodes}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

このトピックでは、Preferences Manager サービス API (Java) を使用して、環境設定ノードをプログラムで管理する方法について説明します。

構成設定は、管理者 UI から手動で変更できます。オプションを変更するには、`Home>Settings>User Management> Configuration>Manual Configuration` に移動してください。変更を加えた後に `config.xml` をインポートすると、`/Adobe/Adobe Experience Manager Forms/Config/UM persist` ノードで行われた変更以外のすべての変更内容が失われます。User Management のインポートとエクスポートのプレビューでは、他のコンポーネントの構成設定の変更はサポートされていません。現在では、これらの変更は `PreferencesManagerServiceClient` APIを使用して行うことができます。

**手順の概要**&#x200B;プログラムによって環境設定ノードを管理するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. PreferencesManagerService クライアントを作成します
1. 適切な役割または権限の操作の呼び出し

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めるようにします。

**PreferencesManagerService クライアントの作成**

User Management PreferencesManagerService 操作をプログラムで実行する前に、PreferencesManagerService クライアントを作成する必要があります。 Java API では、PreferencesManagerServiceClient オブジェクトを作成することで実現されます。

**適切な役割または権限の操作を呼び出す**

サービスクライアントを作成したら、Preferences Manager 操作を呼び出すことができます。 サービスクライアントを使用すると、権限の読み取りと設定が可能です。
