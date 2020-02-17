---
title: APIを使用したAEM Formsの呼び出し
seo-title: APIを使用したAEM Formsの呼び出し
description: 'null'
seo-description: 'null'
uuid: d100e106-e508-4d3c-ba8c-b5fe13c9e2d6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: development-tools
discoiquuid: 1825e12c-0306-4e0a-9643-47ce1ce82132
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# APIを使用したAEM Formsの呼び出し {#invoking-aem-forms-using-apis}

Adobe Experience Manager Formsは、共有インフラストラクチャ内で動作するサービスで構成されるJ2EEベースのエンタープライズソフトウェアです。 サービス操作は通常、ドキュメントを使用または生成します。 AEM Formsを使用すると、フォームワークフローと電子フォーム、ドキュメントセキュリティ、ドキュメント生成を統合されたまとまったサービスのセットで組み合わせることができます。 これらのサービスは、ファイアウォールの内外からアクセスできます。

クライアントアプリケーションは、Java API、Webサービス、Remoting、RESTを使用してAEM Formsサービスをプログラムで呼び出すことができます。 管理コンソールを使用して、AEM Formsサービスをプログラム的に呼び出すことでAEM Formsサービスを公開できるエンドポイントを公開するようにサービスを設定できます。 デフォルトでは、ほとんどのサービスは、Remoting、JavaおよびWebサービスエンドポイントを公開するように事前に設定されています。

使用する呼び出し方法は、ビジネス要件によって決まります。 例えば、Java APIを使用して、JavaエンティティーやメッセージBeanなどのJavaエンタープライズアプリケーションにAEM Forms機能を統合できます。 同様に、Webサービスを使用して、AEM Formsの機能を.NETプロジェクト（または、Webサービス標準をサポートする開発環境で開発された他のプロジェクト）に統合できます。

Enterprise javaBeans™(EJB)でJ2EEコンテナが必要な場合と同様に、サービスコンテナを実行する必要があります。 AEM Formsには、サービスコンテナの実装が1つだけ含まれています。 サービスコンテナは、サービスのデプロイや、すべての要求が正しいサービスに送信されることを含む、サービスの有効期間を管理する役割を持ちます。 また、サービスが使用または生成するドキュメントも管理します。

>[!NOTE]
>
>AEM Formsによるプログラミングには、監視フォルダーや電子メールを使用したAEM formsの呼び出し方法に関する情報は含まれません。

