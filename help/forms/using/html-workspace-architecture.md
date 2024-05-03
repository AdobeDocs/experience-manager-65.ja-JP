---
title: AEM Forms Workspace のアーキテクチャ
description: LiveCycle AEM Forms workspace の概要と概念情報です。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: c6f216d4-781c-4356-b9f0-3324903a28e7
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 100%

---

# AEM Forms Workspace のアーキテクチャ {#aem-forms-workspace-architecture}

AEM Forms Workspace は、CRX™ にホスティングされている web アプリケーションです。Workspace がサポートされているブラウザーで開かれると、CRX リソースがアクセスされ、アプリケーションがブラウザー内で HTML ページとしてレンダリングされます。

アプリケーションは REST エンドポイント上にある AEM Forms サーバーにアクセスして、次のことを行います。

* ユーザーのタスク、プロセススタートポイント、プロセス履歴、およびユーザー情報の取得
* タスクに対するアクションの実行
* データベースでのクエリタスク
* ユーザーの環境設定の更新など

AEM Forms サーバーは、JDBC を通して AEM Forms データベースにアクセスします。データベースは、タスク、プロセスとそのインスタンス、ユーザー、および関連情報を維持します。

AEM Forms Workspace は、モジュール形式の JavaScript™ コンポーネントで組み立てられており、これらのコンポーネントは他の Web アプリケーションで個々にカスタマイズしたり再利用することができます。コンポーネントは web アプリケーションに構造を提供する JavaScript ライブラリである BackBone に基づいています。コンポーネントと BackBone とのインタラクションを説明する記事について詳しくは、[こちら](/help/forms/using/backbone-interaction.md)を参照してください。CRX フォルダー構造のコンポーネントの組織については、[この記事](/help/forms/using/folder-structure.md)で説明しています。

AEM Forms Workspace のために配信されるパッケージを以下に示しています。

* `adobe-lc-workspace-pkg-<version>.zip`：これは CRX パッケージです。すなわち、Package Manager を使用して CRX 内にデプロイできます。
* `adobe-lc-workspace-<version>-src.zip`：デプロイパッケージ（Ship、Debug、および Dev パッケージ）を作成するための AEM Forms Workspace とスクリプトの完全なコードを含むアーカイブです。
