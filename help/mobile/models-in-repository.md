---
title: リポジトリ内のモデル
seo-title: リポジトリ内のモデル
description: 'null'
seo-description: 'null'
uuid: 54f81180-4178-4e33-a6f0-e9e6ea50798e
contentOwner: User
content-type: reference
discoiquuid: ae1a72f4-d8c1-4c75-ba2c-7322f3743b17
noindex: true
redirecttarget: /content/help/en/experience-manager/6-4/mobile/using/administer-mobile-apps
source-git-commit: 5120bbdefea528ad6d07a9c99df565555b6a8444
workflow-type: tm+mt
source-wordcount: '1332'
ht-degree: 73%

---


# リポジトリ内のモデル{#models-in-repository}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)

モデルには、最終的にコンテンツサービスによってレンダリングされるプロパティを定義した、一連のデータタイプが含まれています。さらに、データの整合性を維持するために、他のモデルとの関係も定義されます。

開発者は、リポジトリ内のモデル構造を熟知している必要があります。アプリの要件に従って、独自のモデルやエンティティを作成することができます。

## モデルタイプの作成  {#creating-model-types}

*/libs/settings/mobileapps/model-types* に、システム提供のモデルタイプが 2 つ含まれています。これらのシステムモデルタイプを上書きする場合は、上書きの適用先となる設定ノードの下に *mobileapps/model-types* ノードを作成する必要があります。

例えば、*/conf/myconf1* と */conf/myconf2* に設定を作成している場合に、*conf1* に対してのみシステムモデルタイプの上書きを適用するには、*conf1* の設定の下に *mobileapps/model-types* ノードを作成します。

モデルにデータタイプを追加できるようにするには、モデルタイプに「cq:Page」タイプの「scaffolding」という名前の子ノードと、リソースタイプ「*wcm/scaffolding/components/scaffolding*」を設定する必要があります。

また、基礎モードページで、このモデルタイプから作成されたモデルで使用可能なデータタイプを示す *dataTypesConfig* プロパティを PageContent ノードに含める必要があります。

>[!NOTE]
>
>**基礎モード**&#x200B;は、モデルに基づいてエンティティが編集できるデータタイプを定義するページです。 個々のデータタイプについて、UI 上でフィールドをどのように表示するかや、データ値をどのように永続化するかを定義することもできます。

### データタイプ設定  {#data-types-config}

データタイプ設定ノードには、データタイプ項目のリストが含まれます。各データタイプ項目では、そのデータタイプをモデルエディターでどのように表示するかと、最終的にエンティティによってレンダリングされるためにどのように永続化する必要があるかを指定します。

| **プロパティ名** | **説明** |
|---|---|
| fieldIcon | データタイプを表すCoralUIアイコンのクラス |
| fieldPropResourceType | データ型を設定するためのすべてのプロパティをレンダリングするコンポーネント |
| fieldProperties | fieldPropResourceTypeが&#x200B;*mobileapps/caas/gui/components/models/editor/datatypes/field*&#x200B;の場合に使用されるプロパティコンポーネントの複数値リスト |
| fieldResourceType | データタイプの永続化されたノードのresourceType（つまり、エンティティエディターでプロパティをレンダリングするコンポーネント） |
| fieldViewResourceType | モデルエディタービューでデータ型のレンダリングに使用するコンポーネント（このプロパティを省略した場合はfieldResourceTypeが使用されます） |
| fieldTitle | モデルエディターに表示されるデータタイプの名前 |
| multiFieldResourceType | 複数値が選択されている場合に、永続化されたノードで使用するリソースタイプ |
| renderType | クライアントサイドレンダリングのヒントのレンダリング |

### データタイプ設定のオーバーレイ {#data-types-config-overlay}

「dataTypesConfig」プロパティは、Sling リソースの統合をサポートしています。つまり、システムモデルタイプ（またはカスタムモデルタイプ）で使用されるデータタイプを、オーバーレイノードを使用してカスタマイズできます。

*/libs/settings/mobileapps/models/formbuilderconfig/datatypes* のオーバーレイを作成し、必要に応じてカスタマイズする必要があります。

例えば、fieldResourceType をカスタムコンポーネントに変更するために、String データタイプのオーバーレイを追加することができます。

Sling リソースの統合について詳しくは、[AEM での Sling Resource Merger の使用](/help/sites-developing/sling-resource-merger.md)を参照してください。

![chlimage_1-7](assets/chlimage_1-7.png)

### データタイプ {#data-types}

モデルデータタイプは、フォーム投稿時に組み込まれるデータを含むことのできるフォームコンポーネントです。データタイプコンポーネントは、必要なだけ複雑にすることができます。カスタムデータタイプの使用例の 1 つが、特定の国用の住所ブロックです。このようにすると、プリミティブデータタイプを使用して住所ブロックを毎回作成し直す必要がなくなります。

カスタムデータタイプの例は、「/libs/mobileapps/caas/components/form/contentreference」を参照してください。

