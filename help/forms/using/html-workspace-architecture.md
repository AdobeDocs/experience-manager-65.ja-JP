---
title: AEM Forms Workspace のアーキテクチャ
seo-title: AEM Forms Workspace のアーキテクチャ
description: LiveCycle AEM Forms workspace の概要と概念情報です。
seo-description: LiveCycle AEM Forms workspace の概要と概念情報です。
uuid: e1a48452-ed44-4ea7-ba38-d961c8faafa5
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c3a312fb-f684-477d-916d-2d3c99aa7607
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# AEM Forms Workspace のアーキテクチャ {#aem-forms-workspace-architecture}

AEM Forms Workspace は、CRX™ にホスティングされている Web アプリケーションです。ワークスペースがサポートされているブラウザーで開かれると、CRX リソースがアクセスされ、アプリケーションがブラウザー内で HTML ページとしてレンダリングされます。

アプリケーションは REST エンドポイント上にある AEM Forms サーバーにアクセスして、次のことを行います。

* ユーザーのタスク、プロセススタートポイント、プロセス履歴、およびユーザー情報の取得
* タスクに対する実行
* データベースでのクエリータスク
* ユーザーの環境設定の更新など

AEM Forms サーバーは、JDBC を通して AEM Forms データベースにアクセスします。データベースは、タスク、プロセスとそのインスタンス、ユーザー、および関連情報を維持します。

AEM Forms Workspaceは、モジュール式のJavaScript™コンポーネントで構成されており、これらのコンポーネントは、他のWebアプリケーションで個別にカスタマイズしたり、再利用したりできます。 コンポーネントは Web アプリケーションに構造を提供する JavaScript ライブラリである BackBone に基づいています。コンポーネントと BackBone とのインタラクションを説明する記事の詳細については、[ここ](/help/forms/using/backbone-interaction.md)を参照してください。CRX フォルダー構造のコンポーネントの組織については、[この記事](/help/forms/using/folder-structure.md)で説明しています。

AEM Forms Workspace のために配信されるパッケージを以下に示しています。

* `adobe-lc-workspace-pkg-<version>.zip`：これは CRX パッケージです。すなわち、Package Manager を使用して CRX 内にデプロイできます。
* `adobe-lc-workspace-<version>-src.zip`:これは、デプロイパッケージ（Ship、Debug、Devの各パッケージ）を作成するためのAEM Forms Workspaceとスクリプトの完全なコードを含むアーカイブです。
