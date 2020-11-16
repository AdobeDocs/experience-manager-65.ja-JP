---
title: AEM の開発 - ガイドラインとベストプラクティス
seo-title: AEM の開発 - ガイドラインとベストプラクティス
description: AEM での開発に関するガイドラインとベストプラクティス
seo-description: AEM での開発に関するガイドラインとベストプラクティス
uuid: a67de085-4441-4a1d-bec3-2f27892a67ff
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: b4cf0ffc-973a-473b-80c8-7f530d111435
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 85%

---


# AEM の開発 - ガイドラインとベストプラクティス{#aem-development-guidelines-and-best-practices}

## テンプレートとコンポーネントの使用に関するガイドライン {#guidelines-for-using-templates-and-components}

AEM のコンポーネントとテンプレートは非常に強力なツールキットです。開発者はこれらを使用して、Web サイトビジネスのユーザー、エディターおよび管理者が変化の激しいビジネスニーズに適応しつつ（コンテンツの迅速性）、サイトのレイアウトを統一する（ブランド保護）ための機能を提供します。

特定の Web サイト、または一連の Web サイト（グローバル企業の支社など）の責任者によくある課題は、自身の Web サイトで新しいタイプのコンテンツプレゼンテーションを導入することです。

ここでは、公開済みの他の記事からの抜粋をリストするニュースリストページを Web サイトに追加する必要がある場合について考えます。このページのデザインおよび構造は、Web サイトの他の部分と同じにする必要があります。

このような課題への対応として、以下の方法が推奨されます。

* 既存のテンプレートを再利用して新しいタイプのページを作成します。テンプレートでページ構造（ナビゲーション要素、パネルなど）を大まかに定義し、それをデザイン（CSS、グラフィック）によってさらに微調整します。
* 新しいページで段落システム（parsys または iparsys）を使用します。
* 段落システムのデザインモードに対するアクセス権を定義して、権限のある人物（通常は管理者）のみが変更できるようにします。
* 特定の段落システムで許可されるコンポーネントを定義して、エディターが必要なコンポーネントをページに配置できるようにします。例えば、リストコンポーネントを定義すると、ページのサブツリーを移動して、事前に定義されたルールに従って情報を抽出できます。
* エディターは、担当するページ上で許可されているコンポーネントを追加および設定して、ビジネスに要求されている機能（情報）を提供します。

このアプローチによって、Web サイトに寄与しているユーザーおよび管理者が、開発チームに頼ることなく、ビジネスニーズにいかに迅速に対応できるかについて説明します。新しいテンプレートの作成など、代替の方法の場合、通常はコストがかさみ、変更管理プロセスや開発チームの関与が必要になります。これにより、プロセス全体の所用時間とコストが大幅に増大します。

したがって、AEM ベースのシステムの開発者は以下を使用する必要があります。

* 統一性とブランド保護のためのテンプレートおよび段落システムデザインに対するアクセス制御
* 柔軟性のための設定オプションを含む段落システム

以下の開発者向けの一般的ルールが、通常のプロジェクトの大多数に該当します。

* テンプレートの数を少なく保つこと。Web サイト上の根本的に異なるページ構造の数と同じ数にします。
* カスタムコンポーネントに必要な柔軟性および設定機能を備えること。
* AEM 段落システム（parsys コンポーネントと iparsys コンポーネント）の能力と柔軟性を最大限に利用すること。

### コンポーネントおよびその他の要素のカスタマイズ {#customizing-components-and-other-elements}

独自のコンポーネントを作成したり、既存のコンポーネントをカスタマイズしたりするとき、多くの場合は、既存の定義を再利用する方法が最も簡単（かつ安全）です。同じ原則が、エラーハンドラーなど、AEM 内の他の要素にも当てはまります。

これは、既存の定義をコピーしてオーバーレイすることで実行できます。 つまり、からに定義をコピー `/libs` し `/apps/<your-project>`ます。 では、この新しい定義 `/apps`は、要件に応じて更新できます。

>[!NOTE]
>
>詳しくは、[オーバーレイの使用方法](/help/sites-developing/overlays.md)を参照してください。

次に例を示します。

* [コンポーネントのカスタマイズ](/help/sites-developing/components.md)

   これには、コンポーネント定義のオーバーレイが含まれます。

   * Create a new component folder in `/apps/<website-name>/components/<MyComponent>` by copying an existing component:

      * 例えば、テキストコンポーネントをカスタマイズするには、次のようにコピーします。

         * `/libs/foundation/components/text` から
         * を `/apps/myProject/components/text`

