---
title: フォルダー構造について
description: AEM Forms Workspace ソースコードのフォルダー構造を理解してカスタマイズする方法。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: a4c1d3d8-477e-4edf-9dde-4ef9c766be5a
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 100%

---

# フォルダー構造について {#understanding-the-folder-structure}

AEM Forms Workspace は Backbone を使用して MVC アーキテクチャ上で設計されています。各コンポーネントには次のファイルがあります。

* ビジネスロジックを含むモデル。
* インターフェイスコントロールを含む HTML ファイルであるテンプレート。
* コントローラークラスとしてテンプレートに対して動作する表示。

すべてのコンポーネントのアセットは、以下に示すフォルダー構造内に配置されています。アセットにアクセスするには、CRXDE Lite にログインし、`/libs/ws/js/runtime/` を参照します。

**models**：バックボーンモデルが含まれます。

**views**：バックボーンビューが含まれます。

**templates**：コンポーネント用の HTML テンプレートのみが含まれます。

**routes**：ユニバーサルルートが含まれます。routes 内部の Templates フォルダーには、HTML コードとコンポーネントへの参照が含まれます。

**services**：REST エンドポイント上の Adobe Experience Manager サーバーの API を呼び出すためのサービスインターフェイスが含まれます。

**util**：複数のコンポーネントによって使用可能な一般ユーティリティが含まれます。
