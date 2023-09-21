---
title: MSM ロールアウトの競合
description: Multi Site Manager のロールアウトの競合を処理する方法を説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
feature: Multi Site Manager
exl-id: e145e79a-c363-4a33-b9f9-99502ed20563
source-git-commit: 6799f1d371734b69c547f3c0c68e1e633aa63229
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 45%

---

# MSM ロールアウトの競合{#msm-rollout-conflicts}

ブループリントのブランチと依存するライブコピーのブランチの両方で同じ名前の新しいページが作成されると、競合が発生することがあります。

このような競合は、ロールアウト時に処理および解決する必要があります。

## 競合の処理 {#conflict-handling}

競合するページが（ブループリントとライブコピーのブランチ内に）存在する場合、MSM ではそれらの処理方法（または処理する場合も）を定義できます。

ロールアウトがブロックされないように、次の内容を定義します。

* ロールアウト時に優先されるページ（ブループリントまたはライブコピー）
* どのページの名前が変更されたか（およびその方法）
* これが公開されたコンテンツに与える影響

  Adobe Experience Manager(AEM)（標準）のデフォルトの動作では、公開されたコンテンツに影響はありません。 したがって、ライブコピーのブランチで手動で作成されたページが公開されても、競合の処理とロールアウトの後でそのコンテンツが公開されたままになります。

標準の機能に加えて、カスタマイズされた競合ハンドラーを追加して、異なるルールを実装できます。 また、公開アクションを個々のプロセスとして使用することもできます。

### サンプルシナリオ {#example-scenario}

以降のセクションでは、新しいページの例を使用する必要があります `b`（手動で作成された）ブループリントとライブコピーのブランチの両方に作成され、競合を解決する様々な方法を示します。

* ブループリント：`/b`

  1 つの子ページ、bp-level-1 を持つマスターページ。

* ライブコピー：`/b`

  ライブコピーのブランチで手動で作成されたページで、子ページが 1 つあるもの `lc-level-1`.

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

## Rollout Manager and Conflict Handling {#rollout-manager-and-conflict-handling}

ロールアウトマネージャを使用して、競合の管理をアクティブ化または非アクティブ化できます。

これは、 [OSGi 設定](/help/sites-deploying/configuring-osgi.md) / **Day CQ WCM Rollout Manager**:

* **手動で作成したページとの競合の処理**:

  ( `rolloutmgr.conflicthandling.enabled`)

  ロールアウトマネージャーが、ブループリントに存在する名前を使用してライブコピーで作成されたページからの競合を処理する場合は、true に設定します。

AEM には[競合の処理のアクティベートが解除されたときの動作が事前定義](#behavior-when-conflict-handling-deactivated)されています。

## 競合ハンドラー {#conflict-handlers}

AEMは、競合ハンドラーを使用して、コンテンツをブループリントからライブコピーにロールアウトする際に存在するページの競合を解決します。 ページ名の変更は、（通常の）競合を解決する方法の 1 つです。 複数の競合ハンドラーを操作して、異なる動作を選択できます。

AEM には次の機能があります。

* The [デフォルトの競合ハンドラー](#default-conflict-handler):

   * `ResourceNameRolloutConflictHandler`

* [カスタマイズされたハンドラー](#customized-handlers)を実装可能。
* 個々のハンドラーの優先度を設定できるサービスランキングメカニズム。 最もランキングの高いサービスが使用されます。

### デフォルトの競合ハンドラー {#default-conflict-handler}

デフォルトの競合ハンドラーは次のとおりです。

* `ResourceNameRolloutConflictHandler`と呼ばれます。

* このハンドラーを使用すると、ブループリントページが優先されます。
* このハンドラーのサービスランキングは、低く設定されます ( つまり、 `service.ranking` プロパティ ) を使用します。カスタマイズされたハンドラーは、より高いランクを必要とします。 ただし、必要に応じて柔軟性を確保するために、ランキングは絶対最小値ではありません。

この競合ハンドラーは、ブループリントを優先します。 ライブコピーページ`/b`（ライブコピーのブランチ内で）`/b_msm_moved`に移動されます。

* ライブコピー： `/b`

  （ライブコピー内で） `/b_msm_moved` に移動されます。これはバックアップとして機能し、コンテンツが失われないようにします。

   * `lc-level-1` は移動されません。

* ブループリント：`/b`

  ライブコピーページ`/b`にロールアウトされます。

   * `bp-level-1` がライブコピーにロールアウトされます。

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

カスタマイズされた競合ハンドラーを使用して、独自のルールを実装できます。 また、サービスのランキングメカニズムを使用して、他のハンドラーとのやり取りを定義することもできます。

カスタマイズされた競合ハンドラーは、次の条件を満たすことができます。

* 要件に従って名前が付けられます。
* 要件に応じて開発/設定します。例えば、ライブコピーページが優先されるようにハンドラーを開発できます。
* を使用して設定するように設計されている [OSGi 設定](/help/sites-deploying/configuring-osgi.md)（特に以下を含む）

   * **サービスランキング**：

     他の競合ハンドラーと関連する順序を定義します（`service.ranking`）。

     デフォルト値は 0 です。

### 競合の処理のアクティベートが解除されたときの動作 {#behavior-when-conflict-handling-deactivated}

手動で [競合処理を無効にする](#rollout-manager-and-conflict-handling)を指定した場合、AEMは、競合するページでは何のアクションも実行しません（競合しないページは想定どおりにロールアウトされます）。

>[!CAUTION]
>
>AEMでは、この動作を明示的に設定する必要があるので、競合が無視されていることを示すものはありません。そのため、競合が必要な動作であると見なされます。

この場合、ライブコピーが効果的に優先されます。 ブループリントページ `/b`はコピーされず、ライブコピーページ `/b`はそのまま残ります。

* ブループリント：`/b`

  まったくコピーされませんが、無視されます。

* ライブコピー：`/b`

  同じ。

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