* [エラーハンドラーで表示されるページのカスタマイズ](/help/sites-developing/customizing-errorhandler-pages.md#how-to-customize-pages-shown-by-the-error-handler)

   この場合、サーブレットをオーバーレイします。

   * リポジトリ内で、デフォルトスクリプトをコピーします。

      * `/libs/sling/servlet/errorhandler/` から
      * を `/apps/sling/servlet/errorhandler/`

>[!CAUTION]
>
>**パス内の設定は**`/libs`一切変更しないでください。
>
>`/libs` コンテンツは、インスタンスを次回アップグレードするとき（場合によってはホットフィックスまたは機能パックを適用したとき）に上書きされるからです。
>
>設定およびその他の変更の手順は以下のとおりです。
>
>1. copy the item in `/libs` to `/apps`
>1. make any changes within `/apps`


## JCR クエリを使用する場合と使用しない場合 {#when-to-use-jcr-queries-and-when-not-to-use-them}

JCR クエリは、正しく採用すれば強力なツールとなります。以下の場合に適しています。

* コンテンツのフルテキスト検索など、実際のエンドユーザークエリ。
* 構造化されたコンテンツがリポジトリ全体で見つかる必要がある場合。

   そのような場合は、クエリは、コンポーネントのアクティベーション時やキャッシュの無効化時など、絶対に必要な場合にのみ実行してください(例：ワークフローステップ、コンテンツの変更やフィルター時にトリガーするイベントハンドラーなど)。

JCR クエリは、純粋なレンダリング要求には決して使用しないでください。JCR クエリが不適切な場合の例は以下のとおりです。

* ナビゲーションのレンダリング
* 「最新ニュース上位 10 項目」の概要の作成
* コンテンツ項目の数の表示

コンテンツをレンダリングするためには、JCR クエリを実行する代わりに、コンテンツツリーへのナビゲーションアクセスを使用します。

>[!NOTE]
>
>[Query Builder](/help/sites-developing/querybuilder-api.md) を使用する場合は、JCR クエリを使用します。Query Builder では、内部で JCR クエリが生成されるからです。


## セキュリティに関する考慮事項 {#security-considerations}

>[!NOTE]
>
>It is also worthwhile to reference the [security checklist](/help/sites-administering/security-checklist.md).

### JCR（リポジトリ）セッション {#jcr-repository-sessions}

管理セッションではなくユーザーセッションを使用してください。つまり、以下を使用するということです。

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### クロスサイトスクリプティング（XSS）に対する保護 {#protect-against-cross-site-scripting-xss}

クロスサイトスクリプティング（XSS）を利用することにより、攻撃者は他のユーザーが表示する Web ページにコードを埋め込むことができます。このセキュリティ脆弱性が悪意のある Web ユーザーに悪用され、アクセス制御が擦り抜けられる可能性があります。

AEM では、ユーザーが提供するコンテンツをすべて出力時にフィルタリングする原則を適用しています。XSS を回避することは、開発時にもテスト時にも第一優先となります。

Additionally, a web application firewall, such as [mod_security for Apache](https://modsecurity.org), can provide reliable, central control over the security of the deployment environment and protect against previously undetected cross-site scripting attacks.

>[!CAUTION]
>
>AEM に用意されているサンプルコードは、それ自体ではこのような攻撃に対する保護はおこなわない場合があり、通常は Web アプリケーションファイアウォールによる要求フィルタリングに依存します。

XSS API チートシートには、XSS API を使用して AEM アプリケーションのセキュリティを強化するために知っておく必要のある情報が含まれています。このチートシートは、こちらからダウンロードできます。

XSSAPI チートシート

[ファイルを入手](assets/xss_cheat_sheet_2016.pdf)

### 機密情報のための通信のセキュリティ強化 {#securing-communication-for-confidential-information}

どのインターネットアプリケーションでも同じですが、機密情報を転送する際は、以下の点を確認してください。

* SSL によってトラフィックのセキュリティが保護されていること
* 適宜 HTTP POST が使用されていること

これは、システムに対して機密の情報（設定や管理アクセスなど）とユーザーに対して機密の情報（個人情報の詳細など）の両方に該当します。

## 個別の開発タスク {#distinct-development-tasks}

### エラーページのカスタマイズ {#customizing-error-pages}

エラーページは AEM 用にカスタマイズできます。内部サーバーエラー時にインスタンスが Sling トレースを表示しないようにするために、これをお勧めします。

詳しくは、[エラーハンドラーによって表示されるページのカスタマイズ](/help/sites-developing/customizing-errorhandler-pages.md)を参照してください。

### Java プロセス内の開いているファイル {#open-files-in-the-java-process}

AEM は多数のファイルにアクセスできるので、[Java プロセス用に開いているファイル](/help/sites-deploying/configuring.md#open-files-in-the-java-process)の数を AEM 用に明示的に設定することをお勧めします。

この問題を最小限に留めるために、開発の際は、開かれるすべてのファイルができるだけ早く（ただし合理的な範囲で）、正しく閉じられることを確認する必要があります。
