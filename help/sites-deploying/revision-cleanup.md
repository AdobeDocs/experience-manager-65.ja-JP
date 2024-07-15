---
title: リビジョンクリーンアップ
description: Adobe Experience Manager 6.5 でのリビジョンクリーンアップ機能の使用方法について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
feature: Administering
exl-id: e53c4c81-f62e-4b6d-929a-6649c8ced23c
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: a2d7d82e0d6729e08b464d3843a9b44bcabd154b
workflow-type: tm+mt
source-wordcount: '5696'
ht-degree: 98%

---

# リビジョンクリーンアップ {#revision-cleanup}

## はじめに {#introduction}

リポジトリを更新するたびに、コンテンツのリビジョンが作成されます。その結果、更新のたびにリポジトリのサイズが大きくなります。ディスクリソースを解放するには、古いリビジョンをクリーンアップする必要があります。これは、リポジトリが無制限に増大するのを防ぐのに重要です。このメンテナンス機能は、リビジョンクリーンアップと呼ばれます。Adobe Experience Manager（AEM）6.0 以降、オフラインルーチンとして使用可能になりました。

AEM 6.3 以降では、この機能のオンラインバージョンである「オンラインでのリビジョンクリーンアップ」が導入されました。オフラインのリビジョンクリーンアップでは AEM インスタンスをシャットダウンする必要があるのに対し、オンラインのリビジョンクリーンアップでは AEM インスタンスがオンラインの間に実行できます。オンラインのリビジョンクリーンアップはデフォルトでオンになっており、リビジョンのクリーンアップを実行する方法として推奨されます。

**メモ**：オンラインでのリビジョンクリーンアップの概要および使用方法について詳しくは、[ビデオを参照してください](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/administration/use-online-revision-clean-up.html?lang=ja)。

リビジョンクリーンアップのプロセスは、**見積もり**、**コンパクション**、**クリーンアップ**&#x200B;の 3 つのフェーズで構成されます。見積もりフェーズでは、収集されるガベージの量に基づいて、次のフェーズ（コンパクション）を実行するかどうかが判断されます。コンパクションフェーズでは、未使用のコンテンツを除いて、セグメントと tar ファイルが書き換えられます。その後のクリーンアップフェーズでは、ガベージも含めて、古いセグメントが削除されます。通常、オフラインモードではより多くのスペースを再利用できます。これは、オンラインモードでは、追加のセグメントを収集しないようにする AEM の作業セットを考慮する必要があるからです。

リビジョンクリーンアップについて詳しくは、次のリンクを参照してください。

* [オンラインでのリビジョンクリーンアップの実行方法](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup)
* [オンラインでのリビジョンクリーンアップに関するよくある質問](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions)
* [オフラインでのリビジョンクリーンアップの実行方法](/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup)

また、[Oak の公式ドキュメント](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html)も参考になります。

### オフラインでのリビジョンクリーンアップではなく、オンラインのリビジョンクリーンアップを使用する場合 {#when-to-use-online-revision-cleanup-as-opposed-to-offline-revision-cleanup}

**リビジョンのクリーンアップを実行する場合は、オンラインでのリビジョンクリーンアップをお勧めします。** オフラインでのリビジョンクリーンアップは、例外的な場合にのみ使用してください。例えば、新しいストレージ形式に移行する前や、アドビカスタマーケアから依頼された場合です。

## オンラインでのリビジョンクリーンアップの実行方法 {#how-to-run-online-revision-cleanup}

オンラインでのリビジョンクリーンアップは、AEM のオーサーインスタンスとパブリッシュインスタンスの両方で、1 日に 1 回自動的に実行されるようにデフォルトで設定されています。必要な操作は、ユーザーアクティビティが最も少ない時間帯に、メンテナンスウィンドウを定義することだけです。オンラインでのリビジョンクリーンアップタスクは、次のように設定します。

1. メイン AEM ウィンドウで、**ツール／運営／ダッシュボード／メンテナンス**&#x200B;に移動するか、ブラウザーで `https://serveraddress:serverport/libs/granite/operations/content/maintenance.html` を指定してください。

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. **日別メンテナンスウィンドウ**&#x200B;にマウスポインターを置き、「**設定**」アイコンをクリックしてください。

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. 必要な値（繰り返し、開始時刻、終了時刻）を入力し、「**保存**」をクリックします。

   ![chlimage_1-92](assets/chlimage_1-92.png)

または、リビジョンクリーンアップのタスクを手動で実行する場合は、次の手順を実行します。

1. **ツール／運営／ダッシュボード／メンテナンス**&#x200B;に移動するか、`https://serveraddress:serverport/libs/granite/operations/content/maintenance.html` を直接参照してください。
1. **日別メンテナンスウィンドウ**&#x200B;をクリックします。
1. **リビジョンクリーンアップ** のアイコンにマウスポインターを置きます。
1. 「**実行**」をクリックします。

   ![chlimage_1-93](assets/chlimage_1-93.png)

### オフラインでのリビジョンクリーンアップ後のオンラインでのリビジョンクリーンアップの実行 {#running-online-revision-cleanup-after-offline-revision-cleanup}

リビジョンクリーンアップのプロセスでは、古いリビジョンが世代ごとに再利用されます。つまり、リビジョンクリーンアップを実行するたびに、新しい世代が作成されてディスクに保持されます。ただし、リビジョンクリーンアップにはオフラインとオンラインの 2 種類があり、オフラインでのリビジョンクリーンアップは 1 つの世代を保持し、オンラインでのリビジョンクリーンアップは 2 つの世代を保持するという違いがあります。そのため、オフラインでのリビジョンクリーンアップを実行した&#x200B;**後** にオンラインでのリビジョンクリーンアップを実行した場合は、以下のようになります。

1. オンラインでのリビジョンクリーンアップを初めて実行した後は、リポジトリのサイズが 2 倍になります。これは、ディスク上に 2 つの世代が保持されるからです。
1. その後の実行では、新しい世代が作成されるときに一時的にリポジトリのサイズが大きくなりますが、オンラインでのリビジョンクリーンアッププロセスにより以前の世代が再利用されるので、初めて実行した後のサイズで落ち着きます。

また、コミットの種類と数に応じて、各世代のサイズが以前の世代と異なる場合があるため、最終的なサイズは実行によって異なる可能性があります。

そのため、当初予測していたたリポジトリサイズよりも、少なくとも 2 倍または 3 倍大きなディスクサイズにすることをお勧めします。

## フルコンパクションモードとテールコンパクションモード  {#full-and-tail-compaction-modes}

**AEM 6.5** では、オンラインでのリビジョンクリーンアッププロセスの&#x200B;**コンパクション**&#x200B;フェーズ用に **2 つの新しいモード**&#x200B;が導入されています。

