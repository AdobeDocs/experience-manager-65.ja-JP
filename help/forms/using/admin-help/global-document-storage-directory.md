---
title: グローバルドキュメントストレージディレクトリ
description: グローバルドキュメントストレージ (GDS) ディレクトリは、プロセス内で使用される長期間有効なファイルの保存に使用されるディレクトリです。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7a64a643-808b-4644-8fd3-0dafe83e8dd9
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 7%

---

# グローバルドキュメントストレージディレクトリ{#global-document-storage-directory}

The *グローバルドキュメントストレージ (GDS)* directory は、プロセス内で使用される長期間有効なファイルを保存するために使用されるディレクトリです。 これらのファイルには、PDF、ポリシー、フォームテンプレートが含まれます。 長期間有効なファイルは、多くのAEM forms デプロイメントの全体的な状態の重要な部分です。 長期間有効なドキュメントの一部またはすべてが失われたり破損したりした場合は、Forms Server が不安定になる可能性があります。 非同期ジョブ呼び出しの入力ドキュメントも GDS ディレクトリに保存されます。このドキュメントを使用して要求を処理する必要があります。 GDS ディレクトリをホストするファイルシステムの信頼性を考慮することが重要です。 品質とサービスレベルのニーズに応じて、RAID(Redundant Array of Independent Disks) やその他のテクノロジーを使用します。

長期間有効なファイルには、機密性の高いユーザー情報が含まれている場合があります。 この情報には、AEM forms API またはユーザーインターフェイスを使用してアクセスする際に、特別な資格情報が必要になる場合があります。 GDS ディレクトリがオペレーティングシステムを通じて適切に保護されていることが重要です。 GDS ディレクトリへの読み取り/書き込みアクセス権を持つのは、アプリケーションサーバーの実行に使用される管理者アカウントだけです。

GDS 用の安全で可用性の高いディレクトリを選択するほか、データベースでのドキュメントの保存を有効にすることもできます。 ドキュメントの保存にAEM forms データベースを使用している場合でも、AEM forms には GDS ディレクトリが必要です。 ( 詳しくは、 [データベースをドキュメントストレージに使用する場合のバックアップオプション](/help/forms/using/admin-help/files-back-recover.md#backup-options-when-database-is-used-for-document-storage).)

AEM forms アプリケーションデータは、GDS ディレクトリとAEM forms データベースに格納されます。 次の表に、データとその場所を示します。

<table>
 <thead>
  <tr>
   <th><p>AEM forms Data</p></th>
   <th><p>データベース</p></th>
   <th><p>GDS</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>アプリケーションデータ（ユーザー、役割、プロセス、ポリシー、エンドポイント、イベントなど）</p></td>
   <td><p>はい</p></td>
   <td><p>いいえ</p></td>
  </tr>
  <tr>
   <td><p>デプロイ済みのサービスコンテナ</p></td>
   <td><p>はい</p></td>
   <td><p>いいえ</p></td>
  </tr>
  <tr>
   <td><p>Document Manager </p></td>
   <td><p>いいえ</p></td>
   <td><p>はい</p></td>
  </tr>
  <tr>
   <td><p>Forms Repository</p></td>
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

GDS ディレクトリの場所は、AEM forms のインストールプロセス中に手動で設定できます。 インストール時に場所の設定が空のままの場合、アプリケーションサーバーのインストール下のディレクトリは、次のようにデフォルトで次のようになります。

* （JBoss）`[appserver root]/server/[type]/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/DocumentServer/DocumentStorage`
* （WebSphere）`[appserver root]/installedApps/adobe/'server'/DocumentStorage`

## デフォルトの GDS の場所の変更 {#change-the-default-gds-location}

AEM forms のインストールが完了したら、管理コンソールで GDS の場所を変更できます。 プロセスを完了するために、データを手動で再配置します。

>[!NOTE]
>
>次の方法でデータを移行します。そうしないと、データが失われます。

1. 管理コンソールにログインし、設定/コアシステム設定/設定をクリックします。
1. 「グローバルドキュメントストレージディレクトリ」ボックスに、新しい GDS ディレクトリへのフルパスを入力し、「OK」をクリックします。
1. 直ちにアプリケーションサーバーをシャットダウンします。
1. 内部ディレクトリ構造を維持しながら、古い GDS ディレクトリから新しい場所にすべてのファイルを移動します。
1. アプリケーションサーバーを再起動します。

## デプロイメントファイルについて {#about-deployment-files}

AEM forms は、サービスコンテナと Java 2 Platform, Enterprise Edition(J2EE)EAR ファイルの 2 種類のデプロイメントファイルで構成されています。 EAR ファイルは、AEM forms のコア機能を含む、標準の J2EE アプリケーションバンドルで構成されています。 アプリケーションサーバー固有の EAR ファイルは、次のとおりです。

* adobe-core-*[appserver]*.ear
* adobe-core-*[appserver]*-*[OS]*.ear

AEM forms の実装では、組み立てられた EAR ファイルとサポートファイルを、AEM forms ソリューションを実行する予定のアプリケーションサーバーにデプロイします。 複数のモジュールを設定してアセンブリした場合、デプロイ可能なモジュールはデプロイ可能な EAR ファイル内にパッケージ化されます。 これらのファイルをデプロイするには、ファイルを *[appserver home]*\server\all\deploy ディレクトリにコピーします。

モジュールとAEM forms アーカイブファイルは、JAR ファイルにパッケージ化されます。 J2EE タイプのファイルではないので、アプリケーションサーバーにはデプロイされません。 代わりに、GDS ディレクトリにコピーされ、その場所への参照がAEM forms データベースに保存されます。 この理由から、GDS ディレクトリをクラスターのすべてのノードで共有する必要があります。 すべてのノードは、DSC の中央ストレージディレクトリにアクセスできる必要があります。

>[!NOTE]
>
>サービスコンテナをデプロイする前に、GDS ディレクトリを作成して設定していることを確認してください。 ( 詳しくは、 [GDS ディレクトリの設定](global-document-storage-directory.md#configuring-the-gds-directory))
