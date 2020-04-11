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
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# フォルダー構造について {#understanding-the-folder-structure}

AEM Forms Workspace は Backbone を使用して MVC アーキテクチャ上で設計されています。各コンポーネントは次のものに対してファイルを持ちます。

* ビジネスロジックを含むモデル 。
* インターフェイスコントロールを含む HTML ファイルであるテンプレート。
* コントローラークラスとしてテンプレートに対して動作する表示。

すべてのコンポーネントのアセットは、以下に示すフォルダー構造内に配置されています。To access the assets, log in to CRXDE Lite and browse to `/libs/ws/js/runtime/`.

**models** ：バックボーンモデルを含みます。

**表示** ：バックボーン表示を含む。

**templates** ：コンポーネントのHTMLテンプレートのみが含まれます。

**routes** ：ユニバーサルルートを含みます。 routes 内部の Templates フォルダーには、HTML コードとコンポーネントへの参照が含まれます。

**services** RESTエンドポイントでAdobe Experience ManagerサーバーAPIを呼び出すためのサービスインターフェイスが含まれます。

**util** ：複数のコンポーネントで使用できる汎用ユーティリティを含みます。
