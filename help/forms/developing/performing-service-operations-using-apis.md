---
title: API を使用したサービス操作の実行
description: AEM Forms API を使用してクライアントアプリケーションを開発してください。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 62489194-82ca-44f6-b5be-4411c95f6f80
source-git-commit: a56d5121a6ce11b42a6c30dae9e479564d16af27
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 52%

---

# API を使用したサービス操作の実行 {#performing-service-operations-using-apis}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

AEM Forms API を使用してクライアントアプリケーションの開発を開始する前に、まずAEM Formsの呼び出しをお読みください。ここでは、サービスを呼び出す様々な方法について説明しています。 （ [サービスコンテナ](/help/forms/developing/service-container.md#service-container)を参照。）

様々な呼び出し方法に慣れたら、各サービスをプログラムで操作する方法を学ぶことができます。クライアントアプリケーションは、AdobeFlex® Builder™、Java™開発環境、またはMicrosoft® Visual Studio .NET などの環境で開発できます。この環境では、ネイティブの SOAP スタックでの使用に公開された WSDL を使用できます。

各トピックには、基本的な情報（手順の概要セクションを含む）、コードのチュートリアル、およびコード例が含まれています。手順の概要では、必要なサブタスクと、各サブタスクがコードの手順のセクションにリンクされていることを説明します。 すべてのトピックにはクイックスタートへのリンクがあります。これは完全なコード例であり、コードをコピーしてプロジェクトに貼り付けることですばやく作業を開始できるように設計されています。
