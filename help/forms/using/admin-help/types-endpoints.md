---
title: エンドポイントの種類
description: 様々なエンドポイントの種類について説明します。メール、監視フォルダーなど、様々な種類のエンドポイントをサービスに追加できます。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 380cab7f-e7f7-4cb7-bd20-ea530a349fac
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: ht
source-wordcount: '455'
ht-degree: 100%

---

# エンドポイントの種類 {#types-of-endpoints}

サービスを使用する前に、エンドポイントを設定して有効にする必要があります。エンドポイントには、サービスを呼び出す方法が指定されています。

>[!NOTE]
>
>Workbench では、エンドポイントは開始ポイントと呼ばれます。

次の種類のエンドポイントをサービスに追加できます。すべてのサービスですべてのエンドポイントサポートがサポートされているわけではありません。

**メール**：1 つ以上の添付ファイルがあるメールメッセージを指定されたメールアカウントに送信することで、ユーザーがサービスを呼び出せるようにします。メールエンドポイントを設定する前に、必要なメールアカウントを設定する必要があります（メールエンドポイントの設定を参照）。

**監視フォルダー**：ファイルを定義済みの間隔でスキャンされるフォルダーに配置することで、ユーザーがサービスを呼び出せるようにします。（監視フォルダーエンドポイントの設定を参照）。

**TaskManager**：Workspace ユーザーがサービスを呼び出せるようにします。

**Remoting** ：Flex で作成されたアプリケーションから AEM forms Remoting（AEM forms では非推奨）を使用してサービスを呼び出せるようにします。リモートエンドポイントは、アクティブ化された各サービスに対して自動的に作成されます。エンドポイントと同じ名前を持つ Flex の宛先が作成され、Flex クライアントは、関連するサービスの操作を呼び出すために、この宛先を指すリモートオブジェクトを作成できます。

**SOAP** ：AEM Forms プログラミング API を使用して開発されたクライアントアプリケーションから、SOAP モードを使用してサービスを呼び出せるようにします。SOAP エンドポイントは、アクティブ化された各サービスに対して自動的に作成されます。

**注意**：*Adobe Acrobat または Adobe Reader でドキュメントを表示しているときに SOAP エンドポイントが使用されると、Document Security ドキュメントからセキュリティが除去される可能性があります。LCRM ドキュメントで SOAP エンドポイントを無効にする方法について詳しくは、「[Document Security ドキュメントの SOAP エンドポイントの無効化](/help/forms/using/admin-help/configuring-client-server-options.md#disable-soap-endpoints-for-document-security-documents)*」を参照してください。

**EJB**：AEM forms プログラミング API を使用して開発されたクライアントアプリケーションから、Enterprise JavaBeans（EJB）モードを使用してサービスを呼び出せるようにします。EJB エンドポイントは、アクティブ化された各サービスに対して自動的に作成されます。

**WSDL** ：AEM Forms プログラミング API を使用して開発されたクライアントアプリケーションから、Web サービス記述言語（WSDL）を使用してサービスを呼び出せるようにします。コア設定ページには、AEM Forms に属するすべてのサービスで WSDL の生成を有効にするオプションが含まれています。（一般的な AEM Forms の設定を参照）。

**REST**：Representational State Transfer（REST）要求で呼び出せるように、Workbench で作成したプロセスを設定できます。REST リクエストは HTML ページから送信されます。つまり、REST 要求を使用して、web ページから直接 AEM Forms プロセスを呼び出すことができます。

メール、タスクマネージャー、監視フォルダーおよびリモートの各エンドポイントでは、サービスの特定の操作のみが表示されます。これらのエンドポイントを追加する場合は、サービスの呼び出し方法の選択、設定パラメーターの指定、入力および出力のパラメーターマッピングの指定を行うので、もう一段階の設定手順が必要になります。
