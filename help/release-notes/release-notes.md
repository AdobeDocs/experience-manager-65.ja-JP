---
title: ' [!DNL Adobe Experience Manager]  6.5 のリリースノート'
description: ' [!DNL Adobe Experience Manager] 6.5 のリリース情報、新機能、インストール方法、詳細な変更リストを確認します。'
mini-toc-levels: 3
exl-id: fed4e110-9415-4740-aba1-75da522039a9
source-git-commit: 206242583fcbf651dbc6234dc01be5140d0cfca7
workflow-type: tm+mt
source-wordcount: '3537'
ht-degree: 30%

---

# [!DNL Adobe Experience Manager] 6.5 の最新のサービスパックのリリースノート {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/Documents/issue_tracker_sp_cfp_updates.xlsx?d=w3ea81ae4e6054153b132f2698c86f84e&csf=1&web=1&e=7yhrWb&nav=MTVfe0U0RjdDQUM3LTZCQ0EtNDk1Qy04Mjc1LTM2MUJEMzE1OEVGN30 -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, June 1, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## リリース情報 {#release-information}

| 製品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| バージョン | 6.5.17.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| タイプ | サービスパックのリリース |
| 日付 | 2023 年 5 月 25 日木曜日 <!-- UPDATE FOR EACH NEW RELEASE --> |
| ダウンロード URL | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/jp/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.17.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## [!DNL Experience Manager] 6.5.17.0 の内容 {#what-is-included-in-aem-6517}

