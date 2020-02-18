---
title: テンプレート
seo-title: テンプレート
description: テンプレートは、新しいページのベースとして使用するページを作成する際に使用します
seo-description: テンプレートは、新しいページのベースとして使用するページを作成する際に使用します
uuid: 6fa3dafc-dfa1-42d8-b296-d4be57449411
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 7c723773-7c23-43d7-85dc-53e54556b648
legacypath: /content/docs/en/aem/6-1/develop/the-basics/templates
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6

---


# テンプレート{#templates}

テンプレートは、AEM の様々な場面で使用されます。

* [ページの作成時にテンプレートを選択](#templates-pages)します。このテンプレートは、新しいページのベースとして使用されます。テンプレートは、作成されるページの構造、初期コンテンツおよび使用可能な[コンポーネント](/help/sites-authoring/default-components.md)（デザインプロパティ）を定義します。

* [コンテンツフラグメントの作成時にテンプレートを選択](#templates-content-fragments)します。このテンプレートは、構造、初期要素およびバリエーションを定義します。

ここでは、次のテンプレートについて詳しく説明します。

* [ページテンプレート - 編集可能](/help/sites-developing/page-templates-editable.md)
* [ページテンプレート - 静的](/help/sites-developing/page-templates-static.md)
* [コンテンツフラグメントテンプレート](/help/sites-developing/content-fragment-templates.md)
* [アダプティブテンプレートレンダリング](/help/sites-developing/templates-adaptive-rendering.md)

## テンプレート - ページ {#templates-pages}

現在、AEM には、ページ作成用として 2 つの基本的なタイプのテンプレートが用意されています。

>[!NOTE]
>
>[新しいページを作成](/help/sites-authoring/managing-pages.md#creating-a-new-page)するときにテンプレートを使用する際、ページ編集者にとって見た目的な違いはなく、またどちらのタイプのテンプレートを使用しているかについての表示もありません。

### 編集可能テンプレート {#editable-templates}

編集可能なテンプレートは、AEMでの開発に関するベストプラクティスと見なされるようになりました。

編集可能テンプレートのメリットは次のとおりです。

* 作成者が[作成](/help/sites-authoring/templates.md#creating-a-new-template-template-author)および[編集](/help/sites-authoring/templates.md#editing-a-template-structure-template-author)できます。

* テンプレートを使用して作成される任意のページで、以下の項目を定義できます。

   * 構造
   * 初期コンテンツ
   * コンテンツポリシー

* 新しいページの作成後も、そのページとテンプレートの間に動的接続が維持されます。つまり、テンプレートの構造に対する変更は、そのテンプレートを使用して作成されるすべてのページに反映されます（初期コンテンツに対する変更は反映されません）。
* デザインプロパティを保持するには、テンプレートエディターから編集できるコンテンツポリシーを使用します（ページエディター内のデザインモードは使用しません）。
* Are stored under `/conf`
* 詳しくは、[編集可能テンプレート](/help/sites-developing/page-templates-editable.md)を参照してください。

>[!NOTE]
>
>An AEM Community Article is available explaining how to develop an Experience Manager site with Editable Templates, see [Creating an Adobe Experience Manager 6.5 website using Editable Templates](https://helpx.adobe.com/experience-manager/using/first_aem64_website.html).

### 静的テンプレート {#static-templates}

静的テンプレートには、次の特徴があります。

* 開発者が定義および設定する必要があります。
* これはAEMの元のテンプレート化システムで、多くのバージョンで利用できました。
* 作成されるページと同じ構造のノード階層を含んでいますが、実際のコンテンツはありません。
* 新しいページはテンプレートをコピーして作成されるので、動的接続は存在しません。
* デザインプロパティを保持するには、[デザインモード](/help/sites-authoring/default-components-designmode.md)を使用します。
* Are stored under `/apps`
* 詳しくは、[静的テンプレート](/help/sites-developing/page-templates-static.md)を参照してください。

>[!NOTE]
>
>AEM 6.5では、静的テンプレートの使用はベストプラクティスとは見なされません。 その代わりに編集可能テンプレートを使用してください。
>
>[AEM最新化ツールは](modernization-tools.md) 、静的なテンプレートから編集可能なテンプレートに移行する際に役立ちます。

### Template Availability {#template-availability}

>[!CAUTION]
>
>AEMは、「サイト」で許可されるテンプレートを制御する複数のプロパティを提 **供します**。 ただし、組み合わせると、追跡と管理が困難な非常に複雑なルールになる可能性があります。
>
>したがって、以下を定義することで、シンプルに開始することをお勧めします。
>
>* 財産のみ `cq:allowedTemplates` である
   >
   >
* サイトのルートにのみ
>
>
For an example, see We.Retail: `/content/we-retail/jcr:content`
>
>また、プロパ `allowedPaths`ティ、 `allowedParents`およびをテ `allowedChildren` ンプレートに配置して、より高度なルールを定義することもできます。 ただし、可能な場合は、許可され *るテンプレートを*`cq:allowedTemplates` さらに制限する必要がある場合は、サイトのサブセクションでさらにプロパティを定義する方がはるかに簡単です。
>
>また、ページプロパティの「詳細 `cq:allowedTemplates` 」タブで作成者がプロパティを更新でき **るという利点もあ** ります ****。 その他のテンプレートプロパティは、（標準） UIを使用して更新できないので、変更が行われるたびにルールとコードのデプロイメントを管理する開発者が必要になります。

サイト管理インターフェイスで新しいページを作成する場合、使用可能なテンプレートのリストは、新しいページの場所と、各テンプレートで指定されている配置制限によって異なります。

次のプロパティは、新しいペ `T` ージをページの子として配置する際にテンプレートを使用できるかどうかを決定しま `P`す。 これらの各プロパティは、パスとの一致に使用される0個以上の正規表現を保持する複数値の文字列です。

* The `cq:allowedTemplates` property of the `jcr:content` subnode of `P` or an ancestor of `P`.

* のプ `allowedPaths` ロパティ `T`。

* のプ `allowedParents` ロパティ `T`。

* The `allowedChildren` property of the template of `P`.

評価は次のようにおこなわれます。

* で始まるページ階層を昇 `cq:allowedTemplates` 順に見つけた最初の、空でないプロパティ `P` は、のパスと一致しま `T`す。 いずれの値も一致しない場合、は拒否 `T` されます。

* If `T` has a non-empty `allowedPaths` property, but none of the values match the path of `P`, `T` is rejected.

* 上記のプロパティの両方が空か存在しない場合、と同じアプリケーシ `T` ョンに属していない限りは拒否されま `P`す。 `T` は、パスの第2レベル `P` の名前がパスの第2レベルの名前と同じである場合に限り、ifと同じアプリケ `T` ーションに属します `P`。 例えば、テンプレートはペ `/apps/geometrixx/templates/foo` ージと同じアプリに属しているとしま `/content/geometrixx`す。

* If `T` has an non-empty `allowedParents` property, but none of the values match the path of `P`, `T` is rejected.

* If the template of `P` has a non-empty `allowedChildren` property, but none of the values match the path of `T`, `T` is rejected.

* その他すべての場合は、`T` は許可されます。

以下の図は、テンプレートの評価プロセスを示しています。

![chlimage_1-176](assets/chlimage_1-176.png)

#### 子ページで使用するテンプレートの制限 {#limiting-templates-used-in-child-pages}

特定のページの下に子ページを作成するために使用できるテンプレートを制限するには、ページのノードのプロパティを使用して、子ページとして許可するテンプレートのリスト `cq:allowedTemplates``jcr:content` を指定します。 例えば、リスト内の各値は、許可された子ページのテンプレートへの絶対パスである必要がありま `/apps/geometrixx/templates/contentpage`す。

You can use the `cq:allowedTemplates` property on the template&#39;s  `jcr:content` node to have this configuration applied to all newly created pages that use this template.

テンプレート階層など、さらに制約を追加する場合は、テンプレートのプロパティ `allowedParents/allowedChildren` を使用できます。 その後、テンプレートTから作成されたページを、テンプレートTから作成されたページの親/子にする必要があることを明示的に指定できます。

## テンプレート - コンテンツフラグメント {#templates-content-fragments}

詳しくは、[コンテンツフラグメントテンプレート](/help/sites-developing/content-fragment-templates.md)を参照してください。
