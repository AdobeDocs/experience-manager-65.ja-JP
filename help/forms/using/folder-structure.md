---
title: フォルダー構造について
seo-title: フォルダー構造について
description: AEM Forms Workspace ソースコードのフォルダー構造を理解してカスタマイズする方法。
seo-description: AEM Forms Workspace ソースコードのフォルダー構造を理解してカスタマイズする方法。
uuid: ee844f89-887e-4f07-9db3-389859baa374
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 7427858d-8eec-423d-a0a9-444140420620
exl-id: a4c1d3d8-477e-4edf-9dde-4ef9c766be5a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 66%

---

# フォルダー構造について  {#understanding-the-folder-structure}

AEM Forms Workspace は Backbone を使用して MVC アーキテクチャ上で設計されています。各コンポーネントは次のものに対してファイルを持ちます。

* ビジネスロジックを含むモデル 。
* インターフェイスコントロールを含む HTML ファイルであるテンプレート。
* コントローラークラスとしてテンプレートに対して動作する表示。

すべてのコンポーネントのアセットは、以下に示すフォルダー構造内に配置されています。アセットにアクセスするには、CRXDE Liteにログインし、`/libs/ws/js/runtime/`を参照します。

**** modelsバックボーンモデルが含まれます。

**** viewsBackboneビューを含みます。

**** templatesコンポーネントのHTMLテンプレートのみが含まれます。

**** routesContains universal routes.routes 内部の Templates フォルダーには、HTML コードとコンポーネントへの参照が含まれます。

**** servicesRESTエンドポイントでAdobe Experience ManagerサーバーAPIを呼び出すためのサービスインターフェイスが含まれます。

**** utilContains複数のコンポーネントで使用できる汎用ユーティリティ。
