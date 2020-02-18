---
title: コンテンツフラグメントレンダリング用のコンポーネントの設定
seo-title: コンテンツフラグメントレンダリング用のコンポーネントの設定
description: コンテンツフラグメントレンダリング用のコンポーネントの設定
seo-description: コンテンツフラグメントレンダリング用のコンポーネントの設定
uuid: 3f5aaf36-e6a7-4a3c-b305-e35ebcc98d0d
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 2aef9048-9d6e-4f5d-b443-5e73f8066d76
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# コンテンツフラグメントレンダリング用のコンポーネントの設定{#content-fragments-configuring-components-for-rendering}

コンテンツフラグメ [ントのレンダリングに](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration) 、いくつかの高度なサービスがあります。 これらのサービスを使用するには、そのようなコンポーネントのリソースタイプがコンテンツフラグメントフレームワークに対して自らを認識する必要があります。

これは、 [OSGiサービス — コンテンツフラグメントコンポーネントの設定で行います](#osgi-service-content-fragment-component-configuration)。

>[!CAUTION]
>
>以下に説明する高度なサービス [が不要な場合](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration) 、この設定は無視できます。

>[!CAUTION]
>
>標準搭載のコンポーネントを拡張する場合や使用する場合は、設定を変更しないことをお勧めします。

>[!CAUTION]
>
>高度なサービスを使用しないで、コンテンツフラグメントAPIのみを使用するコンポーネントを新規に作成できます。 ただし、このような場合は、適切な処理を行えるようにコンポーネントを開発する必要があります。
>
>したがって、コアコンポーネントを使用することをお勧めします。

## 設定が必要なアドバンスサービスの定義 {#definition-of-advanced-services-that-need-configuration}

コンポーネントの登録を必要とするサービスは次のとおりです。

* 発行中に依存関係を正しく判断する（例えば、前回の発行以降に変更があった場合は、フラグメントとモデルをページと共に自動的に発行できるようにする）。
* 全文検索でのコンテンツフラグメントのサポート。
* 中間コンテンツの *管理/処理。*
* 混在メディアアセットの *管理/処理。*
* ディスパッチャーは、参照先のフラグメントをフラッシュします（フラグメントを含むページが再公開される場合）。
* 段落ベースのレンダリングを使用する。

これらの機能が1つ以上必要な場合は（通常）、初期設定の機能を使用する方が、一から開発するよりも簡単です。

## OSGiサービス — コンテンツフラグメントコンポーネントの設定 {#osgi-service-content-fragment-component-configuration}

設定は、OSGiサービスコンテンツフラグメントコンポーネントの設定にバ **インドする必要があります**。

`com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl`

>[!NOTE]
>
>詳しく [は、「OSGiの設定](/help/sites-deploying/configuring-osgi.md) 」を参照してください。

次に例を示します。

![cfm-01](assets/cfm-01.png)

OSGiの設定は次のとおりです。

<table>
 <tbody>
  <tr>
   <td>ラベル</td>
   <td>OSGi設定<br /> </td>
   <td>説明</td>
  </tr>
  <tr>
   <td><strong>リソースタイプ</strong></td>
   <td><code>dam.cfm.component.resourceType</code></td>
   <td>登録するリソースの種類例： <br /> <p><span class="cmp-examples-demo__property-value"><code>core/wcm/components/contentfragment/v1/contentfragment</code></code></p> </td>
  </tr>
  <tr>
   <td><strong>Referenceプロパティ</strong></td>
   <td><code>dam.cfm.component.fileReferenceProp</code></td>
   <td>フラグメントへの参照を含むプロパティの名前。例えば、 <code>fragmentPath</code> <code>fileReference</code></td>
  </tr>
  <tr>
   <td><strong>Element(s)プロパティ</strong></td>
   <td><code>dam.cfm.component.elementsProp</code></td>
   <td>レンダリングする要素の名前を含むプロパティの名前。例：<code>elementName</code></td>
  </tr>
  <tr>
   <td><strong>バリエーションのプロパティ</strong><br /> </td>
   <td><code>dam.cfm.component.variationProp</code></td>
   <td>レンダリングするバリエーションの名前を含むプロパティの名前。例：<code>variationName</code></td>
  </tr>
 </tbody>
</table>

一部の機能（例えば、段落範囲のみをレンダリングする場合）では、次の規則に従う必要があります。

<table>
 <tbody>
  <tr>
   <td>プロパティ名</td>
   <td>説明</td>
  </tr>
  <tr>
   <td><code>paragraphRange</code></td>
   <td><p>単一要素のレンダリングモードの場合に出力する段落の範囲を定義する <em>stringプロパティ</em>。</p> <p>形式:</p>
    <ul>
     <li><code>1</code> また <code>1-3</code> は <code>1-3;6;7-8</code> <code>*-3;5-*</code></li>
     <li>が <code>paragraphScope</code> <code>range</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphScope</code></td>
   <td><p>単一要素のレンダリングモードで段落を出力する方法を定義する <em>stringプロパティ</em>。</p> <p>値:</p>
    <ul>
     <li><code>all</code> :すべての段落をレンダリングする</li>
     <li><code>range</code> :段落の範囲を描く <code>paragraphRange</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphHeadings</code></td>
   <td>見出し（例えば、、、など）を段落( <code>h1</code><code>h2</code>)とし <code>h3</code>てカウントするか(<code>true</code>)、カウントしないか(<code>false</code>)を定義するbooleanプロパティ</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>これは、以降の6.5マイルストーンで変更される可能性があります。

## 例 {#example}

例として、次を参照してください（標準搭載のAEMインスタンス上）。

```
/apps/core/wcm/config/com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl-core-comp-v1.config
```

次を含みます。

```
dam.cfm.component.resourceType="core/wcm/components/contentfragment/v1/contentfragment"
dam.cfm.component.fileReferenceProp="fragmentPath"
dam.cfm.component.elementsProp="elementName"
dam.cfm.component.variationProp="variationName"
```

