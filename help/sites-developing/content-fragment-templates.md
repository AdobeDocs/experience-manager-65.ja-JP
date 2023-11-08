---
title: コンテンツフラグメントテンプレート
seo-title: Content Fragment Templates
description: コンテンツフラグメントを作成する際にテンプレートを選択し、新しいフラグメントに基本的な構造、要素、バリエーションを提供します。
seo-description: Templates are selected when creating a content fragmen and provide the new fragment with the basic structure, element, and variation
uuid: d147bac8-b710-40ed-9664-decb5ffcf8e7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: a975ea2e-5e24-4a96-bd62-63bb98836ff2
docset: aem65
exl-id: 1b75721c-b223-41f0-88d9-bd855b529f31
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 61%

---

# コンテンツフラグメントテンプレート{#content-fragment-templates}

>[!CAUTION]
>
>[コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)は、すべてのコンテンツフラグメントの新規作成で使用することが推奨されています。
>
>コンテンツフラグメントモデルは、WKND のすべてのサンプルでも使用されています。

>[!NOTE]
>
>AEM 6.3 以前は、モデルではなくテンプレートに基づいてコンテンツフラグメントを作成していました。
>
>コンテンツフラグメントテンプレートは現在は廃止されています。フラグメントの作成には引き続き使用できますが、代わりにコンテンツフラグメントモデルを使用することをお勧めします。フラグメントテンプレートには新機能は追加されず、今後のバージョンで削除されます。

コンテンツフラグメントの作成時に、テンプレートが選択されます。 新しいフラグメントには、基本的な構造、要素およびバリエーションが提供されます。 コンテンツフラグメントに使用するテンプレートは、Granite 設定マネージャーに依存しています。

既製のテンプレートは次の場所に保持されます。

* `/libs/settings/dam/cfm/templates`

次の場所に、サイト固有のコンテンツフラグメントテンプレートを作成できます。

* `/apps/settings/dam/cfm/templates`
既製のテンプレートをオーバーレイしたり、実行時に拡張／変更されないお客様固有のアプリケーションレベルのテンプレートを提供したりするための場所です。

* `/conf/global/settings/dam/cfm/templates`
実行時に変更する必要があるお客様固有のインスタンスレベルのテンプレートを提供するための場所です。

優先順位は（上から順に）`/conf`、`/apps`、`/libs` です。

>[!CAUTION]
>
>`/libs` パス内の設定は&#x200B;***一切***&#x200B;変更しないでください。
>
>`/libs` コンテンツは、インスタンスを次回アップグレードするとき（場合によってはホットフィックスまたは機能パックを適用したとき）に上書きされるからです。
>
>設定およびその他の変更に推奨される方法は次のとおりです。
>
>1. 必要な項目（内に存在）を再作成します。 `/libs`) （下） `/apps`
>
>1. `/apps` 内で変更作業を行う
>

テンプレートの基本構造は、次の場所に保持されます。

```xml
conf
  global
    settings
      dam
        cfm
          templates
            <template-name>
              ...
```

特定の構造は次のようになります。

```xml
+ <template-name>
    - jcr:primaryType
    - jcr:title
    - jcr:description
    - initialAssociatedContent
    - precreateElements
    - version
    + elements
        - jcr:primaryType
        + <element-name>
            - jcr:primaryType
            - jcr:title
            - defaultContent
            - initialContentType
            - name
        ... + other element definitions
    + variations
        - jcr:primaryType
        + <variation-name>
            - jcr:primaryType
            - jcr:title
            - jcr:description
            - name
        ... + other variation definitions
```

ノードとプロパティの詳細を以下に示します。

* **テンプレート**

  <table>
   <tbody>
    <tr>
     <th>名前</th>
     <th>タイプ</th>
     <th>値</th>
    </tr>
    <tr>
     <td><code>&lt;<em>template-name</em>&gt;</code></td>
     <td><code>nt:unstructured</code></td>
     <td>このノードは、各テンプレートのルートです。 これは必須で、一意の名前を持つ必要があります。</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>必須<br /> </p> </td>
     <td>テンプレートのタイトル ( <strong>フラグメントを作成</strong> ウィザード ) を使用します。</td>
    </tr>
    <tr>
     <td><code>jcr:description</code></td>
     <td><p><code>String</code></p> <p>オプション</p> </td>
     <td>テンプレートの目的を説明するテキスト ( <strong>フラグメントを作成</strong> ウィザード ) を使用します。</td>
    </tr>
    <tr>
     <td><code>initialAssociatedContent</code></td>
     <td><p><code>String[]</code></p> <p>オプション</p> </td>
     <td>デフォルトで新しく作成されたコンテンツフラグメントに関連付ける必要があるコレクションへのパスを含む配列。</td>
    </tr>
    <tr>
     <td><code>precreateElements</code></td>
     <td><p><code>Boolean</code></p> <p>必須</p> </td>
     <td><p><code>true</code>コンテンツフラグメントの作成時に、コンテンツフラグメントの要素（マスター要素を除く）を表すサブアセットを作成する必要がある場合は、その場で作成する場合は <em>false</em> に設定します。</p> <p><strong>注意</strong>：現在、このパラメーターは <code>true</code> に設定する必要があります。</p> </td>
    </tr>
    <tr>
     <td><code>version</code></td>
     <td><p><code>Long</code></p> <p>必須</p> </td>
     <td><p>コンテンツ構造のバージョン。現在サポートされています：</p> <p><strong>注意</strong>：現在、このパラメーターは <code>2</code> に設定する必要があります。<br /> </p> </td>
    </tr>
   </tbody>
  </table>

