---
title: リビジョンクリーンアップ
seo-title: Revision Cleanup
description: AEM 6.5 でのリビジョンクリーンアップ機能の使用方法を説明します。
seo-description: Learn how to use the Revision Cleanup functionality in AEM 6.5.
uuid: 321f5038-44b0-4f1e-a1aa-2d29074eed70
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: f03ebe60-88c0-4fc0-969f-949490a8e768
feature: Configuring
exl-id: e53c4c81-f62e-4b6d-929a-6649c8ced23c
source-git-commit: b7f9b5256e07d4bfbc0c3454e8d2fe112ea650e8
workflow-type: tm+mt
source-wordcount: '5918'
ht-degree: 96%

---

# リビジョンクリーンアップ{#revision-cleanup}

## はじめに {#introduction}

リポジトリが更新されるたびに、新しいコンテンツのリビジョンが作成されます。その結果、更新のたびにリポジトリのサイズが大きくなります。リポジトリのサイズが無制限に増大しないように、古いリビジョンをクリーンアップして、ディスクリソースを解放する必要があります。このメンテナンス機能は、リビジョンクリーンアップと呼ばれます。AEM 6.0 以降では、この機能をオフラインルーチンとして使用できます。

AEM 6.3 以降では、この機能のオンラインバージョンとして、オンラインでのリビジョンクリーンアップが導入されました。 AEM インスタンスをシャットダウンする必要があったオフラインのリビジョンクリーンアップとは異なり、オンラインでのリビジョンクリーンアップは AEM インスタンスがオンラインの状態で実行できます。オンラインでのリビジョンクリーンアップはデフォルトで有効になります。リビジョンクリーンアップを実行する際はこの方法を使用することが推奨されます。

**メモ**：オンラインでのリビジョンクリーンアップの概要および使用方法について詳しくは、[ビデオを参照してください](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/administration/use-online-revision-clean-up.html?lang=ja)。

リビジョンクリーンアップのプロセスは、**見積もり**、**コンパクション**&#x200B;および&#x200B;**クリーンアップ**&#x200B;の 3 つのフェーズで構成されます。見積もりでは、収集される可能性があるガベージの量に基づいて、次のフェーズ（コンパクション）を実行するかどうかが判別されます。コンパクションフェーズでは、セグメントおよび tar ファイルが未使用のコンテンツを除いて再作成されます。次のクリーンアップフェーズでは、含まれているガベージを含め、古いセグメントが削除されます。通常、オフラインモードのほうが多くの領域を再利用できます。これは、オンラインモードでは AEM の作業セットを保持する必要があり、収集されないセグメントがあるためです。

リビジョンクリーンアップについて詳しくは、以下のリンクを参照してください。

* [オンラインでのリビジョンクリーンアップの実行方法](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup)
* [オンラインでのリビジョンクリーンアップに関するよくある質問](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions)
* [オフラインでのリビジョンクリーンアップの実行方法](/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup)

また、[Oak の公式ドキュメント](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html) も参考になります。

### どのような場合に、オフラインでのリビジョンクリーンアップではなく、オンラインでのリビジョンクリーンアップを使用するか {#when-to-use-online-revision-cleanup-as-opposed-to-offline-revision-cleanup}

**推奨されているリビジョンクリーンアップの実行方法は、オンラインでのリビジョンクリーンアップです。** オフラインでのリビジョンクリーンアップは、例外的な場合にのみ使用してください。例えば、新しいストレージ形式に移行する前や、アドビカスタマーケアから依頼された場合です。

## オンラインでのリビジョンクリーンアップの実行方法 {#how-to-run-online-revision-cleanup}

オンラインでのリビジョンクリーンアップは、デフォルトで、AEM のオーサーインスタンスとパブリッシュインスタンスの両方で、自動的に 1 日に 1 回実行されるように設定されています。必要な作業は、ユーザーアクティビティが最も少ない時間帯にメンテナンスウィンドウを定義することのみです。オンラインでのリビジョンクリーンアップのタスクを設定するには、以下のようにします。

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

### オフラインでのリビジョンクリーンアップの実行後にオンラインでのリビジョンクリーンアップを実行した場合 {#running-online-revision-cleanup-after-offline-revision-cleanup}

リビジョンクリーンアップのプロセスでは、古いリビジョンを世代ごとに再利用します。つまり、リビジョンクリーンアップを実行するたびに新しい世代を作成し、ディスク上に保持します。ただし、リビジョンクリーンアップにはオフラインとオンラインの 2 種類があり、オフラインでのリビジョンクリーンアップは 1 つの世代を保持し、オンラインでのリビジョンクリーンアップは 2 つの世代を保持するという違いがあります。そのため、オフラインでのリビジョンクリーンアップを実行した&#x200B;**後** にオンラインでのリビジョンクリーンアップを実行した場合は、以下のようになります。

1. オンラインでのリビジョンクリーンアップを初めて実行した後は、リポジトリのサイズが 2 倍になります。これは、ディスク上に 2 つの世代が保持されるからです。
1. その後の実行では、新しい世代が作成されるときに一時的にリポジトリのサイズが大きくなりますが、オンラインでのリビジョンクリーンアッププロセスにより以前の世代が再利用されるので、初めて実行した後のサイズで落ち着きます。

また、コミットの種類と回数に応じて、各世代のサイズが以前の世代とは変わってくる場合があります。したがって、最終的なサイズは実行ごとに変動する可能性があります。

