---
title: '[!DNL Experience Manager] 6.5サービスパックリリースノート'
description: リリースノート( [!DNL Adobe Experience Manager] 6.5 service pack 8)
docset: aem65
mini-toc-levels: 1
exl-id: 28a5ed58-b024-4dde-a849-0b3edc7b8472
source-git-commit: 024f03c04a980c544ac59e736caeaa24f7565582
workflow-type: tm+mt
source-wordcount: '3409'
ht-degree: 5%

---

# [!DNL Adobe Experience Manager] 6.5サービスパックリリースノート  {#aem-service-pack-release-notes}

## リリース情報 {#release-information}

| 製品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| バージョン | 6.5.8.0 |
| タイプ | Service Pack のリリース |
| 日付 | 2021 年 3 月 11 日 |
| ダウンロード URL | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.8.zip) |

<!-- TBD: Update the SD link when SP8 is available. Same link is duplicated below in install -->

## [!DNL Adobe Experience Manager] 6.5.8.0 {#what-s-included-in-aem}に含まれる内容

[!DNL Adobe Experience Manager] 6.5.8.0には、2019年4月の6.5リリースのリリース以降にリリースされた新機能、お客様からリクエストされた主な機能強化、パフォーマンス、安定性、セキュリティの改善が含まれています。サービスパックは[!DNL Adobe Experience Manager] 6.5にインストールされています。

[!DNL Adobe Experience Manager] 6.5.8.0で導入された主な機能と機能強化は次のとおりです。

<!-- TBD:
* Using the Connected Assets functionality, it is now possible to connect up to 3 [!DNL Sites] instances with 1 [!DNL Assets] instances. The configuration user interface now allows the administrators to provide the details of these [!DNL Sites] instances. -->

* [Connected Assets機能](/help/assets/use-assets-across-connected-assets-instances.md)を使用する場合、そのアセットを使用するすべての[!DNL Sites]ページのリストを表示できるようになりました。 アセットへのこれらの参照は、アセットの[!UICONTROL プロパティ]ページで使用できます。 これにより、管理者、マーケター、ライブラリ担当者がアセットの使用状況を完全に把握でき、トラッキング、管理、ブランドの一貫性を向上させることができます。

