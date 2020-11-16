---
title: エンドポイントの種類
seo-title: エンドポイントの種類
description: 様々なエンドポイントの種類について説明します。
seo-description: 様々なエンドポイントの種類について説明します。
uuid: c899245c-14cc-4035-9440-95a5b6c1e47f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8fe572e0-8a53-4129-940f-3fdb990073fe
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 59%

---


# エンドポイントの種類 {#types-of-endpoints}

サービスを使用する前に、エンドポイントを設定して有効にする必要があります。エンドポイントには、サービスを呼び出す方法が指定されています。

>[!NOTE]
>
>Workbench でエンドポイントは開始点と呼ばれます。

次の種類のエンドポイントをサービスに追加できます。すべてのエンドポイントをサポートしていないサービスもあります。

**電子メール：** 1つ以上の添付ファイルを含む電子メールメッセージを指定した電子メールアカウントに送信することで、ユーザーがサービスを呼び出せるようにします。 電子メールエンドポイントを設定する前に、必要な電子メールアカウントを設定する必要があります（電子メールエンドポイントの設定を参照）。

**監視フォルダー：** ユーザーがファイルを定義された間隔でスキャンされるフォルダーに配置することで、サービスを呼び出せるようにします。 （監視フォルダーエンドポイントの設定を参照）。

**TaskManager:** Workspaceユーザーがサービスを呼び出せるようにします。

**Remoting:** Flexで作成されたアプリケーションから、(AEM formsでは廃止されています)AEM forms Remotingを使用してサービスを呼び出せるようにします。 リモートエンドポイントは、アクティブ化された各サービスに対して自動的に作成されます。エンドポイントと同じ名前を持つ Flex の宛先が作成され、Flex クライアントは、関連するサービスの操作を呼び出すために、この宛先を指すリモートオブジェクトを作成できます。

**SOAP:** AEM formsプログラミングAPIを使用して開発されたクライアントアプリケーションから、SOAPモードを使用してサービスを呼び出せるようにします。 SOAP エンドポイントは、アクティブ化された各サービスに対して自動的に作成されます。

**注意**: *Adobe AcrobatまたはAdobe Readerでドキュメントを表示中にSOAPエンドポイントが使用される場合、セキュリティはドキュメントセキュリティドキュメントから削除できます。 LCRM ドキュメントで SOAP エンドポイントを無効にする方法について詳しくは、「[Document Security ドキュメントの SOAP エンドポイントの無効化](/help/forms/using/admin-help/configuring-client-server-options.md#disable-soap-endpoints-for-document-security-documents)*」を参照してください。

**EJB:** AEM formsプログラミングAPIを使用して開発されたクライアントアプリケーションから、Enterprise JavaBeans(EJB)モードを使用してサービスを呼び出せるようにします。 EJB エンドポイントは、アクティブ化された各サービスに対して自動的に作成されます。

**WSDL:** AEM formsプログラミングAPIを使用して開発されたクライアントアプリケーションから、Web Service Definition Language(WSDL)を使用してサービスを呼び出せるようにします。 コア設定ページには、AEM Forms に属するすべてのサービスで WSDL の生成を有効にするオプションが含まれています（一般的な AEM Forms の設定を参照してください。）

**REST:** Representational State Transfer(REST)要求を介して呼び出せるように、Workbenchで作成されたプロセスを設定できます。 REST 要求は HTML ページから送信されます。つまり、REST 要求を使用して、Web ページから直接 AEM Forms プロセスを呼び出すことができます。

電子メール、タスクマネージャー、監視フォルダーおよびリモートの各エンドポイントによって使用可能になるのは、サービスの特定の操作だけです。これらのエンドポイントを追加する場合は、サービスの呼び出し方法の選択、設定パラメーターの指定、入力および出力のパラメーターマッピングの指定を行うので、もう一段階の設定手順が必要になります。