この点を考慮し、最初に予測したリポジトリサイズよりも少なくとも 2 倍または 3 倍大きなディスクサイズにすることをお勧めします。

## フルコンパクションモードとテールコンパクションモード  {#full-and-tail-compaction-modes}

**AEM 6.5** では、オンラインでのリビジョンクリーンアッププロセスの&#x200B;**コンパクション**&#x200B;フェーズ用に **2 つの新しいモード**&#x200B;が導入されています。

* **フルコンパクション**&#x200B;モードでは、リポジトリ全体のすべてのセグメントと tar ファイルが書き換えられます。したがって、後続のクリーンアップフェーズでは、リポジトリ全体の最大量のガベージを削除できます。フルコンパクションはリポジトリ全体に影響を与えるので、完了するにはかなりの量のシステムリソースと時間が必要です。フルコンパクションは、AEM 6.3 のコンパクションフェーズに対応しています。
* **テールコンパクション**&#x200B;モードでは、リポジトリの最新のセグメントと tar ファイルのみが書き換えられます。最新のセグメントと tar ファイルとは、フルコンパクションまたはテールコンパクションの前回の実行以降に追加されたセグメントと tar ファイルのことです。したがって、後続のクリーンアップフェーズでは、リポジトリの新しい部分に含まれるガベージのみを削除できます。テールコンパクションはリポジトリの一部にのみ影響するので、完了するために必要なシステムリソースと時間がフルコンパクションよりも大幅に少なくなります。

この 2 つのコンパクションモードでは、効果とリソース消費がトレードオフの関係にあります。テールコンパクションは効果は低くなりますが、システムの通常運用に与える影響も少なくなります。これに対し、フルコンパクションは効果は高くなりますが、システムの通常運用に大きな影響を与えます。

また、AEM 6.5 では、コンパクション時のより効率的なコンテンツの重複除外メカニズムが導入されました。これにより、リポジトリのディスク上のフットプリントがさらに削減されます。

次の 2 つの図は、AEM 6.3 と比較した AEM 6.5 の平均実行時間とディスク上の平均フットプリントの減少を示す社内ラボでのテスト結果を示しています。

![onrc-duration-6_4vs63](assets/onrc-duration-6_4vs63.png) ![segmentstore-6_4vs63](assets/segmentstore-6_4vs63.png)

### フルコンパクションとテールコンパクションの設定方法 {#how-to-configure-full-and-tail-compaction}

デフォルト設定では、テールコンパクションを平日に、フルコンパクションを日曜日に実行します。デフォルト設定は、`RevisionCleanupTask` [ メンテナンスタスク](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup) の新しい設定値 `full.gc.days` を使用することで変更できます。

`full.gc.days` 値を設定する場合、フルコンパクションは値で定義された日に実行され、テールコンパクションは値で定義されていない日に実行されることにご注意ください。例えば、フルコンパクションを日曜日に実行するように設定すると、テールコンパクションは月曜日から土曜日に実行されます。例えば、フルコンパクションを毎日実行するように設定すると、テールコンパクションはまったく実行されません。

また、次のことを考慮に入れてください。

* **テールコンパクション**&#x200B;は、効果が低く、システムの通常運用に対する影響が少なくなります。そのため、テールコンパクションは営業日に実行することを意図しています。
* **フルコンパクション**&#x200B;は、効果は高くなりますが、システムの通常運用に大きな影響を与えます。そのため、原則的には休業日に実行します。
* テールコンパクションとフルコンパクションは両方とも、オフピークの時間帯に実行するように計画することをお勧めします。

### トラブルシューティング {#troubleshooting}

新しいコンパクションモードを使用する場合、次の点に注意してください。

* 入出力（I/O）アクティビティ（例：I/O 操作、I/O を待機する CPU、コミットキューサイズ）を監視できます。これは、システムが I/O バウンドになりつつあり、アップサイジングが必要かどうかを特定するのに役立ちます。
* `RevisionCleanupTaskHealthCheck` は、オンラインでのリビジョンクリーンアップの全体的なヘルスステータスを示します。AEM 6.3 と同じように機能し、フルコンパクションとテールコンパクションを区別しません。
* ログメッセージは、コンパクションモードについての関連情報を伝えます。例えば、オンラインでのリビジョンクリーンアップを開始する際に、対応するログメッセージはコンパクションモードを示します。また、まれに、テールコンパクションを実行するようスケジュールされていたがシステムがフルコンパクションに戻った場合は、ログメッセージにこの変更が示されます。次のログサンプルは、コンパクションモード、およびテールコンパクションからフルコンパクションへの変更を示しています。

```
TarMK GC: running tail compaction
TarMK GC: no base state available, running full compaction instead
```

### 既知の制限事項 {#known-limitations}

