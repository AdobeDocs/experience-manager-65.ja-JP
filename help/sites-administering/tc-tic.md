---
title: 翻訳統合フレームワークの設定
description: Adobe Experience Manager での翻訳統合フレームワークの設定方法について説明します。
contentOwner: Guillaume Carlino
feature: Language Copy
exl-id: 7562754b-d9fd-441b-8ae5-c7eebe458cef
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: b7082aaee83fba88b47447b8553563264eedb713
workflow-type: tm+mt
source-wordcount: '1493'
ht-degree: 99%

---

# 翻訳統合フレームワークの設定{#configuring-the-translation-integration-framework}

翻訳統合フレームワークは、AEM コンテンツの翻訳を組織化するためにサードパーティの翻訳サービスと統合されます。

* 翻訳サービスプロバイダーに接続します。
* 翻訳統合フレームワーク設定を作成します。
* クラウド設定をページに関連付けます。

AEM のコンテンツ翻訳機能の概要については、[多言語サイトのコンテンツの翻訳](/help/sites-administering/translation.md)を参照してください。

## 翻訳サービスプロバイダーへの接続 {#connecting-to-a-translation-service-provider}

AEM を翻訳サービスプロバイダーに接続するためのクラウド設定を作成します。AEM には、Microsoft Translator にデフォルトで接続する機能が用意されています。
 次の翻訳ベンダーは翻訳プロジェクト用の新しい API の実装を提供します。統合の詳細については、次のリンクを参照してください。

