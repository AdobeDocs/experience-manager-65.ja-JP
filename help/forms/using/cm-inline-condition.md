---
title: インタラクティブ通信とレターのインライン条件と繰り返し構造
seo-title: Inline condition and repeat in Interactive Communications and letters
description: インタラクティブ通信とレターでインライン条件と繰り返しを使用すると、コンテキストに応じた、適切に構造化された通信を作成できます。
seo-description: Using inline condition and repeat in Interactive Communications and letters, you can create communications that are highly contextual and well structured.
uuid: 32b48a8b-431d-4f9c-9f51-8e7e9ac624a0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4
topic-tags: interactive-communications, correspondence-management
discoiquuid: bbaba39b-e15a-4143-b6fc-7789fa2917b4
docset: aem65
feature: Correspondence Management
exl-id: bc5d6c5b-c833-4849-aace-e07f8a522b32
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1659'
ht-degree: 32%

---

# インタラクティブ通信とレターのインライン条件と繰り返し構造{#inline-condition-and-repeat-in-interactive-communications-and-letters}

## インライン条件 {#inline-conditions}

AEM Formsを使用すると、テキストモジュールでインライン条件を使用して、フォームデータモデル（インタラクティブ通信内）またはデータディクショナリ（レター内）に関連付けられたコンテキストやデータに依存するテキストのレンダリングを自動化できます。 インライン条件は、true または false の条件評価に基づいて特定のコンテンツを表示します。

条件は、フォームデータモデル/データディクショナリ (Data Dictionary) またはエンドユーザーが指定したデータ値に対して計算を実行します。 インライン条件を使用すると、状況に応じてパーソナライズされたインタラクティブ通信/レターを作成しながら、時間を節約し、人間のエラーを減らすことができます。

詳しくは、次を参照してください。

* [インタラクティブ通信を作成](../../forms/using/create-interactive-communication.md)
* [Correspondence Management の概要](/help/forms/using/cm-overview.md)
* [インタラクティブ通信内のテキスト](../../forms/using/texts-interactive-communications.md)

### 例：ルールを使用してインタラクティブ通信内のインラインテキストに条件を設定する {#example-using-rules-to-conditionalize-inline-text-in-interactive-communication}

インタラクティブ通信内の文、段落、または文字列に条件を設定するには、適切なテキストドキュメントフラグメント内にルールを作成します。 次の例では、インタラクティブ通信の米国の受信者にのみフリーダイヤル番号を表示するルールを使用します。

詳しくは、[インタラクティブ通信内のテキスト](../../forms/using/texts-interactive-communications.md)の「テキスト内でルールを作成する」を参照してください。

この例では、テキストフラグメントをインタラクティブ通信に含めると、エージェントがエージェント UI を使用してインタラクティブ通信の準備をおこない、受信者用のフォームデータモデルのデータが評価され、米国の受信者だけにテキストが表示されます。

### 例：レターでインライン条件を使用して適切なアドレスをレンダリングする  {#example-using-inline-condition-in-a-letter-to-render-the-appropriate-address}

インライン条件を適切なテキストモジュールに挿入することで、レターにインライン条件を挿入できます。 次の例では、DD 要素の性別に基づくレターで、適切な住所（Sir または Ma&#39;am）を評価して表示する 2 つの条件を使用します。 同様の手順を使用して、他の条件を作成できます。

>[!NOTE]
>
>既存のアセットに古い（6.2 SP1 CFP 4 より前の）条件式や繰り返し式が含まれている場合は、アセットに古い構文の条件や繰り返しが表示されます。ただし、古い条件や繰り返しも正常に機能します。新しい条件式／繰り返し式と古い条件式／繰り返し式は互換性があるため、新しい式と古い式を混在できます。

1. 関連するテキストモジュールで、条件を付けるテキスト部分を選択し、**条件**&#x200B;をタップします。

   ![1_selecttext](assets/1_selecttext.png)

   条件ダイアログボックスが開き、空の条件が表示されます。

   ![2_conditiondialog](assets/2_conditiondialog.png)

   >[!NOTE]
   >
   >空の条件式や無効な条件式は保存できません。条件式を保存するには、`${}` の内部に有効な条件式が必要です。

1. 次の手順を実行して、選択または条件付きのテキストがレターに表示されるかどうかを評価する条件を作成し、チェックマークをタップして式を保存します。

   DD 要素をダブルタップして、条件に挿入します。 適切な演算子を挿入し、ダイアログで次の条件を作成します。

   ```javascript
   ${DD_creditcard_Gender=="Male"}
   ```

   式の作成について詳しくは、 **式ビルダーを使用した式とリモート関数の作成** in [式ビルダー](../../forms/using/expression-builder.md). 式で指定された値は、データディクショナリの要素でサポートされている必要があります。 詳しくは、[データディクショナリ](../../forms/using/data-dictionary.md)を参照してください。

   条件を挿入したら、条件の左側にあるハンドルの上にマウスポインターを置くと、条件が表示されます。 ハンドルをタップすると、条件のポップアップメニューが表示され、条件を編集または削除できます。

   ![3_hoverhandle](assets/3_hoverhandle.png) ![4_editconditionremoveconditionpopup](assets/4_editconditionremoveconditionpopup.png)

