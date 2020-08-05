---
title: AEM 6.5 のカスタムユーザグループマッピング
seo-title: AEM 6.5 のカスタムユーザグループマッピング
description: AEM でカスタムユーザーグループマッピングがどのように機能するか説明します。
seo-description: AEM でカスタムユーザーグループマッピングがどのように機能するか説明します。
uuid: 7520351a-ab71-4661-b214-a0ef012c0c93
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 13085dd3-d283-4354-874b-cd837a9db9f9
docset: aem65
translation-type: tm+mt
source-git-commit: c2937a1989c6cfe33cc3f56f89c307cb5fb8d272
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 74%

---


# AEM 6.5 のカスタムユーザグループマッピング {#custom-user-group-mapping-in-aem}

## CUG に関連する JCR コンテンツの比較 {#comparison-of-jcr-content-related-to-cug}

<table>
 <tbody>
  <tr>
   <td><strong>古い AEM バージョン</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>コメント</strong></td>
  </tr>
  <tr>
   <td><p>プロパティ：cq:cugEnabled</p> <p>ノードタイプの宣言：該当なし、残余プロパティ</p> </td>
   <td><p>認証：</p> <p>ノード：rep:cugPolicyのノードタイプ rep:CugPolicy</p> <p>ノードタイプの宣言：rep:CugMixin</p> <p> </p> <p> </p> <p> </p> 認証：</p> <p>Mixin タイプ：granite:AuthenticationRequired</p> </td>
   <td><p>読み取りアクセスを制限するために、専用の CUG ポリシーがターゲットノードに適用されます。</p> <p>メモ：ポリシーは、設定されているサポート対象パスにのみ適用できます。</p> <p>rep:cugPolicy および rep:CugPolicy という名前のノードは保護されており、通常の JCR の API 呼び出しを使用して書き込むことはできません。代わりに JCR アクセス制御管理を使用してください。</p> <p>詳しくは、<a href="https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html">このページ</a>を参照してください。</p> <p>ノードで認証要件を適用するには、mixin type granite:AuthenticationRequiredを追加すれば十分です。</p> <p>メモ：設定済みのサポートパスの下でのみ適用されます。</p> </td>
  </tr>
  <tr>
   <td><p>プロパティ：cq:cugPrincipals</p> <p>ノードタイプの宣言：該当なし、残余プロパティ</p> </td>
   <td><p>プロパティ：rep:principalNames</p> <p>ノードタイプの宣言：rep:CugPolicy</p> </td>
   <td><p>制限付き CUG の下の内容を読み取ることが許可されているプリンシパルの名前を含むプロパティは保護されており、通常の JCR の API 呼び出しを使用して書き込むことはできません。代わりに JCR アクセス制御管理を使用してください。</p> <p>実装について詳しくは、<a href="https://svn.apache.org/repos/asf/jackrabbit/trunk/jackrabbitapi/src/main/java/org/apache/jackrabbit/api/security/authorization/PrincipalSetPolicy.java">このページ</a>を参照してください。</p> </td>
  </tr>
  <tr>
   <td><p>プロパティ：cq:cugLoginPage</p> <p>ノードタイプの宣言：該当なし、残余プロパティ</p> </td>
   <td><p>プロパティ：granite:loginPath（オプション）</p> <p>ノードタイプの宣言：granite:AuthenticationRequired</p> </td>
   <td><p>mixinタイプgranite:AuthenticationRequiredが定義されたJCRノード。オプションで別のログインパスを定義できます。</p> <p>メモ：設定済みのサポートパスの下でのみ適用されます。</p> </td>
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
* レーベル：Adobe Granite 認証要件とログインパスハンドラー

   名前：com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler

   ConfigurationPolicy = REQUIRED

**コメント**

* CUG 認証の設定および評価の有効化/無効化CUG認証の影響を受けないプリンシパルの除外リストを設定するサービス。

   >[!NOTE]
   > 
   >が設定され `CugExcludeImpl` ていない場合は、がデフォルト `CugConfiguration` に戻ります。

   特別なニーズがある場合は、カスタム CugExclude 実装をプラグインすることが可能です。

* LoginSelectorHandler に一致するログインパスを公開する LoginPathProvider を実装する OSGi コンポーネント。これは、granite:AuthenticationRequired mixin タイプによって、コンテンツに格納されている変更された認証要件を監視するオブザーバを登録するために使用される RequirementHandler への必須参照を持っています。
* SlingAuthenticatorに認証要件の変更を通知するRequirementHandlerの実装OSGiコンポーネント。

   このコンポーネントの構成ポリシーはREQUIREなので、サポートされるパスのセットが指定されている場合にのみアクティブ化されます。

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
       <td><p>Service to configure exclusion list of principals which should not be affected by the CUG authorization.</p> <p>NOTE: If the CugExcludeImpl is not configured, the CugConfiguration will fall back to the default.</p> <p>It is possible to plug a custom CugExclude implementation in case of special needs.</p> </td>
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

