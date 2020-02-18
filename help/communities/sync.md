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
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# コミュニティのユーザーの同期{#communities-user-synchronization}

## 概要 {#introduction}

In AEM Communities, from the publish environment (depending on permissions configured), *site visitors* may become *members*, create *user groups*, and edit their *member profile* .

*ユーザーデータ* (User data *)は、ユーザー、ユーザープロファイ*&#x200B;ル *、ユーザーグル* ープを指しま **&#x200B;す。

メンバーという用語は、オーサー環境で登録されたユーザーではなく、パブリッシュ環境で登録されたユーザーを指します。****

ユーザーデータについて詳しくは、[ユーザーとユーザーグループの管理](/help/communities/users.md)を参照してください。

## パブリッシュファーム間のユーザーの同期 {#synchronizing-users-across-a-publish-farm}

仕様上、パブリッシュ環境で作成されたデータは、オーサー環境では表示されません。

オーサー環境で作成されたほとんどのユーザーデータは、オーサー環境に残されたままとなり、パブリッシュインスタンスには同期もレプリケートもされません。

When the [topology](/help/communities/topologies.md) is a [publish farm](/help/sites-deploying/recommended-deploys.md#tarmk-farm), registration  and  modifications made on one publish instance need to be synchronized with other publish instances. メンバーは、ログインして、任意の発行ノード上でそのデータを確認できる必要があります。

ユーザーの同期を有効にすると、ファーム内のパブリッシュインスタンス間でユーザーデータが自動的に同期されます。

### ユーザーの同期のセットアップ手順 {#user-sync-setup-instructions}

詳細なステップバイステップの手順については、以下を参照してください。

* [ユーザーの同期](/help/sites-administering/sync.md)

## バックグラウンドでのユーザー同期 {#user-sync-in-the-background}

![sling-dist-workflow](assets/sling-dist-workflow.png)

* **vltパッケージ**:は、発行者に対して行われたすべての変更を含むzipファイルです。発行者に配布する必要があります。 パブリッシャーに対する変更は、変更イベントリスナーによって取得されるイベントを生成します。 これにより、すべての変更を含むvltパッケージが作成されます。

* **配布パッケージ**:Slingの配布情報が含まれます。 これは、コンテンツの配布が必要な場所と、最後に配布された日時に関する情報です。

## What Happens When ... {#what-happens-when}

### コミュニティのサイトコンソールでのサイトの公開 {#publish-site-from-communities-sites-console}

オーサー環境で、コミュニティサイトを[コミュニティサイトコンソール](/help/communities/sites-console.md)から公開すると、関連するページが[レプリケート](/help/sites-deploying/configuring.md#replication-reverse-replication-and-replication-agents)されます。また、Sling によって、動的に作成されたコミュニティユーザーグループ（メンバーシップを含む）が配信されます。

### パブリッシュ環境でのユーザーの作成またはプロファイルの編集 {#user-is-created-or-edits-profile-on-publish}

仕様上、パブリッシュ環境で（自己登録、ソーシャルログイン、LDAP 認証などで）作成されたユーザーやプロファイルはオーサー環境では表示されません。

When the topology is a [publish farm](/help/communities/topologies.md) and user sync has been correctly configured, the *user* and *user profile* is synchronized across the publish farm using Sling distribution.

### パブリッシュ環境での新しいコミュニティグループの作成 {#new-community-group-is-created-on-publish}

発行インスタンスから開始されますが、新しいサイトページと新しいユーザーグループが生じるコミュニティグループの作成は、実際に作成者インスタンスで行われます。

このプロセスの一環として、新しいサイトページがすべてのパブリッシュインスタンスにレプリケートされます。動的に作成されたコミュニティユーザーグループとそのメンバーシップは、Slingですべての発行インスタンスに配布されます。

### セキュリティコンソールでのユーザーまたはユーザーグループの作成 {#users-or-user-groups-are-created-using-security-console}

仕様上、パブリッシュ環境で作成されたユーザーデータは、オーサー環境では表示されません。その反対も同様です。

[ユーザー管理およびセキュリティ](/help/sites-administering/security.md)コンソールを使用してパブリッシュ環境で新しいユーザーを追加すると、ユーザーの同期機能により、新しいユーザーとそのグループメンバーシップがその他のパブリッシュインスタンスに同期されます（必要な場合）。また、ユーザー同期は、セキュリティコンソールを使用して作成されたユーザーグループを同期します。

### ユーザーによるパブリッシュ環境でのコンテンツの投稿 {#user-posts-content-on-publish}

ユーザー生成コンテンツ（UGC）に関しては、パブリッシュインスタンスで入力されたデータへのアクセスは、[設定済みの SRP](/help/communities/srp-config.md) を通じておこなわれます。

## ベストプラクティス {#bestpractices}

デフォルトでは、ユーザー同期は&#x200B;**無効**&#x200B;になっています。ユーザー同期を有効にするには、OSGi の既存の&#x200B;**&#x200B;設定を変更する必要があります。ユーザー同期を有効にした結果、新しい設定が追加されることはありません。

ユーザー同期では、オーサー環境で作成されていないユーザーデータでもその配布の管理はオーサー環境に依存します。

**前提条件**

1. If users and user groups have already been created on one publisher, it is recommended to [manually sync](/help/sites-administering/sync.md#manually-syncing-users-and-user-groups) the user data to all publishers prior to configuring and enabling user sync.
ユーザー同期を有効にすると、新規に作成されたユーザーおよびグループのみが同期されるようになります。

1. 最新のコードがインストールされていることを確認します。

   * [AEM プラットフォームの更新](https://helpx.adobe.com/experience-manager/kb/aem62-available-hotfixes.html)
   * [AEM Communities の更新](/help/communities/deploy-communities.md#latestfeaturepack)

AEM Communitiesでユーザー同期を有効にするには、次の設定が必要です。 Slingコンテンツの配信に失敗するのを防ぐために、これらの設定が正しいことを確認します。

### Apache Sling Distribution Agent - Sync Agents Factory {#apache-sling-distribution-agent-sync-agents-factory}

この設定は、発行者間で同期されるコンテンツを取得します。 設定は作成者インスタンスに対して行われます。 作成者は、そこに存在するすべての発行者と、すべての情報を同期する場所を追跡する必要があります。

設定のデフォルト値は、単一の発行インスタンス用です。 ユーザー同期は、複数の発行インスタンス（例えば、発行ファーム）を同期するのに役立つので、設定に追加の発行インスタンスを追加する必要があります。

**コンテンツはどのように同期されますか。**

発行者インスタンスは、発行者のエクスポーターエンドポイントにpingを送信します。 特定の発行者(n)に対してユーザーが作成または更新されるたびに、作成者は、書き出しエンドポイントからコンテンツを取得し、そのコンテンツを他の発行者 [(コンテンツの取得元とは別の発行者](/help/communities/sync.md#main-pars-image-1413756164) )にプッシュします。

Apache Sling同期エージェントの設定を行うには

AEM作成者インスタンス上：

1. 管理者権限でサインインします。
1. Access the [Web Console](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html). For example, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Locate **Apache Sling Distribution Agent - Sync Agents Factory.**

   * 編集用に開く既存の設定を選択します（鉛筆アイコン）。
   確認名：socialpubsync **。**

   * Select the **Enabled** checkbox.
   * 「 **Use Multiple queues」を選択します。**
   * 「エクスポー **ターエンドポイント** 」と「インポ **ーターエンドポイント」を指定します** （エクスポーターエンドポイントとインポーターエンドポイントをさらに追加できます）。

      これらのエンドポイントは、コンテンツの取得元とプッシュ先を定義します。 「作成者」は、指定した書き出しエンドポイントからコンテンツを取得し、（コンテンツの取得元の発行者以外の）発行者にコンテンツをプッシュします。


![sync-agent-fact](assets/sync-agent-fact.png)

### Adobe Granite Distribution - Encrypted Password Transport Secret Provider {#adobe-granite-distribution-encrypted-password-transport-secret-provider}

これにより、作成者は、発行するユーザーデータを同期する権限を持つ、承認されたユーザーを識別できます。

すべての [発行インスタンスで作成された](/help/sites-administering/sync.md#createauthuser) 、許可されたユーザーは、発行者が作成者と接続し、発行者のSling配布を設定するのに役立ちます。 この権限を持つユーザーは、必要なACLをすべて持っ [ています](/help/sites-administering/sync.md#howtoaddacl)。

発行者にデータをインストールしたり、発行者からデータを取得したりする場合は、この設定で設定した資格情報（ユーザー名とパスワード）を使用して発行者と接続します。

許可されたユーザーを使用して発行者に作成者を接続するには

AEM作成者インスタンス上：

1. 管理者権限でサインインします。
1. Access the [Web Console](/help/sites-deploying/configuring-osgi.md).

   For example, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Locate **Adobe Granite Distribution - Encrypted Password Transport Secret Provider.**
1. 編集用に開く既存の設定を選択します（鉛筆アイコン）。

   Verifyプロパテ **ィsocialpubsync** - **publishUser.**

1. ユーザー名とパスワードを許可されたユーザー [に設定します](/help/sites-administering/sync.md#createauthorizeduser)。

   例えば、 **usersync - admin**

![花崗岩 — パスワード —trans](assets/granite-paswrd-trans.png)

### Apache Sling Distribution Agent - Queue Agents Factory {#apache-sling-distribution-agent-queue-agents-factory}

この設定は、発行者間で同期するデータを設定するために使用します。 許可されたルートで指定されたパスでデータが作成/更新されると ****、「var/community/distribution/diff」がアクティブ化され、作成されたレプリケーターはパブリッシャーからデータを取得して他のパブリッシャーにインストールします。

同期するデータ（ノードパス）を設定するには

AEM発行インスタンス：

1. 管理者権限でサインインします。
1. Access the [Web Console](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html).

   For example, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. Locate **Apache Sling Distribution Agent - Queue Agents Factory.**
1. 編集用に開く既存の設定を選択します（鉛筆アイコン）。

   確認名：socialpubsync - **reverse。**

1. 「 **Enabled** 」チェック・ボックスを選択して保存します。
1. 許可されたルートに複製するノードパスを指 **定します**。
1. Repeat for each **publish** instance.

![queue-agents-fact](assets/queue-agents-fact.png)

### Adobe Granite Distribution - Diff Observer Factory {#adobe-granite-distribution-diff-observer-factory}

この設定は、発行者間でグループメンバーシップを同期します。
あるパブリッシャーでグループのメンバーシップを変更しても、他のパブリッシャーのメンバーシップが更新されない場合は、 **ref** :membersが検索されたプロパティ名に追加されてい **ることを確認します**。

メンバーの同期を確実に行うには

各AEM発行インスタンスで、次の操作を行います。

1. 管理者権限でサインインします。
1. Access the [Web Console](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html).

   For example, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. Locate **Adobe Granite Distribution - Diff Observer Factory.**
1. 編集用に開く既存の設定を選択します（鉛筆アイコン）。

   エージェント **名の確認：socialpubsync -reverse**.

1. Select the **Enabled** checkbox.
1. 検索プ **ロパティ名のpropertyNameの説明とし** てrep:membersを指定し ****、「保存」を選択します。

![diff-obs](assets/diff-obs.png)

### Apache Sling Distribution Trigger - Scheduled Triggers Factory {#apache-sling-distribution-trigger-scheduled-triggers-factory}

この設定では、（発行者が署名され、変更が発行者によって取り込まれた後に）発行者間で変更を同期するポーリング間隔を設定できます。

発行者は30秒（デフォルト）ごとに投稿者をポーリングします。 フォルダー/var/sling/distribution/packages/ socialpubsync - vlt /shared **&#x200B;にパッケージが存在する場合は、それらのパッケージを取得して他の発行者にインストールします。

ポーリング間隔を変更するには

AEM作成者インスタンス上：

1. 管理者権限でサインインします。
1. Webコンソー [ルにアクセスします](/help/sites-deploying/configuring-osgi.md)(例：https://localhost:4502/system/console/configMgr)。 [](https://localhost:4502/system/console/configMgr)
1. Locate **Apache Sling Distribution Trigger - Scheduled Triggers Factory**

   * 編集用に開く既存の設定を選択します（鉛筆アイコン）

      socialpubsync - **scheduled-triggerの確認**

   * 「間隔（秒）」を目的の間隔に設定し、保存します。

![scheduled-trigger](assets/scheduled-trigger.png)

### AEM Communities User Sync Listener {#aem-communities-user-sync-listener}

Sling配布で、購読に相違があり、続く問題については、 **AEM CommunitiesのUser Sync Listener設定で次のプロパティが設定されているかどうかを確認します** 。

* NodeTypes
* IgnorableProperties
* IgnorableNodes
* DistributedFolders

購読、フォロー、通知を同期するには

各AEM発行インスタンスで、次の操作を行います。

1. 管理者権限でサインインします。
1. Access the [Web Console](/help/sites-deploying/configuring-osgi.md). For example, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. Locate **AEM Communities User Sync Listener.**
1. 編集用に開く既存の設定を選択します（鉛筆アイコン）

   確認名：socialpubsync **-scheduled-trigger**

1. 次のNodeTypesを設定 **します**。

   rep:User

   nt:unstructured

   nt:resource

   rep:ACL

   sling:Folder

   sling:OrderedFolder

   このプロパティで指定されたノードタイプが同期され、通知情報（ブログと設定が実行される）が異なる発行者間で同期されます。

1. 同期するすべてのフォルダを **DistributedFoldersに追加します**。 例：

   segments/scoring

   social/relationships

   activities

1. 無視ノードを **次に設定** :

   .tokens

   system

   rep:cache（スティッキーセッションを使用するので、このノードを別のパブリッシャーと同期する必要はありません）

![user-sync-listner](assets/user-sync-listner.png)

### 一意の Sling ID{#unique-sling-id} の節を参照してください 

AEM作成者インスタンスは、Sling IDを使用して、データの送信元と、パッケージの返送先（または送り返す必要のない発行者）を識別します。

発行ファーム内のすべての発行者が一意のSling IDを持っていることを確認します。 Sling IDが、発行ファーム内の複数の発行インスタンスに対して同じである場合、ユーザーの同期は失敗します。 作成者はパッケージの取得元とインストール先を知りません。

発行ファームで発行者のSling IDを一意にするには

各パブリッシュインスタンスで以下をおこないます。

1. Browse to [https://_host:port_/system/console/status-slingsettings](https://localhost:4503/system/console/status-slingsettings).
1. Check the value of **Sling ID.**

![slingid](assets/slingid.png)

あるパブリッシュインスタンスの Sling ID が他のパブリッシュインスタンスの Sling ID と一致する場合は、次のようにします。

1. 一致するSling IDを持つ発行インスタンスの1つを停止します。
1. ディレクトリ `crx-quickstart/launchpad/felix` で、sling.id.fileという名前のファイルを検索して削除 *します。*

   例えば、Linuxシステムでは：

   `rm -i $(find . -type f -name sling.id.file)`

   例えば、Windowsシステムの場合は、次のようになります。

   Windowsエクスプローラーを使用して、 `sling.id.file`

1. 発行インスタンスを起動します。起動時に、新しいSling IDが割り当てられます。
1. Validate that the **Sling ID** is now unique.

すべてのパブリッシュインスタンスの Sling ID が一意になるまでこの手順を繰り返します。

### Vault Package Builder Factory {#vault-package-builder-factory}

アップデートを正しく同期するには、ユーザ同期用にVaultパッケージビルダを変更する必要があります。
/home **/usersに**、***/rep:cache **nodeが作成されます。 ノードのプリンシパル名を問い合わせると、このキャッシュを直接使用できることを見つけるために使用されるキャッシュです。

ノードが発行者間で同期されている場 `rep :cache `合、ユーザーの同期は停止する可能性があります。

アップデートが発行者間で適切に同期されるようにするには

各AEM発行インスタンスで、次の操作を行います。

1. Access the [Web Console](/help/sites-deploying/configuring-osgi.md)

   for example, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. Locate the **Apache Sling Distribution Packaging - Vault Package Builder Factory**

   ビルダー名：socialpubsync-vlt.

1. 編集アイコンを選択します。
1. 2つのパッケージノードフィルターの追加：
   * /home/users|-.*/.tokens
   * /home/users|**-**.*/rep:cache

1. ポリシー処理

   * 既存の rep:policy ノードを新しいノードで上書きするには、3 つ目のパッケージフィルターを追加します

      /home/users|**+**.*/rep:policy

   * ポリシーが配布されないようにするには、次のように設定します

      Acl処理：IGNORE

![Vaultパッケージビルダーファクトリ](assets/vault-package-builder-factory.png)

## AEM CommunitiesでのSlingの配布のトラブルシューティング {#troubleshoot-sling-distribution-in-aem-communities}

Sling配布が失敗した場合は、次のデバッグ手順を試してください。

1. **不適切に追加さ[れた設定を確認します](/help/sites-administering/sync.md#improperconfig)。** 複数の設定を追加または編集しないでください。既存のデフォルト設定は必ず編集してください。
1. **設定を確認します**。 「ベストプラクティス」で [](/help/communities/sync.md#bestpractices)説明されているように、AEM作成者インスタンスにすべての設定が適切に設定されている [ことを確認します](/help/communities/sync.md#main-pars-header-863110628)。
1. **許可されたユーザー権限を確認します**。 パッケージが正しくインストールされていない場合は、最初の発行インスタ [ンスで作成された](/help/sites-administering/sync.md#createauthuser) 、許可されたユーザーのACLが正しいことを確認します。

   これを検証するには、作成した認証済みユ [ーザーの代わりに](/help/sites-administering/sync.md#createauthuser) 、作成者インスタンスの [](/help/sites-administering/sync.md#adobegraniteencpasswrd) Adobe Granite Distribution - Encrypted Password Transport Secret Provider設定を、管理者ユーザーの資格情報を使用するように変更します。 次に、パッケージのインストールを再試行します。 ユーザー同期が管理者の資格情報で正常に機能する場合は、作成された発行ユーザーに適切なACLがないことを意味します。

1. **Diff Observer Factoryの設定を確認します**。 特定のノードのみがパブリッシュファーム全体で同期されない場合（例えば、グループメンバーが同期されない場合）、 [Adobe Granite Distribution - Diff Observer Factoryの設定が有効になっていて、](/help/sites-administering/sync.md#diffobserver)**rep:メンバー** は、ルックされたプロパ **ティ名で設定されます**。
1. **AEM Communitiesのユーザー同期リスナー設定を確認します。** 作成したユーザーが同期されているが、購読と次の条件が機能しない場合は、AEM CommunitiesのUser Sync Listener設定に次の設定が含まれていることを確認します。

   * ノードタイプ — **rep:User, nt :unstructured**, **nt :resource**, **rep:ACL**, ******sling Folder Folder, and Ordered Folderに設定**
   * 無視可能なノード — .tokens **、** system **、****rep :cacheに設定**
   * 分散フォルダ — 配布するフォルダに設定

1. **発行インスタンスでのユーザー作成時に生成されたログを確認します**。 上記の設定が適切に設定されているにもかかわらず、ユーザーの同期が機能していない場合は、ユーザーの作成時に生成されたログを確認します。

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
   1. AEMオーサーインスタンスで、管理者権限を使用してサインインします。

      1. Access the [Web Console](/help/sites-deploying/configuring-osgi.md). For example, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
      1. Locate the configuration **Apache Sling Distribution Agent - Sync Agents Factory**.
      1. 「有効」チェック **ボックスの選択** を解除します。
作成者インスタンスでユーザー同期を無効にすると、（エクスポーターおよびインポーター）エンドポイントが無効になり、作成者インスタンスは静的になります。 vltパッ **ケージは** 、作成者によってpingまたは取得されません。
現在は、ユーザーが発行インスタンスで作成された場合、 **vlt** パッケージは/var/sling/distribution/packages/ socialpubsync - vlt /data ** nodeに作成されます。 作成者がこのパッケージを別のサービスにプッシュした場合、 このデータをダウンロードして抽出し、すべてのプロパティが他のサービスにプッシュされているかどうかを確認できます。
   1. 投稿者に移動し、その投稿でユーザーを作成します。 その結果、イベントが作成されます。
   1. ユーザーの作 [成時に作成された](/help/communities/sync.md#troubleshoot-sling-distribution-in-aem-communities)、ログの順序を確認します。
   1. **vlt **パッケージが/var/sling/distribution/packages/socialpubsync-vlt/dataに作成されている **かどうかを確認します**。
   1. 次に、AEM作成者インスタンスでユーザー同期を有効にします。
   1. 発行者で、 **Apache Sling Distribution Agent - Sync Agents Factoryのエクスポーターまたはインポーターエンドポイントを変更します**。
パッケージデータをダウンロードして抽出し、他の発行者にプッシュされるすべてのプロパティと、失われるデータを確認できます。