すべてのプリミティブデータタイプでは、既存の Granite フォームコンポーネントが利用されます。詳しくは、[https://docs.adobe.com/docs/en/aem/6-3/develop/ref/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/index.html](https://docs.adobe.com/docs/en/aem/6-3/develop/ref/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/index.html)

データタイプ設定にカスタムデータタイプを追加すると、そのデータタイプをモデルエディターで使用できるようになります。

## モデルの作成  {#creating-models}

必要なすべてのモデルタイプとデータタイプを開発したら、モデルの作成に進むことができます。最終的に、作成者はモデルを使用してエンティティを作成し、コンテンツサービスはエンティティを使用してデータをレンダリングします。

モデルを作成するには、現在の設定に基づき使用可能なモデルタイプを選択し、タイトルと説明を指定します。

ダッシュボードからのモデルの作成および管理について詳しくは、モバイルアプリのオーサリングに関する節の[モデルの作成](/help/mobile/administer-mobile-apps.md)を参照してください。

### モデルのプロパティ  {#properties-of-a-model}

以下の表では、モデルに定義されたプロパティを示します。

| **プロパティ名** | **説明** |
|---|---|
| モデルタイトル | モデルの名前 |
| 説明 | モデルの説明 |
| サムネール | モデルのサムネール画像 |
| モデルタイプ | モデルのタイプ（単純な文字列または実際のコンポーネントへのパス） |
| 許可されている子 | このテンプレートの子として許可されているテンプレートのパス |
| 許可された親 | このテンプレートの親として許可されているテンプレートのパス |

>[!NOTE]
>
>「許可されている子」**&#x200B;および「許可された親」**&#x200B;プロパティは、ページテンプレートと同じルールに従います。詳しくは、[ページテンプレート](/help/sites-developing/page-templates-static.md)を参照してください。
>
>「モデルタイプ」**&#x200B;に関して、すべてのモデルは *mobileapps/caas/components/data/entity* のスーパータイプを持っている必要がありますが、サブタイプを指定して、コンテンツ配信をカスタマイズできます。また、すべてのモデルタイプを一意にすることで、コンテンツサービスのクライアントがデータのオブジェクトを識別できるようになります。

### モデルの編集  {#editing-a-model}

モデルを編集するには、編集するモデルに関連付けられている基礎モードダイアログフォームを開きます。通常、基礎モードはモデルの子ノードですが、「cq:scaffolding」プロパティを使用してパスを指定すれば、必要に応じてモデルの外に配置することができます。この方法は、異なるプロパティを指定する必要がある複数のモデルで同じ基礎モードを共有する場合に便利です。

モデルの基礎モードが配置されている場合、モデルエディターは「jcr:content/cq:dialog/content」の下に配置されているものをレンダリングします。現在、クライアント側のフォームビルダーエンジンは、最大で 3 列の固定レイアウトのみをサポートしています。レンダリングされたフォームダイアログの右側に、データタイプ設定に指定されたすべてのデータタイプのリストが表示されます。それらをクリックしてデータタイプを編集できます。右側のレールが、選択したデータタイプの「プロパティ」タブに切り替わります。新しいデータタイプをプレビューキャンバスにドラッグすると、そのデータタイプが追加されます。「保存」をクリックすると、変更がサーバに反映されます。 「キャンセル」をクリックすると、モデルエディターが閉じます。

>[!NOTE]
>
>すべてのモデルはテンプレートなので、すべての AEM テンプレートルールに従います。これにより、*allowedParents*&#x200B;や&#x200B;*allowedChildren*&#x200B;などのプロパティを使用できます。 これらは、モデルに基づいて新しいエンティティを作成するときに有効になります。テンプレートルールにより、エンティティの階層に応じた特定のモデルのみに基づいてエンティティを作成することができます。
>
>ダッシュボードからのモデルの編集については、モバイルアプリのオーサリングの節の[モデル](/help/mobile/administer-mobile-apps.md)の作成を参照してください。

### システムモデル {#system-models}

単純なコンテンツ再利用のために、2 種類のシステムモデルがあらかじめ用意されています。これらのモデルは編集できません。

**ページモ** デルページモデルは、Sitesの既存のコンテンツを、コンテンツサービスによる配信に再利用するための迅速な方法を提供します。

ページモデルに基づくエンティティのresourceTypeは次のとおりです。mobileapps/caas/components/data/pages

パス：Sites ページへのパスです。このパス（およびその子）のコンテンツは、コンテンツサービスハンドラーによってレンダリングされます。

**アセッ** トモデルアセットモデルを使用すると、アセットの既存のコンテンツをすばやく再利用して、コンテンツサービスによる配信をおこなうことができます。

ページモデルに基づくエンティティのresourceTypeは次のとおりです。*mobileapps/caas/components/data/assets.*

アセットリスト：Assets からのパスのリストです。各アセットは子エンティティノードとして追加され、resourceType は *wcm/foundation/components/image* となります。

>[!NOTE]
>
>ダッシュボードからモデルを作成するためにこれらのテンプレートを使用する方法について詳しくは、モバイルアプリのオーサリングの節の[モデル](/help/mobile/administer-mobile-apps.md)の作成を参照してください。
