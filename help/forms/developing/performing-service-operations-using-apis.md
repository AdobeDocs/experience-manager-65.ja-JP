---
title: API を使用したサービス操作の実行
description: AEM Forms API を使用してクライアントアプリケーションを開発します。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 62489194-82ca-44f6-b5be-4411c95f6f80
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 100%
---
# API を使用したサービス操作の実行 {#performing-service-operations-using-apis}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

AEM Forms API を使用してクライアントアプリケーションの開発を開始する前に、まず「AEM Forms の呼び出し」を読むことをお勧めします。ここでは、サービスを呼び出す様々な方法について説明しています。 （ [サービスコンテナ](/help/forms/developing/service-container.md#service-container)を参照。）

様々な呼び出し方法に慣れたら、各サービスをプログラムで操作する方法を学ぶことができます。 クライアントアプリケーションは、Adobe Flex® Builder™、Java™ 開発環境、または Microsoft® Visual Studio .NET などの環境で開発できます。これらの環境では、ネイティブの SOAP スタックで使用するために公開された WSDL を使用できます。

各トピックには、基本的な情報（手順の概要セクションを含む）、コードのチュートリアル、およびコード例が含まれています。 手順の概要では、必要なサブタスクを説明し、各サブタスクはコードのチュートリアルのセクションにリンクしています。 すべてのトピックにはクイックスタートへのリンクがあります。クイックスタートは完全なコード例であり、コードをコピーしてプロジェクトに貼り付けるだけですばやく使い始められるように設計されています。