* **フルコンパクション**&#x200B;モードでは、リポジトリ全体のすべてのセグメントと tar ファイルが書き換えられます。そのため、後続のクリーンアップフェーズでは、リポジトリ全体で最大量のガベージを削除できます。フルコンパクションはリポジトリ全体に影響を与えるので、完了させるには大量のシステムリソースと時間が必要になります。フルコンパクションは、AEM 6.3 のコンパクションフェーズに対応します。
* **テールコンパクション**&#x200B;モードでは、リポジトリ内の最新のセグメントと tar ファイルのみが書き換えられます。最新のセグメントと tar ファイルは、フルコンパクションまたはテールコンパクションが最後に実行された後に追加されたものです。そのため、後続のクリーンアップフェーズでは、リポジトリの最新の部分に含まれるガベージのみを削除できます。テールコンパクションはリポジトリの一部にのみ影響するので、完了に必要なシステムリソースと時間がフルコンパクションよりも大幅に少なくなります。

これらのコンパクションモードでは、効率とリソース消費がトレードオフされます。テールコンパクションは効果が低いものの、通常のシステム運用に対する影響も少なくなります。一方、フルコンパクションはより効果的ですが、通常のシステム運用に大きな影響を与えます。

また、AEM 6.5 では、コンパクション時のより効率的なコンテンツの重複除外メカニズムが導入されました。これにより、リポジトリのディスク上のフットプリントがさらに削減されます。

次の 2 つの図は、AEM 6.3 と比較した AEM 6.5 の平均実行時間とディスク上の平均フットプリントの減少を示す社内ラボでのテスト結果を示しています。

![onrc-duration-6_4vs63](assets/onrc-duration-6_4vs63.png) ![segmentstore-6_4vs63](assets/segmentstore-6_4vs63.png)

### フルコンパクションおよびテールコンパクションの設定方法 {#how-to-configure-full-and-tail-compaction}

デフォルト設定では、テールコンパクションを平日に、フルコンパクションを日曜日に実行します。デフォルト設定は、`RevisionCleanupTask` [メンテナンスタスク](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup)の新しい設定値 `full.gc.days` を使用することで変更できます。

`full.gc.days` 値を設定する場合、フルコンパクションは値で定義された日に実行され、テールコンパクションは値で定義されていない日に実行されます。例えば、フルコンパクションを日曜日に実行するように設定した場合、テールコンパクションは月曜日から土曜日に実行されます。例えば、フルコンパクションを毎日実行するように設定した場合、テールコンパクションはまったく実行されません。

また、次の点も考慮します。

* **テールコンパクション**&#x200B;は効果が低いものの、通常のシステム運用に対する影響が少ない。そのため、営業日に実行することが想定されている。
* **フルコンパクション**&#x200B;はより効果的なものの、通常のシステム運用に大きな影響を与える。そのため、営業日以外に使用することが想定されている。
* テールコンパクションとフルコンパクションはいずれも、ピーク時を避けて実行するようにスケジュールする必要がある。

### トラブルシューティング {#troubleshooting}

新しいコンパクションモードを使用する場合は、次の点に注意してください。

* 入出力（I/O）アクティビティ（I/O 操作、CPU の I/O 待機 、コミットキューサイズなど）を監視できます。これは、システムが I/O バウンドしているかどうか、アップサイジングが必要かどうかを判断するのに役立ちます。
* `RevisionCleanupTaskHealthCheck` は、オンラインでのリビジョンクリーンアップの全体的なヘルスステータスを示します。AEM 6.3 と同様に機能し、フルコンパクションとテールコンパクションは区別されません。
* ログメッセージには、コンパクションモードについての関連情報が記録されます。例えば、オンラインでのリビジョンクリーンアップが開始されると、対応するログメッセージにコンパクションモードが表示されます。また、一部の例外的なケースでは、テールコンパクションの実行がスケジュールされていると、システムがフルコンパクションに戻り、ログメッセージにこの変更が示されることがあります。以下のログのサンプルは、コンパクションモードとテールコンパクションからフルコンパクションへの変更を示しています。

```
TarMK GC: running tail compaction
TarMK GC: no base state available, running full compaction instead
```

### 既知の制限事項 {#known-limitations}

テールコンパクションモードとフルコンパクションモードを切り替えると、クリーンアッププロセスが遅れる場合があります。より正確には、フルコンパクションの後にリポジトリは増大します（2 倍のサイズ）。リポジトリがフルコンパクション前のサイズより小さくなると、余分なスペースは後続のテールコンパクションで再利用されます。メンテナンスタスクの並列実行も避ける必要があります。

**最初に予測したリポジトリサイズよりも少なくとも 2 倍または 3 倍大きなディスクサイズにすることをお勧めします。**

## オンラインでのリビジョンクリーンアップに関するよくある質問 {#online-revision-cleanup-frequently-asked-questions}

### AEM 6.5 のアップグレードに関する考慮事項 {#aem-upgrade-considerations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td>質問 </td>
   <td>回答</td>
  </tr>
  <tr>
   <td>AEM 6.5 にアップグレードするときの注意点を教えてください。</td>
   <td><p>TarMK の永続性形式が AEM 6.5 で変更されます。これらの変更には、事前の移行手順は必要ありません。既存のリポジトリは、周期的な移行を実行します。これはユーザーに対して透過的です。AEM 6.5（または関連ツール）がリポジトリに初めてアクセスすると、移行プロセスが開始されます。</p> <p><strong>AEM 6.5 永続性形式への移行が開始されると、リポジトリを以前の AEM 6.3 永続性形式に戻すことはできません。</strong></p> </td>
  </tr>
 </tbody>
</table>