* **要素**

  <table>
   <tbody>
    <tr>
     <th>名前</th>
     <th>タイプ</th>
     <th>値</th>
    </tr>
    <tr>
     <td><code>elements</code><br /> </td>
     <td><p><code>nt:unstructured</code></p> <p>必須</p> </td>
     <td><p>コンテンツフラグメントの要素の定義を含むノード。 このノードは必須で、<strong>メイン</strong>要素の子ノードを 1 つ以上格納する必要がありますが、格納できる子ノードは [1..n] 個の子ノード。</p> <p>テンプレートを使用すると、要素のサブブランチがフラグメントのモデルのサブブランチにコピーされます。</p> <p>CRXDE Lite に表示される最初の要素は、自動的にメイン要素と見なされます。ノード名に意味はなく、メインアセットによって表されるという点を除き、ノード自体に特別な重要性はありません。その他の要素はサブアセットとして扱われます<i>。</i></p> </td>
    </tr>
   </tbody>
  </table>

* **要素名**

  <table>
   <tbody>
    <tr>
     <th>名前</th>
     <th>タイプ</th>
     <th>値</th>
    </tr>
    <tr>
     <td><code>&lt;<i>element-name</i>&gt;</code></td>
     <td><code>nt:unstructured</code></td>
     <td>このノードは要素を定義します。 これは必須で、一意の名前を持つ必要があります。</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>必須</p> </td>
     <td>要素のタイトル（フラグメントエディターの要素セレクターに表示されます）。</td>
    </tr>
    <tr>
     <td><code>defaultContent</code></td>
     <td><p><code>String</code></p> <p>オプション</p> <p>デフォルト：""</p> </td>
     <td>要素の初期コンテンツで、<code>precreateElements</code><i> = </i><code>true</code> の場合にのみ使用されます。</td>
    </tr>
    <tr>
     <td><code>initialContentType</code></td>
     <td><p><code>String</code></p> <p>オプション</p> <p>デフォルト： <code>text/html</code></p> </td>
     <td><p>要素の初期コンテンツタイプで、<code>precreateElements</code><i> = </i><code>true</code> の場合にのみ使用されます。現在、次のタイプがサポートされています。</p>
      <ul>
       <li><code>text/html</code></li>
       <li><code>text/plain</code></li>
       <li><code>text/x-markdown</code></li>
      </ul> </td>
    </tr>
    <tr>
     <td><code>name</code></td>
     <td><p><code>String</code></p> <p>必須</p> </td>
     <td>要素の内部名。フラグメントタイプに対して一意である必要があります。</td>
    </tr>
   </tbody>
  </table>

* **バリエーション**

  <table>
   <tbody>
    <tr>
     <th>名前</th>
     <th>タイプ</th>
     <th>値</th>
    </tr>
    <tr>
     <td><code>variations</code><br /> </td>
     <td><p><code>nt:unstructured</code></p> <p>オプション</p> </td>
     <td>このオプションのノードには、コンテンツフラグメントの初期バリエーションの定義が含まれます。</td>
    </tr>
   </tbody>
  </table>

* **バリエーション名**

  <table>
   <tbody>
    <tr>
     <th>名前</th>
     <th>タイプ</th>
     <th>値</th>
    </tr>
    <tr>
     <td><code>&lt;<i>variation-name</i>&gt;</code><br /> </td>
     <td><p><code>nt:unstructured</code></p> <p>バリエーションノードが存在する場合は必須</p> </td>
     <td><p>初期バリエーションを定義します。<br /> バリエーションは、デフォルトでコンテンツフラグメントのすべての要素に追加されます。</p> <p>バリエーションは、それぞれの要素と同じ初期コンテンツを持ちます（<code class="code">defaultContent/
       initialContentType</code> を参照してください）。</p> </td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>必須</p> </td>
     <td>バリエーションのタイトル ( フラグメントエディターの <strong>バリエーション</strong> タブ（左側のレール）を使用 ) に切り替えます。</td>
    </tr>
    <tr>
     <td><code>jcr:desciption</code></td>
     <td><p><code>String</code></p> <p>オプション</p> <p>デフォルト：""</p> </td>
     <td>バリエーションを説明するテキスト<span>（フラグメントエディターの「<strong>バリエーション</strong>」タブ（左レール）に表示されます）。</code></td>
    </tr>
   </tbody>
  </table>
