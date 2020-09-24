---
title: MSM のベストプラクティス
seo-title: MSM のベストプラクティス
description: Adobe のエンジニアリングおよびコンサルティングチームがまとめたベストプラクティスを確認し、AEM マルチサイトマネージャーの導入および運用に役立ててください。
seo-description: Adobe のエンジニアリングおよびコンサルティングチームがまとめたベストプラクティスを確認し、AEM マルチサイトマネージャーの導入および運用に役立ててください。
uuid: cbb598bb-ec8f-4985-97af-7c87f5891c66
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features, best-practices
content-type: reference
discoiquuid: 04344537-7485-40a9-ad14-804ba448f1e2
translation-type: tm+mt
source-git-commit: a929252a13f66da8ac3e52aea0655b12bdd1425f
workflow-type: tm+mt
source-wordcount: '1530'
ht-degree: 64%

---


# MSM のベストプラクティス{#msm-best-practices}

## 一般 {#general}

MSM は、コンテンツのデプロイメントを自動化するための設定可能なフレームワークです。多くの場合、実装は Web サイトの主要な部分に影響を及ぼし、複数の組織や地域にわたっておこなわれます。そのため、Web サイトの計画時と同様に、最大限の注意を払って MSM の実装を計画することを強くお勧めします。

* Carefully **plan structure and content flows** before starting implementation.
* **最小限必要なカスタマイズだけをおこなってください。** MSMは高度なカスタマイズ（展開設定など）をサポートしていますが、通常、Webサイトのパフォーマンス、信頼性、アップグレード性のベストプラクティスは、カスタマイズを最小限に抑えることです。
* Establish a **governance** model early, and train users accordingly, to ensure success. A best practice from a governance point of view is to **minimize the authority that local content producers have** to allocate/connect content to other local users and their respective live copies. これは、非管理型の連鎖継承は、MSM構造の複雑さを大幅に増し、パフォーマンスと信頼性に悪影響を及ぼす可能性があるからです。

* Once a plan exists for your structure, content flows, automation and governance - **prototype and thoroughly test your system**, before starting live implementation.
* Keep in mind that **Adobe Consulting and leading System Integrators** have deep experience planning and implementing content automation with MSM, so they can help you both get started with your MSM project and throughout its entire implementation.

