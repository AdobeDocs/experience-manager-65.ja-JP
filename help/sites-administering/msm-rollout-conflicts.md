---
title: MSM ロールアウトの競合
seo-title: MSM ロールアウトの競合
description: マルチサイトマネージャーでのロールアウトの競合に対処する方法について説明します。
seo-description: マルチサイトマネージャーでのロールアウトの競合に対処する方法について説明します。
uuid: 7a640905-aae2-498e-b95c-2c73008fa1cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 16db5334-604f-44e2-9993-10d683dee5bb
feature: マルチサイトマネージャー
exl-id: e145e79a-c363-4a33-b9f9-99502ed20563
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 78%

---

# MSM ロールアウトの競合{#msm-rollout-conflicts}

ブループリントブランチと依存ライブコピーブランチの両方で同じページ名の新しいページが作成されると、競合が発生する可能性があります。

このような競合はロールアウト時に処理および解決する必要があります。

## 競合の処理  {#conflict-handling}

競合するページが（ブループリントやライブコピーのブランチ内に）存在するとき、MSM ではそれらの処理方法（処理の有無を含む）を定義できます。

ロールアウトがブロックされないように、次の内容を定義します。

* ロールアウト時にどのページ（ブループリントまたはライブコピー）が優先されるか
* どのページの名前が変更になるか（およびその方法）
* 公開済みのコンテンツにどのような影響があるか

    （標準の）AEM のデフォルトの動作では、公開済みのコンテンツに影響はありません。つまり、ライブコピーのブランチに手動で作成されたページが公開されている場合、競合の処理およびロールアウト後にもそのコンテンツは公開されたままになります。

標準の機能に加えて、カスタマイズされた競合ハンドラーを追加して別のルールを実装できます。これらは、アクションを個別のプロセスとして公開することも許可します。

### サンプルシナリオ {#example-scenario}

以降の節では、（手動で作成された）ブループリントとライブコピーのブランチの両方で作成された新しいサンプルページ `b` を使用して、競合を解決する様々な方法について説明します。

* ブループリント：`/b`

   マスターページ子ページが1つある場合は、bp-level-1

* ライブコピー：`/b`

   ライブコピーのブランチで手動で作成されたページ子ページ`lc-level-1`が1つあります。

   * 公開時に子ページと共に`/b`としてアクティブ化されます。

**ロールアウト前**

<table>
 <tbody>
  <tr>
   <td><strong>ロールアウト前のブループリント</strong></td>
   <td><strong>ロールアウト前のライブコピー</strong></td>
   <td><strong>ロールアウト前の公開</strong></td>
  </tr>
  <tr>
   <td><code>b</code> <br /> （ブループリントブランチで作成され、ロールアウトの準備ができました）。<br /> </td>
   <td><code>b</code> <br /> （ライブコピーのブランチで手動で作成）<br /> </td>
   <td><code>b</code> <br />   （ライブコピーのブランチで手動で作成された、ページ b のコンテンツを含む）</td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code> /lc-level-1</code> <br /> （ライブコピーのブランチで手動で作成）<br /> </td>
   <td><code> /lc-level-1</code> <br />   （ライブコピーのブランチで手動で作成された、ページ <br /> child-level-1 のコンテンツを含む）</td>
  </tr>
 </tbody>
</table>

## Rollout Manager and Conflict Handling {#rollout-manager-and-conflict-handling}

ロールアウトマネージャーを使用すると、競合の管理をアクティベートまたはアクティベートを解除できます。

これは、**Day CQ WCM Rollout Manager** の [OSGi の設定](/help/sites-deploying/configuring-osgi.md) を使用しておこないます。

* **手動で作成したページとの競合を処理します**。

   ( `rolloutmgr.conflicthandling.enabled` )

   ロールアウトマネージャーが、ライブコピーで作成されたページからの競合をブループリント内に存在する名前で処理する必要がある場合は、trueに設定します。

