---
title: テンプレート
description: テンプレートは、新しいページのベースとして使用するページを作成する際に使用します。
uuid: 6fa3dafc-dfa1-42d8-b296-d4be57449411
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 7c723773-7c23-43d7-85dc-53e54556b648
legacypath: /content/docs/en/aem/6-1/develop/the-basics/templates
exl-id: 59f01bb1-4ff1-42b6-afc9-56d448b1f803
source-git-commit: 95638b6dd9527c567b38d8cd9da14633bd4142b5
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 54%

---

# テンプレート{#templates}

テンプレートは、AEMの様々なポイントで使用されます。

* [ページを作成する場合、テンプレートを選択します](#templates-pages). このテンプレートは、新しいページのベースとして使用されます。 テンプレートは、ページの構造、初期コンテンツおよび [コンポーネント](/help/sites-authoring/default-components.md) 使用可能（デザインプロパティ）

* [コンテンツフラグメントを作成する際は、テンプレートも選択します](#templates-content-fragments). このテンプレートは、構造、初期要素およびバリエーションを定義します。

ここでは、次のテンプレートについて詳しく説明します。

* [ページテンプレート - 編集可能](/help/sites-developing/page-templates-editable.md)
* [ページテンプレート - 静的](/help/sites-developing/page-templates-static.md)
* [コンテンツフラグメントテンプレート](/help/sites-developing/content-fragment-templates.md)
* [アダプティブテンプレートレンダリング](/help/sites-developing/templates-adaptive-rendering.md)

## テンプレート — ページ {#templates-pages}

AEMには、ページを作成するための 2 つの基本的なタイプのテンプレートが用意されています。

>[!NOTE]
>
>テンプレートを使用して [ページの作成](/help/sites-authoring/managing-pages.md#creating-a-new-page)の場合、（ページ作成者に対する）目に見える違いはなく、使用されているテンプレートの種類も示されません。

### 編集可能なテンプレート {#editable-templates}

AEM で開発を行う場合は、編集可能テンプレートを使用することをお勧めします。

編集可能テンプレートの利点は次のとおりです。

* 可能 [作成済み](/help/sites-authoring/templates.md#creating-a-new-template-template-author) および [編集済み](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) 作成者によって

* テンプレートで作成されたすべてのページで以下を定義できるようにが導入されました。

   * 構造
   * 初期コンテンツ
   * コンテンツポリシー

* 新しいページが作成されると、ページとテンプレートの間に動的な接続が維持されます。 つまり、テンプレート構造の変更は、そのテンプレートで作成されたすべてのページに反映されます。初期コンテンツの変更は反映されません。
* デザインプロパティを保持するには、テンプレートエディターから編集できるコンテンツポリシーを使用します（ページエディター内のデザインモードは使用しません）。
* `/conf` に保存されます。
* 詳しくは、[編集可能テンプレート](/help/sites-developing/page-templates-editable.md)を参照してください。

>[!NOTE]
>
>詳しくは、 [編集可能なページテンプレートを使用したExperience Managerサイトの開発](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/template-editor-feature-video-use.html?lang=en).

### 静的テンプレート {#static-templates}

静的テンプレート：

* 開発者が定義および設定する必要があります。
* AEMの元のテンプレートシステムです。多くのバージョンで使用できます。
* 静的テンプレートは、作成するページと同じ構造を持ち、実際のコンテンツを持たないノードの階層です。
* ページを作成するためにコピーされ、その後は動的接続は存在しません。
* デザインプロパティを保持するには、[デザインモード](/help/sites-authoring/default-components-designmode.md)を使用します。
* `/apps` に保存されます
* 詳しくは、[静的テンプレート](/help/sites-developing/page-templates-static.md)を参照してください。

>[!NOTE]
>
>AEM 6.5 以降では、静的テンプレートの使用はベストプラクティスとは見なされていません。その代わりに編集可能テンプレートを使用してください。
>
>[AEM 最新化](modernization-tools.md)ツールは、静的テンプレートから編集可能テンプレートへの移行に役立ちます。

### 使用可能なテンプレート {#template-availability}

>[!CAUTION]
>
>AEM は、複数のプロパティをオファーして、**Sites** で許可されるテンプレートを制御します。ただし、組み合わせると複雑なルールになり、追跡や管理が困難になる場合があります。
>
>したがって、アドビでは、次の項目を定義して、単純に開始することをお勧めします。
>
>* プロパティは `cq:allowedTemplates` のみ
>
>* サイトのルートにのみ
>
>例えば、We.Retail `/content/we-retail/jcr:content` を参照してください。
>
>プロパティ `allowedPaths`、`allowedParents`、`allowedChildren` をテンプレートに配置して、より高度なルールを定義することもできます。しかし、可能な場合は、 *多い* さらに定義しやすい `cq:allowedTemplates` 許可されるテンプレートをさらに制限する必要がある場合は、サイトのサブセクションのプロパティ。
>
>特に利点は、 `cq:allowedTemplates` プロパティは、 **詳細** タブ **ページプロパティ**. その他のテンプレートプロパティは、（標準）UI を使用して更新することはできないので、変更するたびに、ルールとコードのデプロイメントを管理する開発者が必要になります。

サイト管理インターフェイスでページを作成する場合、使用可能なテンプレートのリストは、新しいページの場所と、各テンプレートで指定されている配置制限によって異なります。

次のプロパティは、テンプレートが `T` は、新しいページをページの子として配置するために使用されます `P`. これらの各プロパティは、0 個以上の正規表現を保持する複数値の文字列で、パスの照合に使用されます。

* `jcr:content` サブノードの `P` または `P` の上位ページの `cq:allowedTemplates` プロパティ。

* `T` の `allowedPaths` プロパティ。

* `T` の `allowedParents` プロパティ。

* `P` のテンプレートの `allowedChildren` プロパティ。

評価は次のように行われます。

* `P` で始まるページ階層を昇順にしているときに見つかった、最初の空でない `cq:allowedTemplates` プロパティは、`T` のパスと一致します。一致する値がない場合、`T` は拒否されます。

* `T` に空でない `allowedPaths` プロパティがあるものの、 `P` のパスと一致する値がない場合、`T` は拒否されます。

* 上記のプロパティの両方が空または存在しない場合、`P` と同じアプリケーションに属さない限り、`T` は拒否されます。`T` は、`T` のパスの 2 番目のレベルの名前が `P` のパスの 2 番目のレベルの名前と同じである場合に限り、`P` と同じアプリケーションに属します。例えば、テンプレート `/apps/geometrixx/templates/foo` は、ページ `/content/geometrixx` と同じアプリに属しています。

* `T` に空でない `allowedParents` プロパティがあるものの、 `P` のパスと一致する値がない場合、`T` は拒否されます。

* `P` のテンプレートに空でない `allowedChildren` プロパティがあるものの、`T` のパスと一致する値がない場合、`T` は拒否されます。

* その他すべての場合は、`T` は許可されます。

以下の図は、テンプレートの評価プロセスを示しています。

![chlimage_1-176](assets/chlimage_1-176.png)

#### 子ページで使用するテンプレートの制限 {#limiting-templates-used-in-child-pages}

特定のページの下に子ページを作成するために使用できるテンプレートを制限するには、ページの `jcr:content` ノードの `cq:allowedTemplates` プロパティを使用して、子ページとして許可するテンプレートのリストを指定します。例えば、`/apps/geometrixx/templates/contentpage` リストの各値は、許可されている子ページのテンプレートへの絶対パスである必要があります。

テンプレートの `jcr:content` ノードの `cq:allowedTemplates` プロパティを使用すると、このテンプレートを使用するすべての新規作成ページにこの設定を適用できます。

テンプレート階層に関する制約などをさらに追加する場合は、 `allowedParents/allowedChildren` プロパティを使用します。 その後、テンプレート T から作成されたページが、テンプレート T から作成されたページと親子である必要があることを明示的に指定できます。

## テンプレート — コンテンツフラグメント {#templates-content-fragments}

詳しくは、 [コンテンツフラグメントテンプレート](/help/sites-developing/content-fragment-templates.md).