場合によっては、テールとフルのコンパクションモードの変更によりクリーンアッププロセスが遅延します。正確には、フルコンパクションの後にリポジトリが大きくなります（倍のサイズになります）。リポジトリがフルコンパクション前のサイズ以下になると、余分のスペースが後続のテールコンパクションで再利用されます。メンテナンスタスクの並列実行も回避する必要があります。

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
   <td><p>TarMK の永続性形式が AEM 6.5 で変更されます。これらの変更には、事前の移行手順は必要ありません。既存のリポジトリは、周期的な移行を実行します。これはユーザーに対して透過的です。AEM 6.5（または関連ツール）がリポジトリに初めてアクセスすると、移行プロセスが開始されます。</p> <p><strong>AEM 6.5 永続性形式への移行が開始されると、リポジトリを以前の AEM 6.3 永続性形式に戻すことはできなくなります。</strong></p> </td>
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
   <td><p>AEM 6.3 で、特にオンラインでのリビジョンクリーンアップのパフォーマンスと効果を高めるために、ストレージ形式の変更が必要となりました。この変更には後方互換性がないので、古い Oak セグメント（AEM 6.2 以前）で作成されたリポジトリを移行する必要があります。</p> <p>ストレージ形式の変更には、他にも次のような利点があります。</p>
    <ul>
     <li>スケーラビリティの向上（セグメントサイズの最適化）</li>
     <li><a href="/help/sites-administering/data-store-garbage-collection.md" target="_blank">データストアのガベージコレクション</a>の高速化<br /> </li>
     <li>将来の機能拡張に備えた基盤整備</li>
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
   <td>はい。新しいインスタンスを使用する場合を除き、常にコンテンツを移行する必要があります。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>6.3 以降にアップグレードし、後で移行を行うことはできますか（別のメンテナンスウィンドウを使用するなど）。</strong></td>
   <td>できません。前述のとおり、コンテンツの移行は必須です。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>移行時のダウンタイムは回避できますか。</strong></td>
   <td>いいえ。これは一度におこなう作業であり、実行中のインスタンスでは実行できません。</td>
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
   <td>移行とは、セグメントストアを新しい形式で作成し直すことと同義です。これを利用して、移行中に必要な追加のディスク領域を推定できます。移行後は、領域を再利用するために古いセグメントストアを削除できます。</td>
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
   <td>1 日に 1 回です。これが操作ダッシュボードでのデフォルト設定です。</td>
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
   <td>オンラインでのリビジョンクリーンアップでは、古いリビジョンを世代ごとに再利用します。リビジョンクリーンアップが実行されるたびに、新しい世代が生成されます。2 世代以上前のコンテンツのみが再利用されるので、初回実行時には再利用するコンテンツがありません。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>オフラインでのリビジョンクリーンアップの実行後に初めてオンラインでのリビジョンクリーンアップを実行したときに、領域が再利用されないのはなぜですか。</strong></td>
   <td><p>オフラインでのリビジョンクリーンアップでは最新の世代だけを残して他をすべて再利用しますが、オンラインでのリビジョンクリーンアップでは最新の 2 つの世代を残します。新しいリポジトリの場合、オフラインでのリビジョンクリーンアップの実行後に初めてオンラインでのリビジョンクリーンアップが実行されるときには、再利用できる古い世代が存在しないので、領域は再利用されません。</p> <p><a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">この章</a>の「オフラインでのリビジョンクリーンアップの実行後にオンラインでのリビジョンクリーンアップを実行した場合」の節も参照してください。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>オンラインでのリビジョンクリーンアップは、通常、オーサーとパブリッシュでは異なる時間帯に実行しますか。</strong></td>
   <td>いつ実行すべきかは、営業時間と顧客のオンラインプレゼンスのトラフィックパターンによって異なります。クリーンアップの効果を最大限に高めるには、メンテナンスウィンドウを主要な実稼動時間外に設定する必要があります。AEM パブリッシュインスタンス（TarMK ファーム）が複数ある場合は、オンラインでのリビジョンクリーンアップのメンテナンスウィンドウが重ならないように調整する必要があります。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>オンラインでのリビジョンクリーンアップを実行するための前提条件はありますか。</strong></td>
   <td><p>オンラインでのリビジョンクリーンアップは、AEM 6.3 以降のリリースでのみ使用できます。 また、古いバージョンの AEM を使用している場合は、新しい <a href="/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar">Oak Segment Tar</a> に移行する必要があります。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>オンラインでのリビジョンクリーンアップの時間に作用する要因は何ですか。</strong></td>
   <td>次の要因があります。<br />
    <ul>
     <li>リポジトリのサイズ</li>
     <li>システムの負荷（要求数/分、特に書き込み操作）</li>
     <li>アクティビティのパターン（読み取りと書き込み）</li>
     <li>ハードウェアの仕様（CPU の性能、メモリ、IOPS）</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>オンラインでのリビジョンクリーンアップの実行中も作成者は作業できますか。</strong></td>
   <td>できます。オンラインでのリビジョンクリーンアップは、同時書き込みに対応しています。ただし、同時書き込みトランザクションがおこなわれていないほうが、オンラインでのリビジョンクリーンアップの動作は高速かつ効率的になります。オンラインでのリビジョンクリーンアップのメンテナンスタスクは、大量のトラフィックがない、比較的処理が少ない時間帯にスケジュールすることをお勧めします。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>オンラインでのリビジョンクリーンアップを実行するときのディスク領域とヒープメモリの最小要件を教えてください。</strong></td>
   <td><p>オンラインでのリビジョンクリーンアップ中、ディスク領域は継続的に監視されます。使用可能なディスク領域が臨界値を下回ると、プロセスがキャンセルされます。臨界値はリポジトリの現在のディスクフットプリントの 25 ％で、設定はできません。</p> <p><strong>最初に予測したリポジトリサイズよりも少なくとも 2 倍または 3 倍大きなディスクサイズにすることをお勧めします。</strong></p> <p>クリーンアッププロセス中、空きヒープ領域が継続的に監視されます。空きヒープ領域が臨界値を下回ると、プロセスがキャンセルされます。臨界値は、org.apache.jackrabbit.oak.segment.SegmentNodeStoreService#MEMORY_THRESHOLD を使用して設定します。デフォルト値は 15％です。</p> <p>推奨されるコンパクションヒープの最小サイズは、AEM のメモリサイズの推奨値と関係があります。原則として、<strong>AEM インスタンスのサイズが使用例およびそこで予想されるペイロードに対処するために十分なサイズであれば、クリーンアッププロセスで十分なメモリが確保されます。</strong></p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>オンラインでのリビジョンクリーンアップの実行中、パフォーマンスにはどのような影響があると予想されますか。</strong></td>
   <td>オンラインでのリビジョンクリーンアップでは、通常のシステム操作と並行して、リポジトリからの読み取りおよびリポジトリへの書き込みをバックグラウンドプロセスとして実行します。状況によっては、リポジトリに対する短時間の排他的アクセスが必要になり、他のスレッドがリポジトリに書き込めなくなる場合があります。</td>
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
   <td>他のメンテナンスタスクがリビジョンクリーンアップの実行を遅延させていないかを確認してください。これは、同じメンテナンスウィンドウ内で、オンラインでのリビジョンクリーンアップ以外のメンテナンスタスクも実行されている場合に発生することがあります。メンテナンスタスクは順番に実行されますが、順序は設定できないことに注意してください。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>リビジョンのガベージコレクションがスキップされるのはなぜですか。</strong></td>
   <td><p>リビジョンクリーンアップでは、まず見積もりフェーズによって、クリーンアップが必要なガベージが累積しているかどうかが判断されます。見積もりでは、最後のコンパクション後のリポジトリサイズと現在のサイズを比較します。このサイズが設定されている差分を超えている場合、クリーンアップが実行されます。サイズの差分は 1 GB に設定されています。これは、リポジトリーのサイズが前回のクリーンアップの実行から 1 GB 増加しなかった場合、新しいリビジョンのクリーンアップの反復がスキップされることを事実上意味します。 </p> <p>見積もりフェーズに関連するログエントリは以下のとおりです。</p>
    <ul>
     <li>リビジョンの GC が実行される：<em>サイズ差分は N% または N/N（N/N バイト）であるため、コンパクションを実行</em></li>
     <li>リビジョンの GC が実行 <strong>されない</strong>：<em>サイズ差分は N% または N/N（N/N バイト）であるため、とりあえずコンパクションをスキップ</em></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>パフォーマンスへの影響が大きすぎる場合に、自動コンパクションを安全に中止できますか。</strong></td>
   <td>はい。AEM 6.3 以降では、操作ダッシュボード内のメンテナンスタスクウィンドウまたは JMX を使用して、安全に停止できます。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>スケジュールされたクリーンアップタスクの実行中に AEM インスタンスがシャットダウンされた場合、プロセスは安全に中止されますか。またはコンパクションが終了するまでシャットダウンがブロックされますか。</strong></td>
   <td>リビジョンクリーンアップが中断され、リポジトリは安全にシャットダウンされます。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>オンラインでのリビジョンクリーンアップ中にシステムがクラッシュした場合はどうなりますか。</strong></td>
   <td>そのような場合も、データが破損するリスクはありません。ガベージの残りは後続の実行でクリーンアップされます。</td>
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
   <td><p>同時書き込みが可能なシステムでは、コンパクションサイクルの終了時に変更をコミットできるように、オンラインでのリビジョンクリーンアップで排他書き込みアクセスが必要になる場合があります。システムは <strong>forceCompact モード</strong>になります。詳細に関しては、<a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html" target="_blank">oak のドキュメント</a>を参照してください。強制コンパクション中は、同時書き込みによる干渉を受けることなく最終的に変更をコミットするために、排他書き込みロックが取得されます。応答時間に対する影響を制限するために、タイムアウト値を定義できます。デフォルトでは、この値は 1 分に設定されています。これは、1 分以内に強制コンパクションが完了しない場合、同時コミットが優先されてコンパクションプロセスが中止されることを意味します。</p> <p>強制コンパクションの実行時間は以下の要素によって変動します。</p>
    <ul>
     <li>ハードウェア（具体的には IOPS）：IOPS が増えると実行時間が短縮されます。</li>
     <li>セグメントストアサイズ：実行時間はセグメントストアのサイズに伴って増大します。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>スタンバイインスタンスでは、オンラインでのリビジョンクリーンアップはどのように実行されますか。</strong></p> </td>
   <td><p>コールドスタンバイセットアップでは、オンラインでのリビジョンクリーンアップの実行を設定する必要があるのは、プライマリインスタンスのみです。スタンバイインスタンスで、オンラインでのリビジョンクリーンアップを明示的にスケジュールする必要はありません。</p> <p>スタンバイインスタンスでの対応する操作は自動クリーンアップです。これは、オンラインでのリビジョンクリーンアップのクリーンアップフェーズに相当します。プライマリインスタンスでオンラインでのリビジョンクリーンアップが実行された後に、スタンバイインスタンスで自動クリーンアップが実行されます。</p> <p>見積もりフェーズとコンパクションフェーズはスタンバイインスタンスでは実行されません。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>オフラインでのリビジョンクリーンアップでは、オンラインでのリビジョンクリーンアップよりも多くのディスク領域を解放できますか。</strong></td>
   <td><p>オフラインでのリビジョンクリーンアップでは古いリビジョンをすぐに削除できますが、オンラインでのリビジョンクリーンアップでは、古いリビジョンが引き続きアプリケーションスタックによって参照されていることを考慮する必要があります。そのため、オフラインのほうがオンラインよりも積極的にガベージを削除できますが、ガベージコレクションサイクルを数回経ると、この効果は薄れます。</p> <p><a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">この章</a>の「オフラインでのリビジョンクリーンアップの実行後にオンラインでのリビジョンクリーンアップを実行した場合」の節も参照してください。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>メモリマップファイル操作に関する考慮事項はありますか。</td>
   <td>
    <ul>
     <li><strong>Windows 環境</strong>では、通常のファイルアクセスが常に強制的に利用されるので、メモリマップアクセスは使用されません。一般的に、利用可能なすべての RAM をヒープに割り当て、segmentCache サイズを大きくする必要があります。segmentCache のサイズは、org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config に segmentCache.size オプションを追加して大きくします（例：segmentCache.size=20480）。オペレーティングシステムや他のプロセス用に、一定の RAM を残しておいてください。</li>
     <li><strong>Windows 以外の環境</strong>では、物理メモリのサイズを大きくすることで、リポジトリのメモリマップの効率性を向上できます。</li>
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
     <li>オンラインでのリビジョンクリーンアップが有効な場合は、ディスクスペースを監視する必要があります。ディスク領域が不十分な場合、クリーンアップは実行されないか、早期に終了します。</li>
     <li>オンラインでのリビジョンクリーンアップの完了時間をログで確認してください。これは 2 時間以下である必要があります。</li>
     <li>チェックポイントの数。コンパクションの実行時にチェックポイントが 4 つ以上ある場合は、チェックポイントをクリーンアップすることをお勧めします。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>オンラインでのリビジョンクリーンアップが正常に完了したかどうかを確認する方法を教えてください。</strong></td>
   <td><p>オンラインでのリビジョンクリーンアップが正常に完了したかどうかは、ログを確認して確認できます。</p> <p>例：「<code>TarMK GC #{}: compaction completed in {} ({} ms), after {} cycles</code> 」は、メッセージ「<code>TarMK GC #{}: compaction gave up compacting concurrent commits after {} cycles</code>」（同時負荷が大きすぎることを意味する）が先行しない限り、コンパクションステップが正常に完了したことを意味します。</p> <p>それに伴い、クリーンアップステップの正常終了を示すメッセージ「<code>TarMK GC #{}: cleanup completed in {} ({} ms</code>」が表示されます。</p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><strong>最新のオンラインでのリビジョンクリーンアップの実行に関する統計はどこで確認できますか。</strong></td>
   <td><p>ステータス、進行状況および統計は、JMX（<code>SegmentRevisionGarbageCollection</code> MBean）経由で表示されます。<code>SegmentRevisionGarbageCollection</code> MBean の詳細に関しては、<a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">次の段落</a> を参照してください。</p> <p>進行状況は、 <code>EstimatedRevisionGCCompletion</code> のフィールド名で追跡できます。 <code>SegmentRevisionGarbageCollection MBean.</code></p> <p>MBean の参照を取得するには、 <code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection"</code> を使用します。</p> <p>確認できるのは、システムを最後に起動した以降の統計情報のみであることにご注意ください。外部の監視ツールを利用すると、AEM の稼動時間外もデータを監視できます。詳細に関しては、 <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios" target="_blank">外部の監視ツールの例として、Nagios にヘルスチェックを接続するための AEM のドキュメント</a>を参照してください。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>関連するログエントリは何ですか？</strong></td>
   <td>
    <ul>
     <li>オンラインでのリビジョンクリーンアップが開始/停止しました
      <ul>
       <li>オンラインでのリビジョンクリーンアップは、見積もり、コンパクション、クリーンアップの 3 つのフェーズで構成されます。リポジトリに十分な量のガベージが含まれていない場合は、見積もりによってコンパクションとクリーンアップがスキップされることがあります。最新バージョンのAEMでは、「<code>TarMK GC #{}: estimation started</code>「見積もりの開始を示す」<code>TarMK GC #{}: compaction started, strategy={}</code>"コンパクションの開始をマークし、"T<code>arMK GC #{}: cleanup started. Current repository size is {} ({} bytes</code>"は、クリーンアップの開始をマークします。</li>
      </ul> </li>
     <li>リビジョンのクリーンアップで取得したディスクスペース
      <ul>
       <li>スペースは、クリーンアップフェーズが完了した場合にのみ再利用されます。クリーンアップフェーズの完了は、ログメッセージ「T<code>arMK GC #{}: cleanup completed in {} ({} ms</code>」で示されます。クリーンアップ後のサイズは {}（{} バイト）で、再利用された領域は {}（{} バイト）です。コンパクションマップの重み/深さは {}/{} （{} バイト/{}）です。"</li>
      </ul> </li>
     <li>リビジョンのクリーンアップ中に問題が発生しました
      <ul>
       <li>多くの障害状態があり、すべての障害は、「TarMK GC」で始まる WARN または ERROR ログメッセージでマークされます。</li>
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
   <td>障害状態は、「TarMK GC」で始まる WARN または ERROR ログメッセージで示されます。 また、<a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">エラーメッセージに基づくトラブルシューティング</a>の節を参照してください。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>リビジョンクリーンアップのヘルスチェックではどのような情報が表示されますか。ステータスレベルの色分けとの対応も教えてください。 </strong></td>
   <td><p>リビジョンのクリーンアップヘルスチェックは、 <a href="/help/sites-administering/operations-dashboard.md#health-reports" target="_blank">操作ダッシュボード</a>の一部です。<br /> </p> <p>オンラインでのリビジョンクリーンアップメンテナンスタスクの最後の実行が正常に完了した場合、ステータスは<strong>緑</strong>になります。</p> <p>オンラインでのリビジョンクリーンアップのメンテナンスタスクが 1 回キャンセルされた場合、ステータスは<strong>イエロー</strong>になります。<br /> </p> <p>オンラインでのリビジョンクリーンアップのメンテナンスタスクを 3 回連続でキャンセルした場合は、<strong>赤</strong>になります。<strong>この場合、手動の操作が必要であるか</strong>、オンラインでのリビジョンクリーンアップが再び失敗する可能性が高くなります。詳細情報に関しては、以下の<a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-online-revision-cleanup">トラブルシューティング</a>の節を参照してください。<br /> </p> <p>システムの再起動後に、ヘルスチェックステータスがリセットされることにもご注意ください。そのため、新たに再起動されたインスタンスでは、リビジョンクリーンアップヘルスチェックで緑色のステータスが示されます。外部の監視ツールを利用すると、AEM の稼動時間外もデータを監視できます。<a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios">外部の監視ツールの例として、Nagios にヘルスチェックを接続するための AEM のドキュメント</a>を参照してください。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>スタンバイインスタンスで自動クリーンアップを監視する方法を教えてください。</strong></p> </td>
   <td><p>ステータス、進行状況および統計は、<code>SegmentRevisionGarbageCollection</code> MBean を使用し、JMX 経由で表示されます。次の <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">Oak ドキュメント</a>も参照してください。 </p> <p>MBean の参照は、<code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection"</code> を使用して取得できます。</p> <p>確認できるのは、システムが最後に起動されて以降の統計情報のみであることにご注意ください。外部の監視ツールを利用すると、AEM の稼動時間外もデータを監視できます。また、 <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios" target="_blank">外部の監視ツールの例として、Nagios にヘルスチェックを接続するための AEM のドキュメント</a>も参照してください。</p> <p>ログファイルを使用して、自動クリーンアップのステータス、進行状況および統計情報を確認することもできます。</p> </td>
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
   <td>問題を検出して修正するには、以下の手順を実行します。<br />
    <ul>
     <li>まず、ログエントリを確認します。<br /> </li>
     <li>ログの情報に基づいて、適切な操作を実行します。
      <ul>
       <li>ログに、5 回の失敗したコンパクションサイクルと<code>forceCompact</code>サイクルでのタイムアウトが示されている場合は、リポジトリへの書き込みが少ない、処理が少ない時間帯にメンテナンスウィンドウをスケジュールします。リポジトリーへの書き込みは、<em>https://serveraddress:serverport/libs/granite/operations/content/monitoring/page.html</em> にあるリポジトリー指標の監視ツールで確認できます。</li>
       <li>メンテナンスウィンドウの終わりにクリーンアップが停止した場合は、メンテナンスタスクのユーザーインターフェイスで、メンテナンスウィンドウの長さの設定が十分であることを確認してください。</li>
       <li>使用可能なヒープメモリが不足している場合は、インスタンスに十分なメモリがあることを確認してください。</li>
       <li>応答が遅い場合は、セグメントストアが大きくなりすぎて、メンテナンスウィンドウを長くしてもオンラインでのリビジョンクリーンアップを完了できない可能性があります。例えば、先週、オンラインでのリビジョンクリーンアップが一度も正常に完了してない場合は、セグメントストアを対処可能なサイズに戻すために、オフラインでのメンテナンスを計画し、オフラインでのリビジョンクリーンアップを実行することをお勧めします。</li>
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
   <td>オンラインでのリビジョンクリーンアップはキャンセルされ、残りの手順は削除されます。メンテナンスウィンドウが次回スケジュールされたときに、クリーンアップが再度開始されます。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong><code>SegmentNotFoundException</code> インスタンスが <code>error.log</code> に記録される理由と復旧方法を教えてください。</strong></td>
   <td><p><code>SegmentNotFoundException</code> は、TarMK がアクセスを試みたストレージユニット（セグメント）が見つからなかったときに、TarMK によってログに記録されます。次の 3 つのシナリオで、この問題が発生する可能性があります。</p>
    <ol>
     <li>アプリケーションが、推奨されるアクセス方法（Sling や JCR API など）を使用せずに、下位レベルの API／SPI を使用してリポジトリにアクセスし、セグメントの保持時間を超えている場合。つまり、アプリケーションがオンラインでのリビジョンクリーンアップで許可される保持時間（デフォルトは 24 時間）よりも長くエンティティへの参照を保持している場合です。この状況は一時的で、データの破損にはつながりません。復旧するには、oak-run ツールを使用して、この例外が一時的なものである（oak-run チェックでエラーが報告されない）ことを確認する必要があります。このためには、インスタンスをオフラインにし、後で再起動する必要があります。</li>
     <li>外部イベントによってディスクのデータが破損している場合。これは、ディスクの障害、ディスク領域の不足または必要なデータファイルが誤って変更されたことが原因である可能性があります。この場合は、インスタンスをオフラインにして、oak-run チェックを使用して修復する必要があります。oak-run チェックの実行方法についての詳細は、以下の <a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">Apache ドキュメント</a> を参照してください。</li>
     <li>他のすべての状況では、<a href="https://helpx.adobe.com/jp/marketing-cloud/contact-support.html" target="_blank">アドビカスタマーケア</a> に連絡して対処する必要があります。</li>
    </ol> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### エラーメッセージに基づくトラブルシューティング {#troubleshooting-based-on-error-messages}

