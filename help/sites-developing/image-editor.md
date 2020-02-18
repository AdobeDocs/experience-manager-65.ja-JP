---
title: 画像エディター
seo-title: 画像エディター
description: 画像エディターはAEMの中核的な要素で、コンポーネントを使用して、コンテンツ作成者による画像の操作を容易にすることができます。
seo-description: 画像エディターはAEMの中核的な要素で、コンポーネントを使用して、コンテンツ作成者による画像の操作を容易にすることができます。
uuid: de6ac71b-380a-4b67-b697-ac34a79a9cc4
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: f6347492-cf48-4835-b8fd-ce9a75a09abe
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 画像エディター{#image-editor}

画像エディターはAEMの中核的な要素で、コンポーネントを使用して、コンテンツ作成者による画像の操作を容易にすることができます。

>[!CAUTION]
>
>この記事で説明するイメージエディタの機能を使用するには、機能パック24267 [をインストールする必要があります](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/featurepack/cq-6.4.0-featurepack-24267) 。

## 画像マップの相対単位 {#relative-units-for-image-map}

画像エディタは、画像マップ領域を絶対単位と相対単位の両方として保持します。 相対単位は、レスポンシブ画像コンポーネントのクライアント側で画像マップのサイズを動的に（画像サイズに対して）変更するデータ属性として指定する場合に役立ちます。

### imageMapプロパティ {#imagemap-property}

画像マップの座標は、画像エディターによってプロパティとし `imageMap` てJCRに保持されます。 形式は次のとおりです。

このプロパティは、マップ領域を次のように格納します。

`[area1][area2][...]`

面の形式：

`[SHAPE(COORDINATES)"HREF"|"TARGET"|"ALT"|(RELATIVE_COORDINATES)]`

例:

`[rect(0,0,10,10)"https://www.adobe.com"|"_self"|"alt"|(0,0,0.8,0.8)]`
`[circle(10,10,10)"https://www.adobe.com"|"_self"|"alt"|(0.8,0.8,0.8)]`

## SVG画像のサポート {#support-for-svg-images}

Scalable Vector Graphics(SVG)は、画像エディターでサポートされています。

* DAM からの SVG アセットのドラッグ＆ドロップと、ローカルファイルシステムからの SVG ファイルのアップロード、はどちらもサポートされます。

## MIMEタイプ別のプラグインの有効化 {#enabling-plugins-by-mime-type}

特定の状況では、サーバー側処理のサポートがないため、特定のMIMEタイプに対してオーサリングアクションを制限する必要があります。 例えば、SVG画像の編集は許可されない場合があります。

画像エディター内のプラグインは、個々のプラグインの設定ノードでプロパティを設定することにより、MIMEタ `supportedMimeTypes` イプによって選択的に有効にすることができます。

### 例 {#example}

例えば、切り抜き機能はGIF、JPEG、PNG、WEBPおよびTIFF画像に対してのみ許可する必要があるとします。

次に、 `supportedMimeTypes` このプロパティを、画像コンポーネントのノード上のプラグインの設定ノードで許可されているMIMEタイプの文字列とし `cq:editConfig` て設定する必要があります。

`/apps/core/wcm/components/image/v2/image/cq:editConfig`

```xml
 jcr:primaryType="cq:EditConfig">
     <cq:dropTargets jcr:primaryType="nt:unstructured">
         <image ...>
            ...
         </image>
     </cq:dropTargets>
     <cq:inplaceEditing
         jcr:primaryType="cq:InplaceEditingConfig"
         active="{Boolean}true"
         editorType="image">
         <config jcr:primaryType="nt:unstructured">
             <plugins jcr:primaryType="nt:unstructured">
                 <crop
                     jcr:primaryType="nt:unstructured"
                     supportedMimeTypes="[image/gif,image/jpeg,image/png,image/webp,image/tiff]"
                     features="*">
                     <aspectRatios jcr:primaryType="nt:unstructured">
                        ...
                     </aspectRatios>
                 </crop>
                 ...
             </plugins>
             <ui jcr:primaryType="nt:unstructured">
                 ...
             </ui>
         </config>
     </cq:inplaceEditing>
 </jcr:root>
```

