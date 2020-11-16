---
title: 6.4 における AEM Communities のリポジトリ再構築
seo-title: 6.4 における AEM Communities のリポジトリ再構築
description: AEM 6.4 for Communities の新しいリポジトリ構造に移行するために必要な変更を加える方法について説明します。
seo-description: AEM 6.4 for Communities の新しいリポジトリ構造に移行するために必要な変更を加える方法について説明します。
uuid: d161655f-4074-44a7-8d69-38e80934c58b
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 7383265b-0ed4-4ea7-b741-0a417d187bdd
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 59%

---


# 6.5 における AEM Communities のリポジトリ再構築 {#repository-restructuring-for-aem-communities-in}

As described on the parent [Repository Restructuring in AEM 6.4](/help/sites-deploying/repository-restructuring.md) page, customers upgrading to AEM 6.5 should use this page to assess the work effort associated with repository changes impacting the AEM Communities Solution. 一部の変更ではAEM 6.5のアップグレードプロセス中に作業が必要になり、残りの変更は将来のアップグレードまで延期できます。

**6.5 へのアップグレード時におこなう変更**

* [電子メール通知テンプレート](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#e-mail-notification-templates)
* [サブスクリプション設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#subscription-configurations)

**今後のアップグレードの前**

* [バッジ設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#badging-configurations)
* [従来のコミュニティコンソールデザイン](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#classic-communities-console-designs)
* [Facebook ソーシャルログイン設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#facebook-social-login-configurations)
* [言語オプション設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#language-options-configurations)

* [Pinterest ソーシャルログイン設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#pinterest-social-login-configurations)
* [スコアリング設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#scoring-configurations)
* [Twitter ソーシャルログイン設定](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#twitter-social-login-configurations)
* [その他](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#misc)

## 6.5 へのアップグレード時におこなう変更 {#with-upgrade}

### 電子メール通知テンプレート {#e-mail-notification-templates}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/community/notifications</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><code>/libs/settings/community/notifications</code></td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>Manual migration ia needed if you want to move to new path under "<code>/apps/settings</code>". Granite 設定マネージャーを使用して、移行を実行できます。</p> <p>You can perform the migration by setting the property <code>mergeList</code> to <code>true</code> on the "<code>/libs/settings/community/subscriptions</code>" node and add an <code>nt:unstructured</code> child node.</p> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし<br /> </td>
  </tr>
 </tbody>
</table>

### サブスクリプション設定 {#subscription-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/community/subscriptions</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><code>/libs/settings/community/subscriptions</code></td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>Manual migration ia needed if you want to move to new path under "<code>/apps/settings</code>". Granite 設定マネージャーを使用して、移行を実行できます。</p> <p>You can perform the migration by setting the property <code>mergeList</code> to <code>true</code> on the "<code>/libs/settings/community/subscriptions</code>" node and add an <code>nt:unstructured</code> child node.</p> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし<br /> </td>
  </tr>
 </tbody>
</table>

### 監視ワード設定 {#watchwords-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td>/etc/watchwords</td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td>/libs/community/watchwords</td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td>Communities 設定をクリーンアップするために、遅延移行タスクを利用できます。<br /> <p>タスクは監視ワードを間 <code>/etc/watchwords</code> 隔で移動し <code>/conf/global/settings/community/watchwords</code>ます。</p> <p>If customized watchwords are stored in SCM, then they should be deployed to <code>/apps/settings/...</code> and you must ensure that there is not an overlaying <code>/conf/global/settings/...</code> configuration that would take precedence.</p> <p>Migration task removes <code>/etc</code> locations.</p> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし<br /> </td>
  </tr>
 </tbody>
</table>

## 今後のアップグレードの前 {#prior-to-upgrade}

### バッジ設定 {#badging-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/community/badging</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><p><strong>バッジルール：</strong></p> <p><code>/libs/settings/community/badging</code></p> <p><strong>バッジ画像：</strong></p> <p>初期設定の画像の場合： <code>/etc/community/badging/images are moved to /libs/community/badging/images</code></p> <p>カスタム画像の場合： <code>/content/community/badging/images</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>手動移行が必要です。</p> <p>インスタンスがバッジ／スコアルールをカスタマイズしている場合、すべてのルールをバケットの下に自動的に配置する方法はありません。サイトに使用する conf バケット（グローバルまたはサイト固有）に関する顧客からの情報が必要です。</p> <p>サイトのバッジおよびスコア設定に使用できる UI はありません。</p> <p>新しいリポジトリ構造に合わせるには：</p>
    <ol>
     <li><strong>ツール</strong>の下の<strong>設定ブラウザー</strong>を使用して、サイトコンテキストバケットを作成します。</li>
     <li>サイトのルートに移動します。</li>
     <li>Set <code>cq:confproperty</code> to the bucket path where you want to store all your settings. 同じ設定をサイトの「<strong>編集ウィザード - クラウド設定入力</strong>」でおこなうこともできます。</li>
     <li>Move relevant badging rules and scoring rules from <code>/etc/community/*</code> to the site context bucket created in the previous step.</li>
     <li>新しいルールの場所への相対参照を使用するように、サイトルートのバッジルールおよびスコアルールプロパティを調整します。
      <ol>
       <li>For example, if the poperty for <code>cq:conf = /conf/we-retail</code>, then <code>badgingRules [] = community/badging/rules</code> if rules are now moved to this new bucket.</li>
      </ol> </li>
     <li>同様に、バッジルールノードのスコアルールへの参照も相対パスに変更します。</li>
    </ol> <p> </p> <p>最後に、リソースを削除してクリーンアップします <code>/etc/community/badging</code></p> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし<br /> </td>
  </tr>
 </tbody>
</table>

### 従来のコミュニティコンソールデザイン {#classic-communities-console-designs}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/designs/social/console</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><p><code>/libs/settings/wcm/designs/social/console</code></p> <p><code>/apps/settings/wcm/designs/social/console</code></p> </td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td>該当なし</td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし<br /> </td>
  </tr>
 </tbody>
</table>

### Facebook ソーシャルログイン設定 {#facebook-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/cloudservices/facebookconnect</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/facebookconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/facebookconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>新しい Facebook クラウド設定をすべて、新しい場所に移行する必要があります。</p>
    <ol>
     <li>以前の場所にある既存の設定を新しい場所に移行します。
      <ol>
       <li><strong>ツール／クラウドサービス／Facebook ソーシャルログイン設定</strong>で、AEM オーサリング UI を使用して新しい Facebook ソーシャルログイン設定を手動で再作成します。<br /> か <br /> のどちらかにする必要があります。 </li>
       <li>Copy any new Facebook Cloud Configurations from Previous Location to the appropriate New Location, under <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Update any AEM Communities Site root to reference the new Facebook Social Login Configuration by setting the <code>[cq:Page]/jcr:content@cq:conf</code> property to the absolute path in the New Location.</li>
     <li>新しい場所を参照するように更新した AEM Communities サイトのルートから、従来の Facebook Connect クラウドサービスの関連付けを解除します。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし<br /> </td>
  </tr>
 </tbody>
</table>

### 言語オプション設定 {#language-options-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/social/config/languageOpts</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><code>/libs/social/translation/languageOpts</code></td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td>該当なし<br /> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし<br /> </td>
  </tr>
 </tbody>
</table>

### Pinterest ソーシャルログイン設定 {#pinterest-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/cloudservices/pinterestconnect</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/pinterestconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/pinterestconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>新しい Pinterest クラウド設定をすべて、新しい場所に移行する必要があります。</p>
    <ol>
     <li>以前の場所にある既存の設定を新しい場所に移行します。
      <ol>
       <li><strong>ツール／クラウドサービス／Pinterest ソーシャルログイン設定</strong>で、AEM オーサリング UI を使用して新しい Pinterest ソーシャルログイン設定を手動で再作成します。<br /> か  のどちらかにする必要があります。</li>
       <li>Copy any new Pinterest Cloud Configurations from Previous Location to the appropriate New Location under <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Update any AEM Communities Site root to reference the new Pinterest Social Login Configuration by settings the <code>[cq:Page]/jcr:content@cq:conf</code> property to the absolute path in the New Location.</li>
     <li>新しい場所を参照するように更新した AEM Communities サイトのルートから、従来の Pinterest Connect クラウドサービスの関連付けを解除します。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし<br /> </td>
  </tr>
 </tbody>
</table>

### スコアリング設定 {#scoring-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/community/scoring</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><code>/libs/settings/community/scoring</code></td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>To align with new repository structure, scoring rules can be stored in <code>/apps/settings/</code> or /<code>conf/.../settings</code></p>
    <ol>
     <li>For <code>/apps/settings</code>, this would act as global or default rules managed in SCM.</li>
    </ol> <p>Create context-aware configs in <code>/conf/</code> by using CRXDELite:</p>
    <ol>
     <li>Create the configs in the desired <code>/conf/.../settings</code> location<br /> </li>
     <li>Communities site must have the <code>cq:conf </code>property property set.
      <ol>
       <li>If no <code>cq:conf</code> is set, scoring rules would be directly read from the given path for property '<code>scoringRules</code>' at the site's root node, for example: <code>/content/we-retail/us/en/community/jcr:content</code></li>
      </ol> </li>
    </ol> <p>クリーンアップ：リソースの削除 <code>/etc/community/scoring</code></p> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし<br /> </td>
  </tr>
 </tbody>
</table>

### Twitter ソーシャルログイン設定 {#twitter-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/cloudservices/twitterconnect</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/twitterconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/twitterconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>新しい Twitter クラウド設定をすべて、新しい場所に移行する必要があります。</p>
    <ol>
     <li>以前の場所にある既存の設定を新しい場所に移行します。
      <ol>
       <li><strong>ツール／クラウドサービス／Twitter ソーシャルログイン設定</strong>で、AEM オーサリング UI を使用して新しい Twitter ソーシャルログイン設定を手動で再作成します。<br /> か <br /> のどちらかにする必要があります。 </li>
       <li>Copy any new Twitter Cloud Configurations from Previous Location to the appropriate New Location, under <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Update any AEM Communities Site root to reference the new Twitter Social Login Configuration by setting the <code>[cq:Page]/jcr:content@cq:conf</code> property to the absolute path in the New Location.</li>
     <li>新しい場所を参照するように更新した AEM Communities サイトのルートから、従来の Twitter Connect クラウドサービスの関連付けを解除します。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし<br /> </td>
  </tr>
 </tbody>
</table>

### その他 {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/community/templates</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><code>/libs/settings/community/templates</code></td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>アドビでは、以下で移行ユーティリティを提供しています。</p> <p><a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration">https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration</a></p> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>既存のカスタムテンプレートは、 <code>/conf/global/settings/community/template/&lt;groups/sites/functions&gt;</code></td>
  </tr>
 </tbody>
</table>

