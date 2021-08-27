---
title: コンテンツフラグメントテンプレート
seo-title: Content Fragment Templates
description: テンプレートは、コンテンツフラグメントの作成時に選択され、新しいフラグメントに基本構造、要素、バリエーションを提供します
seo-description: Templates are selected when creating a content fragmen and provide the new fragment with the basic structure, element, and variation
uuid: d147bac8-b710-40ed-9664-decb5ffcf8e7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: a975ea2e-5e24-4a96-bd62-63bb98836ff2
docset: aem65
exl-id: 1b75721c-b223-41f0-88d9-bd855b529f31
source-git-commit: 2ec9625d480eb8cae23f44aa247fce2a519dec31
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 79%

---

# コンテンツフラグメントテンプレート{#content-fragment-templates}

>[!CAUTION]
>
>[コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)は、すべてのフラグメント作成で使用することが推奨されています。
>
>コンテンツフラグメントモデルは、We.Retail のすべてのサンプルでも使用されています。

>[!NOTE]
>
>AEM 6.3より前のコンテンツフラグメントは、モデルの代わりにテンプレートを使用して作成されていました。 新しいフラグメントを作成する際に、テンプレートは使用できなくなりましたが、そのようなテンプレートで作成されたフラグメントは引き続きサポートされます。

コンテンツフラグメントの作成時に選択されるテンプレートです。このテンプレートは、新しいフラグメントに基本構造、要素、バリエーションを提供します。コンテンツフラグメントに使用されるテンプレートは、Granite 設定マネージャーに従います。

既製のテンプレートは次の場所に保持されます。

* `/libs/settings/dam/cfm/templates`

次の場所に、サイト固有のコンテンツフラグメントテンプレートを作成できます。

* `/apps/settings/dam/cfm/templates`
標準のテンプレートをオーバーレイする場所、または実行時に拡張/変更することを意図していない、顧客固有のアプリケーション全体のテンプレートを提供する場所。

* `/conf/global/settings/dam/cfm/templates`
実行時に変更する必要がある、インスタンス全体の顧客固有のテンプレートの場所。

優先順位は（降順に）`/conf`、`/apps`、`/libs`です。

>[!CAUTION]
>
>`/libs` パス内の設定は&#x200B;***一切***&#x200B;変更しないでください。
>
>`/libs` コンテンツは、インスタンスを次回アップグレードするとき（場合によってはホットフィックスまたは機能パックを適用したとき）に上書きされるからです。
>
>設定およびその他の変更に推奨される方法は次のとおりです。
>
>1. `/apps`の下で、必要な項目（`/libs`に存在）を再作成します。
>
>1. `/apps` 内で変更作業をおこないます。

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

具体的な構造は次のようになります。

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
     <td>このノードは各テンプレートのルートです。このノードは必須で、一意の名前が必要です。</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>required<br /> </p> </td>
     <td>テンプレートのタイトル（<strong>フラグメントを作成</strong>ウィザードに表示されます）。</td>
    </tr>
    <tr>
     <td><code>jcr:description</code></td>
     <td><p><code>String</code></p> <p>オプション</p> </td>
     <td>テンプレートの目的を説明するテキスト（<strong>フラグメントを作成</strong>ウィザードに表示されます）。</td>
    </tr>
    <tr>
     <td><code>initialAssociatedContent</code></td>
     <td><p><code>String[]</code></p> <p>オプション</p> </td>
     <td>新規作成されたコンテンツフラグメントにデフォルトで関連付ける必要があるコレクションへのパスが格納された配列です。</td>
    </tr>
    <tr>
     <td><code>precreateElements</code></td>
     <td><p><code>Boolean</code></p> <p>required</p> </td>
     <td><p><code>true</code>コンテンツフラグメントの要素（マスター要素を除く）を表すサブアセットをコンテンツフラグメントの作成時に作成する必要がある場合は 、、そのつど作成する場合は <em>false</em> に設定します。</p> <p><strong>注意</strong>：現在、このパラメーターは <code>true</code> に設定する必要があります。</p> </td>
    </tr>
    <tr>
     <td><code>version</code></td>
     <td><p><code>Long</code></p> <p>必須</p> </td>
     <td><p>コンテンツ構造のバージョン。現在サポートされています。</p> <p><strong>注意</strong>:現在、このパラメーターはに設定する必要があり <code>2</code>ます。<br /> </p> </td>
    </tr>
   </tbody>
  </table>

