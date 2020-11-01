---
title: APIを使用したAEM Formsの呼び出し
seo-title: APIを使用したAEM Formsの呼び出し
description: APIを使用したAEM Formsの呼び出し
uuid: d100e106-e508-4d3c-ba8c-b5fe13c9e2d6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
discoiquuid: 1825e12c-0306-4e0a-9643-47ce1ce82132
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---


# APIを使用したAEM Formsの呼び出し {#invoking-aem-forms-using-apis}

Adobe Experience Manager Formsは、共有インフラストラクチャ内で動作するサービスで構成されるJ2EEベースのエンタープライズソフトウェアです。 サービス操作は、通常、ドキュメントを消費または生産します。 AEM Formsを使用すると、フォームワークフローと電子フォーム、ドキュメントセキュリティ、ドキュメント生成を組み合わせて、統合されたまとまったサービスのセットを作成できます。 これらのサービスは、ファイアウォールの内外からアクセスできます。

クライアントアプリケーションは、Java API、Webサービス、Remoting、およびRESTを使用して、AEM Formsサービスをプログラムで呼び出すことができます。 管理コンソールを使用して、AEM Formsサービスをプログラム的に呼び出すことで可能にするエンドポイントを公開するようにサービスを設定できます。 デフォルトでは、ほとんどのサービスは、リモート、Java、Webサービスのエンドポイントを公開するように事前に設定されています。

使用する呼び出し方法は、ビジネス要件によって決まります。 例えば、Java APIを使用すると、JavaエンティティやメッセージBeanなどのJavaエンタープライズアプリケーションにAEM Forms機能を統合できます。 同様に、AEM Forms機能をWebサービスを使用して.NETプロジェクト(または、Webサービス標準をサポートする開発環境で開発された他のプロジェクト)に統合できます。

サービスを実行するには、Enterprise JavaBeans™(EJB)がJ2EEコンテナを必要とするのと同じように、サービスコンテナが必要です。 AEM Formsでは、サービスコンテナの実装が1つだけ含まれています。 サービスコンテナは、サービスのデプロイや、すべての要求が正しいサービスに送信されるような、サービスの有効期間を管理する役割を持ちます。 また、サービスが消費または生成するドキュメントも管理します。

>[!NOTE]
>
>AEM Formsを使用したプログラミングには、監視フォルダーや電子メールを使用したAEM Formsの呼び出し方法に関する情報は含まれていません。