>[!NOTE]
>
>MSM での作業に関するその他の情報については、ナレッジベースの記事を参照してください。
>
>* [MSM に関する FAQ](https://helpx.adobe.com/jp/experience-manager/kb/index/msm_faq.html)
>* [MSM の問題のトラブルシューティング](https://helpx.adobe.com/jp/experience-manager/kb/troubleshooting-aem-msm-issues.html)

>



>[!NOTE]
>
>また、[参照コンポーネント](/help/sites-authoring/default-components-foundation.md#reference)を使用して、単一のページまたは段落を再利用することもできます。ただし、次の点に注意してください。
>
>* MSM のほうが柔軟性が高く、同期するコンテンツや同期のタイミングを詳細に制御できます。
>* [コアコンポーネント](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/introduction.html)は基礎コンポーネントよりも推奨されています。

>



## ライブコピーのソースとブループリント設定 {#live-copy-sources-and-blueprint-configurations}

ライブコピーは[通常のページ](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)または[ブループリント設定](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)を使用して作成できます。どちらも有効なソースです。

ブループリント設定を使用する追加の利点は次のとおりです。

* Allow the author to use the **Rollout** option on a blueprint - to (explicitly) push modifications to live copies that inherit from this blueprint.
* Allow the author to use **Create Site**; this allows the user to easily select languages and configure the structure of the live copy.
* ブループリントと関係があるライブコピーのデフォルトのロールアウト設定を定義できます。

ブループリント設定が参照されない場合、ロールアウトはライブコピー自体からのみ開始でき、基本的にはソースからコンテンツを引っ張ってきます。

ライブコピーで新しいサイトを作成する際には、ブループリント設定を作成して MSM のすべての機能セットを使用可能にすると便利です。

## コンポーネントとコンテナの同期 {#components-and-container-synchronization}

一般に、コンポーネントの同期に関する MSM のロールアウトルールは、次のとおりです。

* コンポーネントは、ブループリントに含まれるリソースを同期してロールアウトされます。
* コンテナは、現在のリソースのみを同期します。

これは、コンポーネントが集計として扱われ、ロールアウトでは、コンポーネント自体およびそのすべての子がブループリントのものと置き換えられることを意味します。これは、リソースがそのようなコンポーネントにローカルで追加されると、ロールアウト時にブループリントのコンテンツでなくなることを意味します。

コンポーネントのネストをサポートするには、そうしたローカルで追加されたコンポーネントがロールアウトで維持され、そのコンポーネントがコンテナとして宣言される必要があります。例えば、デフォルトの parsys がコンテナとして宣言されるので、ローカルで追加されたコンテンツをサポートできます。

>[!NOTE]
>
>プロパティ `cq:isContainer` をコンポーネントに追加し、コンテナとして指定します。

## サイトの作成 {#create-site}

AEM でライブコピーを作成する方法は、主に次の 2 つです。

* When [creating a Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   これは、任意のページからライブコピーを作成できる、より一般的な方法と考えることができます。 ライブコピーのコンテンツ構造はソースと完全に一致します。

* サイトの [作成時](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)

   これは、主に多言語構造を持つWebサイトを作成する場合に、より専門的なアプローチです。

サイトを作成する際に留意する点のいくつかを次に示します。

* To create a new site, you need a [blueprint configuration](/help/sites-administering/msm-livecopy.md#managing-blueprint-configurations).
* 言語パスを選択して新しいサイトに作成できるようにするには、対応する言語ルートが設計図（ソース）に存在する必要があります。
* Once a [new site has been created as a live copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (using **Create**, then **Site**), the first two levels of this live copy are *shallow*. ページの子はライブ関係には属しませんが、トリガーに一致するライブ関係が見つかった場合には引き続きロールアウトが引き継がれます。

    次のことがおこなわれるのを防ぎます。

   * ブループリント（最初のレベルの下）に言語を手動で追加する
   * 言語ルートの直下にコンテンツを手動で追加する
   * ロールアウト時にこの新しいコンテンツがライブコピーに自動的に持ち越される結果にならない

## MSM と多言語の Web サイト {#msm-and-multilingual-websites}

MSM は、次の 2 つの方法で多言語 Web サイトを作成するために役立ちます。

* 言語マスターの作成時

   * MSM 自体に&#x200B;**コンテンツ翻訳機能は備わっていません**&#x200B;が、翻訳に対応したサードパーティの翻訳コネクターと統合できます。次の点に留意してください。

      * MSM では、ページレベルまたはコンポーネントレベルで継承をキャンセルできます。これにより、次回ロールアウト時にライブコピーの翻訳済みコンテンツがブループリントの未翻訳コンテンツで上書きされるのを防止できます。
      * 一部のサードパーティの翻訳コネクターでは、この MSM の継承の管理が自動化されます。

         詳しくは、翻訳サービスプロバイダーにお問い合わせください。

      * 言語マスターを作成して翻訳する代わりに、言語コピーを AEM の標準翻訳統合フレームワークと組み合わせて使用することもできます。

* 言語マスターからのコンテンツのロールアウト時

   * 例えば、フランス語の言語マスターから国別のサイト（フランス／フランス語、カナダ／フランス語、スイス／フランス語など）にロールアウトできます。

詳しくは、[多言語サイトのコンテンツの翻訳](/help/sites-administering/translation.md)および[翻訳のベストプラクティス](/help/sites-administering/tc-bp.md)を参照してください。

## 構造の変更とロールアウト {#structure-changes-and-rollouts}

ブループリントやソースツリー内のコンテンツ構造の変更は、ライブコピーへの反映のされ方が異なります。これは、変更の内容によって変わります。

* **設計図で新しいページを作成すると** 、標準的なロールアウト設定で展開した後、ライブコピーで対応するページが作成されます。

* **Blueprintでページを削除すると** 、標準的なロールアウト設定で展開した後に、対応するページがライブコピーから削除されます。

* **設計図内でページを移動しても** 、標準的なロールアウト設定で展開した後に、対応するページがライブコピー内で移動する **ことはありません** 。

   * この動作になる理由は、ページの移動にはページの削除が暗黙的に含まれているからです。つまり、オーサー環境でページを削除すると、パブリッシュ環境の対応するコンテンツが自動的にアクティベート解除されることになり、結果として、パブリッシュ環境で予期しない動作が発生する可能性があります。これは、リンクやブックマークなどの関連項目にも影響することがあります。
   * それぞれのライブコピーページにおけるコンテンツの継承は更新され、ブループリントのソースの新しい場所が反映されます。
   * ブループリントからライブコピーへのページの移動を十分に実現するには、以下のベストプラクティスを検討します。

>[!NOTE]
>
>This will work only with the [On Rollout trigger](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/msm-sync.html#rollout-triggers).

* カスタムロールアウト設定を作成します。

   * この新しい設定には、次のアクションを含める必要があります。

      `PageMoveAction`

      この設定には、他のアクションを追加しないでください。

* 新しい設定を配置します。

   * ライブコピーの古い場所にある各ページを削除しながら、ページの移動を完全にロールアウトするには：

      * 新規に作成した設定を標準ロールアウト設定の前に配置します。

         古い場所にあるページは、標準ロールアウト設定に基づいて削除されます。
   * 各ページをライブコピーの古い場所に維持したまま（基本的にコンテンツを複製しながら）ページの移動をロールアウトするには：

      * 新規に作成した設定を標準ロールアウト設定の後に配置します。

         これにより、ライブコピー内のコンテンツが削除されたり、発行からアクティベート解除されたりすることはありません。


## ロールアウトのカスタマイズ {#customizing-rollouts}

MSM のロールアウト設定は高度なカスタマイズが可能です。ロールアウトの自動化は広範囲に影響を及ぼす場合があります。ベストプラクティスとして、次のような場合はきわめて&#x200B;**&#x200B;慎重に事前計画を立てるようにしてください。

* automating rollouts; for example, with [onModify triggers](#onmodify),
* [ノードタイプ／プロパティ](#node-types-properties)をカスタマイズする場合
* 以降のワークフローの開始、
* ロールアウトの一部としてのコンテンツのアクティブ化、またはその両方を行います。

### onModify {#onmodify}

[ロールアウトトリガー](/help/sites-administering/msm-sync.md#rollout-triggers) `onModify` を使用する際には、次の点に留意してください。

* Automating rollouts with `onModify` triggers may have a negative impact on authoring performance as they trigger rollouts after *every* page modification.

* ロールアウト結果は、次のように予想に反する場合があります。

   * 実行される変更イベントの順序は指定できません。
   * イベントベースのアーキテクチャでは、ロールアウトマネージャーに渡されるイベントの順序は保証されません。

* このようなロールアウト設定を使用すると、同じリソースの同時更新が発生した場合にコミットが競合する可能性があります。

Therefore, it is recommended that you *only* use `onModify` triggers if the benefits of automatic rollout initiation outweigh any potential performance issues.

### ノードタイプ／プロパティ {#node-types-properties}

次のことに留意してください。

* ロールアウト操作をカスタマイズするだけでなく、MSMでは、ロールアウトするノードのプロパティをカスタマイズすることもできます。 MSM の OSGi 設定では、ソースからライブコピーにコピーする[ノードタイプを除外できます](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization)。

## その他の情報 {#further-information}

これに関連する問題について、このページと後続のページで説明します。

* [ライブコピーの作成と同期](/help/sites-administering/msm-livecopy.md)
* [ライブコピーの概要コンソール](/help/sites-administering/msm-livecopy-overview.md)
* [ライブコピーの同期の設定](/help/sites-administering/msm-sync.md)
* [MSM ロールアウトの競合](/help/sites-administering/msm-rollout-conflicts.md)