* [Translations.com](https://exchange.adobe.com/experiencecloud.details.90104.globallink-connect-plus-for-aem.html)
* [Clay Tablet Technologies](https://exchange.adobe.com/experiencecloud.details.90064.clay-tablet-translation-for-experience-manager.html)
* [Lionbridge](https://exchange.adobe.com/experiencecloud.details.100064.lionbridge-connector-for-experience-manager-63.html)
* [Memsource](https://exchange.adobe.com/experiencecloud.details.103166.memsource-connector-for-adobe-experience-manager.html)
* [Cloudwords](https://exchange.adobe.com/experiencecloud.details.90019.html)
* [XTM Cloud](https://exchange.adobe.com/experiencecloud.details.105037.xtm-connect-for-adobe-experience-manager.html)
* [Lingotek](https://exchange.adobe.com/experiencecloud.details.90088.lingotek-collaborative-translation-platform.html)
* [RWS](https://exchange.adobe.com/apps/ec/108277/rws-language-cloud)
* [Smartling](https://www.smartling.com/software/integrations/adobe-experience-manager/)
* [Systran](https://exchange.adobe.com/experiencecloud.details.90233.systran-for-adobe-experience-manager.html)
* [Altlang](https://exchange.adobe.com/experiencecloud.details.90222.altlang.html)
* Microsoft（Microsoft Translator は AEM にプリインストールされています）

>[!NOTE]
>
>人間による翻訳と機械翻訳を提供する会社の最新のリストについては、次のページを参照してください。
>
>
>* [AEM 人間翻訳](https://www.adobe.com/go/aem-human-translation-connectors)
>* [AEM 機械翻訳](https://www.adobe.com/go/aem-machine-translation-connectors)
>

コネクタパッケージをインストールしたら、コネクタ用のクラウド設定を作成できます。通常は、翻訳サービスで認証を行うための資格情報を指定する必要があります。Microsft Translator コネクタ用のクラウド設定の追加については、[Microsoft Translator との統合](/help/sites-administering/tc-msconf.md)を参照してください。

必要に応じて、同じコネクターに対して複数のクラウド設定を作成できます。例えば、同じベンダーを使用するアカウントまたはプロジェクトごとに設定を 1 つずつ作成します。

接続の設定が完了したら、その接続を使用する翻訳統合フレームワーク設定を作成できます。

## 翻訳統合フレームワーク設定の作成 {#creating-a-translation-integration-configuration}

翻訳統合フレームワーク設定を作成して、コンテンツの翻訳方法を指定します。この設定には以下の情報が含まれます。

* どの翻訳サービスプロバイダーを利用するか。
* 人間による翻訳と機械翻訳のどちらを実行するか。
* ページまたはアセットに関連付けられている他のコンテンツ（タグなど）を翻訳するかどうか。

フレームワーク設定を作成したら、その設定に従って、翻訳するページにクラウド設定を関連付けます。翻訳プロセスが開始すると、関連付けられているフレームワーク設定に従って翻訳ワークフローが進行します。

Web サイトのセクションごとに翻訳要件が異なる場合は、それに応じて複数のフレームワーク設定を作成します。例えば、多言語の web サイトに英語、スペイン語、日本語の言語コピーが含まれているとします。サイトの所有者は、スペイン語と日本語の翻訳のために 2 つの異なる翻訳サービスプロバイダーを使用します。そのため、フレームワークの設定が 2 つ指定されます。使用する翻訳サービスプロバイダーは設定ごとに異なります。

翻訳統合フレームワークの設定が完了したら、[その設定を使用するページに関連付ける](/help/sites-administering/tc-prep.md)ことができます。

**注意：** AEM のコンテンツ翻訳機能の概要については、[多言語サイトのコンテンツの翻訳](/help/sites-administering/translation.md)を参照してください。

フレームワークの単一の設定によって、ページのコンテンツ、コミュニティのコンテンツおよびアセットの翻訳方法が制御されます。
![chlimage_1-386](assets/translation-config-65.jpg)

### 「Sites」の設定プロパティ  {#sites-configuration-properties}

Sites プロパティは、ページのコンテンツの翻訳を実行する方法を制御します。

<table>
 <tbody>
  <tr>
   <th>プロパティ</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>翻訳ワークフロー</td>
   <td><p>フレームワークがサイトコンテンツに対して実行する翻訳方法を選択します。</p>
    <ul>
     <li>機械翻訳：翻訳プロバイダーが機械翻訳を使用してリアルタイムで翻訳を実行します。</li>
     <li>人間翻訳：コンテンツが翻訳プロバイダーに送信され、翻訳者によって翻訳されます。 </li>
     <li>翻訳しない：コンテンツが翻訳対象として送信されません。翻訳されないものの、最新のコンテンツに更新される可能性があるコンテンツのブランチをスキップする場合に使用します。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>翻訳プロバイダー</td>
   <td>翻訳を実行する翻訳プロバイダーを選択します。対応するコネクターがインストールされている場合は、プロバイダーがリストに表示されます。</td>
  </tr>
  <tr>
   <td>コンテンツのカテゴリ</td>
   <td>（機械翻訳の場合のみ）翻訳するコンテンツを示すカテゴリです。カテゴリは、コンテンツ翻訳時の用語や言葉遣いの選択に影響を与える可能性があります。</td>
  </tr>
  <tr>
   <td>コンポーネントの文字列を翻訳</td>
   <td>ページに関連付けられているコンポーネントのコンポーネント文字列を翻訳する場合に選択します。</td>
  </tr>
  <tr>
   <td>タグを翻訳</td>
   <td>ページに関連付けられているタグを翻訳する場合に選択します。</td>
  </tr>
  <tr>
   <td>ページのアセットを翻訳</td>
   <td><p>ファイルシステムからコンポーネントに追加されるアセット、またはアセットから参照されるアセットを翻訳する方法を選択します。</p>
    <ul>
     <li>翻訳しない：ページのアセットが翻訳されません。</li>
     <li>Sites 翻訳ワークフローの使用：「Sites」タブの設定プロパティに従ってアセットが処理されます。</li>
     <li>Assets 翻訳ワークフローの使用：「Assets」タブのプロパティの設定に従ってアセットが処理されます。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>翻訳を自動実行</td>
   <td>翻訳プロジェクトの作成後に翻訳ジョブを自動的に実行する場合に選択します。このオプションを選択すると、翻訳ジョブのレビューやスコーピングを行う機会はなくなります。</td>
  </tr>
 </tbody>
</table>

### Communities の設定プロパティ {#communities-configuration-properties}

Communities のプロパティは、ユーザー生成コンテンツの翻訳を実行する方法を制御します。ユーザー生成コンテンツの翻訳には、常に機械翻訳を使用します。詳しくは、[ユーザー生成コンテンツの翻訳](/help/communities/translate-ugc.md)を参照してください。

| プロパティ | 説明 |
|---|---|
| 翻訳プロバイダー | 翻訳を実行する翻訳プロバイダーを選択します。クラウド設定の作成対象となるプロバイダーがリストに表示されます。 |
| コンテンツのカテゴリ | 翻訳するコンテンツを示すカテゴリです。カテゴリは、コンテンツを翻訳する際の用語や言葉遣いの選択を左右します。 |
| グローバル共有ストアとして使用するロケールを選択 | （オプション）UGC を格納するためのロケールを選択すると、すべての言語コピーからの投稿が 1 つのグローバルな会話に表示されます。慣例により、web サイトの[ベース言語](/help/communities/sites-console.md#translation)のロケールを選択してください。「共通ストアなし」を選択すると、グローバル翻訳が無効になります。デフォルトでは、グローバル翻訳は無効です。 |

### Assets の設定プロパティ {#assets-configuration-properties}

Assets プロパティは、アセットを設定する方法を制御します。アセットの翻訳について詳しくは、[アセットの言語コピーの作成](/help/assets/translation-projects.md)を参照してください。

<table>
 <tbody>
  <tr>
   <th>プロパティ</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>翻訳ワークフロー</td>
   <td><p>フレームワークがアセットに対して実行する翻訳のタイプを選択します。</p>
    <ul>
     <li>機械翻訳：翻訳プロバイダーが機械翻訳を使用してすぐに翻訳を実行します。</li>
     <li>人間翻訳：コンテンツが自動的に翻訳プロバイダーに送信され、手動で翻訳されます。 </li>
     <li>翻訳しない：アセットが翻訳対象として送信されません。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>翻訳プロバイダー</td>
   <td>翻訳を実行する翻訳プロバイダーを選択します。対応するコネクターがインストールされている場合は、プロバイダーがリストに表示されます。</td>
  </tr>
  <tr>
   <td>コンテンツのカテゴリ</td>
   <td>（機械翻訳の場合のみ）翻訳するコンテンツを示すカテゴリです。カテゴリは、コンテンツを翻訳する際の用語や言葉遣いの選択を左右します。</td>
  </tr>
  <tr>
   <td>アセットを翻訳</td>
   <td>翻訳プロジェクトにアセットを含める場合に選択します。 </td>
  </tr>
  <tr>
   <td>メタデータを翻訳</td>
   <td>アセットメタデータを翻訳する場合に選択します。</td>
  </tr>
  <tr>
   <td>タグを翻訳</td>
   <td>アセットに関連付けられているタグを翻訳する場合に選択します。</td>
  </tr>
  <tr>
   <td>翻訳を自動実行</td>
   <td>翻訳プロジェクトの作成後に翻訳ジョブを自動的に実行する場合に選択します。このオプションを選択すると、翻訳ジョブのレビューやスコーピングを行う機会はなくなります。</td>
  </tr>
 </tbody>
</table>

1. サイドバーで、ツール／運営／クラウド／クラウドサービスをクリックします。
1. 翻訳統合領域に表示されるリンクは、作成された設定に応じて決まります。

   * 設定が作成されていない場合は、「今すぐ設定」をクリックします。
   * 既存の設定がある場合は、「設定を表示」をクリックして、「利用可能な設定」の横に表示される + リンクをクリックします。

1. 設定の名前を入力して、「作成」をクリックします。
1. 「Sites」、「Communities」および「Assets」の各タブのプロパティを設定して、「OK」をクリックします。

## 翻訳するページの設定 {#configuring-pages-for-translation}

ソースページを他の言語に翻訳するように設定するには、そのページを次のクラウド設定に関連付けます。

* AEM を翻訳サービスプロバイダーに接続するためのクラウド設定。
* 翻訳の詳細を設定する翻訳統合フレームワーク。

翻訳統合フレームワークのクラウド設定によって、サービスプロバイダーへの接続に使用するクラウド設定が特定されます。ソースページをフレームワークのクラウド設定に関連付ける場合は、フレームワークのクラウド設定が使用するサービスプロバイダーのクラウド設定にページを関連付ける必要があります。

ページをクラウド設定に関連付ける場合は、そのページの子ページが関連付けを継承します。例えば、/content/geometrixx/en/products ページを翻訳統合フレームワークに関連付けると、「製品」ページとその下にあるすべてのページがフレームワークに従って翻訳されます。

必要に応じて、子ページの関連付けを上書きできます。例えば、web サイトのコンテンツがほとんど衣料品に関するものだとします。しかし、ページの 1 つのブランチには企業の説明が記述されています。サイトのルートページは、「衣料品」カテゴリを使用して、機械翻訳を指定する翻訳統合フレームワークに関連付けられます。企業の説明が記述されているブランチでは、「一般」カテゴリを使用して、機械翻訳を実行するフレームワークを使用します。

また、[SCF コンポーネント](/help/communities/scf.md)をページで使用するコミュニティの場合、ユーザー生成コンテンツ（UGC）には、ユーザーがコンテンツを翻訳する機能が含まれます。詳しくは、[ユーザー生成コンテンツの翻訳](/help/communities/translate-ugc.md)を参照してください。

### 翻訳プロバイダーへのページの関連付け {#associating-a-page-with-a-translation-provider}

ページおよび子ページの翻訳に使用する翻訳プロバイダーにページを関連付けます。

1. Sites コンソールで、設定するページを選択して、「プロパティを表示」をクリックします。
1. 「編集」をクリックし、「クラウドサービス」タブをクリックします。
1. 設定を追加／翻訳統合をクリックします。
1. 使用する翻訳プロバイダーを選択して、「完了」をクリックします。

### 翻訳統合フレームワークへのページの関連付け {#associating-pages-with-a-translation-integration-framework}

ページおよび子ページの翻訳を実行する方法を定義する翻訳統合フレームワークにページを関連付けます。

1. Sites コンソールで、設定するページを選択して、「プロパティを表示」をクリックします。
1. 「編集」をクリックし、「クラウドサービス」タブをクリックします。
1. 設定を追加／翻訳統合をクリックします。
1. 使用する翻訳統合フレームワークを選択して、「完了」をクリックします。