AEM には[競合の処理のアクティベートが解除されたときの動作が事前定義](#behavior-when-conflict-handling-deactivated)されています。

## 競合ハンドラー {#conflict-handlers}

AEM は競合ハンドラーを使用して、コンテンツをブループリントからライブコピーにロールアウトするときに存在するページの競合を解決します。このような競合を解決する（一般的な）方法の 1 つは、ページの名前変更です。別の動作を選択できるように、複数の競合ハンドラーを有効にすることもできます。

AEM には次の機能があります。

* [デフォルトの競合ハンドラー](#default-conflict-handler)：

   * `ResourceNameRolloutConflictHandler`

* [カスタマイズされたハンドラー](#customized-handlers)を実装可能。
* 個別のハンドラーの優先度を設定するためのサービスランキングメカニズム。最もランキングの高いサービスが使用されます。

### デフォルトの競合ハンドラー {#default-conflict-handler}

デフォルトの競合ハンドラーの特徴は次のとおりです。

* `ResourceNameRolloutConflictHandler`と呼ばれます。

* このハンドラーを使用すると、ブループリントページが優先されます。
* このハンドラのサービスランキングは低く設定されています(（ `service.ranking`プロパティのデフォルト値以下）の場合は、カスタマイズされたハンドラーのランキングを上げる必要があると仮定します。 ただし、必要に応じて柔軟に対応するために、ランキングを絶対最小値にはしません。

この競合ハンドラーでは、ブループリントが優先されます。ライブコピーページ`/b`が（ライブコピーの分岐内で）`/b_msm_moved`に移動されます。

* ライブコピー：`/b`

   （ライブコピー内の）が`/b_msm_moved`に移動されます。 これはバックアップとして機能し、コンテンツが失われないようにします。

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
   <td><code>b</code> <br />   （ロールアウトされたブループリントページ b のコンテンツがある）<br /> </td>
   <td></td>
   <td><code>b_msm_moved</code> <br />   （ライブコピーのブランチで手動で作成されたページ b のコンテンツがある）</td>
   <td><code>b</code> <br />   （変更なし。ライブコピーのブランチで作成された元のページ b のコンテンツで、b_msm_moved と呼ばれるようになったコンテンツを含む）<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code class="code"> /bp-level-1</code></td>
   <td><code> /lc-level-1</code> <br /> （変更なし）</td>
   <td><code> </code></td>
   <td><code> /lc-level-1</code> <br /> （変更なし）</td>
  </tr>
 </tbody>
</table>

### カスタマイズされたハンドラー {#customized-handlers}

カスタマイズされた競合ハンドラーを使用すると、独自のルールを実装できます。サービスランキングメカニズムを使用することで、他のハンドラーとの関わり方を定義することもできます。

カスタマイズされた競合ハンドラーでは、次の操作をおこなうことができます。

* 要件に合わせて名前を付けることができます。
* 要件に合わせて開発および設定できます。例えば、ライブコピーページが優先されるハンドラーを開発できます。
* 特に次の [OSGi 設定](/help/sites-deploying/configuring-osgi.md)を使用して設定されるように設計できます。

   * **サービスランキング**:

      他の競合ハンドラー(`service.ranking`)に関連する順序を定義します。

      デフォルト値は 0 です。

### 競合の処理のアクティベートが解除されたときの動作 {#behavior-when-conflict-handling-deactivated}

手動で[競合の処理のアクティベートを解除](#rollout-manager-and-conflict-handling)すると、AEM では競合するページに対してアクションが実行されません（競合しないページは想定どおりにロールアウトされます）。

>[!CAUTION]
>
>この動作は明示的に設定する必要があり、AEM は競合を無視するときに何のサインも示しません。そのため、この動作は必須の動作と見なされます。

この場合、実際にはライブコピーが優先されます。ブループリントページ`/b`はコピーされず、ライブコピーページ`/b`は変更されません。

* ブループリント：`/b`

   コピーされず、無視されます。

* ライブコピー：`/b`

   同じままです。

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
   <td><code>b</code> <br />   （変更なし。ライブコピーのブランチで手動で作成されたページ b のコンテンツがある）</td>
   <td><code>b</code> <br />   （変更なし。ライブコピーのブランチで手動で作成されたページ b のコンテンツが含まれる）<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code> </td>
   <td><code> /lc-level-1</code> <br /> （変更なし）</td>
   <td><code> /lc-level-1</code> <br /> （変更なし）</td>
  </tr>
 </tbody>
</table>

### サービスランキング {#service-rankings}

[OSGi](https://www.osgi.org/) サービスランキングは、個々の競合ハンドラーの優先度を定義するために使用できます。
