---
title: Document Securityサーバーのインストールと設定
seo-title: Document Securityサーバーのインストールと設定
description: 'Document Securityを使用して、サポートされている形式で保存した情報を安全に配布します。 許可されたユーザーのみが保護されたドキュメントにアクセスできます。 '
seo-description: 'Document Securityを使用して、サポートされている形式で保存した情報を安全に配布します。 許可されたユーザーのみが保護されたドキュメントにアクセスできます。 '
uuid: 04c67a84-01ad-45b7-a590-822b1c067d52
contentOwner: khsingh
discoiquuid: 600d13e7-6655-41c5-aab4-c8e9e2a8d14f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Document Securityサーバーのインストールと設定 {#installing-and-configuring-the-document-security-server}

Document Securityを使用して、サポートされている形式で保存した情報を安全に配布します。 許可されたユーザーのみが保護されたドキュメントにアクセスできます。

Adobe Experience Manager Forms の Document Security を使用して、許可されたユーザーだけがドキュメントを使用するように指定できます。Document Security を使用すると、サポートされる形式で保存した情報を安全に配布できます。Adobe Portable Document Format （PDF）、Microsoft Word、Excel および PowerPoint を含むファイル形式に対応しています。

ドキュメントを保護するには、ポリシーを使用します。ポリシーに指定する機密設定によって、ポリシーを適用したドキュメントを受信者が使用できる方法が決まります。例えば、テキストの印刷やコピー、テキストの編集、または保護されたドキュメントへの署名や注釈の追加を実行できるかどうかを指定することができます。

ポリシーは Document Security に保存されます。クライアントアプリケーションを使用してそのポリシーをドキュメントに適用します。ドキュメントにポリシーを適用すると、ドキュメントに含まれる情報は、ポリシーで指定されている機密設定で保護されます。ポリシーで保護されたドキュメントを、ポリシーで許可された受信者に配布できます。

また、Document Securityは、ドキュメントの保護、保護されたドキュメントの表示、および保護されたドキュメントのインデックス作成を行うクライアント、ビューアおよびインデクサーも提供します。 Document Securityについて詳しくは、Document Securityについてを [参照してください](/help/forms/using/admin-help/document-security.md)。

## デプロイメントトポロジ  {#deployment-topology}

Document Security機能は、JEE上のAEM Formsでのみ使用できます。 JEE上のAEM Formsのインスタンスは1つだけ必要です。 必要に応じて、AEM Formsサーバーのクラスターまたはファームを作成することもできます。 次のトポロジは、Document Security機能を実行するトポロジを示しています。 トポロジーについて詳しくは、「[AEM Forms のアーキテクチャとデプロイメントトポロジー](aem-forms-architecture-deployment.md)」を参照してください。

<!--fix above link-->

![](do-not-localize/document-security-server_topology.png)

次の図は、AEM Forms Document Security の一般的なアーキテクチャを示しています。

![](do-not-localize/document-security-typical-environment.png)

## JEE上のAEM Formsのインストール {#installing-aem-forms-on-jee}

JEE上のAEM Formsをインストールして設定するには、次の手順を実行します。

1. JEE 上の AEM 6.5 Forms のインストーラーを、[アドビライセンス Web サイト（LWS）](https://licensing.adobe.com/)からダウンロードします。インストーラーをダウンロードするには、有効なメンテナンス＆サポートの契約が必要です。
1. 『 [JEE上の](/help/forms/using/aem-forms-jee-supported-platforms.md) AEM Formsサポート対象プラットフォーム』ドキュメントを読み、JEE上のAEM formsをインストールするためのソフトウェア、ハードウェア、オペレーティングシステム、アプリケーションサーバー、データベース、JDK、その他のインフラストラクチャが用意されていることを確認します。
1. （自動インストール以外のインストールのみ）「 [AEM Formsシングルサーバーのインストールの準備](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64) 」または「AEM Formsサーバークラスターのインストールの準備 [](https://www.adobe.com/go/learn_aemforms_prepareInstallcluster_64) 」を読み、JEE上のAEM Formsのインストールと設定の準備を行います。
1. 環境とアプリケーションサーバーに応じて、次のドキュメントのいずれかを選択し、指示に従ってインストールを完了します

   * [JEE 上の AEM Forms のインストールとデプロイ（JBoss 自動インストールを使用）](https://www.adobe.com/go/learn_aemforms_installTurnkey_64)
   * [JEE 上の AEM Forms のインストールとデプロイ（JBoss 版）](https://www.adobe.com/go/learn_aemforms_installJBoss_64)
   * [JEE 上の AEM Forms のインストールおよびデプロイ（WebLogic 版）](https://www.adobe.com/go/learn_aemforms_installWebLogic_64)
   * [JEE 上の AEM Forms のインストールおよびデプロイ（WebSphere 版）](https://www.adobe.com/go/learn_aemforms_installWebSphere_64)
   * [JBoss クラスター上の JEE での AEM Forms の設定](https://www.adobe.com/go/learn_aemforms_clusterJBoss_64)
   * [WebLogic クラスターでの AEM Forms の設定](https://www.adobe.com/go/learn_aemforms_clusterWebLogic_64)
   * [WebSphere クラスターでの JEE 上の AEM Forms の設定](https://www.adobe.com/go/learn_aemforms_clusterWebSphere_64)
   >[!NOTE]
   >
   >JEE上のAEM Forms Configuration Managerのモジュール選択画面で、「Document Security」オプションを選択します。 「Document Security」オプションを選択する場合は、他のモジュールを選択する必要はありません。

## 次の手順 {#next-steps}

* [クライアントとサーバーのオプションの設定](/help/forms/using/admin-help/configuring-client-server-options.md)
* [ポリシーの作成と管理](/help/forms/using/admin-help/creating-policies.md)
* [ポリシーセットの作成と管理](/help/forms/using/admin-help/creating-policy-sets.md)