1. テキスト `Ma'am` を選択して、同様の条件を挿入します。

   ```javascript
   ${DD_creditcard_Gender == "Female"}
   ```

1. 関連するレターをプレビューし、インライン条件に従ってテキストがレンダリングされることを確認します。 次を使用して、DD 要素の「性別」の値を入力できます。

   * サンプルデータを使用してレターをプレビューする際に、関連するデータディクショナリに基づいて作成されたサンプル XML データファイル。
   * 関連するデータディクショナリに添付される XML データファイル。

   詳しくは、[データディクショナリ](../../forms/using/data-dictionary.md)を参照してください。

   ![5_letteroutput](assets/5_letteroutput.png)

## 繰り返し {#repeat}

インタラクティブ通信とレターには、動的な情報を含めることができます。例えば、クレジットカードの取引明細書は、レターが生成されるたびに変化します。繰り返し構造を使用すると、テキストドキュメントフラグメント内で、こうした動的な情報の書式設定と構造化をおこなうことができます。

また、繰り返し構造内でルールや条件を指定して、インタラクティブ通信またはレター内でレンダリングされる情報やエントリに条件を設定することもできます。

### 例：インタラクティブ通信内で繰り返し構造を使用して、クレジットカードの取引情報リストの書式設定、構造化、表示をおこなう {#example-using-repeat-in-an-interactive-communication-to-format-structure-and-display-a-list-of-credit-card-transactions}

次の例では、繰り返しを使用して、インタラクティブ通信内のクレジットカードトランザクションを構築し、レンダリングする手順を示します。

1. フォームデータモデルベースのテキストドキュメントフラグメントで、関連するフォームデータモデルオブジェクト（およびこの例のように、ラベルに必要な埋め込みテキスト）を挿入します。

   ![1_elementstext](assets/1_elementstext.png)

   >[!NOTE]
   >
   >繰り返し可能なコンテンツには、コレクション型のプロパティを少なくとも 1 つ含める必要があります。

1. 繰り返しを適用するコンテンツを選択します。

   ![2_selection](assets/2_selection.png)

1. 「繰り返し」をタップします。

   繰り返しダイアログが表示されます。

   ![3_repeatdialog](assets/3_repeatdialog.png)

1. 必要に応じて、区切り文字として「改行」を選択し、「条件を追加」をタップしてルールを作成します。テキストを区切り文字として使用し、区切り文字として使用するテキスト文字を指定することもできます。

   ルール作成ダイアログが表示されます。

1. 2018 年 2 月 28 日以降に発生した取引情報を表示し、2018 年 3 月中に発生した取引情報だけをインタラクティブ通信に含めるためのルールを作成します。

   >[!NOTE]
   >
   >この例では、エージェントが 2018 年 3 月末に文を作成することを前提としています。 それ以外の場合は、2018 年 3 月以降のトランザクションを除外する2018-04-01前のトランザクションを含める別のルールを作成できます。

   ![4_createrule](assets/4_createrule.png)

1. 条件またはルールを保存し、繰り返しを保存します。 条件付き繰り返しが選択したコンテンツに適用されます。

   ![5_onmouseoverconditionrule](assets/5_onmouseoverconditionrule.png)

   テキストドキュメントフラグメントにマウスを置くと、条件と、コンテンツに適用される繰り返しで使用される区切り文字が表示されます。

1. テキストドキュメントフラグメントを保存し、関連するインタラクティブ通信をプレビューします。 フォームデータモデル内のデータに応じて、要素に適用されている繰り返し構造により、取引明細情報が以下のプレビュー画面のようにレンダリングされます。

   ![screen_shot_2018-03-09at155516copy](assets/screen_shot_2018-03-09at155516copy.png)

### 例：レターで繰り返しを使用して、クレジットカードトランザクションのリストを書式設定、構造化、表示する {#example-using-repeat-in-a-letter-to-format-structure-and-display-a-list-of-credit-card-transactions}

次の例では、繰り返しを使用して、レター内のクレジットカードトランザクションを構造化し、レンダリングする手順を示します。 同様の手順を使用すると、別のシナリオで繰り返しを使用できます。

1. 繰り返される/動的データをレンダリングし、必要なテキストを DD 要素の周囲に埋め込む DD 要素を持つテキストモジュールを（編集中または作成中に）開きます。 例えば、テキストモジュールには、クレジットカード上の取引明細書を作成する次の DD 要素が含まれています。

   ```javascript
   {^DD_creditcard_TransactionDate^} {^DD_creditcard_TransactionAmount^}
   {^DD_creditcard_TransactionType^}
   ```

   これらの DD 要素は、クレジットカード上で行われたトランザクションのリストを次の情報と共にレンダリングします。

   取引日、取引金額および取引タイプ（借方または貸方）

