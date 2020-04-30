---
title: ユーザーとユーザーグループの管理
seo-title: ユーザーとユーザーグループの管理
description: AEM Communities のユーザーは自己登録とプロファイルの編集をおこなうことができます
seo-description: AEM Communities のユーザーは自己登録とプロファイルの編集をおこなうことができます
uuid: aeba424e-ea7e-4da5-b94f-ea8af4caa7d2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 774c2553-b629-456b-afa7-5713490f4a0a
translation-type: tm+mt
source-git-commit: 2422ed41b18bc558f0cfc9e80f7eb6f4923aa07c

---


# ユーザーとユーザーグループの管理 {#managing-users-and-user-groups}

## 概要 {#overview}

AEM Communitiesの発行環境で、ユーザーは自己登録とユーザーのプロファイルの編集が可能です。 適切な権限を与えると、次のことも可能です。

* Create sub-communities within the community site (see [community groups](creating-groups.md)).

* [ユーザー生成](moderation.md) (UGC)コンテンツのモデレート。

* Be [enablement resource](resources.md) contacts.

* Be [privileged](#privileged-members-group) to create entries for blogs, calendars, QnA, and forums.

パブリッシュ環境で登録されたユーザーは、オーサー環境の&#x200B;*ユーザー*&#x200B;と区別するために、通常は&#x200B;*コミュニティメンバー（メンバー）*&#x200B;と呼ばれます。

メンバーに権限を付与するには、そのメンバーを、オーサー環境でコミュニティサイトを[作成](sites-console.md)または[変更](sites-console.md#modifying-site-properties)したときに動的に作成される[メンバー（ユーザー）グループ](#publish-group-roles)に割り当てます。When working from the author environment, members are visible from the publish environment by means of the [tunnel service](#tunnel-service).

意図的には、発行環境で作成されたメンバーとメンバーグループは作成者環境に表示されません。 作成者環境で作成されたユーザーとユーザーグループも、同様に作成者環境に残ります。

オーサー環境のユーザーとパブリッシュ環境のメンバーが同じユーザーのリストを基にしている場合も（同じ LDAP ディレクトリから同期される場合など）、それらのユーザーは、オーサー環境とパブリッシュ環境の両方で同じ権限とグループメンバーシップを持つ同一のユーザーとは見なされません。必要に応じて、メンバーとユーザーの役割は、発行時と作成者時に別々に確立する必要があります。

For a [publish farm](topologies.md), registration and modifications made on one publish instance need to be synchronized with other publish instances in order for them to have access to the same user data. For details see [User Synchronization](sync.md), which includes a section describing [What Happens When...](sync.md#what-happens-when).

### 貢献度の制限 {#contribution-limits}

スパムから保護するために、メンバーによるコンテンツの投稿頻度を制限できます。また、新規会員の出資を自動的に制限することも可能である。

詳しくは、[メンバーの貢献度の制限](limits.md)を参照してください。

### 動的に作成されるユーザーグループ {#dynamically-created-user-groups}

コミュニティサイトを作成すると、オーサー環境（[オーサーグループの役割](#author-group-roles)を参照）かパブリッシュ環境（[パブリッシュグループの役割](#publish-group-roles)を参照）のどちらかで、コミュニティサイトを管理するために必要な各種管理機能の適切な権限と一意の ID（uid）を持った新しいユーザーグループが動的に作成されます。

グループの名前は、[コミュニティサイトを作成](sites-console.md#step13asitetemplate)するときに指定した名前から生成されます。一意のIDを使用すると、同じサーバ上の同じ名前のコミュニティサイトとコミュニティグループの名前の競合を回避できます。

例えば、「We.Retail Engage」というタイトルのサイトに「*engage*」というサイト名を付けた場合、作成されるユーザーグループのうち 1 つは次のようになります。

* Community *Engage* Members

## オーサー環境 {#author-environment}

### トンネルサービス {#tunnel-service}

When using the author environment to [create sites](sites-console.md), [modify site properties](sites-console.md#modifying-site-properties) and [manage community members and member groups](members.md), it is necessary to access users and user groups registered in the publish environment.

トンネルサービスは、作成者の複製エージェントを使用してこのアクセスを提供します。

* For details, see [configuration instructions](deploy-communities.md#tunnel-service-on-author) on the deployment page.

The [Communities Members and Groups consoles](members.md) are for the sole purpose of managing users (members) and user groups (member groups) registered only in the publish environment.

オーサー環境で登録されたユーザーとユーザーグループを管理するには、[セキュリティコンソール](../../help/sites-administering/security.md)を使用します。

### Author Group Roles {#author-group-roles}

| メンバーが所属するグループ | 主な役割 |
|---|---|
| 管理者 | 管理者グループは、コミュニティ管理者のすべての権限を持つシステム管理者と、コミュニティ管理者グループを管理する権限を持つシステム管理者で構成されます。 |
| コミュニティ管理者 | コミュニティ管理者グループは、自動的にすべてのコミュニティサイトと、そのサイトで作成されたすべてのコミュニティグループのメンバーになります。コミュニティ管理者グループの初期メンバーは、管理者グループです。オーサー環境で、コミュニティ管理者はコミュニティサイトの作成、サイトの管理、メンバーの管理（メンバーのコミュニティの使用を禁止することが可能）およびコンテンツのモデレートを実行できます。 |
| Community &lt;*site name*> Sitecontentmanager | コミュニティサイトコンテンツマネージャーは、従来の AEM オーサリング、コンテンツ作成およびコミュニティサイトのページの変更を実行できます。 |
| コミュニティイネーブルメントマネージャー | コミュニティイネーブルメントマネージャーグループは、コミュニティサイトのイネーブルメントマネージャーグループの管理者の割り当てに使用できるユーザーで構成されます。 |
| Community &lt;*site name* > Siteenablementmanagers | The Community Site Enablement Managers group consists of users who have been assigned to manage a community site&#39;s enablement [resources](resources.md). |
| なし | 匿名のサイト訪問者はオーサー環境にアクセスできません。 |

### システム管理者 {#system-administrators}

管理者グループのメンバーは、オーサー環境とパブリッシュ環境の両方で AEM のインストールの初期設定を実行できるシステム管理者です。

For demonstration and development purposes, the administrators group has a member whose userid is *admin* and password is *admin*.

実稼動環境では、デフォルトの管理者グループを修正する必要があります。

[セキュリティチェックリスト](../../help/sites-administering/security-checklist.md)に従っているかを確認してください。

## パブリッシュ環境 {#publish-environment}

### メンバーになる {#becoming-a-member}

In the publish environment, depending on the [settings](sites-console.md#user-management) of the community site, a site visitor may become a community member:

* コミュニティサイトが非公開（非公開）の場合：
   * 招待による
   * 管理者の操作による

* コミュニティサイトが公開（開いている）とき：
   * 自己登録による
   * FacebookおよびTwitterでのソーシャルログイン

>[!NOTE]
>
>サイト訪問者が 1 つのオープンコミュニティサイトに登録すると、その訪問者は自動的に、同じパブリッシュ環境上の他のオープンコミュニティサイトのメンバーになります。


### パブリッシュグループの役割 {#publish-group-roles}

| メンバーが所属するグループ | 主な役割 |
|---|---|
| Community &lt;*site name*> Members | コミュニティサイトメンバーは、登録済みのユーザーです。ログイン、プロファイルの変更、オープンコミュニティグループへの参加、コミュニティへのコンテンツの投稿、他のメンバーへのメッセージの送信、サイトのアクティビティの追跡を行うことができます。 |
| Community &lt;*site name*> Moderators | コミュニティサイトモデレーターは、モデレートコンソールを使用した UGC の一括モデレートや、コンテンツが投稿されたページでのコンテキスト内モデレートを実行できる、信頼されているコミュニティメンバーです。 |
| Community &lt;*site name*> &lt;*group name*> Members | コミュニティグループメンバーは、オープンコミュニティグループに参加したコミュニティメンバーか、クローズドコミュニティグループに招待されたコミュニティメンバーのどちらかです。このメンバーは、サイト内のそのコミュニティグループのメンバーの能力を持ちます。 |
| Community &lt;*site name*> Groupadministrators | コミュニティサイトグループ管理者は、コミュニティサイト内のサブコミュニティ（グループ）を作成および管理する権限を持った、信頼されているコミュニティメンバーです。コンテキスト内モデレートを提供する機能が含まれます。 |
| 権限を持つメンバーのセキュリティグループ&#x200B;** | コンテンツ作成を制限するために、手動で作成および保守されるユーザーグループです。[権限を持つメンバーグループ](#privileged-members-group)を参照してください。 |
| なし | サイトを発見した匿名のサイト訪問者は、匿名アクセスが許可されているコミュニティサイトを表示および検索できます。コンテンツに参加し投稿するには、ユーザーが自己登録（許可されている場合）し、コミュニティのメンバーになる必要があります。 |

### パブリッシュグループの役割へのメンバーの割り当て {#assigning-members-to-publish-group-roles}

When [creating a community site](sites-console.md) in the author environment, or when [modifying site properties,](sites-console.md#modifying-site-properties) members may be assigned various roles performed in the publish environment, such as moderators, group administrators, resource contacts, or privileged members.

[トンネルサービスを有効にすると](sync.md#accessingpublishusersfromauthor) 、割り当ての選択肢が、作成者のユーザーではなく、発行時にメンバーから表示されます。

The selected members will be automatically assigned to the [appropriate group](#publish-group-roles) and their memberships will be included when the community site is (re)published.

### Privileged Members Group {#privileged-members-group}

権限を持つメンバーのセキュリティグループの目的は、特定のコミュニティ機能のコンテンツの作成を、権限を持つコミュニティサイトの一部のメンバーだけに限定することです。

権限を持つメンバーグループは、[コミュニティグループコンソール](members.md)を使用して作成および管理します。

権限を持つメンバーグループを作成し、さらに[トンネルサービスを有効](sync.md#accessingpublishusersfromauthor)にしたら、既存のコミュニティサイトの構造を[変更](sites-console.md#modify-structure)してコミュニティ機能の設定を編集し、「権限を持つメンバーを許可」をオンにし、作成済みのグループを追加できます。

以下のコミュニティ機能では、権限を持つメンバーグループを 1 つ以上指定できます。

* [ブログ機能](functions.md#blog-function) — 新しい記事の作成を制限します。
* [カレンダー機能](functions.md#calendar-function) — 新しいイベントの作成を制限
* [フォーラム機能](functions.md#forum-function) — 新しいトピックの作成を制限します。
* [QnA関数](functions.md#qna-function) — 新しい質問の作成を制限します。

コミュニティ機能にセキュリティ制限がない（権限を持つメンバーグループが割り当てられていない）場合は、すべてのコミュニティサイトメンバーが、その機能のコンテンツ（記事、イベント、トピック、質問）を作成できます。

>[!NOTE]
>
>あるコミュニティサイトで、権限を持つメンバーグループにユーザーを追加しても、そのユーザーが同じコミュニティサイトのメンバーでもある場合は、そのユーザーに対して作成権限が与えられるだけです。


## コミュニティメンバーの作成 {#creating-community-members}

### リポジトリの場所 {#repository-location}

特定の機能を正しく動作させるためには、適切な権限を持つユーザーとユーザーグループを作成する必要があります。

When members are created in `/home/users/community`, they inherit the proper ACLs that give read privileges to members&#39; profiles.

Similarly, custom community user groups (such as privileged members groups) should be created in `/home/groups/community`.

[コミュニティメンバーコンソールとグループコンソール](members.md)を使用すると、ユーザーとグループがそれぞれのパスに作成されます。

To specify a custom path requires use of the classic security UI, which is accessible at [https://&lt;server>:&lt;port>/useradmin](http://localhost:4503/useradmin).

To give read privileges for custom member paths, on all publish instances set ACLs similar to `/home/users/community`:

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="everyone"
  rep:privileges="{Name}[jcr:read]" >
  <rep:restrictions
    jcr:primaryType="rep:Restrictions"
    rep:glob="*/profile*" />
</allow>
```

To give the proper privileges for custom member group paths, such as /home/groups/mycompany, on all publish instances set ACLs similar to `/home/groups/community`:

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="community-administrators"
  rep:privileges="{Name}[jcr:read]"  />
```

### コンソール {#consoles}

オーサー環境でのみ使用できる、以下の 4 つの独立したコンソールがあります。

| console | ツール／セキュリティ／ユーザー | ツール／セキュリティ／グループ | コミュニティ／メンバー | コミュニティ／グループ |
|----------|-----------------------|------------------------|------------------------------------------------------------|------------------------------------------------------------|
| 管理対象 | オーサー環境のユーザー | オーサー環境のユーザーグループ | パブリッシュ環境のメンバー | パブリッシュ環境のメンバーグループ |
| 必須 | 管理者権限 | 管理者権限 | 管理者権限、トンネルサービス、ユーザーの同期（パブリッシュファームの場合） | 管理者権限、トンネルサービス、ユーザーの同期（パブリッシュファームの場合） |

### コミュニティイネーブルメントマネージャーの役割 {#community-enablement-manager-role}

[イネーブルメントコミュニティ](overview.md#enablement-community)では、メンバーごとに関連するコストが発生することから、通常は、サイト訪問者による自己登録機能は許可されません。Enablement learners and resources are managed by a user assigned the [role](#author-group-roles) of `enablement manager` [during site creation](sites-console.md#enablement) on author (added as member of group `Community <site-name> Siteenablementmanagers`). The `enablement manager` is also responsible for [assigning learning resources](resources.md) to community members on author.

Only users who are members of the global `Community Enablement Managers` group may be selected as an `enablement manager` for a specific community site.

To create a user who may be assigned the role of `Community Site Enablement Manager`, use the classic UI security console in order to specify the path:

オーサーインスタンスの場合：

1. 管理者権限でログインし、従来のUIセキュリティコンソールを参照します。

   For example, [http://localhost:4502/useradmin](http://localhost:4502/useradmin)

2. From the Edit menu, select **[!UICONTROL Create User]**.
3. ダイアログに入力 `Create User` します。
   * Path must be `/home/users/community`.
4. 「**[!UICONTROL 作成]**」を選択します。

   ![chlimage_1-130](assets/chlimage_1-130.png)

* 左側のペインで、新しく作成されたユーザーを検索し、右側のペインに表示するように選択します。

   ![chlimage_1-131](assets/chlimage_1-131.png)

左側のウィンドウで、

1. Clear the search box and select **[!UICONTROL Hide Users]**.
2. Locate and drag `community-enablementmanagers` to the **[!UICONTROL Groups]** tab of the new user displayed in the right pane.

   ![chlimage_1-132](assets/chlimage_1-132.png)

### コミュニティ管理者の役割 {#community-administrators-role}

[オーサーグループの役割](#author-group-roles)の表に示したとおり、コミュニティ管理者グループのメンバーは、コミュニティサイトの作成、サイトの管理、メンバーの管理（メンバーのコミュニティの使用を禁止できる）、コンテンツのモデレートをおこなうことができます。

Follow the same steps as creating and assigning a user to the role of [enablement manager](#communitysiteenablementmanagerrole), but add c `ommunity-administrators` group under the user&#39;s Groups tab.

### LDAP の統合 {#ldap-integration}

AEM は、ユーザーの認証およびユーザーアカウントの作成で LDAP の使用をサポートします。This is detailed in [Configuring LDAP with AEM 6](../../help/sites-administering/ldap-config.md).

コミュニティメンバーおよびメンバーグループ固有の設定の詳細の一部を次に示します。

1. 各AEM発行インスタンスのLDAPを設定します。
2. [LDAP IDプロバイダ](../../help/sites-administering/ldap-config.md#configuring-the-ldap-identity-provider)

   * 特別な指示はありません

3. [同期ハンドラ](../../help/sites-administering/ldap-config.md#configuring-the-synchronization-handler)

   * 次のプロパティを設定します。

      * **[!UICONTROL User auto membership]**: `community-<site name>-<uid>-members`
      * **[!UICONTROL User Path Prefix]**: `/community`
      * **[!UICONTROL Group Path Prefix]**: `/community`

4. [外部ログインモジュール](../../help/sites-administering/ldap-config.md#the-external-login-module)

   * 特別な指示はありません。

This results in users automatically being assigned to the community site&#39;s members group and the repository location being `/home/users/community` and `/home/groups/community`, so that they inherit the appropriate permissions to see one another&#39;s profile.

* The `User auto membership` value should be the `rep:authorizableId` property, not the `givenName` (display name) from the profile.

## AEM インスタンス間のユーザーの同期 {#synchronizing-users-among-aem-instances}

[パブリッシュファーム](topologies.md)を使用する場合は、まず 1 つのインスタンスにユーザーを読み込みます。続いて[ユーザーの同期を有効](sync.md)にし、ユーザーを Sling で他のパブリッシュインスタンスに配信することによって、各パブリッシュインスタンスで各ユーザーのパスが同じになるようにします。

ユーザーグループを読み込む場合、各パブリッシュインスタンスでユーザーグループのパスが同じになるようにするには、1 つのインスタンスに読み込んでから、エクスポート用の[パッケージを作成](../../help/sites-administering/package-manager.md#creating-a-new-package)し、そのパッケージを他のすべてのパブリッシュインスタンスにインストールします。

現在は、ユーザーの同期を実行すると、ユーザーグループの&#x200B;*メンバーシップ*&#x200B;だけが同期されます。ユーザーの同期によるユーザーグループの同期は、今後のリリースで搭載されます。

## コミュニティグループについて {#about-community-groups}

グループに関しては、以下の 2 種類のトピックがあります。

* **[コミュニティグループ](overview.md#communitygroups)**

   コミュニティグループとは、コミュニティグループの作成をサポートするコミュニティサイトの発行環境で作成できるサブコミュニティです。 コミュニティグループを作成すると、Webサイトに追加されるページが増え、親コミュニティサイトと同じ方法で管理されます。 For more information visit [Community Group Essentials](essentials-groups.md) for developers and [Community Group](creating-groups.md) for authors.

* **[メンバーグループ](../../help/sites-administering/security.md)**

   メンバーグループは、メンバーが属するグループで、グループコンソールを通じて管理されます。 このページに関する議論の多くは、メンバーグループに費やされています。 The member groups automatically created for a community site, which are prefixed with *`Community`*, may be referred to as a community group, therefore the context of the discussion must be considered.
