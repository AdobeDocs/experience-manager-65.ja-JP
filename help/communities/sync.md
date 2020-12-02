---
title: コミュニティのユーザーの同期
seo-title: コミュニティのユーザーの同期
description: ユーザーの同期の仕組み
seo-description: ユーザーの同期の仕組み
uuid: 772b82bd-a66c-4c1d-b80b-dcff77c873a3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 97286c2c-f6e3-43ec-b1a9-2abb58616778
docset: aem65
translation-type: tm+mt
source-git-commit: acc758b83486e8c623e31bb4a68f3c29dd4848ba
workflow-type: tm+mt
source-wordcount: '2509'
ht-degree: 20%

---


# コミュニティのユーザーの同期 {#communities-user-synchronization}

## 概要 {#introduction}

AEM Communitiesでは、公開環境（設定されている権限に応じて異なります）から、*サイト訪問者*&#x200B;が&#x200B;*メンバー*&#x200B;になり、*ユーザーグループ*&#x200B;を作成し、*メンバープロファイル*&#x200B;を編集できます。

*ユーザー* データとは、 *ユーザー*、 *ユーザー* プロファイル、 *ユーザーグループを指す用語*&#x200B;です。

メンバーという用語は、オーサー環境で登録されたユーザーではなく、パブリッシュ環境で登録されたユーザーを指します。****

ユーザーデータについて詳しくは、[ユーザーとユーザーグループの管理](/help/communities/users.md)を参照してください。

## パブリッシュファーム間のユーザーの同期  {#synchronizing-users-across-a-publish-farm}

仕様上、パブリッシュ環境で作成されたデータは、オーサー環境では表示されません。

オーサー環境で作成されたほとんどのユーザーデータは、オーサー環境に残されたままとなり、パブリッシュインスタンスには同期もレプリケートもされません。

