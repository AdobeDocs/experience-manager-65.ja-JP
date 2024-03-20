---
title: MSM ロールアウトの競合
description: マルチサイトマネージャーでのロールアウトの競合に対処する方法について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
feature: Multi Site Manager
exl-id: e145e79a-c363-4a33-b9f9-99502ed20563
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 99%

---

# MSM ロールアウトの競合{#msm-rollout-conflicts}

ブループリントのブランチと依存するライブコピーのブランチの両方で同じ名前の新しいページが作成されると、競合が発生することがあります。

このような競合はロールアウト時に処理および解決する必要があります。

## 競合の処理 {#conflict-handling}

競合するページが（ブループリントやライブコピーのブランチ内に）存在するとき、MSM ではそれらの処理方法（処理の有無を含む）を定義できます。

ロールアウトがブロックされないように、次の内容を定義します。

* ロールアウト時にどのページ（ブループリントまたはライブコピー）が優先されるか
* 名前を変更するページと変更方法
* 公開済みのコンテンツにどのような影響があるか

  （標準の）Adobe Experience Manager（AEM）のデフォルトの動作では、公開済みのコンテンツに影響はありません。つまり、ライブコピーのブランチに手動で作成されたページが公開されている場合、競合の処理およびロールアウト後にもそのコンテンツは公開されたままになります。

標準の機能に加えて、カスタマイズされた競合ハンドラーを追加して別のルールを実装できます。これらは、アクションを個別のプロセスとして公開することも許可します。

### サンプルシナリオ {#example-scenario}

以降の節では、（手動で作成された）ブループリントとライブコピーのブランチの両方で作成された新しいサンプルページ `b` を使用して、競合を解決する様々な方法について説明します。

* ブループリント：`/b`

  1 つの子ページを持つメインページ、bp-level-1。

* ライブコピー：`/b`

  1 つの子ページを持つライブコピーブランチで手動作成されたページ、`lc-level-1`。

   * 公開時に子ページと共に `/b` にアクティベートします。

**ロールアウト前**

<table>
 <tbody>
  <tr>
   <td><strong>ロールアウト前のブループリント</strong></td>
   <td><strong>ロールアウト前のライブコピー</strong></td>
   <td><strong>ロールアウト前の公開</strong></td>
  </tr>
  <tr>
   <td><code>b</code><br /> <br /> (ブループリントのブランチで作成、ロールアウト準備完了)<br /> </td>
   <td><code>b</code><br /> <br /> (ライブコピーのブランチで手動で作成)<br /> </td>
   <td><code>b</code><br /> <br /> （ライブコピーのブランチで手動で作成された、ページ b のコンテンツを含む）</td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code> /lc-level-1</code><br /> <br /> (ライブコピーのブランチで手動で作成)<br /> </td>
   <td><code> /lc-level-1</code><br /> <br /> （ライブコピーのブランチで手動で作成された、ページ <br /> child-level-1 のコンテンツを含む）</td>
  </tr>
 </tbody>
</table>

## ロールアウトマネージャーと競合の処理 {#rollout-manager-and-conflict-handling}

ロールアウトマネージャーを使用すると、競合の管理をアクティベートまたはアクティベート解除できます。

これは、**Day CQ WCM Rollout Manager** の [OSGi 設定](/help/sites-deploying/configuring-osgi.md)を使用して行います。

* **手動で作成したページとの競合の処理**：

  ( `rolloutmgr.conflicthandling.enabled`)

  ロールアウトマネージャーが、ブループリントに存在する名前を使用してライブコピーで作成されたページからの競合を処理する場合は、true に設定します。

