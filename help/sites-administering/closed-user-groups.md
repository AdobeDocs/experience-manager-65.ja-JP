---
title: AEM の閉じられたユーザーグループ
seo-title: AEM の閉じられたユーザーグループ
description: AEM の閉じられたユーザーグループについて説明します。
seo-description: AEM の閉じられたユーザーグループについて説明します。
uuid: 83396163-86ce-406b-b797-2457ed975ccd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: a2bd7045-970f-4245-ad5d-a272a654df0a
docset: aem65
translation-type: tm+mt
source-git-commit: 2142df4f7579e052e18879b437fc43911010b475
workflow-type: tm+mt
source-wordcount: '6890'
ht-degree: 61%

---


# AEM の閉じられたユーザーグループ{#closed-user-groups-in-aem}

## 概要 {#introduction}

AEM 6.3 より、「閉じられたユーザーグループ」という新しい実装が組み込まれています。これは、既存の実装が抱えていたパフォーマンス、スケーラビリティおよびセキュリティ上の問題を解決するためのものです。

>[!NOTE]
>
>このドキュメントでは、説明を簡略にするために、閉じられたユーザーグループ（Closed User Group）を「CUG」という略語で表記します。

新しい実装の目標は、必要に応じて既存の機能を対象とし、古いバージョンの問題や設計上の制限に対処することです。 その結果として、次の特性を持つ新しい CUG デザインが生まれました。

* 認証要素と承認要素の切り離し。これらの要素は、個別に使用することも、一緒に使用することもできます。
* 他のアクセス制御設定や権限要件と競合することなく、設定済みの CUG ツリーで制限付き読み取りアクセスを反映する専用の承認モデル。
* 制限付き読み取りアクセスのアクセス制御設定（通常オーサリングインスタンスで必要）と、通常は公開でのみ必要な権限の評価とは別個の設定です。
* 権限を昇格しなくても、制限付き読み取りアクセスを編集可能。
* 認証要件をマークするための、専用のノードタイプ拡張。
* 認証要件に関連付けられる、オプションのログインパス。

### 新しいカスタムユーザーグループの実装 {#the-new-custom-user-group-implementation}

CUG は、AEM のコンテキストで知られるように、次の手順で構成されます。

* 保護する必要があるツリーに対する読み取りアクセスを制限して、特定の CUG インスタンスと一緒にリストされるプリンシパルか、CUG 評価全体から除外されるプリンシパルにのみ読み取りを許可します。これは、**承認**&#x200B;要素と呼ばれます。
* 特定のツリーに認証を強制的に適用します。オプションで、そのツリー専用のログインページも指定できます（後で除外されます）。これは、**認証**&#x200B;要素と呼ばれます。

この新しい実装では、認証要素と承認要素が切り離されています。AEM 6.3 の時点では、認証要件を明示的に追加しなくても、読み取りアクセスを制限できます。例えば、特定のインスタンス全体で認証が必要な場合や、既に認証を必要としているサブツリー内に特定のツリーが既に存在している場合はそうです。

