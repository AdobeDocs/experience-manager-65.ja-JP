---
title: Document Securityサーバーのインストールと設定
seo-title: Document Securityサーバーのインストールと設定
description: 'Document Securityを使用して、サポートされている形式で保存した情報を安全に配布します。 権限を持つユーザーのみが、保護されたドキュメントにアクセスできます。 '
seo-description: 'Document Securityを使用して、サポートされている形式で保存した情報を安全に配布します。 権限を持つユーザーのみが、保護されたドキュメントにアクセスできます。 '
uuid: 04c67a84-01ad-45b7-a590-822b1c067d52
contentOwner: khsingh
discoiquuid: 600d13e7-6655-41c5-aab4-c8e9e2a8d14f
role: Administrator
exl-id: 4a4bad4a-3e68-43cb-b55c-03b509a5d304
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 42%

---

# Document Securityサーバー{#installing-and-configuring-the-document-security-server}のインストールと設定

Document Securityを使用して、サポートされている形式で保存した情報を安全に配布します。 権限を持つユーザーのみが、保護されたドキュメントにアクセスできます。

Adobe Experience Manager Forms の Document Security を使用して、許可されたユーザーだけがドキュメントを使用するように指定できます。Document Security を使用すると、サポートされる形式で保存した情報を安全に配布できます。Adobe Portable Document Format （PDF）、Microsoft Word、Excel および PowerPoint を含むファイル形式に対応しています。

ドキュメントを保護するには、ポリシーを使用します。ポリシーに指定する機密設定によって、ポリシーを適用したドキュメントを受信者が使用できる方法が決まります。例えば、テキストの印刷やコピー、テキストの編集、または保護されたドキュメントへの署名や注釈の追加を実行できるかどうかを指定することができます。

ポリシーは Document Security に保存されます。クライアントアプリケーションを使用してそのポリシーをドキュメントに適用します。ドキュメントにポリシーを適用すると、ドキュメントに含まれる情報は、ポリシーで指定されている機密設定で保護されます。ポリシーで保護されたドキュメントを、ポリシーで許可された受信者に配布できます。

また、ドキュメントの保護、保護されたドキュメントの表示、および保護されたドキュメントのインデックス作成を行うためのクライアント、ビューア、およびインデクサーも提供します。 Document Securityについて詳しくは、[Document Security](/help/forms/using/admin-help/document-security.md)についてを参照してください。

## デプロイメントトポロジ  {#deployment-topology}

Document Security機能は、JEE上のAEM Formsでのみ使用できます。 JEE上のAEM Formsのインスタンスが1つ必要です。 必要に応じて、AEM Formsサーバーのクラスターまたはファームを作成することもできます。 次のトポロジは、Document Security機能を実行するための指標トポロジです。 トポロジーについて詳しくは、「[AEM Forms のアーキテクチャとデプロイメントトポロジー](aem-forms-architecture-deployment.md)」を参照してください。

<!--fix above link-->

![](do-not-localize/document-security-server_topology.png)

次の図は、AEM Forms Document Security の一般的なアーキテクチャを示しています。

![](do-not-localize/document-security-typical-environment.png)

## JEEへのAEM Formsのインストール{#installing-aem-forms-on-jee}

次の手順を実行して、JEE上のAEM Formsをインストールして設定します。

1. JEE 上の AEM 6.5 Forms のインストーラーを、[アドビライセンス Web サイト（LWS）](https://licensing.adobe.com/)からダウンロードします。インストーラーをダウンロードするには、有効なメンテナンス＆サポートの契約が必要です。
1. 「JEE上のAEM Formsのサポート対象プラットフォーム」のドキュメント](/help/forms/using/aem-forms-jee-supported-platforms.md)を読み、JEE上のAEM Formsをインストールするためのソフトウェア、ハードウェア、オペレーティングシステム、アプリケーションサーバー、データベース、JDK、その他のインフラストラクチャを確認します。[
1. （自動インストール以外のインストールの場合のみ）「 [AEM Formsシングルサーバーのインストールの準備](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64) 」または「 [AEM Formsサーバークラスターのインストールの準備](https://www.adobe.com/go/learn_aemforms_prepareInstallcluster_64) 」を読み、JEE上のAEM Formsのインストールと設定の準備を行います。
1. 環境とアプリケーションサーバーに応じて、次のいずれかのドキュメントを選択し、指示に従ってインストールを完了します

   * [JEE 上の AEM Forms のインストールとデプロイ（JBoss 自動インストールを使用）](https://www.adobe.com/go/learn_aemforms_installTurnkey_64)
   * [JEE 上の AEM Forms のインストールとデプロイ（JBoss 版）](https://www.adobe.com/go/learn_aemforms_installJBoss_64)
   * [JEE 上の AEM Forms のインストールおよびデプロイ（WebLogic 版）](https://www.adobe.com/go/learn_aemforms_installWebLogic_64)
   * [JEE 上の AEM Forms のインストールおよびデプロイ（WebSphere 版）](https://www.adobe.com/go/learn_aemforms_installWebSphere_64)
   * [JBoss クラスター上の JEE での AEM Forms の設定](https://www.adobe.com/go/learn_aemforms_clusterJBoss_64)
   * [WebLogic クラスターでの AEM Forms の設定](https://www.adobe.com/go/learn_aemforms_clusterWebLogic_64)
   * [WebSphere クラスターでの JEE 上の AEM Forms の設定](https://www.adobe.com/go/learn_aemforms_clusterWebSphere_64)

   >[!NOTE]
   >
   >JEE上のAEM Forms Configuration Managerのモジュール選択画面で、「Document Security」オプションを選択します。 「Document Security」オプションを選択するために、他のモジュールは必要ありません。

## 次の手順 {#next-steps}

* [クライアントおよびサーバーオプションの設定](/help/forms/using/admin-help/configuring-client-server-options.md)
* [ポリシーの作成と管理](/help/forms/using/admin-help/creating-policies.md)
* [ポリシーセットの作成と管理](/help/forms/using/admin-help/creating-policy-sets.md)