[!DNL Experience Manager] 6.5.17.0には、2019 年 4 月の 6.5 の初期リリース以降にリリースされた新機能、お客様からリクエストされた主な機能強化、バグ修正、パフォーマンス、安定性、セキュリティの改善が含まれています。 [このサービスパックを [!DNL Experience Manager] 6.5 にインストール](#install)。

<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

このリリースの主な機能と改善点は次のとおりです。

* **検索エクスペリエンスの強化**  — 検索結果に表示されるアセットに対して、次の操作をすばやく実行できるようになりました。
   * ワークフローの作成
   * バージョンを作成します。
   * アセットの関連付けまたは関連付け解除

   これらの操作を実行する場合、アセットの場所に移動してアセットのプロパティを表示する必要はありません。
* **Dynamic Media _スナップショット_**— テスト画像やDynamic Media URL を試して、様々な画像修飾子の出力を確認し、スマートイメージングを最適化してファイルサイズ（WebP および AVIF 配信を使用）、ネットワーク帯域幅、デバイスピクセル比を確認します。 詳しくは、 [Dynamic Media Snapshot](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html).
* **Dynamic Mediaでの DASH ストリーミング** - Dynamic Mediaビデオ配信（CMAF を有効にした場合）でアダプティブストリーミングが開始される新しいプロトコル (DASH - Dynamic Adaptive Streaming over HTTP) のサポート。 すべての地域で利用可能 [サポートチケットを通じて有効化される](/help/assets/video.md#enable-dash-on-your-account-enable-dash).
* **AEM SitesとコンテンツフラグメントのAEM Assets次世代Dynamic Mediaとの統合**:AEM Assetsas a Cloud Serviceの次世代Dynamic Mediaのユーザーは、AEM Sites 6.5 のオンプレミスインスタンスまたはマネージドサービスインスタンスを使用したオーサリングと配信に、これらのクラウドホストアセットを使用できるようになりました。
* **AEM Site ページでのアダプティブFormsの統合**:AEM Sitesエディター内でアダプティブFormsコンポーネントを活用し、以下を使用して、デジタル登録エクスペリエンスをシームレスに作成します。 — アダプティブFormsコンテナとアダプティブForms — 埋め込み (v2) コンポーネント。
* **AEM Formsでの reCAPTCHA Enterprise のサポート**:AEM Formsでの reCAPTCHA Enterprise のサポートを追加し、既存のGoogle reCAPTCHA v2 のサポートに加えて、不正なアクティビティやスパムに対する保護を強化しました。
* **Adobe Acrobat Sign for Government with AEM Formsのサポート**:AEM FormsとAdobe Signの安全で準拠した統合（FedRAMP 準拠）を実現
* **データ交換用にAEM Formsと Salesforce の統合を有効化**:OAuth 2.0 クライアント資格情報フローを使用して、AEM forms と Salesforce アプリケーションの統合を設定します。 これにより、アプリケーションの安全で直接の認証と承認が可能になり、ユーザーの関与なくシームレスな通信が可能になります。
* **ワークフローエンジンの最適化と機能強化**:ワークフローインスタンスの数を最小限に抑えて、ワークフローエンジンのパフォーマンスを向上させます。 に加えて `COMPLETED` および `RUNNING` ステータス値の場合、ワークフローは 3 つの新しいステータス値もサポートします。 `ABORTED`, `SUSPENDED`、および `FAILED`.


<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets]{#assets-6517}

* 40 を超えるPDFを同時に公開する場合、 [!DNL Experience Manager] が応答を停止し、しばらくの間使用できなくなります。 (ASSETS-21789)
* テストユーザーとしてログインしている場合、アセットのプロパティをクリックすると、特定のアセットに関連するアセットが表示されません。 (ASSETS-21648)
* を使用してアセットを編集する際 `Desktop Actions`一度に 6 つ以上のアセットをチェックインしようとする場合は、 `Limit Reached` エラーが表示され、選択したアセットがチェックアウトされます。 (ASSETS-21121)
* コレクション内のアセットを名前で並べ替えることができません。 (ASSETS-20924)
* 画像形式のアセットにサイズを設定できません。 (ASSETS-20835)
* リンクを共有している間、「電子メールアドレスを検索/追加」フィールドのツールチップテキストとその背景に、適切なコントラスト比が表示されません。 (ASSETS-17347)
* を展開すると、 `Notifications`の場合、段落の間隔が原因で、テキストが正しく表示されません。 (ASSETS-17345)
* コレクション内のアセットをコピーする場合、 `Public Collection` チェックボックスが適切に表示されない。 (ASSETS-17343)
* 要素は、役割のない ARIA 属性を使用します。 （Assets-17325、Assets-17323）
* リンクは、 `Notifications`. (ASSETS-17283)
* を開きます。 [!DNL Smart Crop] 」ボタンをクリックすると、コンテンツはリストのように表示されますが、順序なしリストとしてマークアップされません。 その結果、スクリーンリーダーは順序なしのリストを認識せず、プレーンテキストとして読み上げます。 (ASSETS-17247)
* この `Sort By` ラベルは、それぞれのドロップダウンに関連付けられていません。 その結果、スクリーンリーダーはドロップダウンオプションを認識しません。 (ASSETS-17239)
* キーボードの Tab キーまたは矢印キーを使用してユーザーを追加しようとすると、前方または後方に移動できない `Add user` コンボボックス。 (ASSETS-17233)
* スクリーンリーダーがワークフローステップの情報を正しく伝えていない (ASSETS-17285)。
* 次に移動すると、 `Saved Searches` コンボボックスには、名前と役割の両方にラベルが割り当てられていません。 (ASSETS-17329)
* 移動時 `Collection` そして、 *メンバー*&#x200B;を指定した場合、テキストはマークアップされて表示されません。 その結果、スクリーンリーダーは見出しテキストを認識せず、プレーンテキストとして読み上げます。 (ASSETS-17245)
* にアクセスできません `View Settings` オプションを使用する場合は、キーボードから下にスクロールするか上にスクロールします。 (ASSETS-17257)
* 検索フィルターを使用して複数の選択されたアセットに対してワークフローをトリガーできません。 (ASSETS-7689)
* 検索結果から「アセット」（または複数のアセット）を選択すると、「関連付け」または「関連付けを解除」オプションは表示されません。 ただし、オプションは使用可能です。それ以外の場合は、使用可能です。 (ASSETS-7679)
* ログイン後に 1 回だけ検索フィルターパネルが開き、検索ページを終了して検索を再実行した場合は開きません。 (ASSETS-7671)
* リンクを共有する際に、電子メールコンボボックスに適切なコントラスト比が表示されません。 (ASSETS-17349)

<!-- REMOVED BY ENGINEERING FROM TOTAL RELEASE CANDIDATE LIST 
* When you select any file in a Collection and click `Download`, and then navigate to the email checkbox and expand it, regular text and email link is not recognizable due to background color. (ASSETS-17349) 
* When you navigate to `Smart Crop` option, the screen reader does not announce the expand or collapse state of the button. (ASSETS-17335)-->

## [!DNL Assets] - [!DNL Dynamic Media]{#dm-6517}

* Dynamic Mediaクラウド設定が既に存在する場合、Dynamic Mediaへの接続が切断されます。 (ASSETS-23057)
* 多数のDynamic Mediaビデオを含むフォルダーを参照し、解決されたフォルダーカード表示で読み込みに失敗すると、パフォーマンスが向上します。 (ASSETS-23016)
* 次の場所からプレビュートークンが削除されました： `error.log` を使用して、セキュリティで保護されたテストサーバーからセキュリティで保護されたコンテンツを要求できます。 (ASSETS-22685)
* PDFサムネールレンダリングでシャドウを追加。 PDFサムネールのレンダリングの問題を解決するため、Gibson lib バージョン 4.0.1680232194をアップグレードしました。 (ASSETS-22585)
* Dynamic Mediaハイブリッドモードは、New Relicエージェントバージョン 8.0.1 と互換性があるようになりました (ASSETS-22578)。
* Experience Manager上でDynamic Mediaファイルをプレビューする際に、Experience ManagerACL（アクセス制御リスト）が考慮されるようになりました。 (ASSETS-21628)
* スクリーンリーダーで、ユーザーが下向き矢印キーまたは Tab キーを使用して移動しようとしても、非表示の要素に移動しない。 (ASSETS-5617)
* イメージプロファイルユーザーインターフェイスは、同じ名前、同じサイズ、またはその両方のスマート切り抜きに対して制限されています。 (ASSETS-16997)
* イメージプロファイルユーザーインターフェイスでスマート切り抜きのデフォルトの幅と高さが 50 ピクセルに設定されるようになりました。 (ASSETS-16997)

## [!DNL Commerce]{#commerce-6517}

* 移動されたタグはガベージコレクションされますが、次の製品で参照されます： `/var`. （CQ-4351337）

## [!DNL Forms]{#forms-6517}

* ユーザーがAEM 6.5.16.0 Service Pack にアップグレードした場合、添付ファイルが正しく取得されません。 (FORMS-8906)
* AEM 6.5.15.0 Service Pack に更新した後、IE 互換モードの Edge ブラウザーで、HTML5 Forms が機能しないか、正しく読み込まれません。 (FORMS-8526、FORMS-8523)
* ユーザーがAEM 6.5.16.0 Service Pack を適用すると、ルールエディターを開けません。 (FORMS-8290)
* 数値ボックスコンポーネントに検証の最大桁数を適用すると、失敗します。 (FORMS-7938)
* インタラクティブ通信文を作成する際、PDF内のグラフコンポーネントが正しく生成されません。 (FORMS-7827、FORMS-8297)
* Java ガベージコレクションは、AEM Forms OSGi サーバー上の古い生成ヒープをクリアできません。 (FORMS-8207)
* ユーザーがAEM 6.5.16.0 Service Pack にアップグレードした場合、送信後に CRX メタデータのプロパティが欠落します。 (FORMS-8205)
* アダプティブフォーム内の日付選択コンポーネントを無効にした場合でも、編集可能です。 (FORMS-7804)
* AEM 6.5.16.0 Forms Service Pack では、ユーザーがポリシーセットコーディネーターを編集しようとすると、Manager Document Publisher は常にオフのままになります。 (FORMS-7775、FORMS-8599)
* ユーザーがAEM 6.5.16.0 Service Pack にアップグレードすると、翻訳が必要な文字列を処理する「GuideNode.externalize」メソッドが動作を停止します。 (FORMS-7709)
* 内 `Assign task` 手順：ユーザーが「通知メールを送信」を選択してワークフローを起動すると、受信した電子メールにテキストが正しく表示されません。 受信した E メールに含まれるテキストの代わりに、疑問符が受け取られます。 (FORMS-7675)
* レコードのドキュメントが部分的にローカライズされています。 (FORMS-7674、FORMS-7573)
* 割り当てられた特定の権限でも、ユーザーはポリシーセットを編集できません。 (FORMS-7665)
* ユーザーが `forms-users` グループが新しいフォームの作成を試み、AEM Formsインスタンスがクラッシュします。 (FORMS-7629)
* ユーザーがアダプティブフォームの「リセット」、「保存」、「送信」の各ボタンをクリックしても、画面にメッセージは表示されません。 (FORMS-7524)
* AEM 6.5.16.0 Service Pack での PDFG 変換のパフォーマンスを向上させるために、スリープ間隔を設定できるようになりました。 (FORMS-6752)
* 切り替えオプションは同じですが、ユーザーがカーソルを少しドラッグした場合でも、フィールドの表示/非表示は変わります。 (FORMS-6728)
* ユーザーがAEM 6.5.15.0 Service Pack にアップグレードすると、アダプティブフォームが Internet Explorer でレンダリングされると、リダイレクトが機能しなくなります。 (FORMS-6725)
* AEM Designer で作成されたPDFフォーム内のすべての背景オブジェクトに対する PAC 2021 ツールは、 `Path object not tagged`. (FORMS-6707)
* ユーザーがインボックスでフィルターを適用すると、 `NullPointerException` エラー。 (FORMS-6706)
* ユーザーがフラグメントを参照しているテンプレート (.tds) ファイルを読み込むと、AEM Designer がクラッシュします。  (FORMS-6702)
* ユーザーがAEM Forms Designer 6.5 で Output Service を使用して静的PDFを作成した場合、次のようなエラーが発生します。 `OCCD (optional content configuration dictionary) contains AS key`. (FORMS-6691)
* ユーザーが単純なワークフローを作成し、単純な変数を追加すると、 `set variable mapping` エラーが発生しました。 (FORMS-5819)
* ユーザーが Output Service を使用してPDFを生成しようとしたとき（とマークされている場合） `PDF/A-1a`、`Preflight` サービスが失敗しました。 （LC-3920837）
* AEM 6.5.16.0 Service Pack をインストールした後、AEMデザイナーが開けません。 （LC-3921000）
* ユーザーがチェックボックスとラジオボタンを追加した場合、タグツリーの構造は、タグの標準に従ってPDFされません。 （LC-3920838）
* PDFの埋め込みとサブセット化を使用して静的PDFを生成した場合、出力サービスを通じて、生成されるフォントには埋め込みフォントのみが含まれます。 （LC-3920963）
* RTL 形式では、ヘブライ語のテキストが正しく表示されません。 （LC-3919632）
* ユーザーが JBoss Turnkey サーバーでAEM 6.5.16.0 Service Pack にアップグレードした場合、Signature Service は呼び出しに失敗します。 発生したエラー： `java.lang.ClassCastException: com.adobe.xfa.TextNode cannot be cast to com.adobe.xfa.Element`. (FORMS-7833)
* AEM 6.5.14.0 Service Pack にアップグレードした後、CRX ノードを別の場所に移動する処理が機能しなくなる。 エラーは次のように発生します。 `ALC-CRX-30000-000: com.adobe.ep.crx.client.exceptions.CRCException: ALC-CRX-030-000-[Internal Server Error]`.(FORMS-7713)
* ユーザーがAEM 6.5.16.0 Service Pack に更新すると、 `Usage Rights` 申し込みに失敗しました。 (FORMS-7892)
* ユーザーがPDFドキュメントを生成しようとすると、PDF/A-1b 検証が失敗します。 (FORMS-7615)
* ユーザーが `Configure` オプション `Form Container` コンポーネントを使用しない場合、ブラウザーが応答しなくなります (FORMS-7605)。
* ユーザーがAEM Forms 6.5.16.0 Service Pack を更新し、 `LicenseType` から `Production`の場合、変更は反映されません。 (FORMS-7594)
* ユーザーが、 `Chinese Full Width Characters`を含めている場合、 `ValidateForm` プロセス。 (FORMS-7464)
* AEM Forms Designer では、XMLFM は XDP ベースのテンプレート用に、レター、A4、A5 など、様々な用紙サイズで ZPL 出力を生成します。(FORMS-7898)

## 統合{#integrations-6517}

* Adobe Target IMS 設定をレガシークラウド設定のユーザー資格情報に変換する場合、 `connectedWhen` プロパティは変更されません。 この問題により、すべての呼び出しが、設定がまだ IMS ベースであったかのように実行されます。 （CQ-4352810）
* 追加中 `modifyProperties` ～への許可 `fd-cloudservice` Adobe Sign設定のシステムユーザー。 (FORMS-6164)
* Adobe Targetと統合されたExperience Managerでは、AB テストアクティビティを作成すると、そのアクティビティに関連付けられたオーディエンスが Target と同期されません。 （NPR-40085）

## Oak{#oak-6517}

Service Pack 13 以降で、永続性キャッシュに影響する次のエラーログが表示され始めました。

```shell
org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
    at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
    at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
    at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
    at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
    at org.h2.mvstore.db.Store.<init>(Store.java:129)
```

または

```shell
org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
```

この例外を解決するには、次の手順を実行します。

1. 次の 2 つのフォルダーを `crx-quickstart/repository/`

   * `cache`
   * `diff-cache`

1. Service Pack をインストールするか、Experience Managerをas a Cloud Serviceして再起動します。
の新しいフォルダー `cache` および `diff-cache` が自動的に作成され、 `mvstore` 内 `error.log`.

## プラットフォーム{#platform-6517}

* Experience ManagerTag Managementユーザーインターフェイス (/aem/tags/) で、名前空間とタグが作成された順序で表示されます。 ただし、多数の名前空間とタグがある場合、名前空間を表示および管理するのは困難です。 この問題は、他の方法で並べ替えることができないためです。 （NPR-39620）
* 一部のクライアントライブラリで縮小 js が機能しないので、Google閉鎖バージョンの更新が必要です。 （NPR-40043）

## [!DNL Sites]{#sites-6517}

* LinkCheckerTransformer のパフォーマンス低下。 （SITES-11661）
* ページの言語コピーが期待どおりに更新されませんでした。 （SITES-11191）
* キャンペーンページ以外の呼び出しを開く `targeteditor.html` 不必要に を削除します。 `targeteditor` 不要な場合はを呼び出します。 （SITES-12469）
* 注釈の付いたページにはライブコピーを作成できません。 （SITES-12154）
* ページのロールアウトはExperience Manager6.5.16 で動作しています。 （SITES-12008）
* メモリ不足、～による高いごみ収集活動 `NotificationManagerImpl`. `NotificationManager` バンドルをAEM 6.5 にアップグレードします。 （SITES-11440）
* Service Pack 17 をブロックしていた WCM IT テストを修正しました。 （SITES-13089）
* サーブレットでサイト参照の取得に失敗しました。 （SITES-10901）

### [!DNL Sites] - 管理ユーザーインターフェイス{#sites-adminui-6517}

* サムネール画像セレクターのプレビューウィンドウを閉じることができません。 （SITES-10459）

### [!DNL Sites] - [!DNL Content Fragments]{#sites-contentfragments-6517}

* Polaris サービスオブジェクト（URL、資格情報、コールバックなど）に接続するための設定。 （SITES-12149）
* の使用方法 `SemanticDataType.REFERENCE` は、「Remote-Asset-IDs」をサポートする必要があります。 （SITES-12127）
* Polaris アセットセレクターをコンテンツフラグメントエディターに統合します。 （SITES-12125）
* メタデータサービスエンドポイントにアクセスするには、必須の http ヘッダーが必要でした。 （SITES-13068）
* 6.5 のGraphQL実装は、Cloud Service（プライマリ）と同じではありませんでした。特定された問題を修正しました。 （SITES-13096）
* GraphQLのページング/並べ替えおよびハイブリッドフィルタリングは、AEM 6.5/AMS で使用できます。 （SITES-9154）

### [!DNL Sites] - コアコンポーネント{#sites-core-components-6517}

* プロパティ `cq-msm-lockable` の Foundation ページコンポーネントに誤ったリダイレクト値がある。 （SITES-10904）
* リモートアセットピッカーは、常に IMS ステージ環境にリダイレクトされます。 （SITES-13433）

### [!DNL Sites] - [!DNL Experience Fragments]{#sites-experiencefragments-6517}

* Adobe Targetに書き出す際にエクスペリエンスフラグメントで Externalizer 設定を選択すると、誤った外部化された URL が送信されます。 （SITES-12402）
* 含まない用語を削除する。包括的な用語のガイドラインを適用します。 （SITES-11244）

### [!DNL Sites] - ページエディター{#sites-pageeditor-6517}

* カルーセルセットのサムネールは、Experience Managerコンテンツファインダーのサイドレールに表示されません。 （SITES-8593）

## Sling{#sling-6517}

* Sling `ResourceMerger` 架空のパスを提供すると、大量の CPU を消費し、サービス拒否を引き起こします。 （NPR-40338）

## 移動プロジェクト{#translation-6517}

<!-- REMOVED BY ENGINEERING FROM TOTAL RELEASE CANDIDATE LIST * The `translationrules.xml` is sorted poorly when adding a rule to a property by way of the translation configuration user interface. (NPR-40431) -->
* ユーザーが必須以外のフィールドを設定していない場合、言語コピーは作成されません。 （NPR-40036）

## ユーザーインターフェイス{#ui-6517}

* ページプロパティの「キャンセル」ボタンが非アクティブになっている。Site Admin ユーザーインターフェイスが表示されます。 （NPR-40501）

<!-- ## WCM{#wcm-6517}

* TEXT -->

## ワークフロー{#workflow-6517}

* ワークフローコンソールの変更 （NPR-40502）
* `SegmentNotfound errors` クラスの閉じられていないリソースリゾルバーが原因で、実稼動オーサーインスタンスのログ内で発生する問題を修正しました。 `com.day.cq.workflow.impl.email.EMailNotificationServic`. （NPR-40187）
* 閉じていない閉じた状態 `ResourceResolver` 例外がログに記録されています。 (ASSETS-22495)
* 膨大な量のPSD/PDFが発生した場合にExperience Manager作成者がクラッシュする `DocumentAncestors` メタデータ属性がアップロードされます。 (ASSETS-22966)
* クラスのセッションリーク `InboxSharingCache` と `user-reader-service`. （CQ-4352513）
* 「ワークフローイニシエーター参加者選択」ステップで参加者ステップのユーザーとグループが一覧表示されると、不完全なユーザーとグループのリストが表示されます。 この問題は、あるグループが別のグループのメンバーでもあった場合に発生していました。 （NPR-40055）
* ワークフローのパージが強化されました。 （NPR-40459）

## [!DNL Experience Manager] 6.5.17.0 のインストール{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.17.0 には [!DNL Experience Manager] 6.5 が必要です。手順について詳しくは、[アップグレードに関するドキュメント](/help/sites-deploying/upgrade.md)を参照してください。<!-- UPDATE FOR EACH NEW RELEASE -->
* サービスパックは、アドビの[ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/jp/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.17.0.zip)からダウンロードできます。
* MongoDB と複数のインスタンスを含むデプロイメントでは、パッケージマネージャーを使用して、オーサーインスタンスの 1 つに [!DNL Experience Manager] 6.5.17.0 をインストールしてください。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> アドビでは、[!DNL Experience Manager] 6.5.17.0 パッケージを削除またはアンインストールすることを推奨しません。 したがって、パックをインストールする前に、 `crx-repository` 戻す必要がある場合に備えて <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for AEM Forms, see [AEM Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### [!DNL Experience Manager] 6.5 へのサービスパックのインストール{#install-service-pack}

1. インスタンスが更新モードの場合（インスタンスが以前のバージョンから更新された場合）、インストール前にインスタンスを再起動します。インスタンスの現在の稼動時間が長い場合、アドビは再起動することを推奨します。

1. インストールする前に、[!DNL Experience Manager] インスタンスのスナップショットまたは新しいバックアップを作成します。

1. [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/jp/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.17.0.zip)からサービスパックをダウンロードします。 <!-- UPDATE FOR EACH NEW RELEASE -->

1. パッケージマネージャーを開き、「**[!UICONTROL パッケージをアップロード]**」を選択して、パッケージをアップロードします。詳しくは、[パッケージマネージャー](/help/sites-administering/package-manager.md)を参照してください。

1. パッケージを選択して、「**[!UICONTROL インストール]**」を選択します。

1. S3 コネクタを更新するには、サービスパックのインストール後にインスタンスを停止し、既存のコネクタをインストールフォルダーに用意されている新しいバイナリファイルに置き換えて、インスタンスを再起動します。[Amazon S3 データストア](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)を参照してください。

>[!NOTE]
>
>サービスパックのインストール中に、パッケージマネージャー UI のダイアログが終了することがあります。Adobeでは、エラーログが安定するのを待ってから、デプロイメントにアクセスすることをお勧めします。アップデーターバンドルのアンインストールに関連する特定のログが表示されるのを待ってから、インストールが成功したことを確認してください。この問題は、通常 [!DNL Safari] ブラウザーで発生しますが、どのブラウザーでもときどき発生する場合があります。

**自動インストール**

[!DNL Experience Manager] 6.5.17.0. の自動インストールに使用できる方法は 2 つあります<!-- UPDATE FOR EACH NEW RELEASE -->

* サーバーがオンラインで使用可能な場合、パッケージを `../crx-quickstart/install` フォルダーに配置します。パッケージが自動的にインストールされます。
* [パッケージマネージャーの HTTP API](/help/sites-administering/package-manager.md#package-share) を使用します。ネストされたパッケージがインストールされるように、`cmd=install&recursive=true` を使用します。

>[!NOTE]
>
>Experience Manager 6.5.17.0 では、Bootstrap のインストールをサポートしていません。<!-- UPDATE FOR EACH NEW RELEASE -->

**インストールの検証**

このリリースでの動作が認定されたプラットフォームについては、[技術要件](/help/sites-deploying/technical-requirements.md)を参照してください。

1. 製品情報ページ（`/system/console/productinfo`）の[!UICONTROL インストール済み製品]に、更新されたバージョン文字列 `Adobe Experience Manager (6.5.17.0)` が表示されます。<!-- UPDATE FOR EACH NEW RELEASE -->

1. すべての OSGi バンドルは、OSGi コンソールで **[!UICONTROL アクティブ]** または **[!UICONTROL フラグメント]** です（web コンソールを使用：`/system/console/bundles`）。

1. OSGi バンドル `org.apache.jackrabbit.oak-core` はバージョン 1.22.15 以降です（web コンソールを使用：`/system/console/bundles`）。<!-- NPR-40398 for 6.5.17.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### [!DNL Experience Manager] Forms へのサービスパックのインストール{#install-aem-forms-add-on-package}

AEM Forms にサービスパックをインストールする手順については、[AEM Forms サービスパックのインストール手順](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)を参照してください。

### Experience Managerコンテンツフラグメント用のGraphQLインデックスパッケージのインストール{#install-aem-graphql-index-add-on-package}

GraphQLを使用しているお客様は、 [GraphQLインデックスパッケージ 1.1.1 を使用したAEMコンテンツフラグメント](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

これにより、実際に使用する機能に基づいて、必要なインデックス定義を追加できます。

このパッケージをインストールしないと、GraphQLクエリが遅くなったり失敗したりする場合があります。

>[!NOTE]
>
>このパッケージは、インスタンスごとに 1 回だけインストールしてください。すべての Service Pack で再インストールする必要はありません。

### UberJar{#uber-jar}

[!DNL Experience Manager] 6.5.17.0 の UberJar は、[Maven Central リポジトリ](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.17/)で入手できます。<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Maven プロジェクトで UberJar を使用するには、[UberJar の使用方法](/help/sites-developing/ht-projects-maven.md)を参照し、プロジェクト POM に次の依存関係を含めます。<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.17</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar およびその他の関連アーティファクトは、Adobe のパブリック Maven リポジトリー （`repo.adobe.com`） ではなく、Maven Central リポジトリーで入手できます。メインの UberJar ファイルの名前は、「`uber-jar-<version>.jar`」に変更されます。ですので `classifier` がなく、値として `apis` を `dependency` タグに使用します。

## 非推奨（廃止予定）の機能{#removed-deprecated-features}

[!DNL Experience Manager] 6.5.7.0 で非推奨（廃止予定）とマークされた特徴と機能のリストは次のとおりです。 これらの機能は、最初は非推奨とマークされ、将来のリリースでは削除されます。別のオプションが提供されます。

デプロイメントでその特徴または機能を使用しているかどうかを確認します。また、別のオプションを使用するように、実装の変更を計画します。

| 領域 | 機能 | 代替手段 |
|---|---|---|
| 統合 | 画面 **[!UICONTROL AEM クラウドサービスのオプトイン]** は、 [!DNL Experience Manager] および [!DNL Adobe Target] 統合は、 [!DNL Experience Manager] 6.5.この統合は、Adobe Target Standard API をサポートしています。 API は、Adobe IMS と [!DNL Adobe I/O Runtime] の認証方法を使用します。これは、Adobe Experience Platform Launch が分析およびパーソナライゼーション用に [!DNL Experience Manager] ページを構築する役割が増大していることをサポートするもので、オプトインウィザードは機能的に無関係です。 | システム接続、Adobe IMS 認証、 [!DNL Adobe I/O Runtime] 統合を各 [!DNL Experience Manager] クラウドサービスを通じて設定します。 |
| コネクタ | Microsoft® SharePoint 2010 および Microsoft® SharePoint 2013 用の Adobe JCR Connector は、[!DNL Experience Manager] 6.5 で非推奨になりました。 | 該当なし |

## 既知の問題{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->
<!-- REMOVED AS PER CQDOC-20022, JANUARY 23, 2023 * If you install [!DNL Experience Manager] 6.5 Service Pack 10 or a previous service pack on [!DNL Experience Manager] 6.5, the runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) is deleted.
To retrieve your runtime copy, Adobe recommends to synchronize the design-time copy of the custom workflow model with its runtime copy using the HTTP API:
`<designModelPath>/jcr:content.generate.json`. -->

* コンテンツモデルのカスタム API 名を使用した可能性のあるGraphQLクエリを、代わりにコンテンツモデルのデフォルト名を使用するように更新します。

* GraphQLクエリでは、 `damAssetLucene` インデックス `fragments` 索引 このアクションを実行すると、GraphQLクエリが失敗するか、実行に時間がかかる場合があります。

   問題を修正するには、 `damAssetLucene` は、次の 2 つのプロパティを含むように設定する必要があります。

   * `contentFragment`
   * `model`

   インデックス定義を変更した後、インデックス再作成が必要です (`reindex` = `true`) をクリックします。

   これらの手順の後、GraphQLクエリの実行が高速化されます。

* [!DNL Microsoft® Windows Server 2019] は [!DNL MySQL 5.7] および [!DNL JBoss® EAP 7.1] をサポートしていないので、[!DNL Microsoft® Windows Server 2019] は [!DNL AEM Forms 6.5.10.0] の自動インストールをサポートしていません。

* [!DNL Experience Manager] インスタンスを 6.5.0～6.5.4 から Java™ 11 の最新のサービスパックにアップグレードすると、`error.log` ファイルに `RRD4JReporter` 例外が表示されます。例外を停止するには、[!DNL Experience Manager] のインスタンスを再起動します。<!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* ユーザーは、[!DNL Assets] の階層内のフォルダーの名前を変更し、ネストされたフォルダーを [!DNL Brand Portal] に公開できます。ただし、ルートフォルダーが再公開されるまで、[!DNL Brand Portal] でフォルダーのタイトルは更新されません。

* アダプティブフォームでユーザーが初めてフィールドを設定する場合、設定を保存するオプションはプロパティブラウザーに表示されません。同じエディターでアダプティブフォームの他のフィールドを設定するように選択すると、問題が解決します。

* [!DNL Experience Manager] 6.5.x.x のインストール中に、次のエラーや警告メッセージが表示される場合があります。
   * 「Target Standard API（IMS 認証）を使用して [!DNL Experience Manager] に Adobe Target 統合を設定する場合、エクスペリエンスフラグメントを Target に書き出すと、間違ったオファータイプが作成されます。Target では、「エクスペリエンスフラグメント」／ソース「Adobe Experience Manager」タイプではなく、「HTML」／ソース「Adobe Target Classic」タイプのオファーをいくつか作成します。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * SUM、MAX、MIN などの集計関数が使用される場合、アダプティブフォームのサーバー側検証が失敗します （CQ-4274424）。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * ショッパブルバナービューアでアセットをプレビューしている間、Dynamic Media インタラクティブ画像のホットスポットは表示されません。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : 登録状況を未登録に変更する処理が完了するのを待機中にタイムアウトになりました。

* コンテンツフラグメント、サイト、ページのいずれかを移動、削除または公開しようとすると、バックグラウンドクエリが失敗したため、コンテンツフラグメント参照が取得される際に問題が発生します。 つまり、この機能は動作しません。
正しく動作させるには、インデックス定義ノード `/oak:index/damAssetLucene` に次のプロパティを追加する必要があります（インデックスの再作成は不要です）。

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

* JBoss® 7.1.4 プラットフォームで、ユーザーがAEM 6.5.16.0以降の Service Pack をインストールするとき、 `adobe-livecycle-jboss.ear` デプロイに失敗しました。

## 含まれている OSGi バンドルとコンテンツパッケージ{#osgi-bundles-and-content-packages-included}

次のテキストドキュメントには、[!DNL Experience Manager] 6.5.17.0 に含まれている OSGi バンドルとコンテンツパッケージの一覧が記載されています。<!-- UPDATE FOR EACH NEW RELEASE -->

* [Experience Manager 6.5.17.0 に含まれている OSGi バンドルの一覧](/help/release-notes/assets/65170_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5.17.0 に含まれているコンテンツパッケージの一覧](/help/release-notes/assets/65170_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 制限付き Web サイト{#restricted-sites}

以下の web サイトはお客様のみが参照できます。アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [アドビカスタマーサポートに連絡](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=ja)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 製品ページ](https://business.adobe.com/jp/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=ja)
>* [アドビ製品アップデートの優先通知に登録する](https://www.adobe.com/subscription/priority-product-update.html)

