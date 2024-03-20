---
title: ドラフトと送信コンポーネント
description: ドラフトと送信コンポーネントは、ドラフト状態のフォームと、既に送信済みのフォームを一覧表示します。コンポーネントのアピアランスおよびスタイルをカスタマイズできます。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: f3f013a7-a399-4178-a901-d4a8c65ddbd3
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 100%

---

# ドラフトと送信コンポーネント{#drafts-and-submissions-component}

ドラフトと送信コンポーネントは、ドラフト状態のすべてのフォームと、既に送信済みのフォームを一覧表示します。コンポーネントには、ドラフトのフォームと送信済みのフォームで別々のセクション（タブ）があります。ユーザーに表示されるのは、ユーザーのドラフトフォームと送信済みのフォームのみです。

## コンポーネントの設定 {#configuring-the-component}

ドラフトと送信コンポーネントには、「ドラフト」と「送信」の 2 つのタブがあります。

アダプティブフォームの送信を有効化して「送信」タブに表示するには、アダプティブフォームで「**送信アクション**」を「**[フォームポータル送信アクション](../../forms/using/configuring-submit-actions.md)」に設定します。または、** により「フォームポータル送信」オプションが有効になります。ユーザーがフォームを送信するたびに、フォームが「送信」タブに追加されます。

ドラフト機能は初期設定で有効になっています。ユーザーがアダプティブフォームで「**保存**」をクリックすると、フォームが「ドラフト」タブに追加されます。

次の手順に従って、ドラフトと送信コンポーネントを追加して設定します。

1. コンポーネントブラウザーのドキュメントサービスカテゴリにある&#x200B;**ドラフトと送信**&#x200B;コンポーネントを、ページにドラッグ＆ドロップします。
1. コンポーネントを選択し、![settings_icon](assets/settings_icon.png) を選択してコンポーネントの編集画面を開きます。

   ![ドラフトと送信コンポーネント](assets/drafts-submissions-edit.png)

1. 編集ダイアログで、次の内容を指定し、「**完了**」を選択して設定を保存します。

<table>
 <tbody>
  <tr>
   <th>タブ</th>
   <th>設定</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>一般</td>
   <td>合計結果</td>
   <td>表示する結果の最大数を指定します。結果数が合計結果の制限を超えると、「<strong>さらに表示</strong>」というリンクがコンポーネントの下部に表示されます。「<strong>詳細</strong>」をクリックするとすべてのフォームが表示されます。 </td>
  </tr>
  <tr>
   <td> </td>
   <td>スタイルタイプ</td>
   <td>コンポーネントのスタイルを指定します。フォームのリスト表示には、<strong>書式なし</strong>、<strong>デフォルトスタイル</strong>、<strong>カスタムスタイル</strong>のいずれかを指定できます。「カスタムスタイル」オプションの場合、「<strong>カスタムスタイルパス</strong>」フィールドでカスタム CSS ファイルのパスを指定できます<strong>。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>カスタムスタイルパス</td>
   <td>「<strong>スタイルタイプ</strong>」フィールドで「<strong>カスタムスタイル</strong>」オプションを選択する場合、「<strong>カスタムスタイルパス</strong>」フィールドを使用してカスタム CSS ファイルのパスを指定します。 </td>
  </tr>
  <tr>
   <td> </td>
   <td>表示オプション</td>
   <td><p>表示するタブを指定します。「ドラフトフォーム」、「送信済みのフォーム」または「両方」のうちどれを表示するかを選択できます。 </p> <p><strong>メモ</strong>：<em><strong>「表示」オプション</strong>で、「<strong>両方</strong>」以外のオプションを選択した場合、「<strong>デフォルトタブ</strong>」フィールドのオプションは使用されません。</em></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>デフォルトタブ</td>
   <td>フォームのポータルページを読み込むときに表示するタブを指定します。 <strong>「ドラフトフォーム」タブ</strong>または<strong>「送信済みのフォーム」タブ</strong>のいずれかを選択します。</td>
  </tr>
  <tr>
   <td>ドラフトフォームタブの設定</td>
   <td>カスタムタイトル</td>
   <td>「<strong>ドラフトフォーム</strong>」タブのタイトルを指定します。デフォルト値は<strong>ドラフトフォーム</strong>です。</td>
  </tr>
  <tr>
   <td> </td>
   <td>テンプレートのレイアウト</td>
   <td>ドラフトフォームリストに使用するレイアウトを指定します。</td>
  </tr>
  <tr>
   <td>送信済みフォームタブの設定</td>
   <td>カスタムタイトル </td>
   <td>「<strong>送信済みフォーム</strong>」タブのタイトルを指定します。デフォルト値は<strong>送信済みフォーム</strong>です。</td>
  </tr>
  <tr>
   <td> </td>
   <td>テンプレートのレイアウト</td>
   <td>送信済みフォーム<strong> </strong>のリストに使用するレイアウトを指定します。 </td>
  </tr>
 </tbody>