オンラインでのリビジョンクリーンアッププロセス中に問題が発生した場合、詳細な error.log が生成されます。以下のマトリックスでは、最も一般的なメッセージを説明し、解決策を示しています。

<!---| **Phase** |**Log Messages** |**Explanation** |**Next Steps** |
|---|---|---|---|
|   |  |  |  |
| Estimation |TarMK GC #2: estimation skipped because compaction is paused |The estimation phase is skipped when compaction is disabled on the system by configuration. |Enable Online Revision Cleanup. |
|   |TarMK GC #2: estimation interrupted: ${REASON}. Skipping compaction. |The estimation phase terminated prematurely. Some examples of events that could interrupt the estimation phase: not enough memory or disk space on the host system. |Depends on the given reason. |
| Compaction |TarMK GC #2: compaction paused |As long as the compaction phase is paused by configuration, neither the estimation phase nor the compaction phase will be executed. |Enable online revision cleanup. |
|   |TarMK GC #2: compaction cancelled: ${REASON}. |The compaction phase terminated prematurely. Some examples of events that could interrupt the compaction phase: not enough memory or disk space on the host system. Moreover, compaction can also be cancelled by shutting down the system or by explicitly cancelling it via administrative interfaces such as the Maintenance Window within the Operations Dashobard. |Depends on the given reason. |
|   |TarMK GC #2: compaction failed in 32.902 min (1974140 ms), after 5 cycles |This message doesn’t mean that there was an unrecoverable error, but only that compaction was terminated after a certain amount of attempts. Also, read the [following paragraph](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes). |Read the following [Oak documentation](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes), and the last question of the [Running Online Revision Cleanup](/help/sites-deploying/revision-cleanup.md#running-online-revision-cleanup) section. |
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
    <td>TarMK GC #2：圧縮が一時停止されたので、見積もりはスキップされました。</td>
    <td>設定によってシステムでコンパクションが無効になっている場合は、見積もりフェーズがスキップされます。</td>
    <td>オンラインでのリビジョンクリーンアップの有効化.</td>
  </td>
  </tr>
  <tr>
    <td>アプローチ</td>
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
    <td>アプローチ</td>
    <td>TarMK GC #2：コンパクションがキャンセルされました：${REASON}。</td>
    <td>コンパクションフェーズが完了せずに終了しました。コンパクションフェーズを中断させる可能性があるイベントの例としては、ホストシステムでのメモリ不足やディスク領域の不足があります。また、システムをシャットダウンするか、操作ダッシュボード内のメンテナンスウィンドウなどの管理インターフェイスを使用して明示的にキャンセルすることで、コンパクションをキャンセルすることもできます。</td>
    <td>示されている理由によって異なります。</td>
  </td>
  </tr>
  <tr>
    <td>アプローチ</td>
    <td>TarMK GC #2：5 回のサイクル後、32.902 分 (1974140 ms) でコンパクションに失敗しました.</td>
    <td>このメッセージは、復旧不可能なエラーがあったのではなく、一定数の試行の後にコンパクションが終了されたことのみを意味します。また、 <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes">」を参照してください。</a></td>
    <td>以下の <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes">Oak ドキュメント</a> および オンラインでのリビジョンクリーンアップの実行 の節の最後の質問をお読みください。</a></td>
  </td>
  </tr>
  <tr>
    <td>クリーンアップ</td>
    <td>TarMK GC #2：クリーンアップが中断されました。</td>
    <td>リポジトリーをシャットダウンしてクリーンアップがキャンセルされました。整合性への影響はありません。また、ディスク容量が完全に再利用されない可能性が高くなります。 残りの領域は、次のリビジョンクリーンアップサイクルで再利用されます。</td>
    <td>リポジトリがシャットダウンされた理由を調べ、今後はメンテナンスウィンドウ中にリポジトリがシャットダウンされないようにします。</td>
  </td>
  </tr>
  </tbody>
