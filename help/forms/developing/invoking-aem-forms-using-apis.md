---
title: API を使用した AEM Forms の呼び出し方法？
description: Java&trade; API、web サービス、Remoting、REST を使用した AEM Forms サービスの呼び出し方法について説明します。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
role: Developer
exl-id: 0e92d1ad-12bd-4bfd-81cc-9be8e376c5ca
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 939a2efa64c853928a9082aa30d7338e98deb695
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 100%

---

# API を使用した AEM Forms の呼び出し {#invoking-aem-forms-using-apis}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

Adobe Experience Manager Forms は、共有インフラストラクチャで操作されるサービスからなる、J2EE ベースのエンタープライズソフトウェアです。サービス操作では、通常、 ドキュメントを使用または生成します。AEM Forms を使用すると、統合され凝縮された一連のサービスにより、Forms Workflow と電子フォーム、ドキュメントセキュリティ、ドキュメント生成を組み合わせることができます。これらのサービスへは、ファイアウォールの内側からでも外側からでもアクセスできます。

クライアントアプリケーションは、Java™ API、web サービス、Remoting、REST を使用することにより、AEM Forms サービスをプログラムで呼び出すことができます。管理コンソールを使用してサービスを設定すると、AEM Forms サービスをプログラムで呼び出せるエンドポイントを公開できます。デフォルトでは、ほとんどのサービスは、Remoting、Java™、web サービスの各エンドポイントを公開するように事前に設定されています。

ビジネス要件に応じて、使用する呼び出し方法を決定します。例えば、Java™ API を使用すると、Java™ エンティティやメッセージ Bean などの Java™ エンタープライズアプリケーションに AEM Forms 機能を統合できます。同様に、web サービスを使用して、AEM Forms 機能を .NET プロジェクト（または、web サービス標準をサポートする開発環境で開発された他のプロジェクト）に統合できます。

サービスを実行するには、Enterprise JavaBeans™（EJB）が J2EE コンテナを必要とするのと同様に、サービスコンテナが必要です。AEM Forms に含まれているサービスコンテナの実装は 1 つのみです。サービスコンテナは、サービスのデプロイや、すべてのリクエストが正しいサービスに送信されるようにするなど、サービスの全期間を管理する役割を担います。サービスが使用または生成するドキュメントも管理します。

>[!NOTE]
>
>AEM Forms によるプログラミングには、監視フォルダーやメールを使用した AEM Forms の呼び出し方法に関する情報は含まれていません。
