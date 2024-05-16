---
title: AEM 6.5 のカスタムユーザグループマッピング
description: Adobe Experience Manager でカスタムユーザーグループマッピングがどのように機能するかを説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: 661602eb-a117-454d-93d3-a079584f7a5d
feature: Administering
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: ht
source-wordcount: '469'
ht-degree: 100%

---

# AEM 6.5 のカスタムユーザグループマッピング {#custom-user-group-mapping-in-aem}

## CUG（カスタムユーザーグループ）に関連する JCR コンテンツの比較 {#comparison-of-jcr-content-related-to-cug}

<table>
 <tbody>
  <tr>
   <td><strong>古い AEM バージョン</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>コメント</strong></td>
  </tr>
  <tr>
   <td><p>プロパティ：cq:cugEnabled</p> <p>ノードタイプの宣言：該当なし、残余プロパティ</p> </td>
   <td><p>認証：</p> <p>ノード：rep:cugPolicy のノードタイプ rep:CugPolicy</p> <p>ノードタイプの宣言：rep:CugMixin</p> <p> </p> <p> </p> <p> </p> 認証:</p> <p>Mixin タイプ：granite:AuthenticationRequired</p> </td>
   <td><p>読み取りアクセスを制限するために、専用の CUG ポリシーがターゲットノードに適用されます。</p> <p>メモ：ポリシーは、設定されているサポート対象パスにのみ適用できます。</p> <p>名前が rep:cugPolicy およびタイプが rep:CugPolicy のノードは保護されており、通常の JCR の API 呼び出しを使用して書き込むことはできません。代わりに JCR アクセス制御管理を使用してください。</p> <p>詳しくは、<a href="https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html">このページ</a>を参照してください。</p> <p>ノードに認証要件を適用するには、Mixin タイプ granite:AuthenticationRequired を追加することで十分です。</p> <p>メモ：設定済みのサポートパスの下でのみ適用されます。</p> </td>
  </tr>
  <tr>
   <td><p>プロパティ：cq:cugPrincipals</p> <p>ノードタイプの宣言：該当なし、残余プロパティ</p> </td>
   <td><p>プロパティ：rep:principalNames</p> <p>ノードタイプの宣言：rep:CugPolicy</p> </td>
   <td><p>制限付き CUG の下の内容を読み取ることが許可されているプリンシパルの名前を含むプロパティは保護されており、通常の JCR の API 呼び出しを使用して書き込むことはできません。代わりに JCR アクセス制御管理を使用してください。</p> <p>実装について詳しくは、<a href="https://jackrabbit.apache.org/api/2.12/org/apache/jackrabbit/api/security/authorization/PrincipalSetPolicy.html">こちらのページ</a>を参照してください。</p> </td>
  </tr>
  <tr>
   <td><p>プロパティ：cq:cugLoginPage</p> <p>ノードタイプの宣言：該当なし、残余プロパティ</p> </td>
   <td><p>プロパティ：granite:loginPath（オプション）</p> <p>ノードタイプの宣言：granite:AuthenticationRequired</p> </td>
   <td><p>Mixin タイプ granite:AuthenticationRequired が定義されている JCR ノードは、オプションで代替ログインパスを定義できます。</p> <p>メモ：設定済みのサポートパスの下でのみ適用されます。</p> </td>
  </tr>
  <tr>
   <td><p>プロパティ：cq:cugRealm</p> <p>ノードタイプの宣言：該当なし、残余プロパティ</p> </td>
   <td>該当なし</td>
   <td>新しい実装ではサポートされなくなりました。</td>
  </tr>
 </tbody>
</table>

## OSGi サービスの比較 {#comparison-of-osgi-services}

**古い AEM バージョン**

ラベル：Adobe Granite の閉じられたユーザーグループ（CUG）のサポート

名前：com.day.cq.auth.impl.CugSupportImpl

**AEM 6.5**

* ラベル：Apache Jackrabbit Oak CUG の設定

  名前：org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration

  ConfigurationPolicy = REQUIRED

* ラベル：Apache Jackrabbit Oak CUG 除外リスト

  名前：org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl

  ConfigurationPolicy = REQUIRED

* 名前：com.adobe.granite.auth.requirement.impl.RequirementService
* ラベル：Adobe Granite 認証要件とログインパスハンドラー

  名前：com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler

  ConfigurationPolicy = REQUIRED

**コメント**

* CUG 認証の設定および評価の有効化/無効化CUG 認証によって影響を受けるべきではないプリンシパルの除外リストを設定するサービス。

  >[!NOTE]
  > 
  >`CugExcludeImpl` が設定されていない場合、`CugConfiguration` がデフォルトに戻ります。

  特別なニーズがある場合は、カスタム CugExclude 実装をプラグインすることが可能です。

* LoginSelectorHandler に一致するログインパスを公開する LoginPathProvider を実装する OSGi コンポーネント。これは、granite:AuthenticationRequired mixin タイプによって、コンテンツに格納されている変更された認証要件を監視するオブザーバを登録するために使用される RequirementHandler への必須参照を持っています。
* authRequirements の変更について SlingAuthenticator に通知する RequirementHandler を実装する OSGi コンポーネント。

  このコンポーネントの設定ポリシーは REQUIRE なことから、サポートされているパスのセットが指定されている場合にのみ有効になります。

  サービスを有効にすると RequirementService が起動します。

<!-- nested tables not supported - text above is the table>
<table>
 <tbody>
  <tr>
   <td><strong>Older AEM Versions</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>Comments</strong></td>
  </tr>
  <tr>
   <td><p>Label: Adobe Granite Closed User Group (CUG) Support</p> <p>Name: com.day.cq.auth.impl.CugSupportImpl</p> </td>
   <td><p>Label: Apache Jackrabbit Oak CUG Configuration</p> <p>Name: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration</p> <p>ConfigurationPolicy = REQUIRED</p> </td>
    <td><p>Label: Apache Jackrabbit Oak CUG Exclude List</p> <p>Name: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl</p> <p>ConfigurationPolicy = REQUIRED</p> <p> </p> <p> </p> <p> </p> <p> </p> </td>
      </tr>
      <tr>
       <td>Name: com.adobe.granite.auth.requirement.impl.RequirementService</td>
      </tr>
      <tr>
       <td><p>Label: Adobe Granite Authentication Requirement and Login Path Handler</p> <p>Name: com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler</p> <p>ConfigurationPolicy = REQUIRED</p> </td>
      </tr>
     </tbody>
    </table> </td>
   <td>
     <tbody>
      <tr>
       <td>Configuration of the CUG authorization and enable/disable the evaluation.</td>
      </tr>
      <tr>
       <td><p>Service to configure exclusion list of principals which should not be affected by the CUG authorization.</p> <p>NOTE: If the CugExcludeImpl is not configured, the CugConfiguration will fall back to the default.</p> <p>It is possible to plug a custom CugExclude implementation if there are special needs.</p> </td>
      </tr>
      <tr>
       <td>OSGi component implementing LoginPathProvider that exposes a matching login path to the LoginSelectorHandler. It has a mandatory reference to a RequirementHandler which is used to register the observer that listens to changed auth requirements stored in the content by the means of the granite:AuthenticationRequired mixin type. </td>
      </tr>
      <tr>
       <td><p>OSGi component implementing RequirementHandler that notifies the SlingAuthenticator about changes to authrequirements.</p> <p>As configuration policy for this component is REQUIRE it will only be activated if a set of supported paths is specified.</p> <p>Enabling the service will launch the RequirementService.</p> </td>
      </tr>
     </tbody>
     </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->
