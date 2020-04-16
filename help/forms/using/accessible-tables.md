---
title: アクセス可能な複雑なテーブルを HTML5 フォームで作成する
seo-title: アクセス可能な複雑なテーブルを HTML5 フォームで作成する
description: アクセス可能なテーブルを HTML5 フォームで作成する方法について説明します。
seo-description: アクセス可能なテーブルを HTML5 フォームで作成する方法について説明します。
uuid: e52562d2-4dc3-4359-9dbb-c18614921808
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 3504afe1-abf5-4fbf-a0d2-e093361764bd
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3

---


# アクセス可能な複雑なテーブルを HTML5 フォームで作成する {#create-accessible-complex-tables-in-html-forms}

HTML5 フォームでのテーブルのデフォルト実装では、テーブルのレンダリングに HTML DIV 要素が使用されます。さらに、アクセシビリティ要件を満たす目的で ARIA ロールも使用されます。

データテーブルで使用されるARIAの役割を完全にサポートしていないスクリーンリーダーでのアクセシビリティの問題を回避するため、HTML5フォームでは、テーブルの代替レンディションを提供しています。 これらのテーブルは、Designer で導入された新しいテーブル形式に基づいており、次の項目もサポートしています。

* 行ヘッダー
* 行幅

HTML5 フォームで新しい形式を使用するには、テーブルを複雑なテーブルとしてマークする必要があります。複雑なテーブルとしてマークするには、テーブルのサブフォームの XML ソースに `extras` タグを次のように追加します。

```
</extras>
 <text name="complexTable">1</text>
 </extras>
```

The tables which are marked as *complexTable* follow the native HTML rendition, and provide better accessibility support for certain screen readers.  行幅を作成するには、テーブル内の 1 つの列で連続する複数のセルを選択し、選択範囲を右クリックして、「**[!UICONTROL セルの結合]**」をクリックします。

>[!NOTE]
>
>行幅の作成は、一番左のセルに対してのみ機能します。

行を行ヘッダーとしてマークするには、その行のすべてのセルを選択し、選択範囲を右クリックして、「**[!UICONTROL ヘッダーをマーク]**」をクリックします。

セルを列ヘッダーとしてマークするには、その列内の任意のセルを選択し、選択範囲を右クリックして、「**[!UICONTROL ヘッダーをマーク]**」をクリックします。

Limitations in new *AccessibleTable* format:

* テーブルに行幅を設定する場合は、拡大可能なフィールドを使用できない
* ネストされたテーブル（テーブルのセルに含まれている別のテーブル）は使用できない
* 行幅はヘッダー行とヘッダーセルのみに適用できる
* 使用可能なテーブルは標準テーブルのみである
* 行幅が 1 を超えるテーブルではデータを事前入力できない