</table>

## ストレージのカスタマイズ {#customizing-the-storage}

「フォームポータル」送信アクションを使用したり、アダプティブフォームでフォームポータルにデータを保存するオプションを有効にしたりすると、フォームデータは AEM リポジトリーに保存されます。実稼働環境では、ドラフトまたは送信されたフォームデータを AEM リポジトリーに保存しないことをお勧めします。代わりに、ドラフトと送信コンポーネントをエンタープライズデータベースなどの安全なストレージと統合して、ドラフトと送信済みフォームデータを格納する必要があります。

フォームポータルを使用すると、データをローカル AEM リポジトリ、リモート AEM リポジトリ、またはデータベースに保存することができます。AEM Forms では、ドラフトおよび送信用のユーザーデータの保存の実装をカスタマイズできます。デフォルトの方法を上書きして、ドラフトデータや送信データを任意のストレージに保存する方法を指定できます。例えば、組織に現在実装されているデータストアにデータを保存することができます。

フォームポータルには、ローカルとリモートの AEM Forms パブリッシュインスタンスの crx-repository にデータを保存するための、標準のサービス（API）が用意されています。デフォルトの実装は置き換えることができます。その方法について詳しくは、[ドラフトデータと送信データ用のストレージサービスの設定](/help/forms/using/configuring-draft-submission-storage.md)の記事を参照してください。デフォルト機能を置き換えるカスタム実装についての説明もあります。安全な場所にコンテンツを保存するためのカスタム実装に必要な方法について詳しくは、[ドラフトおよび送信データサービスのカスタマイズ](/help/forms/using/custom-draft-submission-data-services.md)と[ドラフトと送信コンポーネントのカスタムストレージ](/help/forms/using/adding-custom-storage-provider-forms.md)を参照してください。

AEM Forms のドキュメントでは、[ドラフトと送信コンポーネントとデータベースの統合のサンプル](integrate-draft-submission-database.md)を示しています。サンプル実装を使用して、独自のカスタム実装を作成できます。

## 関連記事

* [フォームポータルコンポーネントの有効化](/help/forms/using/enabling-forms-portal-components.md)
* [フォームポータルページの作成 ](/help/forms/using/creating-form-portal-page.md)
* [API を使用した Web ページ上のフォームの一覧表示](/help/forms/using/listing-forms-webpage-using-apis.md)
* [ドラフトと送信コンポーネントの使用](/help/forms/using/draft-submission-component.md)
* [ドラフトと送信済みフォームのストレージのカスタマイズ](/help/forms/using/draft-submission-component.md)
* [ドラフトと送信コンポーネントとデータベースの統合のサンプル](/help/forms/using/integrate-draft-submission-database.md)
* [フォームポータルコンポーネントのテンプレートをカスタマイズする](/help/forms/using/customizing-templates-forms-portal-components.md)
* [ポータル上のフォーム公開の概要](/help/forms/using/introduction-publishing-forms.md)