### Oak Segment Tar への移行 {#migrating-to-oak-segment-tar}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>質問</strong></td>
   <td><strong>回答</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>リポジトリを移行する必要があるのはなぜですか。</strong></td>
   <td><p>AEM 6.3 で、特にオンラインでのリビジョンクリーンアップのパフォーマンスと効果を高めるために、ストレージ形式の変更が必要となりました。これらの変更は後方互換性がなく、古い Oak セグメント（AEM 6.2 以前）で作成されたリポジトリは移行する必要があります。</p> <p>ストレージ形式を変更するその他メリットは次のとおりです。</p>
    <ul>
     <li>スケーラビリティの向上（セグメントサイズの最適化）</li>
     <li><a href="/help/sites-administering/data-store-garbage-collection.md" target="_blank">データストアのガベージの収集</a>の迅速化<br /> </li>
     <li>将来の機能強化に向けた基盤整備</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>以前の Tar 形式もサポートされますか。</strong></td>
   <td>AEM 6.3 以降では、新しい Oak Segment Tar のみがサポートされます。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>コンテンツの移行は常に必須ですか。</strong></td>
   <td>はい。新しいインスタンスから始めない限り、常にコンテンツを移行する必要があります。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>6.3 以降にアップグレードしてから、（例えば、別のメンテナンスウィンドウを使用して）後で移行を実行できますか？</strong></td>
   <td>できません。前述のとおり、コンテンツの移行は必須です。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>移行時のダウンタイムは回避できますか。</strong></td>
   <td>いいえ。これは、実行中のインスタンスでは行えない 1 回限りの作業です。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>誤って不適切なリポジトリ形式に対して移行を実行した場合はどうなりますか。</strong></td>
   <td>oak-segment-tar リポジトリに対して oak-segment モジュール（またはその逆）を実行しようとすると、起動が失敗し、「Invalid segment format（セグメント形式が無効です）」というメッセージが表示されて、<em>IllegalStateException</em> が発生します。データが破損することはありません。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>検索インデックスの再作成は必要ですか。</strong></td>
   <td>いいえ。oak-segment から oak-segment-tar への移行によって、コンテナ形式が変更されます。含まれているデータに影響はなく、データは変更されません。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>移行中および移行後に必要と予想されるディスク領域を計算する最適な方法を教えてください。</strong></td>
   <td>この移行は、セグメントストアを新しい形式で再作成することに相当します。これは、移行中に必要な追加のディスク容量を見積もるために使用できます。古いセグメントストアは移行後に削除して、領域を再利用することができます。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>移行時間の最適な見積もり方法を教えてください。</strong></td>
   <td>移行前に<a href="/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup">オフラインでのリビジョンクリーンアップ</a>を実行すると、移行のパフォーマンスを大幅に高めることができます。アップグレードプロセスの前提条件として、オフラインでのリビジョンクリーンアップを実行することをすべての顧客にお勧めします。一般に移行時間は、オフラインでのリビジョンクリーンアップタスクが移行前に実行されていると仮定して、オフラインでのリビジョンクリーンアップ時間と同程度です。</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### オンラインでのリビジョンクリーンアップの実行 {#running-online-revision-cleanup}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>質問</strong></td>
   <td><strong>回答</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>オンラインでのリビジョンクリーンアップは、どのくらいの頻度で実行する必要がありますか。</strong></td>
   <td>1 日に 1 回。これは、操作ダッシュボードのデフォルトの設定です。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>オンラインでのリビジョンクリーンアップのメンテナンスタスクを開始する時間を設定する方法を教えてください。</strong></td>
   <td><a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">オンラインでのリビジョンクリーンアップの実行方法</a> の節を参照してください。 </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>オンラインでのリビジョンクリーンアップには、超過するべきではない実行頻度の上限がありますか。</strong></td>
   <td>オンラインでのリビジョンクリーンアップは、デフォルト設定のとおり、1 日に 1 回実行することをお勧めします。<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>オンラインでのリビジョンクリーンアップの実行頻度を決定する主な指標は何ですか。</strong></td>
   <td>オンラインでのリビジョンクリーンアップはメンテナンスタスクとして設定され、毎日自動的に実行されるので、実行頻度を決定する必要はありません。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>オンラインでのリビジョンクリーンアップを初めて実行したときに、領域が再利用されないのはなぜですか。</strong></td>
   <td>オンラインでのリビジョンクリーンアップでは、古いリビジョンが世代ごとに再利用されます。リビジョンのクリーンアップが実行されるたびに、新しい世代が生成されます。少なくとも 2 世代前のコンテンツのみが再利用されます。つまり、最初の実行時には再利用されるコンテンツが何もありません。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>オフラインでのリビジョンクリーンアップの実行後に初めてオンラインでのリビジョンクリーンアップを実行したときに、領域が再利用されないのはなぜですか。</strong></td>
   <td><p>オフラインでのリビジョンクリーンアップでは、最新の 2 世代のオンラインでのリビジョンクリーンアップと比較して、最新以外のすべての世代が再利用されます。新しいリポジトリの場合、オンラインでのリビジョンクリーンアップでは、オフラインでのリビジョンクリーンアップ後に初めて実行されたとき、再利用できるほど古い世代がないので、領域を再利用できません。</p> <p><a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">この章</a>の「オフラインでのリビジョンクリーンアップの実行後にオンラインでのリビジョンクリーンアップを実行した場合」の節も参照してください。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>オンラインでのリビジョンクリーンアップは、通常、オーサーとパブリッシュでは異なる時間帯に実行しますか。</strong></td>
   <td>いつ実行すべきかは、営業時間と顧客のオンラインプレゼンスのトラフィックパターンによって異なります。クリーンアップの効果を最大限に高めるには、メンテナンスウィンドウを主要な実稼動時間外に設定する必要があります。AEM パブリッシュインスタンス（TarMK ファーム）が複数ある場合は、オンラインでのリビジョンクリーンアップのメンテナンスウィンドウが重ならないように調整する必要があります。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>オンラインでのリビジョンクリーンアップを実行するための前提条件はありますか。</strong></td>
   <td><p>オンラインでのリビジョンクリーンアップは、AEM 6.3 以降のリリースでのみ使用できます。また、古いバージョンの AEM を使用している場合は、新しい <a href="/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar">Oak Segment Tar</a> に移行する必要があります。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>オンラインでのリビジョンクリーンアップの時間に作用する要因は何ですか。</strong></td>
   <td>要因は次のとおりです。<br />
    <ul>
     <li>リポジトリのサイズ</li>
     <li>システムへの負荷（リクエスト/分、特に書き込み操作）</li>
     <li>アクティビティパターン（読み取りと書き込み）</li>
     <li>ハードウェアの仕様（CPU パフォーマンス、メモリ、IOPS）</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>オンラインでのリビジョンクリーンアップの実行中も作成者は作業できますか。</strong></td>
   <td>はい、オンラインでのリビジョンクリーンアップは、同時書き込みに対応しています。ただし、オンラインでのリビジョンクリーンアップは、同時書き込みトランザクションを行わなくても高速かつ効率的に動作します。アドビでは、オンラインでのリビジョンクリーンアップのメンテナンスタスクは、大量のトラフィックが発生しない比較的に静かな時間にスケジュールすることをお勧めします。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>オンラインでのリビジョンクリーンアップを実行するときのディスク領域とヒープメモリの最小要件を教えてください。</strong></td>
   <td><p>オンラインでのリビジョンクリーンアップ中、ディスク領域は継続的に監視されます。使用可能なディスク容量が臨界値を下回った場合、プロセスはキャンセルされます。臨界値とは、リポジトリのその時点でのディスクフットプリントの 25％であり、変更はできません。</p> <p><strong>アドビでは、当初予測していたリポジトリサイズよりも、少なくとも 2 倍または 3 倍大きなディスクサイズにすることをお勧めします。</strong></p> <p>クリーンアッププロセス中、ヒープの空き容量が継続的に監視されます。ヒープの空き容量が臨界値を下回った場合、プロセスはキャンセルされます。臨界値は、org.apache.jackrabbit.oak.segment.SegmentNodeStoreService#MEMORY_THRESHOLD を使用して設定します。デフォルト値は 15% です。</p> <p>最小コンパクションヒープサイズ設定のレコメンデーションは、AEM のメモリサイズ設定のレコメンデーションと切り離されていません。通常、<strong>AEM インスタンスが、ユースケースとそこで予測されるペイロードに対応するのに十分なサイズの場合、クリーンアッププロセスは十分なメモリを取得します。</strong></p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>オンラインでのリビジョンクリーンアップの実行中、パフォーマンスにはどのような影響があると予想されますか。</strong></td>
   <td>オンラインでのリビジョンクリーンアップは、通常のシステム操作と並行してリポジトリの読み取りと書き込みを行うバックグラウンドプロセスです。特に、リポジトリへの排他的なアクセスを短時間取得し、他のスレッドからのリポジトリへの書き込みを阻止する必要がある場合もあります。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>オンラインでのリビジョンクリーンアップの所要時間はどのくらいですか。</strong></td>
   <td>アドビ内部で実行した最新のパフォーマンステストによると、所要時間は 2 時間以下です。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>オンラインでのリビジョンクリーンアップにそれよりも長い時間がかかる場合はどうすればよいですか。</strong></td>
   <td>
    <ul>
     <li>クリーンアップが毎日実行されていることを確認してください。<br /> </li>
     <li>操作ダッシュボードでメンテナンスウィンドウを適切に設定して、リポジトリのアクティビティが最も少ない時間帯にクリーンアップが実行されるようにしてください。</li>
     <li>システムリソース（CPU、メモリ、I/O）を拡張してください。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>設定したメンテナンスウィンドウ中にオンラインでのリビジョンクリーンアップが終わらない場合は、何が起きていますか。</strong></td>
   <td>他のメンテナンスタスクによって、その実行が遅延されないようにします。これは、同じメンテナンスウィンドウ内で、オンラインでのリビジョンクリーンアップの他にもメンテナンスタスクが実行された場合に発生する可能性があります。なお、メンテナンスタスクは順番に実行されます。順番は変更できません。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>リビジョンのガベージコレクションがスキップされるのはなぜですか。</strong></td>
   <td><p>リビジョンクリーンアップでは見積もりフェーズで、クリーンアップするのに十分なガベージがあるかどうかを判断します。見積もりでは、最後のコンパクション後のリポジトリのサイズと現在のサイズが比較されます。サイズが設定されている差分を超えると、クリーンアップが実行されます。サイズの差分は 1 GB に設定されています。これは、リポジトリのサイズが前回のクリーンアップの実行から 1 GB 増加していない場合、新しいリビジョンのクリーンアップの反復がスキップされることになります。 </p> <p>見積もりフェーズに関連するログエントリは以下のとおりです。</p>
    <ul>
     <li>リビジョンの GC が実行される：<em>サイズ差分は N％または N/N（N/N バイト）であるため、コンパクションを実行</em></li>
     <li>リビジョンの GC が実行<strong>されない</strong>：<em>サイズ差分は N％または N/N（N/N バイト）であるため、この時点ではコンパクションをスキップ</em></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>パフォーマンスへの影響が大きすぎる場合に、自動コンパクションを安全に中止できますか。</strong></td>
   <td>はい。AEM 6.3 以降では、操作ダッシュボード内のメンテナンスタスクウィンドウまたは JMX から安全に停止できます。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>スケジュールされたクリーンアップタスクの実行中に AEM インスタンスがシャットダウンされた場合、プロセスは安全に中止されますか。またはコンパクションが終了するまでシャットダウンがブロックされますか。</strong></td>
   <td>リビジョンクリーンアップが中断され、リポジトリは安全にシャットダウンされます。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>オンラインでのリビジョンクリーンアップ中にシステムがクラッシュした場合はどうなりますか。</strong></td>
   <td>このような場合にデータが破損するリスクはありません。残ったガベージは、その後の実行でクリーンアップされます。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>オンラインでのリビジョンクリーンアップを実行しないと、どのような影響がありますか。</strong></td>
   <td>時間の経過に伴いパフォーマンスが低下します。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>どのリビジョンが収集されますか。</strong></td>
   <td>デフォルトでは、オンラインでのリビジョンクリーンアップで収集されるのは 24 時間以上前のリビジョンのみです。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>リポジトリへの同時書き込みからの干渉が多すぎる場合はどうなりますか。</strong></td>
   <td><p>同時書き込みが可能なシステムでは、コンパクションサイクルの終了時に変更をコミットできるように、オンラインでのリビジョンクリーンアップで排他書き込みアクセスが必要になる場合があります。システムは <strong>forceCompact モード</strong>になります。詳しくは、<a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html" target="_blank">oak のドキュメント</a>を参照してください。強制コンパクションでは、排他的な書き込みロックが取得され、同時書き込みの干渉を受けずに最終的に変更をコミットします。応答時間に対する影響を制限するために、タイムアウト値を定義できます。この値はデフォルトで 1 分に設定されています。つまり、1 分以内に強制コンパクションが完了しない場合、同時コミットが優先され、コンパクションプロセスは中止されます。</p> <p>強制コンパクションの実行時間は以下の要素によって変動します。</p>
    <ul>
     <li>ハードウェア：特に IOPS。IOPS が増えるにつれ、処理時間が短くなります。</li>
     <li>セグメントストアのサイズ：時間はセグメントストアのサイズと共に長くなります。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>スタンバイインスタンスでは、オンラインでのリビジョンクリーンアップはどのように実行されますか。</strong></p> </td>
   <td><p>コールドスタンバイセットアップでは、オンラインでのリビジョンクリーンアップの実行するには、プライマリインスタンスのみを設定する必要があります。スタンバイインスタンスで、オンラインでのリビジョンクリーンアップを明示的にスケジュールする必要はありません。</p> <p>スタンバイインスタンスでの対応する操作は自動クリーンアップです。これは、オンラインでのリビジョンクリーンアップのクリーンアップフェーズに相当します。自動クリーンアップは、プライマリインスタンスでオンラインリビジョンクリーンアップが実行された後、スタンバイインスタンスで実行されます。</p> <p>見積もりフェーズとコンパクションフェーズは、スタンバイインスタンスでは実行されません。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>オフラインでのリビジョンクリーンアップでは、オンラインでのリビジョンクリーンアップよりも多くのディスク領域を解放できますか。</strong></td>
   <td><p>オフラインでのリビジョンクリーンアップでは、古いリビジョンを即座に削除できますが、オンラインでのリビジョンクリーンアップでは、アプリケーションスタックによって参照されている古いリビジョンを考慮する必要があります。そのため、前者は後者よりも積極的にガベージを削除でき、数回のガベージコレクションのサイクルで効果が表れます。</p> <p><a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">この章</a>の「オフラインでのリビジョンクリーンアップの実行後にオンラインでのリビジョンクリーンアップを実行した場合」の節も参照してください。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>メモリマップファイル操作に関する考慮事項はありますか。</td>
   <td>
    <ul>
     <li><strong>Windows 環境</strong>では、通常のファイルアクセスが常に強制的に利用されるので、メモリマップアクセスは使用されません。一般的に、利用可能なすべての RAM をヒープに割り当て、segmentCache サイズを大きくする必要があります。segmentCache のサイズは、org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config に segmentCache.size オプションを追加して大きくします（例：segmentCache.size=20480）。オペレーティングシステムや他のプロセス用に、一定の RAM を残しておいてください。</li>
     <li><strong>Windows 以外の環境</strong>では、物理メモリのサイズを大きくすることで、リポジトリのメモリマップの効率性を向上します。</li>
    </ul> </td>
   <td>
    <ul>
     <li> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### オンラインでのリビジョンクリーンアップの監視 {#monitoring-online-revision-cleanup}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>オンラインでのリビジョンクリーンアップ中に監視する必要があるものは何ですか。</strong></td>
   <td>
    <ul>
     <li>オンラインでのリビジョンクリーンアップが有効な場合は、ディスク容量を監視する必要があります。ディスク容量が不十分な場合、クリーンアップは実行されないか、早期に終了します。</li>
     <li>オンラインでのリビジョンクリーンアップの完了時間をログで確認してください。これは 2 時間以下である必要があります。</li>
     <li>チェックポイントの数。コンパクションの実行時にチェックポイントが 3 つ以上ある場合は、チェックポイントをクリーンアップすることをお勧めします。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>オンラインでのリビジョンクリーンアップが正常に完了したかどうかを確認する方法を教えてください。</strong></td>
   <td><p>オンラインでのリビジョンクリーンアップが正常に完了したかどうかは、ログを確認して確認できます。</p> <p>例：「<code>TarMK GC #{}: compaction completed in {} ({} ms), after {} cycles</code> 」は、メッセージ「<code>TarMK GC #{}: compaction gave up compacting concurrent commits after {} cycles</code>」（同時負荷が大きすぎることを意味する）が先行しない限り、コンパクションステップが正常に完了したことを意味します。</p> <p>それに伴い、クリーンアップステップの正常終了を示すメッセージ「<code>TarMK GC #{}: cleanup completed in {} ({} ms</code>」が表示されます。</p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><strong>前回のオンラインでのリビジョンクリーンアップの実行に関する統計はどこで確認できますか。</strong></td>
   <td><p>ステータス、進行状況および統計は、JMX（<code>SegmentRevisionGarbageCollection</code> MBean）経由で公開されます。<code>SegmentRevisionGarbageCollection</code> MBean の詳細に関しては、<a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">次の段落</a> を参照してください。</p> <p>進行状況は、 <code>EstimatedRevisionGCCompletion</code> のフィールド名で追跡できます。 <code>SegmentRevisionGarbageCollection MBean.</code></p> <p>MBean の参照を取得するには、 <code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection"</code> を使用します。</p> <p>確認できるのは、システムを最後に起動した以降の統計情報のみです。<a href="/help/sites-administering/operations-dashboard.md#monitoring-with-external-services" target="_blank"> 外部モニタリングツールを使用すると、AEMの稼動時間外もデータを監視できます </a>。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>関連するログエントリは何ですか？</strong></td>
   <td>
    <ul>
     <li>オンラインでのリビジョンクリーンアップが開始/停止しました
      <ul>
       <li>オンラインでのリビジョンクリーンアップは、見積もり、コンパクション、クリーンアップの 3 つのフェーズで構成されます。リポジトリに十分な量のガベージが含まれていない場合は、見積もりによってコンパクションとクリーンアップがスキップされることがあります。最新バージョンの AEM では、メッセージ「<code>TarMK GC #{}: estimation started</code>」は見積もりの開始を示し、「<code>TarMK GC #{}: compaction started, strategy={}</code>」はコンパクションの開始を示し、「T<code>arMK GC #{}: cleanup started. Current repository size is {} ({} bytes</code>」はクリーンアップの開始を示します。</li>
      </ul> </li>
     <li>リビジョンのクリーンアップで取得したディスクスペース
      <ul>
       <li>スペースは、クリーンアップフェーズが完了した場合にのみ再利用されます。クリーンアップフェーズの完了は、ログメッセージ「T<code>arMK GC #{}: cleanup completed in {} ({} ms</code>」で示されます。クリーンアップ後のサイズは {}（{} バイト）で、再利用された領域は {}（{} バイト）です。コンパクションマップの重み付け／深さは {}／{}（{} バイト／{}）です。</li>
      </ul> </li>
     <li>リビジョンのクリーンアップ中に問題が発生しました
      <ul>
       <li>多くの失敗条件があり、すべての障害は、「TarMK GC」で始まる WARN または ERROR ログメッセージで示されます。</li>
      </ul> </li>
    </ul> <p>また、<a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">エラーメッセージに基づくトラブルシューティング</a>の節を参照してください。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>オンラインでのリビジョンクリーンアップが完了した後に、どのくらいのスペースが再利用されたかを確認する方法は？</strong></td>
   <td>クリーンアップサイクルの最後に、ログに「<code>TarMK GC #3: cleanup completed</code>」メッセージが表示されます。これにはリポジトリのサイズと再利用されたガベージの量も含まれます。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>オンラインでのリビジョンクリーンアップが完了した後に、リポジトリの整合性を確認する方法を教えてください。</strong></td>
   <td><p>オンラインでのリビジョンクリーンアップの後は、リポジトリの整合性チェックは必要ありません。 </p> <p>ただし、クリーンアップ後にリポジトリのステータスを確認するには、次の操作を実行できます。</p>
    <ul>
     <li>リポジトリ<a href="/help/sites-deploying/consistency-check.md" target="_blank">トラバーサルチェック</a></li>
     <li>クリーンアッププロセスが完了したら、oak-run ツールを使用して不整合をチェックします。この方法について詳しくは、 <a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">Apache ドキュメントを参照してください。</a> ツールを実行するために AEM をシャットダウンする必要はありません。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>オンラインでのリビジョンクリーンアップが失敗したかどうかを検出する方法と、回復する手順を教えてください。</strong></td>
   <td>失敗条件は、「TarMK GC」で始まる WARN または ERROR ログメッセージで示されます。 また、<a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">エラーメッセージに基づくトラブルシューティング</a>の節を参照してください。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>リビジョンクリーンアップのヘルスチェックではどのような情報が表示されますか。ステータスレベルの色分けとの対応も教えてください。 </strong></td>
   <td><p>リビジョンのクリーンアップのヘルスチェックは、<a href="/help/sites-administering/operations-dashboard.md#health-reports" target="_blank">操作ダッシュボード</a>の一部です。<br /> </p> <p>最後に実行されたオンラインでのリビジョンクリーンアップメンテナンスタスクが正常に完了した場合、ステータスは<strong>緑色</strong>になります。</p> <p>オンラインでのリビジョンクリーンアップのメンテナンスタスクが 1 回キャンセルされた場合、ステータスは<strong>黄色</strong>になります。<br /> </p> <p>オンラインでのリビジョンクリーンアップのメンテナンスタスクが 3 回連続でキャンセルされた場合、<strong>赤色</strong>になります。<strong>この場合、手動の操作が必要であるか</strong>、オンラインでのリビジョンクリーンアップが再び失敗する可能性が高くなります。詳細情報に関しては、以下の<a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-online-revision-cleanup">トラブルシューティング</a>の節を参照してください。<br /> </p> <p>また、システムの再起動後に、ヘルスチェックのステータスもリセットされます。そのため、新しく再起動したインスタンスは、リビジョンクリーンアップのヘルスチェックが緑色のステータスで表示されます。  <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-external-services" target="_blank"> 外部モニタリングツールを使用すると、AEMの稼動時間外もデータを監視できます </a>。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>スタンバイインスタンスで自動クリーンアップを監視する方法を教えてください。</strong></p> </td>
   <td><p>ステータス、進行状況および統計は、<code>SegmentRevisionGarbageCollection</code> MBean を使用して、JMX 経由で公開されます。次の <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">Oak ドキュメント</a>も参照してください。 </p> <p>MBean の参照は、<code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection"</code> を使用して取得できます。</p> <p>統計は、最後にシステムを起動した後にのみ使用できます。  <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-external-services" target="_blank"> 外部モニタリングツールを使用すると、AEMの稼動時間外もデータを監視できます </a>。</p> <p>また、ログファイルを使用して、自動クリーンアップのステータス、進行状況および統計情報を確認できます。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>スタンバイインスタンスでの自動クリーンアップ中に監視する必要があるものは何ですか。</strong></p> </td>
   <td>
    <ul>
     <li>自動クリーンアップの実行中は、ディスクスペースを監視する必要があります。</li>
     <li>（ログを使用して）完了時間が 2 時間を超えていないことを確認します。</li>
     <li>自動クリーンアップが実行された後のセグメントストアサイズ。スタンバイインスタンスでのセグメントストアのサイズは、プライマリインスタンスでのサイズとほぼ同じである必要があります。</li>
    </ul> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### オンラインでのリビジョンクリーンアップのトラブルシューティング {#troubleshooting-online-revision-cleanup}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>オンラインでのリビジョンクリーンアップを実行しない場合に起こり得る最悪の状況は何ですか。</strong></td>
   <td>AEM インスタンスのディスク領域が不足し、実稼動が停止します。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>パブリッシュインスタンスでオンラインでのリビジョンクリーンアップを実行する場合、ユーザートラフィックが多いことは問題になりますか。</strong></td>
   <td>ユーザートラフィックが多いと、コンパクションフェーズを正常に完了できるかどうかに影響します。<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>ヘルスチェックおよびログエントリによると、オンラインでのリビジョンクリーンアップは 3 回連続で正常に完了していません。オンラインでのリビジョンクリーンアップを正常に完了させるには、何が必要ですか。</strong></td>
   <td>問題を見つけて修正するには、次の手順を実行します。<br />
    <ul>
     <li>まず、ログエントリを確認します。<br /> </li>
     <li>ログの情報に応じて、適切なアクションを実行します。
      <ul>
       <li>ログに、5 回の失敗したコンパクションサイクルと<code>forceCompact</code>サイクルでのタイムアウトが示されている場合は、リポジトリへの書き込みが少ない、処理が少ない時間帯にメンテナンスウィンドウをスケジュールします。リポジトリへの書き込みは、<em>https://serveraddress:serverport/libs/granite/operations/content/monitoring/page.html</em> にあるリポジトリ指標の監視ツールで確認できます。</li>
       <li>メンテナンスウィンドウの最後にクリーンアップが停止した場合は、メンテナンスタスクのユーザーインターフェイスでメンテナンスウィンドウの設定が十分な大きさであることを確認します。</li>
       <li>使用可能なヒープメモリが不十分な場合は、インスタンスに十分なメモリがあることを確認します。</li>
       <li>反応が遅れるとセグメントストアが大きくなりすぎ、メンテナンスウィンドウが長くても、オンラインでのリビジョンクリーンアップを完了できない可能性があります。例えば、先週にオンラインでのリビジョンクリーンアップが正常に完了しなかった場合は、セグメントストアを管理可能なサイズに戻すために、オフラインでのメンテナンスを計画し、オフラインでのリビジョンクリーンアップを実行することをお勧めします。</li>
      </ul> </li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>ヘルスチェックアラートがオンになった場合、何をする必要がありますか。</strong></td>
   <td>この前の項目を参照してください。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>スケジュールされたメンテナンスウィンドウ中にオンラインでのリビジョンクリーンアップが時間切れになった場合、どうなりますか。</strong></td>
   <td>オンラインでのリビジョンクリーンアップはキャンセルされ、残りは削除されます。メンテナンスウィンドウが次回スケジュールされると、再び開始されます。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong><code>SegmentNotFoundException</code> インスタンスが <code>error.log</code> に記録される理由と復旧方法を教えてください。</strong></td>
   <td><p><code>SegmentNotFoundException</code> は、TarMK がアクセスを試みたストレージユニット（セグメント）が見つからなかったときに、TarMK によってログに記録されます。この問題を引き起こす可能性のあるシナリオは次の 3 つです。</p>
    <ol>
     <li>アプリケーションが、推奨されるアクセスメカニズム（Sling や JCR API など）を回避し、下位レベルの API／SPI を使用してリポジトリにアクセスし、セグメントの保持時間を超えている場合。つまり、オンラインでのリビジョンクリーンアップで許可されている保持時間（デフォルトでは 24 時間）より長い間、エンティティへの参照を保持します。このケースは一時的なもので、データの破損にはつながりません。復旧するには、oak-run ツールを使用して、この例外が一時的なものである（oak-run チェックでエラーが報告されない）ことを確認する必要があります。このためには、インスタンスをオフラインにし、後で再起動する必要があります。</li>
     <li>ディスク上のデータの破損を招いた外部イベント。これは、ディスク障害、ディスク容量不足、または必要なデータファイルの誤った変更などになります。この場合は、インスタンスをオフラインにし、oak-run チェックを使用して修復する必要があります。oak-run チェックの実行方法について詳しくは、次の <a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">Apache ドキュメント</a> を参照してください。</li>
     <li>他のすべての状況では、<a href="https://experienceleague.adobe.com/?support-solution=General&amp;lang=ja&amp;support-tab=home#support" target="_blank">アドビカスタマーケア</a>に連絡して対処します。</li>
    </ol> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### エラーメッセージに基づくトラブルシューティング {#troubleshooting-based-on-error-messages}

