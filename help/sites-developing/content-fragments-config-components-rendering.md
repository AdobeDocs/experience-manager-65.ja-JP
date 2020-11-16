---
title: レンダリングコンポーネントのコンテンツフラグメントの設定
seo-title: レンダリングコンポーネントのコンテンツフラグメントの設定
description: レンダリングコンポーネントのコンテンツフラグメントの設定
seo-description: レンダリングコンポーネントのコンテンツフラグメントの設定
uuid: 3f5aaf36-e6a7-4a3c-b305-e35ebcc98d0d
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 2aef9048-9d6e-4f5d-b443-5e73f8066d76
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 86%

---


# レンダリングコンポーネントのコンテンツフラグメントの設定{#content-fragments-configuring-components-for-rendering}

コンテンツフラグメントのレンダリングには、いくつかの[アドバンスドサービス](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration)があります。これらのサービスを使用するには、そのようなコンポーネントのリソースタイプが、コンテンツフラグメントフレームワークに存在を認識させる必要があります。

これは、[OSGi サービス - コンテンツフラグメントコンポーネントの設定](#osgi-service-content-fragment-component-configuration)を設定しておこないます。

>[!CAUTION]
>
>以下に説明する[アドバンスドサービス](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration)が必要ない場合、この設定は無視できます。

>[!CAUTION]
>
>標準搭載のコンポーネントを拡張または使用する場合、 の設定を変更しないことをお勧めします。

>[!CAUTION]
>
>アドバンスドサービスを使用することなく、コンテンツフラグメント API のみを使用するコンポーネントを新規に作成できます。ただし、この場合は、適切な処理をおこなうようにコンポーネントを開発する必要がありますので、
>
>したがって、コアコンポーネントを使用することをお勧めします。

## 設定が必要なアドバンスドサービスの定義 {#definition-of-advanced-services-that-need-configuration}

コンポーネントの登録を必要とするサービスは、次のとおりです。

* 公開中に依存関係を正しく判断する（前回の公開後に変更が加えられた場合は、フラグメントとモデルをページで自動的に公開できることを確認）。
* フルテキスト検索でのコンテンツフラグメントのサポート。
* *中間コンテンツ*&#x200B;の管理および処理。
* *混在メディアアセット*&#x200B;の管理および処理。
* Dispatcher は、参照されるフラグメントをフラッシュします（フラグメントを含むページが再度公開される場合）。
* 段落ベースのレンダリングの使用

これらの機能の1つ以上が必要な場合は（通常）、標準搭載された機能を一から開発する代わりに（標準）使用する方が簡単です。

## OSGi サービス - コンテンツフラグメントコンポーネントの設定 {#osgi-service-content-fragment-component-configuration}

設定は、OSGi サービス&#x200B;**コンテンツフラグメントコンポーネントの設定**&#x200B;に結び付ける必要があります。

`com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl`

>[!NOTE]
>
>詳細は、「OSGiの [設定](/help/sites-deploying/configuring-osgi.md) 」を参照してください。

次に例を示します。

![cfm-01](assets/cfm-01.png)

OSGi の設定は次のとおりです。

<table>
 <tbody>
  <tr>
   <td>ラベル</td>
   <td>OSGi 設定<br /> </td>
   <td>説明</td>
  </tr>
  <tr>
   <td><strong>リソースタイプ</strong></td>
   <td><code>dam.cfm.component.resourceType</code></td>
   <td>登録するリソースの種類。例：<br /> <p><span class="cmp-examples-demo__property-value"><code>core/wcm/components/contentfragment/v1/contentfragment</code></code></p> </td>
  </tr>
  <tr>
   <td><strong>参照のプロパティ</strong></td>
   <td><code>dam.cfm.component.fileReferenceProp</code></td>
   <td>フラグメントへの参照を含むプロパティの名前。例：<code>fragmentPath</code> <code>fileReference</code></td>
  </tr>
  <tr>
   <td><strong>要素のプロパティ</strong></td>
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

一部の機能（例えば、段落範囲のみをレンダリングする場合など）では、いくつかの規則に従う必要があります。

<table>
 <tbody>
  <tr>
   <td>プロパティ名</td>
   <td>説明</td>
  </tr>
  <tr>
   <td><code>paragraphRange</code></td>
   <td><p><em>単一要素のレンダリングモード</em>の場合に出力される段落の範囲を定義する string プロパティ。</p> <p>形式：</p>
    <ul>
     <li><code>1</code> または <code>1-3</code> または <code>1-3;6;7-8</code> または <code>*-3;5-*</code></li>
     <li><code>paragraphScope</code> が次のように設定されている場合のみ利用可能 <code>range</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphScope</code></td>
   <td><p><em>単一要素のレンダリングモード</em>で段落を出力する方法を定義する string プロパティ。</p> <p>値：</p>
    <ul>
     <li><code>all</code> ：すべての段落をレンダリング</li>
     <li><code>range</code> ：次によって提供される段落の範囲をレンダリング <code>paragraphRange</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphHeadings</code></td>
   <td>見出し（例えば、<code>h1</code>、<code>h2</code>、<code>h3</code> など）を段落としてカウントするか（<code>true</code>）、カウントしないか（<code>false</code>）を定義する boolean プロパティ。</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>これは、6.5以降のマイルストーンで変更される可能性があります。

## 例 {#example}

例として、次を参照してください（標準搭載の AEM インスタンス上）。

```
/apps/core/wcm/config/com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl-core-comp-v1.config
```

次を含む：

```
dam.cfm.component.resourceType="core/wcm/components/contentfragment/v1/contentfragment"
dam.cfm.component.fileReferenceProp="fragmentPath"
dam.cfm.component.elementsProp="elementName"
dam.cfm.component.variationProp="variationName"
```