* Webページで参照されているアセットを削除すると、[!DNL Experience Manager] [に警告](/help/assets/use-assets-across-connected-assets-instances.md#asset-usage-references)が表示されます。 参照元のアセットを強制的に削除するか、アセットの[!DNL Properties]ページに表示される参照を確認して変更できます。 参照をクリックすると、ローカルページとリモートページの[!DNL Sites]が開きます。

* [!UICONTROL 名前]、[!UICONTROL 最終変更日、]および[!UICONTROL 最終ロールアウト日]のプロパティを使用して、ロールアウトに使用できるライブコピーページを並べ替えます。

* 組み込み型のリポジトリ(Apache Jackrabbit Oak)が1.22.6に更新されました。 <!-- TBD: Mention the version -->

[!DNL Experience Manager] 6.5.8.0で導入された機能と機能強化の完全なリストについては、 [!DNL Adobe Experience Manager] 6.5サービスパック8](new-features-latest-service-pack.md)の新機能を参照してください。[

[!DNL Experience Manager] 6.5.8.0リリースで提供された修正の一覧を以下に示します。

### [!DNL Sites] {#sites-6580}

* ページがブループリントに移動されても、リンク先は更新されない(NPR-35724)。
* 特定のブラウザーでTizenベースのプレーヤーが認証に失敗する。 この問題は、samesite=none属性をサポートしないブラウザーで発生する(NPR-35589)。
* ロックが解除されたレスポンシブコンテナに許可されているコンポーネントが表示されない(NPR-35565)。
* 新しく追加されたページのライブコピーを作成すると、言語マスターは各ドメインに対して2つのコピーを作成します(NPR-35545)。
* `org.apache.felix.scr.impl.ComponentRegistry`タイマーが原因で多数のスレッドがブロックされた場合、SCRコンポーネントレジストリのデッドロック。 その結果、[!DNL Experience Manager]は無期限に応答を停止します(GRANITE-33125,FELIX-6252)。
* サイドレールで特定のアセットを検索すると、結果には、検索されなかったアセットが含まれます(NPR-35524)。
* Experience Managerインスタンスに対してSSLを有効にすると、コンテキストパスが削除される(NPR-35477)。
* リストを作成し、最初の要素にテキストを追加し、2番目の要素にテーブルを追加し、テーブル内にリストを追加すると、親リストがゆがむ(NPR-35465)。
* 連続するリスト項目で異なるプラグインを使用する場合、リスト項目に<br>タグが追加される(NPR-35464)。
* リストが2つの段落の間に配置されている場合、リストにテーブルを追加できない(NPR-35356)。
* AEMインスタンスをAEM 6.3からAEM 6.5にアップグレードし始めると、アップグレードインスタンスの起動に時間がかかる(NPR-35323)。
* 角括弧()を含むAEMアセットを複製する場合。 名前でレプリケーションが失敗する(GRANITE-27004、NPR-35315)。
* 見出しをリッチテキストエディターに追加すると、段落ボタンが無効になる(NPR-35256)。
* 既存のリストに項目を追加すると、後続の折りたたみ可能なリストまたはトグルリストが削除されます(NPR-35206)。
* 「ページをロールアウト」オプションを選択すると、使用可能なすべてのライブコピーを含むダイアログボックスが表示され、自動ロールアウトが実行されます。 ページのライブコピーは、ユーザーアクションを実行せずに、すべての地域にロールアウトされます(NPR-35138)。
* 「子を含める」オプションを使用する場合、「公開を管理」オプションですべてのページがリストされるわけではありません。 22ページのみが表示される(NPR-35086)。
* ポリシーが編集されると、テキストコンポーネントはポリシーの変更を保持しない(NPR-35070)。
* 番号付きリストの一部の項目をインデントする場合、すべての項目は同じ番号を保持しますが、同じインデントを持つ項目に対しては、番号が1から始まる必要があります(CQ-4313011)。
* 縮小化が有効になっている場合、どのページやコンポーネントも編集できません。 問題は、AEM 6.5 Service Pack 7のインストール後に発生しました(CQ-4311133)。
* オムニサーチおよびアセットフィルターが、無関係な結果または結果を返さない(CQ-4312322、NPR-35793)。
* 複数のページがクライアントライブラリに同時にアクセスする場合、HTMLライブラリマネージャーはクライアントライブラリを読み込めません。 ページの誤ったレンダリングが発生する。(NPR-35538)
* [!DNL Experience Manager]でSSLを設定すると、コンテキストパスが自動的に削除されます(NPR-35294)。
* パッケージマネージャーがログアウトオプションをクリックした後、ユーザーをログアウトしない(NPR-35160)。

### [!DNL Assets] {#assets-6580}

[!DNL Adobe Experience Manager] 6.5.8.0では、次の問 [!DNL Assets] 題が修正され、次の機能強化がおこなわれました。

* 以前のバージョンのアセットを復元すると、OSGiコンソールでDamEvent.Type RESTOREDイベントがトリガーされない(NPR-35789)。
* `IndexWriter.merge` スマートタ `OutOfMemoryError` グ機能で大きなおよびインデッ `/oak:index/lucene` クスが作成さ `/oak:index/ntBaseLucene` れるので、エラーが発生する。(NPR-35651)
* マルチバイト文字を含む[!UICONTROL アセット投稿]タイプのフォルダーを名前に保存しようとすると、エラーメッセージが表示される(NPR-35605)。
* カスケードメタデータサブタイプフィールドを使用すると、誤った「このフィールドに入力してください」エラーが発生する(NPR-35643)。
* 既存のアセットを[!DNL Assets]ユーザーインターフェイスにドラッグして新しいバージョンを作成すると、メタデータの変更が永続的に行われない(NPR-34940)。
* カスケードメニュー用のルールをメタデータスキーマエディターで作成する場合、「[!UICONTROL 依存オン]」オプションは同じ名前を繰り返します(NPR-35596)。
* [!UICONTROL アセット管理者の検索レール]を編集した後、類似性検索が機能しない(NPR-35588)。
* フォルダー内で、左側のレールの「[!UICONTROL フィルター]」をクリックしてアセット検索を開くと、[!UICONTROL ステータス]/[!UICONTROL チェックアウト]/[!UICONTROL チェックアウト]が機能しません(NPR-35530)。
* アセットのすべてのスマートタグを削除して変更を保存しようとしても、タグは削除されません。 ただし、ユーザーインターフェイスは、変更が保存されたことを示します(NPR-35519)。
* 順序指定可能なフォルダーのリスト表示で、ユーザーがアセットの並べ替えや並べ替えを行えない。(NPR-35516)
* デフォルトのメタデータスキーマを編集すると、アセットの[!UICONTROL プロパティ]ページのタグフィールドがテキストフィールドに変わります。 この変更により、ユーザーがオンデマンドタグを追加することを認識できなくなり、タグがリポジトリに文字列として保存される。(NPR-35478)
* アセットをダウンロードする際に、有効な電子メールアドレスを持たない名前を指定した場合、ダウンロードオプションは使用できません。 ただし、ダウンロードダイアログの別のオプションが選択されている場合、このボタンは有効になりますが、電子メールは送信されません(NPR-35365)。
* ユーザーは、[!DNL Adobe InDesign]でアセットを編集した後にチェックインできず、権限の不足に関するエラーが表示される(NPR-35341)。
* Handlebars JavaScriptライブラリがv4.7.6にアップグレードされました(NPR-35333)。
* 一括メタデータ編集を開始し、1つの項目が選択されたままになるまで項目の選択を解除すると、メタデータエディターインターフェイスが期待どおりに動作しなくなる(NPR-35144)。
* `assets.html`ページ内からクリックした場合、グローバルナビゲーションで正しいコンソールが開かれない(CQ-4312311)。
* [!DNL Assets] RGBレンディションを持つアセットのRGBレンディションが表示されない(CQ-4310190)。
* メニューの[!UICONTROL Relate]オプションが[!UICONTROL Properties]ページに正しく表示されません(CQ-4310188)。
* アセットの検索やスマートコレクションの作成にドキュメントのファイルタイプフィルターを使用する場合、コレクションのアクセス時にフィルターが適用されません。 代わりに、すべてのタイプのアセットが検索に表示されます(NPR-35759)。
* [!DNL Assets]ユーザーインターフェイスからLightboxにアセットをドラッグして追加することはできません(NPR-35901)。
* 名前の競合を解決した後に既存のアセットの新しいバージョンを作成すると、元のアセットのメタデータが上書きされます(CQ-4313594)。
* 検索フィルターまたは述語を使用してアセット検索をフィルターする場合は、アセットを開いて表示または編集し、検索結果ページに戻ると、フィルターは機能しません。 検索されたすべてのアセットが、フィルタリングされていない状態で表示される(NPR-35913)。

#### [!DNL Dynamic Media] {#dynamic-media-6580}

* RESS画像プリセットの「 URL 」オプションは、アセットの詳細ページで有効になっています。 動的レンディションセクションでRESS画像プリセットが選択されている場合、アセットの詳細ページでURLオプションとRESSオプションの両方が使用できるようになりました。 (CQ-4311241)
* インタラクティブメディアコンポーネント — インタラクティブビデオは、ユーザーが選択的公開設定の[!DNL Experience Manager]を持っている場合、機能しません(CQ-4311054)。
* フォルダー間でアセットを移動する場合、APIを介した[!DNL Experience Manager]と[!DNL Dynamic Media–Scene7]の同期は非常に遅くなります(CQ-4310001)。
* オムニサーチを使用する場合、ログのサイズが大幅に増加します(CQ-4309153)。
* 選択的同期が有効で、アセットが同期フォルダーにコピー（移動なし）されると、期待どおりに同期されません(CQ-4307122)。
* DMに自動公開されるアップロード済みアセットの場合、ステータスに「AEMで公開済み」が表示されません。 また、「Dynamic Mediaの公開ステータス」列に正しい公開ステータスが表示されません(CQ-4306415)。
* アセットが[!DNL Experience Manager]に公開され、アクティベーション時に[!DNL Dynamic Media]に公開するように設定されている場合、 `scene7FileStatus`メタデータの値は期待どおりに更新されません(CQ-4308269)。
* ビデオプロファイルの編集時に、[!DNL Experience Manager]にはビデオプリセットに設定された高さとビットレートの値が表示されません。 フィールドは空白で表示されます(CQ-4311828)。

### [!DNL Commerce] {#commerce-6580}

* コマースのすべての製品のカスタムタグを作成できない(CQ-4310682)。

* 製品アセットの参照の更新により、ProductAssetListenerスレッドがJCRへのコミットを完了するまで、レプリケーションスレッドが待機状態になる(NPR-35269)。

### Platform {#platform-6580}

* タブを持たないCoralタブビューコンポーネントを使用し、基盤バリデーターをトリガーすると、次のエラーが発生します(NPR-35636)。

   ```TXT
    Uncaught TypeError: Cannot set property 'invalid' of undefined
     at enable (foundation.js:10703)
     at foundation.js:10710
   ```

* 名前にコンマを含むノードのSCD転送レプリケーションが、削除イベントで失敗する(NPR-35191)。

* AEM 6.5.7にアップグレードすると、ビルドが失敗し始めます。 理由は、古いバージョンがuber-jarに埋め込まれているか、jackson-coreがないかです(GRANITE-33006)。

### ユーザーインターフェイス {#ui-6580}

* アセットコンソールで、フォルダー内のドキュメントのカード表示からリスト表示に切り替えると、並べ替えが適切に機能しない(NPR-35842)。

* テキストコンポーネント内のテキストをハイパーリンクすると、検索機能に適切な結果が表示されない(NPR-35849)。

* 値が必須とマークされた非表示フィールドに指定されていない場合、コンポーネントの保存がブロックされます(NPR-35219)。

### 統合 {#integrations-6580}

* IMSテナントIDとTargetクライアントコードに異なる値を使用すると、 [!DNL Experience Manager]と[!DNL Adobe Target]の統合に失敗します(NPR-35342)。

### 翻訳プロジェクト{#translation-6580}

* [!DNL Experience Manager]で翻訳ジョブを書き出すまたは読み込む際の問題(NPR-35259)。

### Campaign {#campaign-6580}

* タッチUIで標準のテンプレートを使用してキャンペーンページを作成し、ページのプロパティダイアログの「 Eメール」タブを開くと、件名フィールドと本文フィールドのパーソナライゼーション変数が無効のままになります(CQ-4312388)。

### [!DNL Communities] {#communities-6580}

* コミュニティグループにページ構造を追加すると、パンくずリストの[!UICONTROL Group]タイトルが、最初の[!UICONTROL Page]のタイトルに変更されます(NPR-35803)。
* モデレーターとは異なり、標準コミュニティメンバーはドラフト投稿にアクセスして編集できません(NPR-35339)。
* `DSRPReindexServlet`によるアクセス制御とサービス拒否が壊れ、インデックス作成が完了するまでコミュニティサイトが停止します(NPR-35591)。
* を[!UICONTROL 管理者]フィールドから削除しても、実際にはバックエンドからは削除されません(NPR-35592、NPR-35611)。
* [!UICONTROL メッセージを構成]コンポーネントは、入力されたテキストが部分一致の場合、結果を返しません(NPR-35666)。

* **[!UICONTROL タグを追加]**&#x200B;を選択して新しいブログにタグを追加しようとすると、パフォーマンスに影響が出たり遅くなったりする場合があります。 パフォーマンスを向上させるには、[cqTagLucene-0.0.1.zip hotfix](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/cqTagLucene-0.0.1.zip)をインストールします。

### [!DNL Brand Portal] {#brandportal-6580}

* [!UICONTROL アセット投稿]タイプのフォルダーにメンバーを追加すると、ユーザーインターフェイスに「[!UICONTROL ユーザーまたはグループを追加]」と表示されます。ただし、Brand Portalのアクティブなユーザーのみがサポートされ、グループはサポートされません。(NPR-35332)

### [!DNL Forms] {#forms-6580}

>[!NOTE]
>
>[!DNL Experience Manager Forms] では、予定されている [!DNL Experience Manager] サービスパックリリース日の 1 週間後にアドオンパッケージをリリースします。

**アダプティブフォーム**

* アダプティブフォーム内に複数のインスタンスを持つ繰り返し可能なパネルに、繰り返し可能な行を含む表を挿入すると、その表は常にパネルの最初のインスタンスに追加される。(NPR-35635)

* アダプティブフォームでタブフォーカスが正常に検証された後にCAPTCHAコンポーネントに再び到達すると、 [!DNL Experience Manager Forms]は`Provide Captcha phrase to proceed`エラーメッセージを表示する(NPR-35539)。

**インタラクティブコミュニケーション**

* 翻訳済みのフォームを送信すると、送信メッセージが英語で表示され、適切な言語に翻訳されない(NPR-35808)。

* 添付されたXDPまたはドキュメントフラグメントに非表示条件を含めると、インタラクティブ通信の読み込みに失敗する。(NPR-35745)

**Correspondence Management**

* レターを編集する際、条件を持つモジュールの読み込みに時間がかかる(NPR-35325)。

* 左側のナビゲーションパネルからレターに含まれていないアセットを選択し、次のアセットを選択した場合、青いハイライトは、以前に選択されたアセットから削除されません(NPR-35851)。

* レターのテキストフィールドを編集すると、[!DNL Experience Manager Forms]に`Text Edit Failed`エラーメッセージが表示されます(CQ-4313770)。

**ワークフロー**

* iOS用の[!DNL Experience Manager Forms]モバイルアプリケーションでアダプティブフォームを開こうとすると、アプリケーションの応答が停止します(CQ-4314825)。

* HTMLワークスペースの[!UICONTROL To-do]タブにHTML文字が表示される(NPR-35298)。

**XMLFM**

* Outputサービスを使用してXMLドキュメントを生成する場合、一部のXMLファイルに対して`OutputServiceException`エラーが発生します(CQ-4311341、CQ-4313893)。

* 箇条書きの最初の文字に上付き文字プロパティを適用すると、箇条書きのサイズが小さくなります(CQ-4306476)。

* Output Serviceを使用して生成されるPDF formsには、境界線は含まれません(CQ-4312564)。

**デザイナー**

* [!DNL Experience Manager Forms] DesignerでXDPファイルを開くと、designer.logファイルがXDPファイルと同じフォルダーに生成されます(CQ-4309427、CQ-4310865)。

**HTML5 のフォーム**

* [!DNL iOS 14.1 or 14.2]の[!DNL Safari] Webブラウザーでアダプティブフォームのチェックボックスをオンにすると、追加のフィールドが表示されない(NPR-35652)。

**Forms Management**

* XDPファイルのCRXリポジトリへの一括アップロードが正常に完了したことを示す確認メッセージが表示されない(NPR-35546)。

**Document Security**

* AdminUIの「[!UICONTROL ポリシー]を編集」オプションに関して複数の問題が報告された(NPR-35747)。

セキュリティ更新について詳しくは、[Experience Managerセキュリティ速報ページ](https://helpx.adobe.com/security/products/experience-manager.html)を参照してください。

## 6.5.8.0 のインストール {#install}

**設定要件と詳細情報**

* Experience Manager6.5.8.0にはExperience Manager6.5が必要です。詳細な手順については、[アップグレードのドキュメント](/help/sites-deploying/upgrade.md)を参照してください。
* サービスパックのダウンロードは、Adobe[「Software Distribution」](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)で入手できます。
* MongoDBおよび複数のインスタンスを使用したデプロイメントで、パッケージマネージャーを使用して、いずれかのオーサーインスタンスにExperience Manager6.5.8.0をインストールします。

>[!NOTE]
>
>Adobeは、[!DNL Adobe Experience Manager] 6.5.8.0パッケージの削除またはアンインストールはお勧めしません。

### サービスパック{#install-service-pack}をインストールします。

[!DNL Adobe Experience Manager] 6.5インスタンスにService Packをインストールするには、次の手順に従います。

1. インスタンスが更新モードの場合（以前のバージョンから更新された場合）は、インストール前にインスタンスを再起動します。 Adobeでは、インスタンスの現在の稼動時間が長い場合に再起動を推奨します。

1. インストールする前に、[!DNL Experience Manager]インスタンスのスナップショットまたは新しいバックアップを作成します。

1. [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.8.zip)からサービスパックをダウンロードします。

1. パッケージマネージャーを開き「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。詳しくは、[パッケージマネージャー](/help/sites-administering/package-manager.md)を参照してください。

1. パッケージを選択し、「**[!UICONTROL インストール]**」をクリックします。

1. S3コネクタを更新するには、Service Packのインストール後にインスタンスを停止し、既存のコネクタをinstallフォルダーに用意されている新しいバイナリファイルで置き換えて、インスタンスを再起動します。 [Amazon S3データストア](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)を参照してください。

>[!NOTE]
>
>サービスパックのインストール中に、パッケージマネージャーUIのダイアログが終了することがあります。 Adobeでは、エラーログが安定するのを待ってから、デプロイメントにアクセスすることをお勧めします。 アップデータバンドルのアンインストールに関連する特定のログが表示されるのを待ってから、インストールが成功したことを確認します。 通常、[!DNL Safari]ではこのような処理が行われますが、どのブラウザーでも断続的に発生する場合があります。

**自動インストール**

作業用インスタンスにAdobe Experience Manager 6.5.8.0を自動的にインストールするには、次の2つの方法があります。

A.サーバーがオンラインで使用可能になったら、 `../crx-quickstart/install`フォルダーにパッケージを配置します。 パッケージが自動的にインストールされます。

B.パッケージマネージャーの[HTTP APIを使用します。](/help/sites-administering/package-manager.md#package-share) `cmd=install&recursive=true`を使用して、ネストされたパッケージをインストールします。

>[!NOTE]
>
>Adobe Experience Manager 6.5.8.0では、Bootstrapのインストールはサポートされていません。

**インストールの検証**

1. 製品情報ページ(`/system/console/productinfo`)に、[!UICONTROL インストール済みの製品]の下に、更新されたバージョン文字列`Adobe Experience Manager (6.5.8.0)`が表示されます。

1. OSGiコンソール内のOSGiバンドルは、すべて&#x200B;**[!UICONTROL ACTIVE]**&#x200B;または&#x200B;**[!UICONTROL FRAGMENT]**&#x200B;です(Webコンソールを使用：`/system/console/bundles`)です。

1. OSGiバンドル`org.apache.jackrabbit.oak-core`は、バージョン1.22.3以降です(Webコンソールを使用：`/system/console/bundles`)です。

このリリースでの動作が認定されたプラットフォームについては、[技術要件](/help/sites-deploying/technical-requirements.md)を参照してください。

### Adobe Experience Manager Formsアドオンパッケージ{#install-aem-forms-add-on-package}をインストールします

>[!NOTE]
>
>Formsを使用していない場合はスキップします。 Experience ManagerFormsの修正は、スケジュールされた[!DNL Experience Manager] Service Packリリースの1週間後に、別のアドオンパッケージを通じて配信されます。

1. Adobe Experience Manager Service Packがインストールされていることを確認します。
1. [AEM Forms リリース](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)のリストから、使用しているオペレーティングシステムに対応する Forms アドオンパッケージをダウンロードします。
1. [AEM Formsアドオンパッケージのインストール](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package)の説明に従って、Formsアドオンパッケージをインストールします。

>[!NOTE]
>
>AEM 6.5.8.0には、[AEM Forms互換性パッケージ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases)の新しいバージョンが含まれています。 古いバージョンのAEM Forms互換パッケージを使用し、AEM 6.5.8.0に更新する場合は、Formsアドオンパッケージのインストール後に、最新バージョンのパッケージをインストールします。

### JEE上のAdobe Experience Manager Forms {#install-aem-forms-jee-installer}のインストール

>[!NOTE]
>
>JEE で AEM Forms を使用していない場合はスキップします。JEE上のAdobe Experience Manager Formsの修正は、別のインストーラーを使用して提供されます。

JEE上のFormsExperience Manager用の累積インストーラーのインストールとデプロイ後の設定について詳しくは、[リリースノート](jee-patch-installer-65.md)を参照してください。

>[!NOTE]
>
>JEE上のFormsExperience Manager用の累積インストーラーをインストールしたら、最新のFormsアドオンパッケージをインストールし、`crx-repository\install`フォルダーからFormsアドオンパッケージを削除して、サーバーを再起動します。

### UberJar {#uber-jar}

Experience Manager6.5.8.0用のUberJarは、[Maven Centralリポジトリ](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.8/)で入手できます。

MavenプロジェクトでUberJarを使用するには、[UberJar](/help/sites-developing/ht-projects-maven.md)の使用方法を参照し、プロジェクトPOMに次の依存関係を含めます。

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.8</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJarおよびその他の関連アーティファクトは、AdobeのパブリックMavenリポジトリ(`repo.adobe.com`)ではなく、Maven Centralリポジトリで使用できます。 メインのUberJarファイルの名前が`uber-jar-<version>.jar`に変更されます。 したがって、`dependency`タグには`apis`を値とする`classifier`はありません。

## 非推奨（廃止予定）の機能 {#removed-deprecated-features}

[!DNL Experience Manager] 6.5.7.0で非推奨とマークされた機能の一覧を以下に示します。機能は、最初に廃止され、後で将来のリリースで削除されます。 通常は、代替オプションが提供されます。

機能または機能をデプロイメントで使用するかどうかを確認します。 また、別のオプションを使用するように実装を変更することを計画します。

| 領域 | 機能 | 代替手段 |
|---|---|---|
| 統合 | **[!UICONTROL AEMクラウドサービスのオプトイン]**&#x200B;画面は非推奨（廃止予定）となりました。 Experience Manager6.5でExperience ManagerとAdobe Targetの統合が更新され、AdobeIMSとI/Oを介した認証を使用するAdobe Target Standard APIがサポートされるようになり、分析とパーソナライゼーション用のExperience Managerページを実装するためのAdobeLaunchの役割が増加しています。 | 各System Cloudサービスを使用して、システム接続、AdobeIMS認証、[!DNL Adobe I/O]統合をExperience Managerします。 |
| コネクタ | Experience Manager6.5では、Microsoft SharePoint 2010およびMicrosoft SharePoint 2013用のAdobeJCR Connectorが非推奨（廃止予定）となりました。 | 該当なし |

## 既知の問題 {#known-issues}

* [!DNL Experience Manager]インスタンスを6.5から6.5.8.0バージョンにアップグレードする場合は、`error.log`ファイルで`RRD4JReporter`例外を表示できます。 インスタンスを再起動して問題を解決します。

* [!DNL Experience Manager] 6.5 Service Pack 5または以前のService Packを[!DNL Experience Manager] 6.5にインストールすると、（`/var/workflow/models/dam`で作成された）アセットカスタムワークフローモデルのランタイムコピーが削除されます。
ランタイムコピーを取得するには、HTTP APIを使用して、カスタムワークフローモデルのデザイン時コピーをそのランタイムコピーと同期することをお勧めします。
   `<designModelPath>/jcr:content.generate.json`

* [!UICONTROL ルールの定義]ダイアログを使用して[!UICONTROL フォルダーメタデータスキーマFormsエディター]および[!UICONTROL メタデータスキーマFormsエディター]でカスケードルールを編集および作成する際に問題が発生した場合は、Adobeカスタマーケアにお問い合わせください。 既に作成および保存されたルールは、期待どおりに動作しています。

* 階層内のフォルダーの名前が[!DNL Experience Manager Assets]で変更され、アセットを含むネストされたフォルダーが[!DNL Brand Portal]に公開された場合、ルートフォルダーが再び公開されるまで、フォルダーのタイトルは[!DNL Brand Portal]で更新されません。

* アダプティブフォームで初めてフィールドの設定を選択した場合、設定を保存するオプションはプロパティブラウザーに表示されません。 同じエディターでアダプティブフォームの他のフィールドを設定するように選択すると、問題が解決します。

* [!UICONTROL Connected assets configuration]ウィザードがインストール後に404エラーメッセージを返した場合は、パッケージマネージャーを使用して`cq-remotedam-client-ui-content`パッケージと`cq-remotedam-client-ui-components`パッケージを手動で再インストールします。

* Experience Manager6.5.x.xのインストール中に、次のエラーおよび警告メッセージが表示される場合があります。
   * 「Adobe Target統合がTarget Standard API（IMS認証）を使用してExperience Managerで設定されている場合、エクスペリエンスフラグメントをTargetに書き出すと、間違ったオファータイプが作成されます。 Target では、「エクスペリエンスフラグメント」/source「Adobe Experience Manager」タイプではなく、「HTML」/source「Adobe Target Classic」タイプのオファーをいくつか作成します。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * SUM、MAX、MINなどの集計関数が使用されると、アダプティブフォームのサーバー側検証が失敗します(CQ-4274424)。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * ショッパブルバナービューアでアセットをプレビューすると、Dynamic Mediaのインタラクティブ画像のホットスポットが表示されない。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` :登録変更が完了するのを待機中のタイムアウトが未登録です。

## {#osgi-bundles-and-content-packages-included}に含まれるOSGiバンドルおよびコンテンツパッケージ

以下のテキストドキュメントは、[!DNL Experience Manager] 6.5.8.0に含まれるOSGiバンドルとコンテンツパッケージの一覧です。

* [Experience Manager6.5.8.0に含まれているOSGiバンドルの一覧](assets/6580_bundles.txt)

* [Experience Manager6.5.8.0に含まれているコンテンツパッケージの一覧](assets/6580_packages.txt)

## 制限付きWebサイト{#restricted-sites}

これらのWebサイトは、お客様のみが利用できます。 アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [Adobeカスタマーケアへの問い合わせ方法](https://experienceleague.adobe.com/docs/customer-one/using/home.html)を参照してください。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5リリースノート](/help/release-notes/release-notes.md)
* [[!DNL Experience Manager] 製品ページ](https://www.adobe.com/marketing/experience-manager.html)
* [[!DNL Experience Manager] 6.5ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=ja)
* [Adobe Priority 製品アップデート](https://www.adobe.com/subscription/priority-product-update.html)のサブスクリプションを購入する

