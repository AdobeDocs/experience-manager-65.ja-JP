---
title: アダプティブフォーム参照用のカスタムインデックスの作成
description: AEM Formsでアダプティブフォーム参照クエリ用のタグ付きLucene インデックスを作成して、エクスペリエンスフラグメントの公開時にトラバーサルクエリを回避する方法を説明します。
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, Developer
source-git-commit: 9240de61985dc32f17593f416e5d054cadb8a392
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 1%
---

# アダプティブフォーム参照用のカスタムインデックスの作成 {#create-custom-index-for-adaptive-forms-references}

Adobe Experience Manager（AEM）Formsがアダプティブフォーム参照を解決する際に、トラバーサルクエリを避けるために、タグ付きのLucene インデックスを作成します。 適切なインデックスがない場合、アダプティブフォーム参照を含むエクスペリエンスフラグメントを公開すると、ログに`Traversal query (query without index)`警告が生成される可能性があります。

AEM Forms 6.5.24.0以降では、参照クエリで`aemformsAFReferences` インデックスタグが使用されます。 これらのリリースにはクエリの変更が含まれていますが、そのタグを使用してカスタムインデックスを作成する必要があります。 この記事では、インデックスを定義してデプロイする方法について説明します。

AEM Forms 6.5 LTSについては、[AEM Forms 6.5 LTS](https://experienceleague.adobe.com/ja/docs/experience-manager-65-lts/content/forms/install-aem-forms/configure-aem-forms/create-custom-index-for-adaptive-forms-references)でアダプティブフォーム参照のカスタムインデックスを作成するを参照してください。

## 前提条件 {#prerequisites}

始める前に、次のことを確認してください。

* 対応するForms アドオンがインストールされたAEM Forms 6.5.24.0以降。
* オーサーインスタンスの`/oak:index`の下にインデックスを作成するためのアクセス権。
* コンテンツパッケージを使用してインデックスをデプロイするか、開発の代替手段としてCRXDE Liteにアクセスする場合は、`ui.apps` モジュールを持つAEM プロジェクト。

実稼動環境にデプロイする前に、開発環境またはステージング環境でインデックスをテストします。 [&#x200B; インデックスの作成には、大きなリポジトリで時間がかかる場合があります](/help/sites-deploying/queries-and-indexing.md#configuring-the-indexes)。

## カスタムインデックスの定義 {#define-the-custom-index}

`/oak:index/customAFReferenceLuceneIndex-1`にインデックスを作成します。 別のインデックスノード名を選択できますが、Forms参照クエリでインデックスを選択できるように、`aemformsAFReferences` タグは変更しないでください。

次の定義を使用します。 `/content`の下の`nt:unstructured` ノードに`sling:resourceType`のインデックスを作成します。

```json
{
  "jcr:primaryType": "oak:QueryIndexDefinition",
  "selectionPolicy": "tag",
  "compatVersion": 2,
  "includedPaths": ["/content"],
  "queryPaths": ["/content"],
  "tags": ["aemformsAFReferences"],
  "type": "lucene",
  "async": ["async"],
  "evaluatePathRestrictions": true,
  "reindex": false,
  "indexRules": {
    "jcr:primaryType": "nt:unstructured",
    "nt:unstructured": {
      "jcr:primaryType": "nt:unstructured",
      "properties": {
        "jcr:primaryType": "nt:unstructured",
        "resourceType": {
          "jcr:primaryType": "nt:unstructured",
          "propertyIndex": true,
          "name": "sling:resourceType"
        }
      }
    }
  }
}
```

`analyzed=true`を追加しないでください。 参照クエリでは、フルテキスト `contains`条件ではなくプロパティ制限を使用するため、設定は不要です。

## コンテンツパッケージを使用したインデックスのデプロイ {#deploy-the-index-with-a-content-package}

実稼動デプロイメントにコンテンツパッケージを使用します。

1. AEM プロジェクトの`ui.apps` モジュールで、`ui.apps/src/main/content/jcr_root/_oak_index/customAFReferenceLuceneIndex-1/`を作成します。
1. 次の定義を使用して、そのディレクトリに`.content.xml`を作成します。

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:oak="http://jackrabbit.apache.org/oak/ns/1.0"
             xmlns:jcr="http://www.jcp.org/jcr/1.0"
             xmlns:nt="http://www.jcp.org/jcr/nt/1.0"
             jcr:primaryType="oak:QueryIndexDefinition"
             async="[async]"
             compatVersion="{Long}2"
             evaluatePathRestrictions="{Boolean}true"
             includedPaths="[/content]"
             queryPaths="[/content]"
             reindex="{Boolean}false"
             selectionPolicy="tag"
             tags="[aemformsAFReferences]"
             type="lucene">
       <indexRules jcr:primaryType="nt:unstructured">
           <nt:unstructured jcr:primaryType="nt:unstructured">
               <properties jcr:primaryType="nt:unstructured">
                   <resourceType jcr:primaryType="nt:unstructured"
                                 name="sling:resourceType"
                                 propertyIndex="{Boolean}true"/>
               </properties>
           </nt:unstructured>
       </indexRules>
   </jcr:root>
   ```

1. `ui.apps/src/main/content/META-INF/vault/filter.xml`の既存の`workspaceFilter`要素の中に次のフィルターを追加します。 プロジェクトのその他のフィルターは変更しないでください。

   ```xml
   <filter root="/oak:index/customAFReferenceLuceneIndex-1"/>
   ```

1. 既存のビルド設定を使用してプロジェクトをビルドし、結果のコンテンツパッケージをオーサーインスタンスにインストールします。 パッケージのアップロードとインストール手順については、[&#x200B; パッケージマネージャー](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system)を参照してください。
1. `/oak:index/customAFReferenceLuceneIndex-1`が存在することを確認します。 クエリ計画を確認する前に、非同期インデックス作成を完了できるようにします。

別のインデックス名を選択した場合は、その名前をディレクトリ、フィルター、リポジトリパスで一貫して使用します。

## CRXDE Liteでインデックスを作成する {#create-the-index-with-crxde-lite}

開発環境では、content-package メソッドの代わりにこの代替手段を使用します。

索引ノードを作成する際は、次のプロパティを使用します。

| Property | タイプ | 値 |
| --- | --- | --- |
| `selectionPolicy` | 文字列 | `tag` |
| `compatVersion` | Long | `2` |
| `includedPaths` | `String[]` | `/content` |
| `queryPaths` | `String[]` | `/content` |
| `tags` | `String[]` | `aemformsAFReferences` |
| `type` | 文字列 | `lucene` |
| `async` | `String[]` | `async` |
| `evaluatePathRestrictions` | ブーリアン | `true` |
| `reindex` | ブーリアン | `false` |

`String[]`は、1つの値のみを含む場合でも、複数値の文字列プロパティを意味します。

1. `http://localhost:4502/crx/de/index.jsp` を開きます。 ホストとポートをオーサーインスタンスのホストとポートに置き換えます。
1. `/oak:index` に移動します。 ノードを右クリックし、[!UICONTROL 作成] / [!UICONTROL &#x200B; ノードを作成]を選択します。
1. タイプ `oak:QueryIndexDefinition`の`customAFReferenceLuceneIndex-1`を作成します。
1. 上記の表のプロパティをインデックスノードに追加します。
1. インデックスノードの下に、次の子ノード階層を作成します。 すべての子ノードのタイプを`nt:unstructured`に設定します。

   ```text
   indexRules
       nt:unstructured
           properties
               resourceType
   ```

1. `resourceType`に、値`sling:resourceType`の`name` （文字列）と値`true`の`propertyIndex` （ブール値）を追加します。
1. [!UICONTROL すべて保存]を選択し、非同期インデックス作成を完了させます。

## クエリでインデックスが使用されていることを確認します {#verify-that-the-query-uses-the-index}

クエリプランを確認して、参照クエリでカスタムインデックスが選択されていることを確認します。

1. 非同期インデックス作成が完了したことを確認します。 [索引マネージャー](/help/sites-administering/operations-dashboard.md#the-index-manager)を使用して、索引の状態を調べます。
1. [!UICONTROL &#x200B; ツール &#x200B;] > [!UICONTROL 操作] > [!UICONTROL 診断] > [!UICONTROL &#x200B; クエリパフォーマンス &#x200B;]を開き、[!UICONTROL &#x200B; クエリの説明]を選択します。 XPath クエリ言語を選択し、次のように入力します。

   ```text
   /jcr:root/content//element(*, nt:unstructured)[
     (@sling:resourceType = 'fd/af/components/aemform'
     or jcr:like(@sling:resourceType, '%components/aemformscontainer%')
     or jcr:like(@sling:resourceType, '%components/adaptiveForm/fragment%'))]
   option (index tag aemformsAFReferences)
   ```

1. 「[!UICONTROL 説明]」を選択します。 クエリのブランチに対して、トラバーサル プランではなく`lucene:customAFReferenceLuceneIndex-1`と`/oak:index/customAFReferenceLuceneIndex-1`、または選択したインデックス名が使用されていることを確認します。 詳しくは、[&#x200B; クエリの説明](/help/sites-administering/operations-dashboard.md#explain-query)を参照してください。
1. 警告を生成したエクスペリエンスフラグメント公開操作を繰り返します。 `com.adobe.aem.formsndocuments.publish.AssetReferenceProvider.resolvePathsToFindReferences`からの新しいトラバーサル警告について、`error.log`を確認してください。

プランでカスタムインデックスが選択されない場合は、上記の例に照らして、タグ、`indexRules`階層、`sling:resourceType` プロパティ定義を確認してください。 詳しい診断については、[Oak インデックスのトラブルシューティング &#x200B;](/help/sites-deploying/troubleshooting-oak-indexes.md)を参照してください。

## 関連タスク {#related-tasks}

クエリのパフォーマンスとインデックス設定について詳しくは、次を参照してください。

* [Oakのクエリとインデックス作成](/help/sites-deploying/queries-and-indexing.md)
* [クエリとインデックス作成のベストプラクティス](/help/sites-deploying/best-practices-for-queries-and-indexing.md)
* [低速クエリのトラブルシューティング](/help/sites-developing/troubleshooting-slow-queries.md)
