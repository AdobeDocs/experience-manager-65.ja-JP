---
title: グローバルドキュメントストレージディレクトリ
description: グローバルドキュメントストレージ（GDS）ディレクトリは、プロセス内で使用される長期間有効なファイルの保存に使用されるディレクトリです。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7a64a643-808b-4644-8fd3-0dafe83e8dd9
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 100%

---

# グローバルドキュメントストレージディレクトリ{#global-document-storage-directory}

*グローバルドキュメントストレージ（GDS）*&#x200B;ディレクトリは、プロセス内で使用される長期間有効なファイルの保存に使用されるディレクトリです。該当するファイルには、PDF、ポリシーおよびフォームテンプレートなどがあります。長期間有効なファイルは、多くの AEM Forms デプロイメントの全体的な状態の中で重要な部分です。長期間有効なドキュメントが一部でも失われたり破損したりすると、Forms サーバーが不安定な状態になる可能性があります。非同期ジョブの呼び出しの入力ドキュメントも GDS ディレクトリに保存されます。これらのドキュメントは、リクエストを処理するために使用可能な状態になっている必要があります。GDS ディレクトリをホストするファイルシステムの信頼性を考慮することが重要です。品質やサービスのレベルのニーズに適した RAID（Redundant Array of Independent Disks）またはその他のテクノロジーを使用します。

長期間有効なファイルには、機密性の高いユーザー情報が含まれる場合があります。この情報では、AEM Forms API またはユーザーインターフェイスを使用してアクセスするときに特殊な証明書が必要となる場合があります。オペレーティングシステムによって GDS ディレクトリが適切に保護されていることが重要です。アプリケーションサーバーを実行するために使用される管理者アカウントのみに対して、GDS ディレクトリの読み取りと書き込みのアクセス権を付与する必要があります。

GDS の可用性が高い保護されたディレクトリを選択するほかに、データベースでドキュメントの保存を有効にすることもできます。ドキュメントの保存に AEM Forms データベースを使用しても、AEM Forms には GDS ディレクトリが必要となります（[ドキュメントの保存にデータベースを使用する場合のバックアップオプション](/help/forms/using/admin-help/files-back-recover.md#backup-options-when-database-is-used-for-document-storage)を参照）。

AEM Forms アプリケーションデータは、GDS ディレクトリおよび AEM Forms データベースに格納されています。次の表では、データとその格納場所を示します。

<table>
 <thead>
  <tr>
   <th><p>AEM Forms データ</p></th>
   <th><p>データベース</p></th>
   <th><p>GDS</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>アプリケーションデータ（ユーザー、ロール、プロセス、ポリシー、エンドポイント、イベントなど）</p></td>
   <td><p>はい</p></td>
   <td><p>いいえ</p></td>
  </tr>
  <tr>
   <td><p>デプロイされたサービスコンテナ</p></td>
   <td><p>はい</p></td>
   <td><p>いいえ</p></td>
  </tr>
  <tr>
   <td><p>Document Manager </p></td>
   <td><p>いいえ</p></td>
   <td><p>はい</p></td>
  </tr>
  <tr>
   <td><p>Forms リポジトリ</p></td>
   <td><p>はい</p></td>
   <td><p>いいえ</p></td>
  </tr>
  <tr>
   <td><p>システム設定</p></td>
   <td><p>はい</p></td>
   <td><p>いいえ</p></td>
  </tr>
  <tr>
   <td><p>監視フォルダー</p></td>
   <td><p>いいえ</p></td>
   <td><p>はい</p></td>
  </tr>
 </tbody>
</table>

## GDS ディレクトリの設定 {#configuring-the-gds-directory}

GDS ディレクトリの場所は、AEM Forms のインストール時に手動で設定できます。インストール時に場所を指定しないと、次に示すアプリケーションサーバーのインストールディレクトリの下にあるディレクトリがデフォルトの場所になります。

* （JBoss）`[appserver root]/server/[type]/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/DocumentServer/DocumentStorage`
* （WebSphere）`[appserver root]/installedApps/adobe/'server'/DocumentStorage`

## GDS のデフォルトの場所の変更 {#change-the-default-gds-location}

AEM Forms のインストールが完了した後、管理コンソールで GDS の場所を変更できます。プロセスを完了するには、データを手動で配置し直します。

>[!NOTE]
>
>データは、次の方法で移行してください。そうしないと、データが失われます。

1. 管理コンソールにログインし、設定／コアシステム設定／設定をクリックします。
1. 「グローバルドキュメントストレージディレクトリ」ボックスに、新しい GDS ディレクトリのフルパスを入力して、「OK」をクリックします。
1. 直ちにアプリケーションサーバーを停止します。
1. 内部のディレクトリ構造はそのままにして、すべてのファイルを古い GDS ディレクトリから新しい場所に移動します。
1. アプリケーションサーバーを再起動します。

## デプロイメントファイルについて {#about-deployment-files}

AEM Forms は、サービスコンテナおよび Java 2 Platform Enterprise Edition（J2EE）EAR ファイルという 2 種類のデプロイメントファイルで構成されています。EAR ファイルは標準の J2EE アプリケーションバンドルで構成されています。これらのアプリケーションバンドルには AEM Forms のコア機能が含まれています。アプリケーションサーバー固有の EAR ファイルを次に示します。

* adobe-core-*[appserver]*.ear
* adobe-core-*[appserver]*-*[OS]*.ear

AEM Forms の実装では、アセンブリされた複数の EAR ファイルといくつかの補助ファイルを、AEM Forms ソリューションを実行する予定のアプリケーションサーバーにデプロイします。複数のモジュールを設定およびアセンブリした場合は、デプロイ可能なモジュールがデプロイ可能な EAR ファイル内にパッケージ化されます。これらのファイルをデプロイするには、ファイルを *[appserver home]*\server\all\deploy ディレクトリにコピーします。

また、モジュールおよび AEM Forms アーカイブファイルは、JAR ファイルにパッケージ化されます。これらのファイルの種類は J2EE ではないので、アプリケーションサーバーにはデプロイされません。代わりに、GDS ディレクトリにコピーされ、それらの場所への参照が AEM Forms データベースに格納されます。このため、GDS ディレクトリをクラスターのすべてのノードで共有する必要があります。すべてのノードが DSC の中央ストレージディレクトリにアクセスできることが必要です。

>[!NOTE]
>
>サービスコンテナをデプロイする前に、GDS ディレクトリの作成と設定を必ず行ってください（[GDS ディレクトリの設定](global-document-storage-directory.md#configuring-the-gds-directory)を参照）。