[トポロジ](/help/communities/topologies.md)が[パブリッシュファーム](/help/sites-deploying/recommended-deploys.md#tarmk-farm)である場合、1つのパブリッシュインスタンスに対する登録と変更を、他のパブリッシュインスタンスと同期する必要があります。 メンバーは、ログインして任意の発行ノードでデータを確認できる必要があります。

ユーザーの同期を有効にすると、ファーム内のパブリッシュインスタンス間でユーザーデータが自動的に同期されます。

### ユーザーの同期のセットアップ手順  {#user-sync-setup-instructions}

発行ファーム全体で同期を有効にする方法に関する詳細な詳細な手順については、次を参照してください。

* [ユーザーの同期](/help/sites-administering/sync.md)

## バックグラウンドでのユーザー同期{#user-sync-in-the-background}

![sling-dist-workflow](assets/sling-dist-workflow.png)

* **vltパッケージ**

   これは発行者に対して行われたすべての変更のzipファイルで、発行者に配布する必要があります。 パブリッシャの変更は、変更イベントリスナーによって選択されたイベントを生成します。 これにより、すべての変更を含むvltパッケージが作成されます。

* **配布パッケージ**

   Slingの配布情報が含まれます。 これは、コンテンツの配布が必要な場所、および最後に配布された日時に関する情報です。

## ... {#what-happens-when}

### コミュニティのサイトコンソールでのサイトの公開 {#publish-site-from-communities-sites-console}

オーサー環境で、コミュニティサイトを[コミュニティサイトコンソール](/help/communities/sites-console.md)から公開すると、関連するページが[レプリケート](/help/sites-deploying/configuring.md#replication-reverse-replication-and-replication-agents)されます。また、Sling によって、動的に作成されたコミュニティユーザーグループ（メンバーシップを含む）が配信されます。

### パブリッシュ環境でのユーザーの作成またはプロファイルの編集  {#user-is-created-or-edits-profile-on-publish}

仕様上、パブリッシュ環境で（自己登録、ソーシャルログイン、LDAP 認証などで）作成されたユーザーやプロファイルはオーサー環境では表示されません。

トポロジが[発行ファーム](/help/communities/topologies.md)で、ユーザー同期が正しく構成されている場合、*user*&#x200B;と&#x200B;*userプロファイル*&#x200B;は、Sling配布を使用して、発行ファーム全体で同期されます。

### パブリッシュ環境での新しいコミュニティグループの作成 {#new-community-group-is-created-on-publish}

発行インスタンスから開始されても、コミュニティグループの作成（新しいサイトページと新しいユーザーグループに結びつく）は、実際には作成者インスタンスで発生します。

このプロセスの一環として、新しいサイトページがすべてのパブリッシュインスタンスにレプリケートされます。動的に作成されるコミュニティユーザーグループとそのメンバーシップは、すべての発行インスタンスに配布されるSlingです。

### セキュリティコンソールでのユーザーまたはユーザーグループの作成 {#users-or-user-groups-are-created-using-security-console}

仕様上、パブリッシュ環境で作成されたユーザーデータは、オーサー環境では表示されません。その反対も同様です。

[ユーザー管理およびセキュリティ](/help/sites-administering/security.md)コンソールを使用してパブリッシュ環境で新しいユーザーを追加すると、ユーザーの同期機能により、新しいユーザーとそのグループメンバーシップがその他のパブリッシュインスタンスに同期されます（必要な場合）。ユーザー同期は、セキュリティコンソールを使用して作成されたユーザーグループも同期します。

### ユーザーによるパブリッシュ環境でのコンテンツの投稿 {#user-posts-content-on-publish}

ユーザー生成コンテンツ（UGC）に関しては、パブリッシュインスタンスで入力されたデータへのアクセスは、[設定済みの SRP](/help/communities/srp-config.md) を通じておこなわれます。

## ベストプラクティス {#bestpractices}

デフォルトでは、ユーザー同期は&#x200B;**無効**&#x200B;になっています。ユーザー同期を有効にするには、OSGi の既存の&#x200B;**&#x200B;設定を変更する必要があります。ユーザー同期を有効にした結果、新しい設定が追加されることはありません。

ユーザー同期では、オーサー環境で作成されていないユーザーデータでもその配布の管理はオーサー環境に依存します。

**前提条件**

1. ユーザーとユーザーグループが既に1つのパブリッシャー上に作成されている場合は、ユーザーの同期を設定および有効にする前に、[ユーザーデータをすべてのパブリッシャーに手動で](/help/sites-administering/sync.md#manually-syncing-users-and-user-groups)同期することをお勧めします。

   ユーザー同期を有効にすると、新規に作成されたユーザーおよびグループのみが同期されるようになります。

1. 最新のコードがインストールされていることを確認します。

   * [AEM プラットフォームの更新](https://helpx.adobe.com/jp/experience-manager/kb/aem62-available-hotfixes.html)
   * [AEM Communities の更新](/help/communities/deploy-communities.md#latestfeaturepack)

AEM Communitiesでユーザー同期を有効にするには、次の設定が必要です。 Slingコンテンツの配信が失敗しないように、これらの設定が正しいことを確認します。

### Apache Sling Distribution Agent - Sync Agents Factory {#apache-sling-distribution-agent-sync-agents-factory}

この設定は、発行者間で同期されるコンテンツを取得します。 設定は作成者インスタンスに対して行われます。 作成者は、そこに存在するすべての発行者と、すべての情報をどこで同期するかを追跡する必要があります。

設定のデフォルト値は、単一の発行インスタンスに対するものです。 ユーザー同期は、発行ファームなど複数の発行インスタンスを同期するのに役立つので、追加の発行インスタンスを設定に追加する必要があります。

**コンテンツはどのように同期されますか。**

発行者インスタンスが発行者のエクスポーターエンドポイントにpingを送信します。 特定の発行者(n)に対してユーザーが作成または更新されるたびに、作成者はエクスポーターのエンドポイントからコンテンツを取得し、[プッシュしてコンテンツ](/help/communities/sync.md#main-pars-image-1413756164)を他の発行者（n-1、つまりコンテンツの取得元とは別の発行者）に送信します。

Apache Sling Sync Agentsを設定するには：

1. AEMオーサーインスタンスでの管理者権限でサインインします。
1. [Webコンソール](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html)にアクセスします。 例：[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)。
1. **Apache Sling Distribution Agent - Sync Agents Factory**&#x200B;を探します。

   * 編集用に開く既存の設定を選択します（鉛筆アイコン）。

      検証名：**socialpubsync.**

   * 「**有効**」チェックボックスを選択します。
   * 「**複数のキューを使用」を選択します。**
   * **エクスポーターエンドポイント**&#x200B;と&#x200B;**インポーターエンドポイント**&#x200B;を指定します（エクスポーターエンドポイントとインポーターエンドポイントをさらに追加できます）。

      これらのエンドポイントは、コンテンツの取得元と、コンテンツのプッシュ先を定義します。 作成者は、指定されたエクスポーターエンドポイントからコンテンツを取得し、コンテンツを（コンテンツの取得元の発行者以外の）発行者にプッシュします。
   ![sync-agent-fact](assets/sync-agent-fact.png)

### Adobe Granite Distribution - Encrypted Password Transport Secret Provider {#adobe-granite-distribution-encrypted-password-transport-secret-provider}

これにより、作成者は、許可されたユーザーを、作成者から発行するユーザーデータを同期する権限を持つユーザーとして識別できます。

[許可されたユーザーがすべての発行インスタンスで](/help/sites-administering/sync.md#createauthuser)を作成すると、発行者は作成者と接続し、発行者のSling配布を設定できます。 この権限を持つユーザーには、必要なすべての[ACL](/help/sites-administering/sync.md#howtoaddacl)があります。

発行者にデータをインストールする場合、または発行者からデータを取得する場合は、この設定で設定された資格情報（ユーザー名とパスワード）を使用して作成者と接続します。

許可されたユーザーを使用して発行者と作成者を接続するには：

1. AEMオーサーインスタンスでの管理者権限でサインインします。
1. [Webコンソール](/help/sites-deploying/configuring-osgi.md)にアクセスします。

   例：[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)。
1. **AdobeGranite配布 — 暗号化パスワードトランスポートシークレットプロバイダーを探します。**
1. 編集用に開く既存の設定を選択します（鉛筆アイコン）。

   Verifyプロパティ&#x200B;**socialpubsync** - **publishUser.**

1. ユーザー名とパスワードを[許可されたユーザー](/help/sites-administering/sync.md#createauthorizeduser)に設定します。

   例：**usersync - admin**

![花崗岩 — パスワード —trans](assets/granite-paswrd-trans.png)

### Apache Sling Distribution Agent - Queue Agents Factory {#apache-sling-distribution-agent-queue-agents-factory}

この設定は、発行者間で同期するデータを設定する場合に使用します。 **許可されているルート**&#x200B;で指定されたパスでデータが作成/更新されると、「var/community/distribution/diff」がアクティブ化され、作成されたレプリケーターはパブリッシャーからデータを取得し、他のパブリッシャーにインストールします。

同期するデータ（ノードパス）を設定するには：

1. 作成者インスタンスに対する管理者権限でログインします。
1. [Webコンソール](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html)にアクセスします。

   例：[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)。

1. **Apache Sling Distribution Agent - Queue Agents Factory**&#x200B;を探します。
1. 編集用に開く既存の設定を選択します（鉛筆アイコン）。

   検証名：**socialpubsync -reverse**

1. 「**有効**」チェックボックスをオンにして保存します。
1. **許可されているルート**&#x200B;にレプリケートするノードパスを指定します。
1. **publish**&#x200B;の各インスタンスに対して同じ手順を繰り返します。

   ![queue-agents-fact](assets/queue-agents-fact.png)

### Adobe Granite Distribution - Diff Observer Factory {#adobe-granite-distribution-diff-observer-factory}

この設定は、パブリッシャー間でグループメンバーシップを同期します。
あるパブリッシャーでグループのメンバーシップを変更しても、他のパブリッシャーでのメンバーシップが更新されない場合は、**ref :members**&#x200B;が&#x200B;**looked properties names**&#x200B;に追加されていることを確認します。

メンバーの同期を確実に行うには：

1. AEMオーサーインスタンスでの管理者権限でサインインします。
1. [Webコンソール](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html)にアクセスします。

   例：[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)。

1. **AdobeGranite Distribution - Diff Observer Factory**&#x200B;を探します。
1. 編集用に開く既存の設定を選択します（鉛筆アイコン）。

   **エージェント名を確認：socialpubsync -reverse**。

1. 「**有効**」チェックボックスを選択します。
1. **looked properties names**&#x200B;のpropertyNameの説明として&#x200B;**rep:members**&#x200B;を指定し、「保存」をクリックします。

   ![diff-obs](assets/diff-obs.png)

### Apache Sling Distribution Trigger - Scheduled Triggers Factory {#apache-sling-distribution-trigger-scheduled-triggers-factory}

この設定では、（発行者がpingを送信し、変更を作成者が取得した後の）ポーリング間隔を設定して、発行者間で変更を同期できます。

作成者は、30秒（デフォルト）ごとに投稿者をポーリングします。 フォルダー`/var/sling/distribution/packages/  socialpubsync -  vlt /shared`にあるパッケージが存在する場合は、それらのパッケージが取得され、他のパブリッシャーにインストールされます。

ポーリング間隔を変更するには：

1. AEMオーサーインスタンスでの管理者権限でサインインします。
1. [Webコンソール](/help/sites-deploying/configuring-osgi.md)にアクセスします(例：[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. **Apache Sling Distribution Trigger - Scheduled Triggers Factory**&#x200B;を探します。

   * 編集用に開く既存の設定を選択します（鉛筆アイコン）。

      **socialpubsync -scheduled-trigger**&#x200B;を確認

   * 間隔（秒）を目的の間隔に設定し、保存します。

   ![scheduled-trigger](assets/scheduled-trigger.png)

### AEM Communities User Sync Listener {#aem-communities-user-sync-listener}

Sling配布で、購読に不一致があり、それに続く問題については、**AEM Communitiesユーザー同期リスナー**&#x200B;の設定に次のプロパティが設定されているかどうかを確認してください。

* NodeTypes
* IgnorableProperties
* IgnorableNodes
* DistributedFolders

購読、フォロー、通知を同期するには

各AEM発行インスタンスで、次の操作を行います。

1. 管理者権限でサインインします。
1. [Webコンソール](/help/sites-deploying/configuring-osgi.md)にアクセスします。 例：[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)。
1. **AEM Communitiesユーザー同期リスナー**&#x200B;を探します。
1. 編集用に開く既存の設定を選択します（鉛筆アイコン）

   検証名：**socialpubsync -scheduled-trigger**

1. 次の&#x200B;**NodeTypes**&#x200B;を設定します。

   `rep:User`

   `nt:unstructured`

   `nt:resource`

   `rep:ACL`

   `sling:Folder`

   `sling:OrderedFolder`

   このプロパティで指定されたノードタイプが同期され、通知情報（ブログと使用された設定）が異なる発行者間で同期されます。

1. &lt;a0/追加>DistributedFolders **内の同期するすべてのフォルダー。**&#x200B;例：

   `segments/scoring`

   `social/relationships`

   `activities`

1. **ignorablenodes**&#x200B;を次のように設定します。

   `.tokens`

   `system`

   `rep:cache` （スティッキーセッションを使用するので、このノードを別の発行者に同期する必要はありません）。

   ![user-sync-listner](assets/user-sync-listner.png)

### 一意の Sling ID{#unique-sling-id} の節を参照してください 

AEM作成者インスタンスは、Sling IDを使用して、データの送信元およびパッケージの返送先（または送り返す必要のない発行者）を識別します。

発行ファーム内のすべての発行者が一意のSling IDを持っていることを確認します。 Sling IDが、発行ファーム内の複数の発行インスタンスに対して同じである場合、ユーザーの同期は失敗します。 作成者はパッケージの取り込み元とインストール先を知りません。

発行ファームで発行者のSling IDを一意にするには、各発行インスタンスで次の手順を実行します。

1. [https://_host:port_/system/console/status-slingsettings](https://localhost:4503/system/console/status-slingsettings)を参照します。
1. **Sling ID**&#x200B;の値を確認します。

   ![slingid](assets/slingid.png)

   あるパブリッシュインスタンスの Sling ID が他のパブリッシュインスタンスの Sling ID と一致する場合は、次のようにします。

1. 一致するSling IDを持つ発行インスタンスの1つを停止します。
1. `crx-quickstart/launchpad/felix`ディレクトリで、*sling.id.file.*&#x200B;という名前のファイルを探して削除します。

   例えば、Linuxシステムの場合は、次のようになります。

   `rm -i $(find . -type f -name sling.id.file)`

   例えば、Windowsシステムの場合は次のようになります。

   Windowsエクスプローラを使用して`sling.id.file`を検索

1. 発行インスタンスを起動します。起動時に、新しいSling IDが割り当てられます。
1. **Sling ID**&#x200B;が一意になったことを検証します。

すべてのパブリッシュインスタンスの Sling ID が一意になるまでこの手順を繰り返します。

### Vault Package Builder Factory  {#vault-package-builder-factory}

アップデートを正しく同期するには、ユーザ同期用にVaultパッケージビルダを変更する必要があります。
`/home/users`に`*/rep:cache`ノードが作成されます。 これは、ノードのプリンシパル名にクエリした場合に、そのキャッシュを直接使用できることを確認するために使用されるキャッシュです。

`rep :cache`ノードがパブリッシャー間で同期されている場合、ユーザーの同期は停止する可能性があります。

各AEM発行インスタンスで、アップデートが発行者間で適切に同期されるようにするには、次の手順を実行します。

1. [Webコンソール](/help/sites-deploying/configuring-osgi.md)にアクセス

   例：[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)。
1. **Apache Sling Distribution Packaging - Vault Package Builder Factory**&#x200B;を探します。

   ビルダー名：socialpubsync-vlt.

1. 編集アイコンを選択します。
1. 2つ追加のパッケージノードフィルター:
   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`
1. ポリシー処理
   * 既存のrep :policyノードを新しいノードで上書きするには、3つ目のパッケージ・フィルタを追加します。`/home/users|+.*/rep:policy`
   * ポリシーの配布を防ぐには、次のように設定します。`Acl Handling: IGNORE`

   ![Vaultパッケージビルダファクトリ](assets/vault-package-builder-factory.png)

## AEM CommunitiesでのSlingの配布のトラブルシューティング{#troubleshoot-sling-distribution-in-aem-communities}

Slingの配布に失敗した場合は、次のデバッグ手順を試してください。

1. **不 [適切に追加された設定の確認](/help/sites-administering/sync.md#improperconfig)**

   複数の設定を追加または編集しないでください。既存のデフォルト設定は、編集する必要があります。
1. **設定の確認**

   [ベストプラクティス](/help/communities/sync.md#main-pars-header-863110628)で説明されているように、AEM Authorインスタンスにすべての[設定](/help/communities/sync.md#bestpractices)が適切に設定されていることを確認します。

1. **許可されたユーザー権限の確認**

   パッケージが正しくインストールされていない場合は、最初の発行インスタンスで作成された[許可されたユーザー](/help/sites-administering/sync.md#createauthuser)に正しいACLが含まれていることを確認します。

   これを検証するには、[作成した認証済みユーザー](/help/sites-administering/sync.md#createauthuser)の代わりに、作成者インスタンスの[AdobeGranite配布 — 暗号化パスワードトランスポートシークレットプロバイダー](/help/sites-administering/sync.md#adobegraniteencpasswrd)の設定を変更し、管理者ユーザー資格情報を使用します。 次に、パッケージのインストールを再試行します。 ユーザー同期が管理者の資格情報で正常に機能する場合は、作成した発行ユーザーに適切なACLがないことを意味します。

1. **相違オブザーバーファクトリ構成の確認**

   特定のノードのみがパブリッシュファーム全体で同期されない場合（例：グループメンバーは同期されない）、[AdobeGranite Distribution - Diff Observer Factory](/help/sites-administering/sync.md#diffobserver)構成が有効で&#x200B;**rep:メンバー**&#x200B;は&#x200B;**lookedプロパティ名**&#x200B;に設定されます。

1. **AEM Communitiesユーザー同期リスナーの設定を確認します。** 作成したユーザーが同期されているが、購読と次のユーザーが機能していない場合は、AEM Communitiesユーザー同期リスナーの構成に次の値が含まれていることを確認します。

   * ノードタイプ — **rep:User, nt :unstructured**, **nt :resource**, **rep:ACL**, **sling:Folder**, **sling:OrderedFolder**&#x200B;に設定。
   * 無視可能なノード — **.tokens**、**system**、**rep :cache**&#x200B;に設定します。
   * 分散フォルダ — 配布するフォルダに設定します。

1. **発行インスタンスでのユーザー作成時に生成されたログの確認**

   上記の設定が適切に設定されているにもかかわらずユーザー同期が機能していない場合は、ユーザーの作成時に生成されたログを確認します。

   次のように、ログの順序が同じかどうかを確認します。

   ```shell
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7422] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C, /home/users/C/Cw-5avWqilmqsNn5hCvK]
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7422] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ2: ADD paths=[/home/users/C, /home/users/C/Cw-5avWqilmqsNn5hCvK], user=communities-user-admin
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7431] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C/Cw-5avWqilmqsNn5hCvK, /home/users/C/Cw-5avWqilmqsNn5hCvK/profile, /home/users/C/Cw-5avWqilmqsNn5hCvK/rep:policy]
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7431] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ3: ADD paths=[/home/users/C/Cw-5avWqilmqsNn5hCvK, /home/users/C/Cw-5avWqilmqsNn5hCvK/profile, /home/users/C/Cw-5avWqilmqsNn5hCvK/rep:policy], user=communities-user-admin
   15.05.2016 18:33:01.757 *INFO* [sling-oak-observation-7431] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337181554_ebb27ad9-a861-4405-9342-d64c916654e2:0.0.1
   15.05.2016 18:33:01.820 *INFO* [sling-oak-observation-7422] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337181554_58811273-5861-48fe-95d2-4aff367b99c3:0.0.1
   15.05.2016 18:33:02.023 *INFO* [sling-oak-observation-7430] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C/Cw-5avWqilmqsNn5hCvK/profile]
   15.05.2016 18:33:02.023 *INFO* [sling-oak-observation-7430] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ4: ADD paths=[/home/users/C/Cw-5avWqilmqsNn5hCvK/profile], user=communities-user-admin
   15.05.2016 18:33:02.273 *INFO* [sling-oak-observation-7430] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337182039_f34f4fa6-10b9-42eb-8740-4da9d4d38f99:0.0.1
   ```

デバッグするには：

1. ユーザー同期を無効にします。
1. AEMオーサーインスタンスで、管理者権限でサインインします。

   1. [Webコンソール](/help/sites-deploying/configuring-osgi.md)にアクセスします。 例：[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)。
   1. 設定&#x200B;**Apache Sling Distribution Agent - Sync Agents Factory**&#x200B;を探します。
   1. 「**有効**」チェックボックスの選択を解除します。

      作成者インスタンスでユーザー同期を無効にすると、（エクスポーターとインポーター）エンドポイントが無効になり、作成者インスタンスは静的になります。 **vlt**&#x200B;パッケージは作成者によってpingまたは取得されません。

      現在は、ユーザーが発行インスタンスで作成された場合、**vlt**&#x200B;パッケージが&#x200B;*/var/sling/distribution/packages/ sociallpubsync - vlt /data*&#x200B;ノードに作成されます。 また、これらのパッケージが作成者によって別のサービスにプッシュされた場合も、 このデータをダウンロードして抽出し、すべてのプロパティが他のサービスにプッシュされたものかどうかを確認できます。

1. 投稿者に移動し、投稿でユーザーを作成します。 その結果、イベントが作成されます。
1. ユーザーの作成時に作成されたログ](/help/communities/sync.md#troubleshoot-sling-distribution-in-aem-communities)の[順序を確認します。
1. **vlt**&#x200B;パッケージが&#x200B;**/var/sling/distribution/packages/socialpubsync-vlt/data**&#x200B;に作成されているかどうかを確認します。
1. 次に、AEMオーサーインスタンスでユーザー同期を有効にします。
1. パブリッシャーで、**Apache Sling Distribution Agent - Sync Agents Factory**のエクスポーターまたはインポーターエンドポイントを変更します。
パッケージデータをダウンロードして抽出し、すべてのプロパティが他の発行者にプッシュされ、どのデータが失われるかを確認できます。