* **エレメント**

   <table>
   <tbody>
    <tr>
     <th>名前</th>
     <th>タイプ</th>
     <th>値</th>
    </tr>
    <tr>
     <td><code>elements</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>必須</p> </td>
     <td><p>コンテンツフラグメントの要素の定義を格納するノードです。必須で、<strong>Main</strong>要素の子ノードを少なくとも1つ含める必要がありますが、[1...n] 個です。</p> <p>テンプレートを使用すると、要素のサブブランチがフラグメントのモデルのサブブランチにコピーされます。</p> <p>CRXDE Lite に表示される最初の要素は、自動的にメイン要素<i></i>と見なされます。ノード名に意味はなく、メインアセットによって表されるという点を除き、ノード自体に特別な重要性はありません。その他の要素はサブアセットとして扱われます。</p> </td>
    </tr>
   </tbody>
  </table>

* **エレメント名**

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
     <td>このノードは要素を定義します。このノードは必須で、一意の名前が必要です。</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>必須</p> </td>
     <td>要素のタイトルです（フラグメントエディターの要素セレクターに表示されます）。</td>
    </tr>
    <tr>
     <td><code>defaultContent</code></td>
     <td><p><code>String</code></p> <p>オプション</p> <p>default: ""</p> </td>
     <td>要素の初期コンテンツ<code>precreateElements</code><i> = </i><code>true</code>の場合にのみ使用されます。</td>
    </tr>
    <tr>
     <td><code>initialContentType</code></td>
     <td><p><code>String</code></p> <p>オプション</p> <p>default: <code>text/html</code></p> </td>
     <td><p>要素の初期コンテンツタイプ<code>precreateElements</code><i> = </i><code>true</code>;現在サポートされている：</p>
      <ul>
       <li><code>text/html</code></li>
       <li><code>text/plain</code></li>
       <li><code>text/x-markdown</code></li>
      </ul> </td>
    </tr>
    <tr>
     <td><code>name</code></td>
     <td><p><code>String</code></p> <p>必須</p> </td>
     <td>要素の初期名で、フラグメントタイプに対して一意である必要があります。</td>
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
     <td><code>variations</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>オプション</p> </td>
     <td>このオプションのノードには、コンテンツフラグメントの初期バリエーションの定義が格納されます。</td>
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
     <td><code>&lt;<i>variation-name</i>&gt;</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>バリエーションノードが存在する場合は必須</p> </td>
     <td><p>初期バリエーションを定義します。<br />バリエーションは、デフォルトでコンテンツフラグメントのすべての要素に追加されます。</p> <p>バリエーションは、それぞれの要素と同じ初期コンテンツを持ちます（<code class="code">defaultContent/
       initialContentType</code> または   を参照してください）。</p> </td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>必須</p> </td>
     <td>バリエーションのタイトルです（フラグメントエディターの「<strong>バリエーション</strong>」タブ（左レール）に表示されます）。</td>
    </tr>
    <tr>
     <td><code>jcr:desciption</code></td>
     <td><p><code>String</code></p> <p>オプション</p> <p>デフォルト：""</p> </td>
     <td>バリエーションを説明するテキスト<span>（フラグメントエディターの「<strong>バリエーション</strong>」タブ（左レール）に表示されます）。</code></td>
    </tr>
   </tbody>
  </table>