同様に、有効な権限設定を変更せずに、特定のツリーに認証要件をマークすることもできます。 これらの組み合わせと結果については、[CUG ポリシーと認証要件の組み合わせ](/help/sites-administering/closed-user-groups.md#combining-cug-policies-and-the-authentication-requirement)の節に示します。

## 概要 {#overview}

### 承認：読み取りアクセスの制限 {#authorization-restricting-read-access}

CUG の重要な機能は、コンテンツリポジトリ内の特定のツリーに対する読み取りアクセスを制限することです（選択されたプリンシパルを除く）。新しい実装では、実行中にデフォルトのアクセス制御コンテンツを操作しません。これまでとは異なるアプローチとして、CUG を表す専用のアクセス制御ポリシータイプを定義します。

#### CUG 用のアクセス制御ポリシー {#access-control-policy-for-cug}

この新しいタイプのポリシーは、次の特性を持ちます。

* org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicyタイプのアクセス制御ポリシー（Apache Jackrabbit APIで定義）;
* PrincipalSetPolicyは、変更可能なプリンシパルのセットに対する権限を付与します。
* 付与される権限とポリシーの有効範囲は、実装の詳細です。

CUGを表すために使用されるPrincipalSetPolicyの実装には、次の定義も含まれます。

* CUG ポリシーは、通常の JCR アイテムへの読み取りアクセスのみを付与します（例えば、アクセス制御コンテンツは除外されます）。
* 有効範囲は、CUG ポリシーを保持する、アクセス制御されたノードによって定義されます。
* CUG ポリシーはネストできます。ネストされた CUG は、「親」CUG のプリンシパルセットを継承しなくても、新しい CUG を開始できます。
* ポリシーの効果は、評価が有効になっている場合は次にネストされた CUG に至るまで、サブツリー全体に継承されます。

これらのCUGポリシーは、oak-authorization-cugと呼ばれる別の認証モジュールを介してAEMインスタンスにデプロイされます。 このモジュールは、独自のアクセス制御管理および権限評価に付属しています。つまり、デフォルトの AEM のセットアップには、複数の承認メカニズムを組み合わせた Oak コンテンツリポジトリ設定が付属しています。For more info, see [this page on the Apache Oak Documentation](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html).

この複合セットアップでは、新しいCUGは、ターゲットノードにアタッチされた既存のアクセス制御コンテンツを置き換えませんが、補助として設計されており、AEMではデフォルトでアクセス制御リストとなり、元のアクセス制御に影響を与えずに後で削除できます。

前の実装とは対照的に、新しい CUG ポリシーは常にアクセス制御コンテンツとして認識、処理されます。つまり、新しい CUG ポリシーは、JCR アクセス制御管理 API を使用して作成、編集されるということです。For more info, see the [Managing CUG Policies](#managing-cug-policies) section.

#### CUG ポリシーの権限評価 {#permission-evaluation-of-cug-policies}

CUG の専用アクセス制御管理とは別に、新しい承認モデルでは、CUG ポリシーの権限評価を条件付きで有効にできます。このモデルでは、CUG ポリシーをステージング環境に設定しておき、実稼動環境にレプリケーションされた後で、有効な権限の評価を有効にするという手法を使用できます。

CUG ポリシーの権限評価と、デフォルトまたは追加の承認モデルとの連携は、Apache Jackrabbit Oak の複数の承認メカニズム用に設計されたパターンに従います。つまり、すべてのモデルがアクセスを付与する場合にのみ、特定の権限セットが付与されます。See [this page](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html) for more details.

CUG ポリシーを処理、評価するために設計された承認モデルに関連付けられる権限評価には、次の特性が適用されます。

* 通常のノードとプロパティの読み取り権限のみを処理し、アクセス制御コンテンツを読み取りません。
* 書き込み権限や、保護されたJCRコンテンツの変更に必要な権限(アクセス制御、ノードタイプ情報、バージョン管理、ロック、ユーザー管理など)は処理されません。これらの権限はCUGポリシーの影響を受けず、関連付けられた承認モデルによって評価されません。 これらの権限が付与されるかどうかは、セキュリティ設定に設定された他のモデルに応じます。

権限評価に対する単一のCUGポリシーの影響を以下に要約できます。

* 読み取りアクセスは拒否されます（除外されたプリンシパルやポリシーにリストされたプリンシパルを含むサブジェクトを除く）。
* ポリシーは、ポリシーとそのプロパティを保持するアクセス制御ノードに対して有効になります。
* この効果は、階層（アクセス制御ノードによって定義される項目ツリー）に追加的に継承されます。
* ただし、アクセス制御ノードの兄弟や先祖には影響しません。
* 特定の CUG の継承は、ネストされた CUG で止まります。

#### ベストプラクティス {#best-practices}

CUG を介した、制限付き読み取りアクセスを定義する際は、次のベストプラクティスを考慮する必要があります。

* CUG は、読み取りアクセスの制限のために必要なのか、認証要件のために必要なのかを判断します。後者の場合、または両方が必要な場合は、認証要件の詳細について、「ベストプラクティス」の項を参照してください。
* 保護する必要があるデータやコンテンツの脅威モデルを作成して、脅威の範囲を識別し、データの感度と、承認されたアクセスに関連付けられている役割を明確にします。
* リポジトリコンテンツと CUG をモデル化して、承認に関する一般事項とベストプラクティスを覚えておきます。

   * 特定の CUG と、セットアップに導入されている他のモジュールの評価によって、特定のサブジェクトが特定のリポジトリアイテムを読み取ることが許可される場合にのみ、読み取り権限が付与されます。
   * 読み取りアクセスが既に他の承認モジュールによって制限されている場合は、冗長 CUG の作成を回避します。
   * ネストされた CUG が大量に必要になる場合は、コンテンツデザインに問題がある可能性があります。
   * CUG が大量に必要な場合（例えば、各ページに CUG が必要な場合）は、そのアプリケーションやコンテンツのセキュリティニーズに見合ったカスタム承認モデルを導入することが必要な可能性があります。

* CUG ポリシーのためにサポートされるパスを、リポジトリ内のいくつかのツリーに制限して、最適なパフォーマンスを維持します。例えば、/contentノードの下のCUGを、AEM 6.3以降のデフォルト値として出荷済みとして許可します。
* CUG ポリシーは、少数のプリンシパルに読み取りアクセスを付与することを想定して設計されています。大量のプリンシパルが必要な場合は、コンテンツやアプリケーションのデザインに関する問題が発生する可能性があるので、再検討する必要があります。

### 認証：認証要件の定義 {#authentication-defining-the-auth-requirement}

CUG 機能の認証関連のパーツにより、認証を必要とするツリーをマークできます。オプションで、専用のログインページも指定できます。In accordance to the previous version, the new implementation allows to mark trees that require authentication in the content repository and conditionally enable synchronization with the `Sling org.apache.sling.api.auth.Authenticator`responsible for ultimately enforcing the requirement and redirecting to a login resource.

これらの要件は、`sling.auth.requirements` 登録プロパティを提供する OSGi サービスによって Authenticator に登録されます。その後、これらのプロパティは、認証要件の動的な拡張に使用されます。詳しくは、[Sling に関するドキュメント](https://sling.apache.org/apidocs/sling7/org/apache/sling/auth/core/AuthConstants.html#AUTH_REQUIREMENTS)を参照してください。

#### 専用の Mixin タイプによる認証要件の定義 {#defining-the-authentication-requirement-with-a-dedicated-mixin-type}

For security reasons the new implementation replaces the usage of a residual JCR property by a dedicated mixin type called `granite:AuthenticationRequired`, which defines a single optional property of type STRING for the login path `granite:loginPath`. この mixin タイプに関連するコンテンツが変更された場合にのみ、Apache Sling Authenticator に登録される要件が更新されます。The modifications are tracked upon persisting any transient modifications and thus require a `javax.jcr.Session.save()` call to become effective.

The same applies for the `granite:loginPath` property. 認証要件に関連するミックスインの種類で定義されている場合にのみ考慮されます。 この名前を持つ残存のプロパティを非構造化JCRノードに追加しても、望ましい効果は表示されず、OSGi登録を更新するハンドラによってそのプロパティは無視されます。

>[!NOTE]
>
>ログインパスプロパティの設定はオプションです。ログインパスプロパティは、認証を必要とするツリーがデフォルトまたは継承されたログインページにフォールバックできない場合にのみ設定する必要があります。詳しくは、後述の[ログインパスの評価](/help/sites-administering/closed-user-groups.md#evaluation-of-login-path)を参照してください。

#### Sling Authenticator への認証要件とログインパスの登録 {#registering-the-authentication-requirement-and-login-path-with-the-sling-authenticator}

この認証要件は、特定の実行モードとコンテンツリポジトリ内の小さなツリーのサブセットに限定されると考えられるので、要件mixinタイプとログインパスプロパティの追跡は、条件付きで、サポートされるパスを定義する対応する設定に連結されます（後述の設定オプションを参照）。 したがって、サポートパスの有効範囲内で変更があった場合にのみ、OSGi 登録の更新が実行され、それ以外の場所では、mixin タイプもログインパスプロパティも無視されます。

現在は、デフォルトのAEM設定でこの設定が使用され、作成者実行モードでのミックスインの設定が許可されますが、パブリッシュインスタンスへの複製時にのみ有効になります。 See [this page](https://sling.apache.org/documentation/the-sling-engine/authentication/authenticationframework.html) for details how Sling enforces the authentication requirement.

Adding the `granite:AuthenticationRequired` mixin type within the configured supported paths will cause the OSGi registration of the responsible handler to be updated containing an new, additional entry with the `sling.auth.requirements` property. If a given authentication requirement specifies the optional `granite:loginPath` property, the value is additionally registered with the Authenticator with a &#39;-&#39; prefix in order to be excluded from authentication requirement.

#### Evaluation and Inheritance of the Authentication Requirement {#evaluation-and-inheritance-of-the-authentication-requirement}

Apache Sling 認証要件は、ページやノード階層を介して継承されることが期待されます。認証要件の継承と評価の詳細（順序や優先順位など）は、実装の詳細になるので、このドキュメントでは説明しません。

#### ログインパスの評価 {#evaluation-of-login-path}

The evaluation of the login path and redirect to the corresponding resource upon authentication is currently an implementation detail of the Adobe Granite Login Selector Authentication Handler ( `com.day.cq.auth.impl.LoginSelectorHandler`), which is an Apache Sling AuthenticationHandler configured with AEM by default.

Upon calling `AuthenticationHandler.requestCredentials` this handler makes an attempt to determine the mapping login page to which the user will be redirected. この決定は、次の手順に従います。

* リダイレクトの理由として、パスワードの失効と、通常のログインに必要な処理を区別します。
* 通常のログインに必要な処理である場合は、ログインパスを取得できるかどうかを、以下の順序で確認します。

   * from the LoginPathProvider as implemented by the new `com.adobe.granite.auth.requirement.impl.RequirementService`,
   * 廃止された古い CUG 実装から
   * from the Login Page Mappings, as defined with the `LoginSelectorHandler`,
   * and finally, fallback to the Default Login Page, as defined with the `LoginSelectorHandler`.

* 前述の呼び出しから有効なログインパスが取得されると、ユーザーのリクエストはすぐに、そのページにリダイレクトされます。

The target of this documentation is the evaluation of the login path as exposed by the internal `LoginPathProvider` interface. AEM 6.3 以降に付属する実装は、次のように動作します。

* ログインパスの登録は、リダイレクトの理由が、パスワードの失効であるか、通常のログインに必要な処理であるかによって異なります。
* 通常のログインに必要な処理である場合は、ログインパスを取得できるかどうかを、以下の順序で確認します。

   * from the `LoginPathProvider` as implemented by the new `com.adobe.granite.auth.requirement.impl.RequirementService`,
   * 廃止された古い CUG 実装から
   * from the Login Page Mappings as defined with the `LoginSelectorHandler`,
   * and finally fallback to the Default Login Page as defined with the `LoginSelectorHandler`.

* 前述の呼び出しから有効なログインパスが取得されると、ユーザーのリクエストはすぐに、そのページにリダイレクトされます。

The `LoginPathProvider` as implemented by the new auth-requirement support in Granite exposes login paths as defined by the `granite:loginPath` properties, which in turn are defined by the mixin type as described above. ログインパスとプロパティ値自体を保持するリソースパスのマッピングはメモリ内に保存され、階層内にある他のノードの適切なログインパスを検出するために評価されます。

>[!NOTE]
>
>この評価は、設定済みのサポートパス内に存在するリソースに関連付けられているリクエストに対してのみ実行されます。それ以外のリクエストについては、ログインパスを判定する別の方法が評価されます。

#### ベストプラクティス {#best-practices-1}

認証要件を定義する際は、次のベストプラクティスを考慮する必要があります。

* 認証要件のネストを回避します。ツリーの先頭部に認証要件マーカーを 1 つ配置するだけで十分です。そのマーカーは、ターゲットノードによって定義されるサブツリー全体に継承されます。そのツリー内に他の認証要件があると、Apache Sling 内で認証要件を評価する際にパフォーマンス上の問題となる可能性があります。承認と認証に関連する CUG エリアを切り離すことで、CUG やその他のポリシーによって読み取りアクセスを制限すると同時に、ツリー全体に認証を適用できます。
* ネストされたサブツリーを再度要件から除外する必要なく、認証要件がツリー全体に適用されるようなモデルリポジトリコンテンツ。
* 余分なログインパスの指定を回避するには、次のようにします。

   * 継承に依存し、ネストされたログインパスを定義しない。
   * オプションのログインパスを、デフォルト値または継承された値に対応する値に設定しないでください。
   * アプリケーション開発者は、`LoginSelectorHandler` に関連付けられるグローバルなログインパス設定（デフォルトとマッピングの両方）に設定する必要があるログインパスを識別してください。

## リポジトリでの表現 {#representation-in-the-repository}

### リポジトリでの CUG ポリシーの表現 {#cug-policy-representation-in-the-repository}

Oakのドキュメントでは、新しいCUGポリシーがリポジトリのコンテンツにどのように反映されるかについて説明します。 詳しくは、[このページ](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#Representation_in_the_Repository)を参照してください。

### リポジトリでの認証要件 {#authentication-requirement-in-the-repository}

個別の認証要件の必要性は、専用のミックスインノードタイプをターゲットノードに配置したリポジトリコンテンツに反映されます。 この mixin タイプは、オプションのプロパティを定義して、ターゲットノードによって定義されるツリーの専用ログインページを指定します。

ログインパスに関連付けられるページは、ツリーの内部または外部のいずれにでも配置できます。このページは、認証要件から除外されます。

```java
[granite:AuthenticationRequired]
      mixin
      - granite:loginPath (STRING)
```

## CUG ポリシーと認証要件の管理 {#managing-cug-policies-and-authentication-requirement}

### CUG ポリシーの管理 {#managing-cug-policies}

The new type of access control policies to restrict read access for a CUG is managed using the JCR access control management API and follows the mechanisms described with the [JCR 2.0 specification](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html).

#### 新しい CUG ポリシーの設定 {#set-a-new-cug-policy}

次のコードは、CUG がまだ設定されていないノードに新しい CUG ポリシーを適用します。Please note that `getApplicablePolicies` will only return new policies that have not been set before. 最後に、このポリシーを書き戻して、変更を保存する必要があります。

```java
String path = [...] // needs to be a supported, absolute path

Principal toAdd1 = [...]
Principal toAdd2 = [...]
Principal toRemove = [...]

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

AccessControlPolicyIterator it = acMgr.getApplicablePolicies(path);
while (it.hasNext()) {
        AccessControlPolicy policy = it.nextAccessControlPolicy();
        if (policy instanceof PrincipalSetPolicy) {
           cugPolicy = (PrincipalSetPolicy) policy;
           break;
        }
}

if (cugPolicy == null) {
   log.debug("no applicable policy"); // path not supported or no applicable policy (e.g.
                                                   // the policy was set before)
   return;
}

cugPolicy.addPrincipals(toAdd1, toAdd2);
cugPolicy.removePrincipals(toRemove));

acMgr.setPolicy(path, cugPolicy); // as of this step the policy can be edited/removed
session.save();
```

#### 既存の CUG ポリシーの編集 {#edit-an-existing-cug-policy}

既存の CUG ポリシーを編集するには、次の手順が必要です。Please note that the modified policy needs to written back and changes needs to be persisted using `javax.jcr.Session.save()`.

```java
String path = [...] // needs to be a supported, absolute path

Principal toAdd1 = [...]
Principal toAdd2 = [...]
Principal toRemove = [...]

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

for (AccessControlPolicy policy : acMgr.getPolicies(path)) {
     if (policy instanceof PrincipalSetPolicy) {
        cugPolicy = (PrincipalSetPolicy) policy;
        break;
     }
}

if (cugPolicy == null) {
   log.debug("no policy to edit"); // path not supported or policy not set before
   return;
}

if (cugPolicy.addPrincipals(toAdd1, toAdd2) || cugPolicy.removePrincipals(toRemove)) {
   acMgr.setPolicy(path, cugPolicy);
   session.save();
} else {
     log.debug("cug policy not modified");
}
```

### 有効な CUG ポリシーの取得 {#retrieve-effective-cug-policies}

JCR アクセス制御管理では、特定のパスで有効なポリシーを取得する最善の方法を定義します。Due to the fact that evaluation of CUG policies is conditional and depends on the corresponding configuration to be enabled, calling `getEffectivePolicies` is a convenient way to verify if a given CUG policy is taking effect in a given installation.

>[!NOTE]
>
>Please note the difference between `getEffectivePolicies` and the subsequent code example that walks up the hierarchy to find if a given path is already part of an existing CUG.

```java
String path = [...] // needs to be a supported, absolute path

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

// log an debug message of all CUG policies that take effect at the given path
// there could be zero, one or many (creating nested CUGs is possible)
for (AccessControlPolicy policy : acMgr.getEffectivePolicies(path) {
     if (policy instanceof PrincipalSetPolicy) {
        String policyPath = "-";
        if (policy instanceof JackrabbitAccessControlPolicy) {
           policyPath = ((JackrabbitAccessControlPolicy) policy).getPath();
        }
        log.debug("Found effective CUG for path '{}' at '{}', path, policyPath);
     }
}
```

#### 継承された CUG ポリシーの取得 {#retrieve-inherited-cug-policies}

ネストされたすべての CUG が有効かどうかに関係なく、特定のパスに定義されているそれらの CUG を検出します。詳しくは、[設定オプション](/help/sites-administering/closed-user-groups.md#configuration-options)の節を参照してください。

```java
String path = [...]

List<AccessControlPolicy> cugPolicies = new ArrayList<AccessControlPolicy>();
while (isSupportedPath(path)) {
     for (AccessControlPolicy policy : acMgr.getPolicies(path)) {
         if (policy instanceof PrincipalSetPolicy) {
            cugPolicies.add(policy);
         }
      }
      path = (PathUtils.denotesRoot(path)) ? null : PathUtils.getAncestorPath(path, 1);
}
```

#### プリンシパルによる CUG ポリシーの管理 {#managing-cug-policies-by-pincipal}

The extensions defined by `JackrabbitAccessControlManager` that allow to edit access control policies by principal are not implemented with CUG access control management, as by definition a CUG policy always affects all principals: those listed with the `PrincipalSetPolicy` are being granted read access while all other principals will be prevented to read content in the tree defined by the target node.

これらに対応するメソッドは常に、空のポリシー配列を返しますが、例外はスローしません。

### 認証要件の管理 {#managing-the-authentication-requirement}

新しい認証要件の作成、変更、または削除は、ターゲットノードの有効なノードタイプを変更することで達成される。 その後、オプションのログインパスプロパティへの書き込みには、通常の JCR API を使用できます。

>[!NOTE]
>
>The modifications to a given target node mentioned above will only be reflected on the Apache Sling Authenticator if the `RequirementHandler` has been configured and the target is contained in the trees defined by the supported paths (see section Configuration Options).
>
>詳しくは、「Mixinノードタイプの [割り当て](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.10.3 Mixinノードタイプの割り当て)」および「ノードの [追加」および「プロパティの設定](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.4ノードの追加とプロパティの設定)」を参照してください。

#### 新しい認証要件の追加 {#adding-a-new-auth-requirement}

次に、新しい認証要件の作成手順を示します。Note that the requirement will only be registered with the Apache Sling Authenticator if the `RequirementHandler` has been configured for the tree containing the target node.

```java
Node targetNode = [...]

targetNode.addMixin("granite:AuthenticationRequired");
session.save();
```

#### ログインパスを含む新しい認証要件の追加 {#add-a-new-auth-requirement-with-login-path}

次に、ログインパスを含む新しい認証要件の作成手順を示します。Note, that the requirement and the exclusion for the login path will only be registered with the Apache Sling Authenticator if the `RequirementHandler` has been configured for the tree containing the target node.

```java
Node targetNode = [...]
String loginPath = [...] // STRING property

Node targetNode = session.getNode(path);
targetNode.addMixin("granite:AuthenticationRequired");

targetNode.setProperty("granite:loginPath", loginPath);
session.save();
```

#### 既存のログインパスの変更 {#modify-an-existing-login-path}

次に、既存のログインパスの変更手順を示します。The modification will only be registered with the Apache Sling Authenticator if the `RequirementHandler` has been configured for the tree containing the target node. 以前のログインパス値は登録から削除されます。ターゲットノードに関連付けられている認証要件は、この変更の影響を受けません。

```java
Node targetNode = [...]
String newLoginPath = [...] // STRING property

if (targetNode.isNodeType("granite:AuthenticationRequired")) {
   targetNode.setProperty("granite:loginPath", newLoginPath);
   session.save();
} else {
     log.debug("cannot modify login path property; mixin type missing");
}
```

#### 既存のログインパスの削除 {#remove-an-existing-login-path}

次に、既存のログインパスの削除手順を示します。ログインパスのエントリは、ターゲットノードを含むツリーに `RequirementHandler` が設定済みの場合にのみ、Apache Sling Authenticator から登録が解除されます。ターゲットノードに関連付けられている認証要件は、影響を受けません。

```java
Node targetNode = [...]

if (targetNode.hasProperty("granite:loginPath") &&
   targetNode.isNodeType("granite:AuthenticationRequired")) {
   targetNode.setProperty("granite:loginPath", null);
   session.save();
} else {
     log.debug("cannot remove login path property; mixin type missing");
}
```

また、次の方法でも、既存のログインパスを削除できます。

```java
String path = [...] // absolute path to target node

String propertyPath = PathUtils.concat(path, "granite:loginPath");
if (session.propertyExists(propertyPath)) {
    session.getProperty(propertyPath).remove();
    // or: session.removeItem(propertyPath);
    session.save();
}
```

#### 認証要件の削除 {#remove-an-auth-requirement}

次に、既存の認証要件の削除手順を示します。The requirement will only be unregistered from the Apache Sling Authenticator if the `RequirementHandler` has been configured for the tree containing the target node.

```java
Node targetNode = [...]
targetNode.removeMixin("granite:AuthenticationRequired");

session.save();
```

#### 有効な認証要件の取得 {#retrieve-effective-auth-requirements}

Apache Sling認証子に登録されている有効な認証要件をすべて読み取るための専用のパブリックAPIはありません。 However, the list is exposed in the system console at `https://<serveraddress>:<serverport>/system/console/slingauth` under the &quot;**Authentication Requirement Configuration**&quot; section.

以下に、デモコンテンツを含む AEM パブリッシュインスタンスの認証要件を示します。ハイライトされているコミュニティページのパスは、このドキュメントに記載される実装によって追加される要件が Apache Sling Authenticator にどのように反映されるかを示しています。

>[!NOTE]
>
>この例では、オプションのログインパスプロパティは設定されていません。したがって、認証に登録される 2 番目のエントリはありません。

![chlimage_1-24](assets/chlimage_1-24.jpeg)

#### 有効なログインパスの取得 {#retrieve-the-effective-login-path}

現在、認証が必要なリソースに匿名でアクセスした場合に有効となるログインパスを取得するパブリックAPIはありません。 ログインパスの取得方法について詳しくは、「ログインパスの評価」の節を参照してください。

ただし、この機能に定義されるログインパスとは別に、ログインへのリダイレクトを指定する他の方法があります。これについては、コンテンツモデルと、特定の AEM インストールの認証要件を設計する際に検討する必要があります。

#### 継承された認証要件の取得 {#retrieve-the-inherited-auth-requirement}

ログインパスの場合と同様に、コンテンツに定義された、継承される認証要件を取得できるパブリック API はありません。次の例は、特定の階層で定義されたすべての認証要件を、それらの要件が有効かどうかに関係なくリストする方法を示しています。 詳しくは、[設定オプション](/help/sites-administering/closed-user-groups.md#configuration-options)を参照してください。

>[!NOTE]
>
>認証要件とログインパスの両方に継承メカニズムを使用し、ネストされた認証要件を作成しないようにすることをお勧めします。
>
>For more information see [Evaluation and Inheritance of Authentication Requirement](#evaluation-and-inheritance-of-the-authentication-requirement), [Evaluation of Login Path](#evaluation-of-login-path) and [Best Practices](#best-practices).

```java
String path = [...]
Node node = session.getNode(path);

Map<String, String> authRequirements = new ArrayList<String, String>();
while (isSupported(node)) {
     if (node.isNodeType("granite:AuthenticationRequired")) {
         String loginPath = (node.hasProperty("granite:loginPath") ?
                                     node.getProperty("granite:loginPath").getString() :
                                     "";
        authRequirements.put(node.getPath(), loginPath);
        node = node.getParent();
     }
}
```

### CUG ポリシーと認証要件の組み合わせ {#combining-cug-policies-and-the-authentication-requirement}

次の表に、両方のモジュールが設定を介して有効になっている AEM インスタンスでの、CUG ポリシーと認証要件の有効な組み合わせを示します。

| **認証が必要です** | **ログインパス** | **制限付き読み取りアクセス** | **期待効果** |
|---|---|---|---|
| はい | 可 | はい | 有効な権限評価でアクセスが許可されている場合、特定のユーザーがCUGポリシーでマークされたサブツリーの表示のみを実行できます。 未認証ユーザーは、指定されたログインページにリダイレクトされます。 |
| はい | 不可 | 可 | 有効な権限評価でアクセスが許可されている場合、特定のユーザーがCUGポリシーでマークされたサブツリーの表示のみを実行できます。 認証されていないユーザーは、継承されたデフォルトのログインページにリダイレクトされます。 |
| はい | はい | 不可 | 未認証ユーザーは、指定されたログインページにリダイレクトされます。 認証要件でマークされているツリーを表示できるかどうかは、そのサブツリーに含まれる個々のアイテムの有効な権限に応じます。読み取りアクセスを制限する専用の CUG はありません。 |
| はい | 不可 | 不可 | 認証されていないユーザーは、継承されたデフォルトのログインページにリダイレクトされます。認証要件でマークされているツリーを表示できるかどうかは、そのサブツリーに含まれる個々のアイテムの有効な権限に応じます。読み取りアクセスを制限する専用の CUG はありません。 |
| 不可 | 不可 | 可 | 特定の認証済みユーザーまたは未認証ユーザーは、有効な権限評価によってアクセスが許可される場合にのみ、CUGポリシーでマークされたサブツリーを表示できます。 認証されていないユーザーも同じように処理され、ログインにリダイレクトされません。 |

>[!NOTE]
>
>「ログインパス」は、認証要件に関連するオプションの属性なので、「認証要件」 = なし、「ログインパス」 = ありの組み合わせは存在しません。定義するmixin型を追加せずにJCRプロパティをその名前で指定しても、影響はなく、対応するハンドラーでは無視されます。

## OSGi コンポーネントと設定 {#osgi-components-and-configuration}

この節では、新しい CUG 実装によって導入された OSGi コンポーネントと個々の設定オプションの概要を示します。

古い実装と新しい実装の設定オプションの包括的なマッピングについては、CUGマッピングのドキュメントも参照してください。

### 承認：セットアップと設定 {#authorization-setup-and-configuration}

新しい承認関連のパーツは、AEM のデフォルトインストールの一部である **Oak CUG Authorization** バンドル（`org.apache.jackrabbit.oak-authorization-cug`）に含まれています。このバンドルは、読み取りアクセスを管理する追加の方法として導入される、別の承認モデルを定義します。

#### CUG 承認のセットアップ {#setting-up-cug-authorization}

Setting up CUG authorization is described in detail in the [relevant Apache Documentation](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability). AEM ではデフォルトで、CUG 承認はすべての実行モードに導入されています。別の承認セットアップを必要とするインストールでは、CUG 承認を無効にすることもできます。

#### Referrer Filter の設定 {#configuring-the-referrer-filter}

You also need to configure the [Sling Referrer Filter](/help/sites-administering/security-checklist.md#the-sling-referrer-filter) with all hostnames that may be used to access AEM; for example, via CDN, Load Balancer, and any others.

Referrer Filter が設定されていないと、ユーザーが CUG サイトへのログインを試みたときに、次のようなエラーが表示されます。

```shell
31.01.2017 13:49:42.321 *INFO* [qtp1263731568-346] org.apache.sling.security.impl.ReferrerFilter Rejected referrer header for POST request to /libs/granite/core/content/login.html/j_security_check : https://hostname/libs/granite/core/content/login.html?resource=%2Fcontent%2Fgeometrixx%2Fen%2Ftest-site%2Ftest-page.html&$$login$$=%24%24login%24%24&j_reason=unknown&j_reason_code=unknown
```

#### OSGi コンポーネントの特性 {#characteristics-of-osgi-components}

認証要件を定義して、専用のログインパスを指定するために、次の 2 つの OSGi コンポーネントが導入されています。

* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration`
* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl`

**org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration**

<table>
 <tbody>
  <tr>
   <td>ラベル</td>
   <td>Apache Jackrabbit Oak CUGの設定</td>
  </tr>
  <tr>
   <td>説明</td>
   <td>CUG権限の設定と評価に専用の認証設定。</td>
  </tr>
  <tr>
   <td>設定プロパティ</td>
   <td>
    <ul>
     <li><code>cugSupportedPaths</code></li>
     <li><code>cugEnabled</code></li>
     <li><code>configurationRanking</code></li>
    </ul> <p>後述の「 <a href="#configuration-options">設定オプション</a> 」も参照してください。</p> </td>
  </tr>
  <tr>
   <td>構成ポリシー</td>
   <td><code>ConfigurationPolicy.REQUIRE</code></td>
  </tr>
  <tr>
   <td>参照</td>
   <td><code>CugExclude (ReferenceCardinality.OPTIONAL_UNARY)</code></td>
  </tr>
 </tbody>
</table>

**org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl**

<table>
 <tbody>
  <tr>
   <td>ラベル</td>
   <td>Apache Jackrabbit Oak CUG除外リスト</td>
  </tr>
  <tr>
   <td>説明</td>
   <td>設定された名前を持つプリンシパルをCUG評価から除外できます。</td>
  </tr>
  <tr>
   <td>設定プロパティ</td>
   <td>
    <ul>
     <li><code>principalNames</code></li>
    </ul> <p>後述の「設定オプション」セクションも参照してください。</p> </td>
  </tr>
  <tr>
   <td>構成ポリシー</td>
   <td><code>ConfigurationPolicy.REQUIRE</code></td>
  </tr>
  <tr>
   <td>参照</td>
   <td>該当なし</td>
  </tr>
 </tbody>
</table>

#### 設定オプション {#configuration-options}

主な設定オプションは次のとおりです。

* `cugSupportedPaths`：CUG を含むことができるサブツリーを指定します。デフォルト値は設定されません。
* `cugEnabled`：現在の CUG ポリシーに対して権限評価を有効にする設定オプション。

CUG 承認モジュールに関連する設定オプションの一覧と、その詳細な説明については、[Apache Oak ドキュメント](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#configuration)を参照してください。

#### CUG 評価からのプリンシパルの除外 {#excluding-principals-from-cug-evaluation}

CUG 評価からの個々のプリンシパルの除外は、前の実装から採用されていました。新しいCUG認証では、CugExcludeという名前の専用インターフェイスがこの機能に対応しています。 Apache Jackrabbit Oak 1.4 には、プリンシパルの固定セットを除外するデフォルト実装と、個々のプリンシパル名を設定できる拡張実装が付属しています。拡張実装は AEM パブリッシュインスタンスに設定されます。

AEM 6.3 以降のデフォルトでは、次のプリンシパルは、CUG ポリシーの影響を受けません。

* 管理プリンシパル（管理者ユーザー、管理者グループ）
* サービスユーザープリンシパル
* リポジトリ内部システムプリンシパル

詳しくは、後述の [AEM 6.3 以降のデフォルト設定](#default-configuration-since-aem)の表を参照してください。

The exclusion of the &#39;administrators&#39; group can be altered or expanded in the system console in the configuration section of **Apache Jackrabbit Oak CUG Exclude List**.

また、特別な必要が生じた場合に除外プリンシパルのセットを調整するために、CugExcludeインターフェイスのカスタム実装を提供およびデプロイすることもできます。 See the documentation on [CUG pluggability](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) for details and an example implementation.

### 認証：セットアップと設定 {#authentication-setup-and-configuration}

新しい認証関連のパーツは、**Adobe Granite Authentication Handler** バンドル（`com.adobe.granite.auth.authhandler` バージョン 5.6.48）に含まれています。このバンドルは AEM のデフォルトインストールの一部です。

廃止された CUG サポートの代わりとなる認証要件をセットアップするには、いくつかの OSGi コンポーネントを AEM インストールに提供してアクティブにする必要があります。詳しくは、後述の **OSGi コンポーネントの特性**&#x200B;を参照してください。

>[!NOTE]
>
>RequirementHandler による必須の設定オプションがあるので、認証関連のパーツは、サポートパスのセットを指定することで、この機能が有効になっている場合にのみアクティブになります。AEM の標準インストールの場合、この機能はオーサー実行モードでは無効で、パブリッシュ実行モードでは /content に対して有効になります。

**OSGi コンポーネントの特性**

認証要件を定義し、専用のログインパスを指定するために、次の 2 つの OSGi コンポーネントが導入されています。

* `com.adobe.granite.auth.requirement.impl.RequirementService`
* `com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler`

**com.adobe.granite.auth.requirement.impl.RequirementService**

<table>
 <tbody>
  <tr>
   <td>ラベル</td>
   <td>-</td>
  </tr>
  <tr>
   <td>説明</td>
   <td>認証要件に影響するコンテンツの変更に関してオブザーバー(Observer)を登録する認証要件専用のOSGiサービス( <code>granite:AuthenticationRequirement</code> mixinタイプを介する)とログインパスは、に公開され <code>LoginSelectorHandler</code>ます。 </td>
  </tr>
  <tr>
   <td>設定プロパティ</td>
   <td>-</td>
  </tr>
  <tr>
   <td>構成ポリシー</td>
   <td><code>ConfigurationPolicy.OPTIONAL</code></td>
  </tr>
  <tr>
   <td>参照</td>
   <td>
    <ul>
     <li><code>RequirementHandler (ReferenceCardinality.MANDATORY_UNARY)</code></li>
     <li><code>Executor (ReferenceCardinality.MANDATORY_UNARY)</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

**com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler**

| ラベル | AdobeGranite認証要件およびログインパスハンドラ |
|---|---|
| 説明 | `RequirementHandler` Apache Sling認証要件と、関連付けられたログインパスの対応する除外を更新する実装。 |
| 設定プロパティ | `supportedPaths` |
| 構成ポリシー | `ConfigurationPolicy.REQUIRE` |
| 参照 | 該当なし |

#### 設定オプション {#configuration-options-1}

CUG のリライトの認証関連のパーツは、Adobe Granite Authentication Requirement and Login Path Handler に関連する単一の設定オプションにのみ付属しています。

**「Authentication Requirement and Login Path Handler」**

<table>
 <tbody>
  <tr>
   <td>プロパティ</td>
   <td>型</td>
   <td>デフォルト値</td>
   <td>説明</td>
  </tr>
  <tr>
   <td><p>Label = Supported Paths</p> <p>Name = 'supportedPaths'</p> </td>
   <td>設定&lt;文字列&gt;</td>
   <td>-</td>
   <td>認証要件がこのハンドラーによって考慮されるパスです。 Leave this configuration unset if you want to add the <code>granite:AuthenticationRequirement</code> mixin type to nodes without having them enforced (for example, on author instances). 未設定にしておくと、この機能は無効になります。 </td>
  </tr>
 </tbody>
</table>

## AEM 6.3 以降のデフォルト設定 {#default-configuration-since-aem}

AEM の新規インストールでは、デフォルトで、CUG 機能の承認関連と認証関連のパーツの両方で新しい実装を使用します。旧実装「Adobe Granite Closed User Group (CUG) Support」は廃止されていて、すべての AEM インストールでデフォルトで無効になります。代わりに、新しい実装は、次のように有効になります。

### オーサーインスタンス {#author-instances}

| **&quot;Apache Jackrabbit Oak CUG Configuration&quot;** | **説明** |
|---|---|
| サポートされるパス `/content` | CUGポリシーのアクセス制御管理が有効になっています。 |
| CUG評価が有効なFALSE | 権限の評価が無効になっています。 CUG ポリシーは無効です。 |
| ランキング | 200 | Oakのドキュメントを参照してください。 |

>[!NOTE]
>
>デフォルトのオーサリングインスタンスに、**Apache Jackrabbit Oak CUG Exclude List** と **Adobe Granite Authentication Requirement and Login Path Handler** の設定は提供されません。

### パブリッシュインスタンス {#publish-instances}

| **&quot;Apache Jackrabbit Oak CUG Configuration&quot;** | **説明** |
|---|---|
| サポートされるパス `/content` | CUGポリシーのアクセス制御管理は、設定されたパスの下で有効になります。 |
| CUG評価が有効なTRUE | 設定されたパスの下で権限の評価が有効になっています。 CUGポリシーは次の場合に有効になり `Session.save()`ます。 |
| ランキング | 200 | Oakのドキュメントを参照してください。 |

| **&quot;Apache Jackrabbit Oak CUG除外リスト&quot;** | **説明** |
|---|---|
| プリンシパル名管理者 | 管理者プリンシパルをCUG評価から除外します。 |

| **「AdobeGranite認証要件とログインパスハンドラー」** | **説明** |
|---|---|
| サポートされるパス  `/content` | ミックスインタイプによってリポジトリで定義される認証要件は、以下の段階 `granite:AuthenticationRequired` で有効になり `/content``Session.save()`ます。 Sling Authenticator は更新されます。mixin タイプをサポートパス外に追加しても無視されます。 |

## CUG 承認および認証要件の無効化 {#disabling-cug-authorization-and-authentication-requirement}

特定のインストールで CUG を使用しない場合、または認証と承認に別の方法を使用する場合は、新しい実装を全体で無効にできます。

### CUG 承認の無効化 {#disable-cug-authorization}

複合承認のセットアップから CUG 承認モデルを削除する方法について詳しくは、[プラグの可／不可](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability)に関するドキュメントを参照してください。

### 認証要件の無効化 {#disable-the-authentication-requirement}

`granite.auth.authhandler` モジュールが提供する認証要件のサポートを無効にするには、**Adobe Granite Authentication Requirement and Login Path Handler** に関連する設定を削除するだけで十分です。

>[!NOTE]
>
>設定を削除しても mixin タイプの登録は解除されません。mixin タイプは、有効にしなくても引き続きノードに適用可能です。

## 他のモジュールの操作 {#interaction-with-other-modules}

### Apache Jackrabbit API {#apache-jackrabbit-api}

CUG 承認モデルで使用する新しいタイプのアクセス制御ポリシーを強化するために、Apache Jackrabbit で定義される API が拡張されています。Since version 2.11.0 of the `jackrabbit-api` module defines a new interface called `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy`, which extends from `javax.jcr.security.AccessControlPolicy`.

### Apache Jackrabbit FileVault {#apache-jackrabbit-filevault}

The import mechanism of Apache Jackrabbit FileVault has been adjusted to deal with access control policies of type `PrincipalSetPolicy`.

### Apache Sling Content Distribution {#apache-sling-content-distribution}

詳しくは、前述の [Apache Jackrabbit FileVault](/help/sites-administering/closed-user-groups.md#apache-jackrabbit-filevault) の節を参照してください。

### Adobe Granite Replication {#adobe-granite-replication}

このレプリケーションモジュールは、異なる AEM インスタンス間で CUG ポリシーをレプリケーションできるように少し調整されています。

* `DurboImportConfiguration.isImportAcl()` は文字通り解釈され、実装するアクセス制御ポリシーにのみ影響を及ぼす `javax.jcr.security.AccessControlList`

* `DurboImportTransformer` は、真のACLに対してのみこの設定を適用します。
* CUG 承認モデルによって作成される `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy` インスタンスなどの他のポリシーは常にレプリケーションされ、設定オプション `DurboImportConfiguration.isImportAcl` () は無視されます。

CUG ポリシーのレプリケーションには 1 つ制約があります。If a given CUG policy gets removed without removing the corresponding mixin node type `rep:CugMixin,` the removal will not be reflected upon replication. これについては、ポリシーを削除する際に mixin も必ず削除することで解消されました。ただし、mixin タイプが手動で追加された場合には、この現象が発生する可能性があります。

### Adobe Granite Authentication Handler {#adobe-granite-authentication-handler}

**バンドルに付属する認証ハンドラー** Adobe Granite HTTP Header Authentication Handler`com.adobe.granite.auth.authhandler` は、同じモジュールによって定義される `CugSupport` インターフェイスへの参照を保持します。これは、特定の環境内での「領域」の計算に使用され、このハンドラーによって設定される領域にフォールバックします。

このモジュールは、`CugSupport` への参照をオプションとして使用できるように調整されました。この調整により、既に廃止されている実装を特定のセットアップで再度有効にしても、最大限の後方互換性を確保できます。Installations using the implementation will no longer get the realm extracted from the CUG implementation but will always display the realm as defined with **Adobe Granite HTTP Header Authentication Handler**.

>[!NOTE]
>
>デフォルトでは、**Adobe Granite HTTP Header Authentication Handler** は、「Disable Login Page」（`auth.http.nologin`）オプションが有効になっているパブリッシュ実行モードでのみ設定されます。

### AEM ライブコピー {#aem-livecopy}

LiveCopyと組み合わせてCUGを設定すると、次のように、1つの追加のノードと1つの追加のプロパティがリポジトリに追加されて表されます。

* `/content/we-retail/us/en/blueprint/rep:cugPolicy`
* `/content/we-retail/us/en/LiveCopy@granite:loginPath`

Both of these elements are created under the `cq:Page`. With the current design, MSM only handles nodes and properties that are under the `cq:PageContent` (`jcr:content`) node.

したがって、CUG グループをブループリントからライブコピーにロールバックすることはできません。ライブコピーを設定するときはご注意ください。

## 新しい CUG 実装による変更 {#changes-with-the-new-cug-implementation}

この節では、CUG 機能に加えられた変更点の概要を示し、新旧の実装を比較します。CUG サポートの設定方法に影響する変更点を挙げます。また、リポジトリコンテンツにおける CUG の管理方法とその管理者についても説明します。

### Differences in CUG Setup and Configuration {#differences-in-cug-setup-and-configuration}

廃止された OSGi コンポーネント **Adobe Granite Closed User Group (CUG) Support**（`com.day.cq.auth.impl.cug.CugSupportImpl`）は、新しいコンポーネントに置き換えられ、前の CUG 機能の承認関連のパーツと認証関連のパーツを分けて扱えるようになりました。

## Differences in Managing CUGs in the Repository Content {#differences-in-managing-cugs-in-the-repository-content}

以下の節では、新旧の実装の違いについて、実装面とセキュリティ面から説明します。新しい実装でも、同じ機能を提供することを目的としていますが、新しい CUG を使用するうえで知っておくべき変更点があります。

### Differences With Regards To Authorization {#differences-with-regards-to-authorization}

認証の観点からの主な違いは、次のリストにまとめられています。

**CUG 専用のアクセス制御コンテンツ**

古い実装では、デフォルトの承認モデルは、公開時にアクセス制御リストポリシーを操作するために使用され、既存の ACE は、CUG が要求するセットアップに置き換えられました。この承認モデルは、公開時に解釈される通常の残余 JCR プロパティを記述することで呼び出されました。

新しい実装では、デフォルトの認証モデルのアクセス制御設定は、作成、変更、または削除されるCUGの影響を受けません。 Instead a new type of policy called `PrincipalSetPolicy` is applied as additional access control content to the target node. この追加ポリシーは、ターゲットノードの子として配置され、デフォルトのポリシーノードがある場合はその兄弟になります。

**アクセス制御管理における CUG ポリシーの編集**

残余 JCR プロパティから専用アクセス制御ポリシーに移行したことで、CUG 機能の承認パーツの作成や変更に必要な権限に影響が出ています。Since this is considered a modification to access control content, it requires `jcr:readAccessControl` and `jcr:modifyAccessControl` privileges in order to be written to the repository. したがって、ページのアクセス制御コンテンツを変更する権限を持つコンテンツ作成者のみ、このコンテンツをセットアップまたは変更できます。これは、通常の JCR プロパティを書き込む機能が十分で、結果として、権限の昇格となる古い実装とは対照的です。

**ポリシーによって定義されるターゲットノード**

CUG ポリシーは、通常は、制限付き読み取りアクセスの対象となるサブツリーを定義する JCR ノードで作成されます。CUG がツリー全体に影響する場合は、これが AEM ページになると思われます。

CUGポリシーを特定のページの下にあるjcr:contentノードにのみ配置すると、特定のページのコンテンツs.strへのアクセスは制限されますが、兄弟ページや子ページには影響しません。 場合によってはこうしたケースも有効で、きめ細かなアクセスコンテンツを適用可能なリポジトリエディターによって達成できます。ただし、前の実装とは異なり、cq:cugEnabledプロパティをjcr:contentノードに配置すると、内部的にページノードに再マッピングされます。 こうしたマッピングは今後はおこなわれません。

**CUG ポリシーによる権限評価**

古い CUG サポートから追加の承認モデルに移行したことで、有効な読み取り権限の評価方法が変更されています。As described in the [Jackrabbit documentation](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html), a given principal allowed to view the `CUGcontent` will only be granted read access if the permission evaluation of all models configured in the Oak repository grant read access.

つまり、有効な権限の評価では、`CUGPolicy` とデフォルトのアクセス制御エントリの両方が考慮され、CUG コンテンツに対する読み取りアクセスは、両方のタイプのポリシーによって付与される場合にのみ付与されます。In a default AEM publish installation where read access to the complete `/content` tree is granted for everyone, the effect of the CUG policies will be the same as with the old implementation.

**オンデマンド評価**

CUG 承認モデルでは、アクセス制御管理と権限評価を個別にオンにできます。

* アクセス制御管理は、CUG を作成できるサポートパスがモジュールに 1 つ以上ある場合に有効になります。
* 権限評価は、「**CUG Evaluation Enabled**」オプションが追加でオンになっている場合にのみ有効になります。

新しい AEM のデフォルトセットアップにおける CUG ポリシーの評価では、オンデマンド評価は「パブリッシュ」実行モードでのみ有効になります。詳しくは、[AEM 6.3 以降のデフォルト設定](#default-configuration-since-aem)を参照してください。これは、特定のパスに対する有効なポリシーと、コンテンツに保存されたポリシーとを比較することで検証できます。 有効なポリシーは、CUG の権限評価が有効になっている場合にのみ表示されます。

As explained above the CUG access control policies are now always stored in the content but evaluation of the effective permissions that result from those policies will only be enforced if **CUG Evaluation Enabled** is turned on in the system console at Apache Jackrabbit Oak **CUG Configuration.** デフォルトでは、「公開」実行モードでのみ有効になります。

### 認証の違い {#differences-with-regards-to-authentication}

以下では、認証の違いを説明します。

#### 認証要件に専用の Mixin タイプ {#dedicated-mixin-type-for-authentication-requirement}

前の実装では、CUG の承認と認証に関連するパーツは、単一の JCR プロパティ（`cq:cugEnabled`）によって呼び出されました。認証に関する限り、これによって、Apache Sling Authenticator 実装で保存される認証要件の更新リストが得られました。新しい実装では、これと同じことが、専用の mixin タイプ（`granite:AuthenticationRequired`）でターゲットノードをマークすることで達成されます。

#### ログインパスを除外するためのプロパティ {#property-for-excluding-login-path}

The mixin type defines a single, optional property called `granite:loginPath`, which basically corresponds to the `cq:cugLoginPage` property. 前の実装とは対照的に、ログインパスプロパティは、その宣言ノードタイプが前述の mixin の場合にのみ考慮されます。mixin タイプを設定せずに、その名前でプロパティを追加しても有効にならず、新しい要件もログインパスの除外も認証にレポートされません。

#### 認証要件の権限 {#privilege-for-authentication-requirement}

mixin タイプを追加または削除するには、`jcr:nodeTypeManagement` 権限が付与されている必要があります。In the previous implementation, the `jcr:modifyProperties` privilege is used to edit the residual property.

`granite:loginPath` に関する限り、残余プロパティを追加、変更または削除するには同じ権限が必要です。

#### Mixin タイプによって定義されるターゲットノード {#target-node-defined-by-mixin-type}

認証要件は、通常は、強制的なログインの対象となるサブツリーを定義する JCR ノードで作成されます。CUG がツリー全体に影響する場合は、これが AEM ページになると思われ、この新しい実装の UI により、結果として、認証要件 mixin タイプがそのページノードに追加されます。

CUGポリシーを特定のページの下にあるjcr:contentノードにのみ配置すると、そのコンテンツへのアクセスは制限されますが、ページノード自体や子ページには影響しません。

場合によってはこうしたケースも有効で、任意のノードに mixin を配置できるリポジトリエディターによって達成できます。ただし、前者の実装とは異なり、jcr:contentノードにcq:cugEnabledまたはcq:cugLoginPageプロパティを配置すると、内部的にページノードに再マッピングされました。 こうしたマッピングは今後はおこなわれません。

#### 設定済みのサポートパス {#configured-supported-paths}

Both the `granite:AuthenticationRequired` mixin type and the granite:loginPath property will only be respected within the scope defined by the set of **Supported Paths** configuration option present with the **Adobe Granite Authentication Requirement and Login Path Handler**. これらのパスが指定されていないと、認証要件機能は全体で無効になります。この場合、ミックスインのタイプやプロパティは、特定のJCRノードに追加または設定されると有効になります。

### JCR コンテンツ、OSGi サービスおよび設定のマッピング {#mapping-of-jcr-content-osgi-services-and-configurations}

以下のドキュメントでは、OSGiサービス、設定、およびリポジトリの内容を、以前の実装と新しい実装の間で包括的にマッピングしています。

AEM 6.3 以降の CUG の対応関係

[ファイルを入手](assets/cug-mapping.pdf)

## CUG のアップグレード {#upgrade-cug}

### 廃止された CUG を使用した既存のインストール {#existing-installations-using-the-deprecated-cug}

古い CUG サポートの実装は廃止され、将来のバージョンでは削除されます。AEM 6.3 より前のバージョンからのアップグレード時に新しい実装に移行することが推奨されます。

アップグレードされた AEM のインストールには、1 つの CUG 実装のみが有効であることを確認してください。新しい CUG サポートと廃止された CUG サポートの組み合わせはテストされていないので、次のような問題が発生する場合があります。

* Sling Authenticator で認証要件が競合する。
* 古い CUG に関連する ACL セットアップと新しい CUG ポリシーが相反して、読み取りアクセスが拒否される。

### 既存の CUG コンテンツの移行 {#migrating-existing-cug-content}

Adobe は、新しい CUG 実装への移行ツールを提供しています。このツールを使用するには、次の手順をおこないます。

1. に移動して、ツール `https://<serveraddress>:<serverport>/system/console/cug-migration` にアクセスします。
1. CUG を調べるルートパスを入力し、「**Perform dry run**」ボタンを押します。選択した場所で変換に適したCUGがスキャンされます。
1. 結果を確認した後、「**Perform migration**」ボタンを押して、新しい実装に移行します。

>[!NOTE]
>
>If you run into issues, it is possible to set up a specific logger at **DEBUG** level on `com.day.cq.auth.impl.cug` to get the output of the migration tool. 詳細については、[ロギング](/help/sites-deploying/configure-logging.md)を参照してください。