AEM には[競合の処理のアクティベートが解除されたときの動作が事前定義](#behavior-when-conflict-handling-deactivated)されています。

## 競合ハンドラー {#conflict-handlers}

AEM では、コンテンツをブループリントからライブコピーにロールアウトするときに存在するページの競合を、競合ハンドラーを使用して解決します。このような競合を解決する（一般的な）方法の 1 つは、ページの名前変更です。別の動作を選択できるように、複数の競合ハンドラーを有効にすることもできます。

AEM には次の機能があります。

* [デフォルトの競合ハンドラー](#default-conflict-handler)：

   * `ResourceNameRolloutConflictHandler`

* を実装する可能性 [カスタマイズされたハンドラー](#customized-handlers).
* 個別のハンドラーの優先度を設定するためのサービスランキングメカニズム。最もランキングの高いサービスが使用されます。

### デフォルトの競合ハンドラー {#default-conflict-handler}

デフォルトの競合ハンドラーは次のとおりです。

* `ResourceNameRolloutConflictHandler`と呼ばれます。

* このハンドラーを使用すると、ブループリントページが優先されます。
* カスタマイズされたハンドラーのランキングを高くする必要があることを前提としているので、このハンドラーのサービスランキングは低く（つまり `service.ranking` プロパティのデフォルト値より下に）設定されます。ただし、必要に応じて柔軟性を確保するために、このランキングは絶対最小値にはなりません。

この競合ハンドラーでは、ブループリントが優先されます。ライブコピーページ`/b`（ライブコピーのブランチ内で）`/b_msm_moved`に移動されます。

* ライブコピー： `/b`

  （ライブコピー内で） `/b_msm_moved` に移動されます。これはバックアップとして機能し、コンテンツが失われないようにします。

   * `lc-level-1` は移動されません。

* ブループリント：`/b`

  ライブコピーページ`/b`にロールアウトされます。

   * `bp-level-1` はライブコピーにロールアウトされます。

**ロールアウト後**

<table>
 <tbody>
  <tr>
   <td><strong>ロールアウト後のブループリント</strong></td>
   <td><strong>ロールアウト後のライブコピー</strong><br /> </td>
   <td></td>
   <td><strong>ロールアウト後のライブコピー</strong><br /> <br /> <br /> </td>
   <td><strong>ロールアウト後の公開</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code><br /> <br /> （ロールアウトされたブループリントページ b のコンテンツがある）<br /> </td>
   <td></td>
   <td><code>b_msm_moved</code><br /> <br /> （ライブコピーのブランチで手動で作成されたページ b のコンテンツがある）</td>
   <td><code>b</code><br /> <br /> （変更なし。ライブコピーのブランチで手動で作成された元のページ b のコンテンツで、b_msm_moved と呼ばれるようになったコンテンツを含む）<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code class="code"> /bp-level-1</code></td>
   <td><code> /lc-level-1</code><br /> <br /> (変更なし)</td>
   <td><code> </code></td>
   <td><code> /lc-level-1</code><br /> <br /> (変更なし)</td>
  </tr>
 </tbody>
</table>

### カスタマイズされたハンドラー {#customized-handlers}

カスタマイズされた競合ハンドラーを使用すると、独自のルールを実装できます。サービスランキングメカニズムを使用して、他のハンドラーとのやり取りのしかたを定義することもできます。

カスタマイズされた競合ハンドラーは、次のようにすることができます。

* 要件に合わせて名前を付けることができます。
* 要件に合わせて作成および設定できます。例えば、ライブコピーページが優先されるようにハンドラーを作成することができます。
* [OSGi 設定](/help/sites-deploying/configuring-osgi.md)、特に次を使用して設定されるように設計できます。

   * **サービスランキング**：

     他の競合ハンドラーと関連する順序を定義します（`service.ranking`）。

     デフォルト値は 0 です。

### 競合の処理のアクティベートが解除されたときの動作 {#behavior-when-conflict-handling-deactivated}

手動で[競合の処理のアクティベートを解除](#rollout-manager-and-conflict-handling)すると、AEM では競合するページに対してアクションが実行されません（競合しないページは期待されたとおりにロールアウトされます）。

>[!CAUTION]
>
>この動作は明示的に設定する必要があり、AEM は競合を無視するときに何のサインも示しません。そのため、この動作は必須の動作と見なされます。

この場合は、事実上ライブコピーが優先されます。ブループリントページ `/b`はコピーされず、ライブコピーページ `/b`はそのまま残ります。

* ブループリント：`/b`

  コピーされず、無視されます。

* ライブコピー：`/b`

  同じです。

<table>
 <caption>
   ロールアウト後
 </caption>
 <tbody>
  <tr>
   <td><strong>ロールアウト後のブループリント</strong></td>
   <td><strong>ロールアウト後のライブコピー</strong><br /> <br /> <br /> </td>
   <td><strong>ロールアウト後の公開</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code><br /> <br /> （変更なし。ライブコピーのブランチで手動で作成されたページ b のコンテンツがある）</td>
   <td><code>b</code><br /> <br /> （変更なし。ライブコピーのブランチで手動で作成されたページ b のコンテンツが含まれる）<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code><br /> </td>
   <td><code> /lc-level-1</code><br /> <br /> (変更なし)</td>
   <td><code> /lc-level-1</code><br /> <br /> (変更なし)</td>
  </tr>
 </tbody>
</table>

### サービスランキング {#service-rankings}

[OSGi](https://www.osgi.org/) サービスランキングは、個々の競合ハンドラーの優先度を定義するために使用できます。