オンラインでのリビジョンクリーンアッププロセス中に問題が発生した場合、詳細な error.log が生成されます。次の一覧では、最も一般的なメッセージを説明し、解決策を提供します。

<!---| **Phase** |**Log Messages** |**Explanation** |**Next Steps** |
|---|---|---|---|
|   |  |  |  |
| Estimation |TarMK GC #2: estimation skipped because compaction is paused |The estimation phase is skipped when compaction is disabled on the system by configuration. |Enable Online Revision Cleanup. |
|   |TarMK GC #2: estimation interrupted: ${REASON}. Skipping compaction. |The estimation phase terminated prematurely. Some examples of events that could interrupt the estimation phase: not enough memory or disk space on the host system. |Depends on the given reason. |
| Compaction |TarMK GC #2: compaction paused |As long as the compaction phase is paused by configuration, neither the estimation phase nor the compaction phase will be executed. |Enable online revision cleanup. |
|   |TarMK GC #2: compaction cancelled: ${REASON}. |The compaction phase terminated prematurely. Some examples of events that could interrupt the compaction phase: not enough memory or disk space on the host system. Moreover, compaction can also be cancelled by shutting down the system or by explicitly cancelling it via administrative interfaces such as the Maintenance Window within the Operations Dashobard. |Depends on the given reason. |
|   |TarMK GC #2: compaction failed in 32.902 min (1974140 ms), after 5 cycles |This message does not mean that there was an unrecoverable error, but only that compaction was terminated after a certain amount of attempts. Also, read the [following paragraph](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes). |Read the following [Oak documentation](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes), and the last question of the [Running Online Revision Cleanup](/help/sites-deploying/revision-cleanup.md#running-online-revision-cleanup) section. |
| Cleanup |TarMK GC #2: cleanup interrupted |Cleanup has been cancelled by shutting down the repository. No impact on consistency is expected. Also, disk space is most likely not reclaimed to full extent. It will be reclaimed during next revision cleanup cycle. |Investigate why repository has been shut down and going forward try to avoid shutting down the repository during maintenance windows. |-->

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>フェーズ</th>
    <th>ログメッセージ</th>
    <th>説明</th>
    <th>次のステップ</th>
  </tr>  
  <tr>
    <td>見積もり</td>
    <td>TarMK GC #2：コンパクションが一時停止されたので、見積もりはスキップされました。</td>
    <td>設定によってシステムでコンパクションが無効になっている場合は、見積もりフェーズがスキップされます。</td>
    <td>オンラインでのリビジョンクリーンアップの有効化。</td>
  </td>
  </tr>
  <tr>
    <td>該当なし</td>
    <td>TarMK GC #2：見積もりが中断されました：${REASON}。Skipping compaction.</td>
    <td>見積もりフェーズが完了せずに終了しました。見積もりフェーズを中断させる可能性があるイベントの例としては、ホストシステムでのメモリ不足やディスク領域の不足があります。</td>
    <td>示されている理由によって異なります。</td>
  </td>
  </tr>
  <tr>
    <td>コンパクション</td>
    <td>TarMK GC #2：コンパクションは一時停止されました。</td>
    <td>設定によってコンパクションフェーズが一時停止している限り、見積もりフェーズもコンパクションフェーズも実行されません。</td>
    <td>オンラインでのリビジョンクリーンアップの有効化。</td>
  </td>
  </tr>
   <tr>
    <td>該当なし</td>
    <td>TarMK GC #2：コンパクションがキャンセルされました：${REASON}。</td>
    <td>コンパクションフェーズが完了せずに終了しました。コンパクションフェーズを中断させる可能性があるイベントの例としては、ホストシステムでのメモリ不足やディスク領域の不足があります。さらに、システムをシャットダウンするか、操作ダッシュボード内のメンテナンスウィンドウなどの管理インターフェイスを使用して明示的にキャンセルした場合も、コンパクションがキャンセルされることがあります。</td>
    <td>示されている理由によって異なります。</td>
  </td>
  </tr>
  <tr>
    <td>該当なし</td>
    <td>TarMK GC #2：5 回のサイクル後、32.902 分（1974140 ms）でコンパクションに失敗しました。</td>
    <td>このメッセージは、復旧不可能なエラーがあったことを意味するものではなく、何度か試行された後にコンパクションが終了されたことを意味します。また、<a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes">次の段落</a>も参照してください。</td>
    <td>以下の <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes">Oak ドキュメント</a> およびオンラインでのリビジョンクリーンアップの実行の節の最後の質問を参照してください。</a></td>
  </td>
  </tr>
  <tr>
    <td>クリーンアップ</td>
    <td>TarMK GC #2：クリーンアップが中断されました。</td>
    <td>リポジトリのシャットダウンによって、クリーンアップがキャンセルされました。整合性への影響はありません。また、多くの場合、ディスク容量は完全には再利用されません。残りの領域は、次のリビジョンクリーンアップサイクルで再利用されます。</td>
    <td>リポジトリがシャットダウンされた理由を調査し、今後はメンテナンスウィンドウ中にリポジトリがシャットダウンされないようにします。</td>
  </td>
  </tr>
  </tbody>
