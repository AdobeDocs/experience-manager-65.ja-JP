---
title: AEM Forms Workspace のアーキテクチャ
description: LiveCycleAEM Forms Workspace の概念情報とアーキテクチャの概要です。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: c6f216d4-781c-4356-b9f0-3324903a28e7
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 31%

---

# AEM Forms Workspace のアーキテクチャ {#aem-forms-workspace-architecture}

AEM Forms workspace は、CRX™でホストされる Web アプリケーションです。 ワークスペースをブラウザーで開くと、CRX リソースにアクセスし、アプリケーションがブラウザーでHTMLページとしてレンダリングされます。

アプリケーションは、REST エンドポイント上のAEM Formsサーバーにアクセスし、次の操作を実行します。

* ユーザータスク、プロセスの開始点、プロセス履歴、およびユーザー情報を取得します
* タスクに対するアクションの実行
* データベースのクエリタスク
* ユーザーの環境設定の更新など

AEM Formsサーバーは、JDBC を介してAEM Formsデータベースにアクセスします。 データベースには、タスク、プロセス、そのインスタンス、ユーザー、および関連情報が保持されます。

AEM Forms Workspace は、モジュール形式の JavaScript™ コンポーネントで組み立てられており、これらのコンポーネントは他の Web アプリケーションで個々にカスタマイズしたり再利用することができます。コンポーネントは、Web アプリケーションに構造を提供する JavaScript ライブラリである BackBone に基づいています。 コンポーネントと BackBone の相互作用を説明する詳細な記事は次のとおりです。 [ここ](/help/forms/using/backbone-interaction.md). CRX フォルダー構造内のコンポーネントの構成については、で説明します。 [この](/help/forms/using/folder-structure.md) 記事。

AEM Forms Workspace 用に配信されたパッケージ：

* `adobe-lc-workspace-pkg-<version>.zip`：これは CRX パッケージです。すなわち、Package Manager を使用して CRX 内にデプロイできます。
* `adobe-lc-workspace-<version>-src.zip`：デプロイパッケージ（Ship、Debug、および Dev パッケージ）を作成するための AEM Forms Workspace とスクリプトの完全なコードを含むアーカイブです。
