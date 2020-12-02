---
title: ドキュメントセキュリティサーバーのインストールと設定
seo-title: ドキュメントセキュリティサーバーのインストールと設定
description: 'ドキュメントセキュリティを使用して、サポートされている形式で保存した情報を安全に配布します。 保護されたドキュメントにアクセスできるのは、許可されたユーザーのみです。 '
seo-description: 'ドキュメントセキュリティを使用して、サポートされている形式で保存した情報を安全に配布します。 保護されたドキュメントにアクセスできるのは、許可されたユーザーのみです。 '
uuid: 04c67a84-01ad-45b7-a590-822b1c067d52
contentOwner: khsingh
discoiquuid: 600d13e7-6655-41c5-aab4-c8e9e2a8d14f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 42%

---


# ドキュメントセキュリティサーバーのインストールと設定{#installing-and-configuring-the-document-security-server}

ドキュメントセキュリティを使用して、サポートされている形式で保存した情報を安全に配布します。 保護されたドキュメントにアクセスできるのは、許可されたユーザーのみです。

Adobe Experience Manager Forms の Document Security を使用して、許可されたユーザーだけがドキュメントを使用するように指定できます。Document Security を使用すると、サポートされる形式で保存した情報を安全に配布できます。Adobe Portable Document Format （PDF）、Microsoft Word、Excel および PowerPoint を含むファイル形式に対応しています。

ドキュメントを保護するには、ポリシーを使用します。ポリシーに指定する機密設定によって、ポリシーを適用したドキュメントを受信者が使用できる方法が決まります。例えば、テキストの印刷やコピー、テキストの編集、または保護されたドキュメントへの署名や注釈の追加を実行できるかどうかを指定することができます。

ポリシーは Document Security に保存されます。クライアントアプリケーションを使用してそのポリシーをドキュメントに適用します。ドキュメントにポリシーを適用すると、ドキュメントに含まれる情報は、ポリシーで指定されている機密設定で保護されます。ポリシーで保護されたドキュメントを、ポリシーで許可された受信者に配布できます。

ドキュメントセキュリティは、ドキュメント、表示で保護されたドキュメント、インデックスで保護されたドキュメントを保護するクライアント、ビューア、インデクサーも提供します。 ドキュメントセキュリティについて詳しくは、[ドキュメントセキュリティ](/help/forms/using/admin-help/document-security.md)を参照してください。

## デプロイメントトポロジ  {#deployment-topology}

ドキュメントセキュリティ機能は、JEE上のAEM Formsでのみ使用できます。 JEE上のAEM Formsのインスタンスは1つだけ必要です。 必要に応じて、AEM Formsサーバーのクラスターまたはファームを作成することもできます。 次のトポロジは、ドキュメントセキュリティ機能を実行するトポロジーを示しています。 トポロジーについて詳しくは、「[AEM Forms のアーキテクチャとデプロイメントトポロジー](aem-forms-architecture-deployment.md)」を参照してください。

<!--fix above link-->

![](do-not-localize/document-security-server_topology.png)

次の図は、AEM Forms Document Security の一般的なアーキテクチャを示しています。

![](do-not-localize/document-security-typical-environment.png)

## JEEへのAEM Formsのインストール{#installing-aem-forms-on-jee}

次の手順を実行して、JEE上のAEM Formsをインストールおよび設定します。

1. JEE 上の AEM 6.5 Forms のインストーラーを、[アドビライセンス Web サイト（LWS）](https://licensing.adobe.com/)からダウンロードします。インストーラーをダウンロードするには、有効なメンテナンス＆サポートの契約が必要です。
1. [JEEサポート対象プラットフォームのAEM Formsドキュメント](/help/forms/using/aem-forms-jee-supported-platforms.md)を読み、JEEにAEM Formsをインストールする準備ができたソフトウェア、ハードウェア、オペレーティングシステム、アプリケーションサーバー、データベース、JDK、およびその他のインフラストラクチャを確認します。
1. （自動インストール以外のインストールの場合のみ）「[AEM Formsシングルサーバーのインストールの準備](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64)」または「[AEM Formsサーバークラスターのインストールの準備](https://www.adobe.com/go/learn_aemforms_prepareInstallcluster_64)」を読み、環境のJEEへのAEM Formsのインストールと設定の準備を行います。
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
   >JEE Configuration ManagerのAEM Formsのモジュール選択画面で、「ドキュメントセキュリティ」オプションを選択します。 「ドキュメントセキュリティ」オプションでは、他のモジュールを選択する必要はありません。

## 次の手順 {#next-steps}

* [クライアント/サーバーオプションの設定](/help/forms/using/admin-help/configuring-client-server-options.md)
* [ポリシーの作成と管理](/help/forms/using/admin-help/creating-policies.md)
* [ポリシーセットの作成と管理](/help/forms/using/admin-help/creating-policy-sets.md)