</table>

## オフラインでのリビジョンクリーンアップの実行方法 {#how-to-run-offline-revision-cleanup}

>[!CAUTION]
>
>AEM インストールの Oak コアバージョンと一致するバージョン番号（メジャーとマイナーの両方）を持つ Oak-run ツールリリースを使用します。例えば、AEM インスタンスに Oak コアバージョン 1.22.x がある場合、Oak-run ツール 1.22.x の最新バージョンを使用する必要があります。

Adobe は、リビジョンクリーンアップを実行するための **Oak-run** というツールを提供しています。このツールは以下のページでダウンロードできます。

[https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/)

このツールは、手動で実行してリポジトリをコンパクションできる実行可能な jar です。このプロセスは、ツールを正しく実行するためにリポジトリをシャットダウンする必要があるので、オフラインでのリビジョンクリーンアップと呼ばれます。メンテナンスウィンドウに従って、クリーンアップを計画してください。

クリーンアッププロセスのパフォーマンスを高める方法のヒントについては、[オフラインでのリビジョンクリーンアップのパフォーマンスの向上](/help/sites-deploying/revision-cleanup.md#increasing-the-performance-of-offline-revision-cleanup)を参照してください。

>[!NOTE]
>
>メンテナンスを行う前に、古いチェックポイントを消去することもできます（以下の手順 2 と 3）。これは、100 を超えるチェックポイントを持つインスタンスに対してのみお勧めします。

1. 常に AEM インスタンスの最新のバックアップがあることを確認してください。

   AEM をシャットダウンします。

1. （オプション）ツールを使用して古いチェックポイントを検索します。

   ```xml
   java -jar oak-run.jar checkpoints install-folder/crx-quickstart/repository/segmentstore
   ```

1. （オプション）次に、未参照のチェックポイントを削除します。

   ```xml
   java -jar oak-run.jar checkpoints install-folder/crx-quickstart/repository/segmentstore rm-unreferenced
   ```

1. コンパクションを実行し、完了するまで待ちます。

   ```xml
   java -jar -Dsun.arch.data.model=32 oak-run.jar compact install-folder/crx-quickstart/repository/segmentstore
   ```

### オフラインでのリビジョンクリーンアップのパフォーマンスの向上 {#increasing-the-performance-of-offline-revision-cleanup}

Oak-run ツールには、リビジョンクリーンアッププロセスのパフォーマンスを向上させ、メンテナンスウィンドウをできる限り最小限に抑えるための機能がいくつか導入されています。

このリストには、以下に示すいくつかのコマンドラインパラメーターが含まれています。

* **-mmap。**&#x200B;これは true または false に設定します。true に設定した場合は、メモリマップアクセスが使用されます。false に設定した場合は、ファイルアクセスが使用されます。指定されていない場合は、64 ビットシステムではメモリマップアクセスが使用され、32 ビットシステムではファイルアクセスが使用されます。Windows では通常のファイルアクセスが常に適用され、このオプションは無視されます。**このパラメーターは、-Dtar.memoryMapped パラメーターを置き換えたものです。**

* **-Dupdate.limit**。ディスクへの一時的なトランザクションのフラッシュのしきい値を定義します。デフォルト値は 10000 です。

* **-Dcompress-interval**。現在のマップを圧縮するまで保持する、コンパクションマップのエントリ数です。デフォルトは 1000000 です。十分なヒープメモリが使用可能な場合、スループットを高めるためにはこの値をさらに大きくする必要があります。**このパラメーターは Oak バージョン 1.6 で削除されており、効果はありません。**

* **-Dcompaction-progress-log**。ログに記録されるコンパクションされたノードの数です。デフォルト値は 150000 です。これは、最初の 150000 個のコンパクションされたノードが操作中にログに記録されることを意味します。これは、以下で説明する次のパラメーターと組み合わせて使用します。

* **-Dtar.PersistCompactionMap。** コンパクションマップを保持するためにヒープメモリの代わりにディスク領域を使用するには、このパラメーターを true に設定します。oak-run ツールの&#x200B;**バージョン 1.4** 以上が必要です。詳しくは、[オフラインでのリビジョンクリーンアップに関するよくある質問](/help/sites-deploying/revision-cleanup.md#offline-revision-cleanup-frequently-asked-questions)の節の質問 3 を参照してください。**このパラメーターは Oak バージョン 1.6 で削除されており、効果はありません。**

* **--force.** コンパクションを強制的に実行し、一致しないセグメントストアバージョンは無視されます。

>[!CAUTION]
>
>`--force` パラメーターを使用すると、セグメントストアが、古い Oak バージョンとは互換性のない最新バージョンにアップグレードされます。また、ダウングレードが不可能であることも考慮します。通常、これらのパラメーターは、使い方に関する知識がある場合にのみ慎重に使用してください。

使用中のパラメーターの例を次に示します。

```xml
java -Dupdate.limit=10000 -Dcompaction-progress-log=150000 -Dlogback.configurationFile=logback.xml -Xmx8g -jar oak-run-*.jar checkpoints <repository>
```

### リビジョンクリーンアップをトリガーするその他の方法 {#additional-methods-of-triggering-revision-cleanup}

上記の方法に加えて、次のように JMX コンソールを使用して、リビジョンのクリーンアップメカニズムをトリガーすることもできます。

1. [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx) にアクセスして JMX コンソールを開きます。
1. **RevisionGarbageCollection** MBean をクリックします。
1. 次のウィンドウで、**startRevisionGC()** をクリックし、**起動**&#x200B;して、リビジョンのガベージコレクションジョブを開始します。

### オフラインでのリビジョンクリーンアップに関するよくある質問 {#offline-revision-cleanup-frequently-asked-questions}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>オフラインでのリビジョンクリーンアップの時間に作用する要因は何ですか。</strong></td>
   <td><p>クリーンアップの実行時間は、リポジトリサイズとクリーンアップする必要があるリビジョンの数によって決まります。</p> </td>
  </tr>
  <tr>
   <td><strong>リビジョンとページバージョンの違いは何ですか。</strong></td>
   <td>
    <ul>
     <li><strong>Oak リビジョン：</strong> Oak では、ノードとプロパティで構成される大規模なツリー階層ですべてのコンテンツを整理しています。このコンテンツツリーの各スナップショットまたはリビジョンは不変であり、ツリーの変更は新しいリビジョンのシーケンスとして表されます。通常、コンテンツを変更するたびに新しいリビジョンがトリガーされます。<a href="https://jackrabbit.apache.org/dev/ngp.html" target="_blank">リンクをフォロー</a> も参照してください。</li>
     <li><strong>ページバージョン：</strong>バージョン管理では、特定の時点でのページの「スナップショット」が作成されます。通常は、ページがアクティベートされたときに新しいバージョンが作成されます。詳細情報に関しては、<a href="/help/sites-authoring/working-with-page-versions.md" target="_blank">ページバージョンの処理</a> を参照してください。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>オフラインでのリビジョンクリーンアップのタスクが 8 時間以内に完了しない場合に、このタスクを高速化するにはどうすればよいですか。</strong></td>
   <td>リビジョンタスクが 8 時間以内に完了せず、<a href="/help/sites-administering/operations-dashboard.md#diagnosis-tools" target="_blank">スレッドダンプ</a>で主なホットスポットが<code>InMemoryCompactionMap.findEntry</code>であると示されている場合は、oak-run ツール<strong>バージョン 1.4</strong>またはそれ以上で以下のパラメーターを使用します：<code>-Dtar.PersistCompactionMap=true</code>。<code>-Dtar.PersistCompactionMap</code> パラメーターは Oak バージョン 1.6 で削除されました。</td>
  </tr>
 </tbody>
</table>
