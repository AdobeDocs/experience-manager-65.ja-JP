---
title: フォルダー構造について
description: カスタマイズするAEM Forms Workspace ソースコードのフォルダー構造を理解する方法です。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: a4c1d3d8-477e-4edf-9dde-4ef9c766be5a
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 53%

---

# フォルダー構造について {#understanding-the-folder-structure}

AEM Forms Workspace コンポーネントは、Backbone を使用した MVC アーキテクチャ上で設計されています。 各コンポーネントには、次の用のファイルがあります。

* ビジネスロジックを含むモデル。
* インターフェイスコントロールを含むHTMLファイルです。
* テンプレートに対するコントローラクラスとして機能する表示。

すべてのコンポーネントのアセットは、以下に説明するフォルダー構造に配置されます。 アセットにアクセスするには、CRXDE Lite にログインし、`/libs/ws/js/runtime/` を参照します。

**models**：バックボーンモデルが含まれます。

**views**：バックボーンビューが含まれます。

**templates**：コンポーネント用の HTML テンプレートのみが含まれます。

**routes**：ユニバーサルルートが含まれます。routes 内部の Templates フォルダーには、HTML コードとコンポーネントへの参照が含まれます。

**services**：REST エンドポイント上の Adobe Experience Manager サーバーの API を呼び出すためのサービスインターフェイスが含まれます。

**util**：複数のコンポーネントによって使用可能な一般ユーティリティが含まれます。