</table>

## オフラインでのリビジョンクリーンアップの実行方法 {#how-to-run-offline-revision-cleanup}

>[!CAUTION]
>
>AEM のインストールで使用する Oak バージョンに応じて、異なるバージョンの Oak-run ツールを使用する必要があります。ツールを使用する前に、以下のバージョン要件を確認してください。
>
>* Oak バージョン **1.0.0 ～ 1.0.11**&#x200B;または&#x200B;**1.1.0 ～ 1.1.6**&#x200B;の場合は、Oak-run バージョン** 1.0.11** を使用します。
>
>* **上述のものよりも新しい** Oak バージョンについては、AEM インストールの Oak コアと一致するバージョンの oak-run を使用します。
>


アドビは、リビジョンクリーンアップを実行するための **Oak-run** というツールを提供しています。このツールは以下のページでダウンロードできます。

[https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/)

このツールは、リポジトリのコンパクションを実行するために手動で実行できる実行可能 jar です。このプロセスはオフラインでのリビジョンクリーンアップと呼ばれます。これは、ツールを適切に実行するためにリポジトリをシャットダウンする必要があるためです。メンテナンスウィンドウに合わせてクリーンアップを計画してください。

クリーンアッププロセスのパフォーマンスを高める方法のヒントについては、[オフラインでのリビジョンクリーンアップのパフォーマンスの向上](/help/sites-deploying/revision-cleanup.md#increasing-the-performance-of-offline-revision-cleanup)を参照してください。

>[!NOTE]
>
>メンテナンスが発生する前に、古いチェックポイントを削除することもできます（後述の手順 2 および 3）。これは、チェックポイントが 100 個を超えるインスタンスにのみ推奨されます。

1. AEM インスタンスの最新バックアップがあることを必ず確認します。

   AEM をシャットダウンします。

1. （オプション）ツールを使用して古いチェックポイントを探します。

   ```xml
   java -jar oak-run.jar checkpoints install-folder/crx-quickstart/repository/segmentstore
   ```

1. （オプション）次に、参照されていないチェックポイントを削除します。

   ```xml
   java -jar oak-run.jar checkpoints install-folder/crx-quickstart/repository/segmentstore rm-unreferenced
   ```

1. コンパクションを実行して完了するまで待ちます。

   ```xml
   java -jar -Dsun.arch.data.model=32 oak-run.jar compact install-folder/crx-quickstart/repository/segmentstore
   ```

### オフラインでのリビジョンクリーンアップのパフォーマンスの向上 {#increasing-the-performance-of-offline-revision-cleanup}

oak-run ツールには、リビジョンクリーンアッププロセスのパフォーマンスを向上させ、メンテナンスウィンドウをできる限り最短化するための複数の機能が導入されています。

このような機能には、以下に示すコマンドラインパラメーターが含まれます。

* **-mmap。**&#x200B;これは true または false に設定します。true に設定すると、メモリマップアクセスが使用されます。false に設定すると、ファイルアクセスが使用されます。指定しない場合、64 ビットシステムではメモリマップアクセスが、32 ビットシステムではファイルアクセスが使用されます。Windows では通常のファイルアクセスが常に強制的に利用されるので、このオプションは無視されます。**このパラメーターは、-Dtar.memoryMapped パラメーターを置き換えたものです。**

* **-Dupdate.limit**。一時トランザクションをディスクにフラッシュするためのしきい値を定義します。デフォルト値は 10000 です。

* **-Dcompress-interval**。現在のマップを圧縮するまで保持するコンパクションマップエントリの数です。デフォルトは 1000000 です。十分なヒープメモリが使用可能な場合は、スループットを高速化するために、この値をさらに大きい数に増やします。**このパラメーターは Oak バージョン 1.6 で削除されており、効果はありません。**

* **-Dcompaction-progress-log**。ログに記録される、コンパクションされたノードの数です。デフォルト値は 150000 です。これは、最初の 150000 個のコンパクションされたノードが操作中にログに記録されることを意味します。このパラメーターは、次に示すパラメーターとともに使用します。

* **-Dtar.PersistCompactionMap。**&#x200B;コンパクションマップを保持するためにヒープメモリの代わりにディスク領域を使用するには、このパラメーターを true に設定します。oak-run ツールの&#x200B;**バージョン 1.4** 以上が必要です。詳しくは、[オフラインでのリビジョンクリーンアップに関するよくある質問](/help/sites-deploying/revision-cleanup.md#offline-revision-cleanup-frequently-asked-questions)の節の質問 3 を参照してください。**このパラメーターは Oak バージョン 1.6 で削除されており、効果はありません。**

* **--force.**&#x200B;コンパクションを強制的に実行し、一致しないセグメントストアバージョンは無視されます。

>[!CAUTION]
>
>`--force` パラメーターを使用すると、セグメントストアが、古い Oak バージョンとは互換性のない最新バージョンにアップグレードされます。また、ダウングレードができなくなる点に注意してください。原則として、これらのパラメーターは、使用方法について確実に把握している場合にのみ慎重に使用してください。

パラメーターの使用例を示します。

```xml
java -Dupdate.limit=10000 -Dcompaction-progress-log=150000 -Dlogback.configurationFile=logback.xml -Xmx8g -jar oak-run-*.jar checkpoints <repository>
```

### リビジョンクリーンアップをトリガーするその他の方法 {#additional-methods-of-triggering-revision-cleanup}

前述の方法に加えて、以下のように JMX コンソールを使用してリビジョンクリーンアップのメカニズムをトリガーすることもできます。

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
     <li><strong>Oak リビジョン：</strong> Oak では、ノードとプロパティで構成される大規模なツリー階層ですべてのコンテンツを整理しています。このコンテンツツリーの各スナップショットまたはリビジョンは不変で、ツリーに対する変更は一連の新しいリビジョンとして表されます。通常は、コンテンツが変更されるたびに新しいリビジョンがトリガーされます。<a href="https://jackrabbit.apache.org/dev/ngp.html" target="_blank">リンクをフォロー</a> も参照してください。</li>
     <li><strong>ページバージョン：</strong>バージョン管理では、特定の時点でのページの「スナップショット」が作成されます。通常は、ページがアクティベートされたときに新しいバージョンが作成されます。詳細情報に関しては、<a href="/help/sites-authoring/working-with-page-versions.md" target="_blank">ページバージョンの処理</a> を参照してください。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>オフラインでのリビジョンクリーンアップのタスクが 8 時間以内に完了しない場合に、このタスクを高速化するにはどうすればよいですか。</strong></td>
   <td>リビジョンタスクが 8 時間以内に完了せず、<a href="/help/sites-administering/operations-dashboard.md#diagnosis-tools" target="_blank">スレッドダンプ</a>で主なホットスポットが<code>InMemoryCompactionMap.findEntry</code>であると示されている場合は、oak-run ツール<strong>バージョン 1.4</strong>またはそれ以上で以下のパラメーターを使用します：<code>-Dtar.PersistCompactionMap=true</code>。<code>-Dtar.PersistCompactionMap</code> パラメーターは Oak バージョン 1.6 で削除されたことにご注意ください。</td>
  </tr>
 </tbody>
</table>
