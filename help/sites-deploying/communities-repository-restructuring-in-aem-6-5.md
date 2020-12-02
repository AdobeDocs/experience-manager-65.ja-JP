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

AEM 6.4](/help/sites-deploying/repository-restructuring.md)の親ページ[リポジトリの再構築に関する説明に従って、AEM 6.5にアップグレードしたお客様は、このページを使用して、AEM Communities・ソリューションに影響を与えるリポジトリの変更に関連する作業量を評価する必要があります。 一部の変更ではAEM 6.5のアップグレードプロセス中に作業が必要になり、残りの変更は将来のアップグレードまで延期できます。

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
   <td><p>"<code>/apps/settings</code>"の下の新しいパスに移動する場合は、手動の移行が必要です。 Granite 設定マネージャーを使用して、移行を実行できます。</p> <p>移行は、「<code>/libs/settings/community/subscriptions</code>」ノードでプロパティ<code>mergeList</code>を<code>true</code>に設定し、<code>nt:unstructured</code>子ノードを追加することで実行できます。</p> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし<br /> </td>
  </tr>
 </tbody>
</table>

### サブスクリプション設定  {#subscription-configurations}

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
   <td><p>"<code>/apps/settings</code>"の下の新しいパスに移動する場合は、手動の移行が必要です。 Granite 設定マネージャーを使用して、移行を実行できます。</p> <p>移行は、「<code>/libs/settings/community/subscriptions</code>」ノードでプロパティ<code>mergeList</code>を<code>true</code>に設定し、<code>nt:unstructured</code>子ノードを追加することで実行できます。</p> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし<br /> </td>
  </tr>
 </tbody>
</table>

### 監視ワード設定  {#watchwords-configurations}

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
   <td>Communities 設定をクリーンアップするために、遅延移行タスクを利用できます。<br /> <p>タスクは監視ワードを<code>/etc/watchwords</code>から<code>/conf/global/settings/community/watchwords</code>に移動します。</p> <p>カスタマイズした監視ワードがSCMに格納されている場合、それらを<code>/apps/settings/...</code>にデプロイし、優先するオーバーレイ<code>/conf/global/settings/...</code>設定がないことを確認する必要があります。</p> <p>移行タスクは<code>/etc</code>の場所を削除します。</p> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし<br /> </td>
  </tr>
 </tbody>
</table>

## 将来のアップグレードの前{#prior-to-upgrade}

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
     <li><code>cq:confproperty</code>を、すべての設定を保存するバケットパスに設定します。 同じ設定をサイトの「<strong>編集ウィザード - クラウド設定入力</strong>」でおこなうこともできます。</li>
     <li>関連するバッジングルールとスコアリングルールを<code>/etc/community/*</code>から、前の手順で作成したサイトコンテキストバケットに移動します。</li>
     <li>新しいルールの場所への相対参照を使用するように、サイトルートのバッジルールおよびスコアルールプロパティを調整します。
      <ol>
       <li>例えば、<code>cq:conf = /conf/we-retail</code>のプロパティの場合、ルールが現在この新しいバケットに移動された場合は<code>badgingRules [] = community/badging/rules</code>となります。</li>
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

### 従来のコミュニティコンソールデザイン  {#classic-communities-console-designs}

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

### Facebook ソーシャルログイン設定  {#facebook-social-login-configurations}

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
       <li>新しいFacebook Cloud設定を「前の場所」から「新しい場所」にコピーします（<code>/conf/global or /conf/&lt;tenant&gt;</code>の下）。</li>
      </ol> </li>
     <li>「新しい場所」で<code>[cq:Page]/jcr:content@cq:conf</code>プロパティを絶対パスに設定して、新しいFacebookソーシャルログイン設定を参照するようにAEM Communitiesサイトのルートを更新します。</li>
     <li>新しい場所を参照するように更新した AEM Communities サイトのルートから、従来の Facebook Connect クラウドサービスの関連付けを解除します。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし<br /> </td>
  </tr>
 </tbody>
</table>

### 言語オプション設定  {#language-options-configurations}

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

### Pinterest ソーシャルログイン設定  {#pinterest-social-login-configurations}

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
       <li><strong>ツール／クラウドサービス／Pinterest ソーシャルログイン設定</strong>で、AEM オーサリング UI を使用して新しい Pinterest ソーシャルログイン設定を手動で再作成します。<br /> または</li>
       <li>新しいPinterest Cloud設定を「前の場所」から「<code>/conf/global or /conf/&lt;tenant&gt;</code>」の下の適切な「新しい場所」にコピーします。</li>
      </ol> </li>
     <li>新しいPinterest Socialログイン設定を参照するように、AEM Communitiesサイトのルートを更新します。その際には、<code>[cq:Page]/jcr:content@cq:conf</code>プロパティを「新しい場所」の絶対パスに設定します。</li>
     <li>新しい場所を参照するように更新した AEM Communities サイトのルートから、従来の Pinterest Connect クラウドサービスの関連付けを解除します。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし<br /> </td>
  </tr>
 </tbody>
</table>

### スコアリング設定  {#scoring-configurations}

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
   <td><p>新しいリポジトリ構造に合わせて、スコアリングルールを<code>/apps/settings/</code>または/に保存できます<code>conf/.../settings</code></p>
    <ol>
     <li><code>/apps/settings</code>の場合、これはSCMで管理されるグローバルルールまたはデフォルトルールとして機能します。</li>
    </ol> <p>CRXDELiteを使用して、<code>/conf/</code>内にコンテキスト対応設定を作成します。</p>
    <ol>
     <li>目的の<code>/conf/.../settings</code>場所<br />に設定を作成します </li>
     <li>コミュニティサイトには<code>cq:conf </code>プロパティの設定が必要です。
      <ol>
       <li><code>cq:conf</code>が設定されていない場合、スコアリングルールは、サイトのルートノードにあるプロパティ'<code>scoringRules</code>'の指定されたパスから直接読み取られます。次に例を示します。 <code>/content/we-retail/us/en/community/jcr:content</code></li>
      </ol> </li>
    </ol> <p>クリーンアップ：リソースの削除 <code>/etc/community/scoring</code></p> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし<br /> </td>
  </tr>
 </tbody>
</table>

### Twitter ソーシャルログイン設定  {#twitter-social-login-configurations}

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
       <li>新しいTwitter Cloud設定を「前の場所」から「新しい場所」（<code>/conf/global or /conf/&lt;tenant&gt;</code>下）にコピーします。</li>
      </ol> </li>
     <li>「新しい場所」で<code>[cq:Page]/jcr:content@cq:conf</code>プロパティを絶対パスに設定して、新しいTwitterソーシャルログイン設定を参照するようにAEM Communitiesサイトのルートを更新します。</li>
     <li>新しい場所を参照するように更新した AEM Communities サイトのルートから、従来の Twitter Connect クラウドサービスの関連付けを解除します。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし<br /> </td>
  </tr>
 </tbody>
</table>

### その他  {#misc}

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