1. DD 要素内にテキストを埋め込んで、ステートメントがより読みやすくする（例：次のように）。

   ![1_repeat](assets/1_repeat.png)

   ```javascript
   Date: {^DD_creditcard_TransactionDate^} Amount (USD): {^DD_creditcard_TransactionAmount^} Transaction Type: {^DD_creditcard_TransactionType^}
   ```

   ただし、適切な形式の文をレンダリングするジョブはまだ実行されていません。 これまでの作業に基づいてレターをレンダリングすると、次のように表示されます。

   ![1_1renderwithoutrepeat](assets/1_1renderwithoutrepeat.png)

   DD 要素と共に静的テキストを繰り返すには、後の手順で説明するように繰り返しを適用する必要があります。

1. 次に示すように、繰り返す静的テキストと DD 要素を選択します。

   ![2_repeat_selecttext](assets/2_repeat_selecttext.png)

1. 「**繰り返し**」をタップします。繰り返しダイアログボックスが開き、空のインライン条件が表示されます。

   ![3_repeat_dialog](assets/3_repeat_dialog.png)

1. 必要に応じて、取引を選択的にレンダリングする（例えば、50 セントを超える取引額をレンダリングする）ための条件を挿入します。

   ```javascript
   ${DD_creditcard_TransactionAmount > 0.5}
   ```

   情報（ここでは取引）を選択的にレンダリングする必要がない場合は、ダイアログボックス内の `${}` を削除して条件を空にします。繰り返し式の保存は、繰り返し式ウィンドウが空（$を除く）の場合に有効になります{} 繰り返しが不要な場合 )、または繰り返しに有効な条件が含まれている場合。

1. 動的テキストの書式設定用の区切り文字を選択し、チェックマークをタップして保存します。

   * **改行**：出力レターの各トランザクションエントリの後に改行を挿入します。
   * **テキスト**：指定されたテキスト文字を、出力レターの各トランザクションエントリの後に挿入します。

   条件を挿入すると、繰り返しを含むテキストが赤でハイライト表示され、左側にハンドルが表示されます。 繰り返しの左側のハンドルにマウスポインターを置くと、繰り返し構成体が表示されます。

   ![4_repeat_hoverdetail](assets/4_repeat_hoverdetail.png)

   ハンドルをタップして、繰り返しのポップアップメニューを表示し、繰り返し構成体を編集または削除できます。

   ![5_repeateditremove](assets/5_repeateditremove.png)

1. 関連するレターをプレビューし、繰り返しに従ってテキストがレンダリングされることを確認します。 DD 要素の値を入力するには、次のオプションを使用します。

   * サンプルデータを使用してレターをプレビューする際に、関連するデータディクショナリに基づいて作成されたサンプル XML データファイル。
   * 関連するデータディクショナリに添付される XML データファイル。

   詳しくは、[データディクショナリ](https://helpx.adobe.com/jp/aem-forms/6-2/data-dictionary.html)を参照してください。

   ![6_repeatoutputpreview](assets/6_repeatoutputpreview.png)

   取引の明細とともに静的テキストが繰り返されています。この手順でテキストに適用した繰り返しによって、静的テキストの繰り返しが円滑におこなわれます。条件${DD_creditcard_TransactionAmount > 0。5}を使用すると、USD.5 未満のトランザクションがレターでレンダリングされなくなります。

   >[!NOTE]
   >
   >条件を挿入して繰り返すことは、関連するテキストモジュールの作成または編集時にのみ可能です。 レターをプレビューする際、テキストモジュールを編集することはできますが、条件を挿入したり、繰り返しを行うことはできません。

## インライン条件と繰り返しの使用 — 一部の使用例  {#using-inline-condition-and-repeat-some-use-cases}

### 条件内で繰り返し {#repeat-within-condition}

1 つの条件内で繰り返しを使用する必要が生じる場合があります。 Correspondence Management では、インライン条件構成体内で繰り返しを使用できます。

例えば、条件内で繰り返し（赤い書式）を次に示します（緑で書式設定）。

繰り返しによってクレジットカードトランザクションがレンダリングされる間、条件${DD_creditcard_nooftransactions > 0} 1 つ以上のトランザクションがある場合にのみ、繰り返し構成体がレンダリングされるようにします。

![repeatwitincondition](assets/repeatwitincondition.png)

同様に、必要に応じて、以下を作成できます。

* 条件内の 1 つ以上の条件
* 繰り返し内の 1 つ以上の条件
* 条件または繰り返し内の条件と繰り返しの組み合わせ

### 空のインライン条件 {#empty-inline-condition}

空のインライン条件を挿入し、後でテキストと DD 要素を埋め込む必要が生じる場合があります。 Correspondence Management では、これを実行できます。

![emptycondition](assets/emptycondition.png)

ただし、可能な場合は、最初に意図した書式設定（箇条書きなど）でテキストモジュールにテキストと DD 要素を挿入し、後でインライン条件を適用することをお勧めします。
