---
title: '[!DNL Experience Manager] 6.5サービスパックリリースノート'
description: ' [!DNL Adobe Experience Manager] 6.5 service pack 8に固有のリリースノート'
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: d96730eed6447815c40307a8d60b6ffc9ff45c2e
workflow-type: tm+mt
source-wordcount: '2822'
ht-degree: 5%

---


# [!DNL Adobe Experience Manager] 6.5サービスパックリリースノート  {#aem-service-pack-release-notes}

## リリース情報 {#release-information}

| 製品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| バージョン | 6.5.8.0 |
| タイプ | Service Pack のリリース |
| 日付 | 2021年3月11日 |
| ダウンロード URL | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.8.zip) |

<!-- TBD: Update the SD link when SP8 is available. Same link is duplicated below in install -->

## [!DNL Adobe Experience Manager] 6.5.8.0 {#what-s-included-in-aem}に含まれるもの

[!DNL Adobe Experience Manager] 6.5.8.0には、新機能、お客様からリクエストされた主な機能強化、パフォーマンス、安定性、セキュリティの向上が含まれています。これらの機能は、2019年4月の6.5リリースのリリース以降にリリースされました。サービスパックは[!DNL Adobe Experience Manager] 6.5にインストールされています。

[!DNL Adobe Experience Manager] 6.5.8.0で導入された主な機能と拡張機能は次のとおりです。

<!-- TBD:
* Using the Connected Assets functionality, it is now possible to connect up to 3 [!DNL Sites] instances with 1 [!DNL Assets] instances. The configuration user interface now allows the administrators to provide the details of these [!DNL Sites] instances. -->

* [接続されたアセット機能](/help/assets/use-assets-across-connected-assets-instances.md)を使用する場合、アセットを使用するすべての[!DNL Sites]ページのリストを表示できるようになりました。 アセットへのこれらの参照は、アセットの[!UICONTROL プロパティ]ページで利用できます。 これにより、管理者、マーケターおよびライブラリは、アセットの使用に関する完全な表示を得ることができ、トラッキング、管理、ブランドの一貫性を向上できます。

* Webページで参照されているアセットを削除すると、[!DNL Experience Manager]に警告が表示されます。 参照されているアセットを強制的に削除するか、アセットの[!DNL Properties]ページに表示されている参照を確認して変更できます。 参照をクリックすると、ローカルページとリモートページの[!DNL Sites]が開きます。

* [!UICONTROL 名前]、[!UICONTROL 最終変更日、]、[!UICONTROL 最終ロールアウト日]の各プロパティを使用して、ロールアウトに使用できるライブコピーページを並べ替えます。

* 組み込み型のリポジトリ(Apache Jackrabbit Oak)が1.22.6に更新されました。 <!-- TBD: Mention the version -->

[!DNL Experience Manager] 6.5.8.0で導入された機能と拡張機能の完全なリストについては、[ [!DNL Adobe Experience Manager] 6.5 Service Pack 8](new-features-latest-service-pack.md)の新機能を参照してください。

[!DNL Experience Manager] 6.5.8.0リリースでの修正のリストを以下に示します。

### [!DNL Sites] {#sites-6580}

* ページをブループリントに移動すると、リンク先は更新されません(NPR-35724)。
* 一部のブラウザーで、Tizenベースのプレイヤーの認証に失敗します。 この問題は、samesite=none属性をサポートしていないブラウザー(NPR-35589)で発生します。
* ロック解除されたレスポンシブコンテナは、許可されているコンポーネントを表示しません(NPR-35565)。
* 新しく追加されたページのライブコピーを作成すると、言語マスターは各ドメインに対して2つのコピーを作成します(NPR-35545)。
* `org.apache.felix.scr.impl.ComponentRegistry`タイマーが原因で多数のスレッドがブロックされた場合、SCRコンポーネントレジストリでデッドロックが発生します。 その結果、[!DNL Experience Manager]は無限に応答を停止します(GRANITE-33125,FELIX-6252)。
* サイドレールで特定のアセットを検索すると、結果には、検索されていないアセットが含まれます(NPR-35524)。
* Experience Managerインスタンスに対してSSLを有効にすると、コンテキストパスが削除されます(NPR-35477)。
* リストを作成する場合、最初の要素としてテキストを追加し、2番目の要素としてテーブルを追加し、テーブル内にリストを追加すると、親リストが歪みます(NPR-35465)。
* 連続するリスト項目で異なるプラグインを使用すると、リスト項目に余分な<br>タグが追加されます(NPR-35464)。
* 2つの段落の間にリストを配置する場合、テーブルをリストに追加することはできません(NPR-35356)。
* AEMインスタンスをAEM 6.3からAEM 6.5にアップグレードすると、アップグレードインスタンスが開始にアップグレードされるまでに時間がかかります(NPR-35323)。
* 括弧()を含むAEMアセットを複製する場合。 名前では、レプリケーションは失敗します(GRANITE-27004、NPR-35315)。
* リッチテキストエディターに見出しを追加すると、段落ボタンは無効になります(NPR-35256)。
* 既存のリストに項目を追加すると、次に表示される折りたたみ可能な項目または切り替え可能なリスト(NPR-35206)が削除されます。
* [ロールアウトページ]オプションを選択すると、使用可能なすべてのライブコピーが含まれたダイアログボックスが表示され、自動ロールアウトが行われます。 ページのライブコピーは、ユーザーの操作なしですべての地域にロールアウトされます(NPR-35138)。
* 「子を含む」オプションを使用する場合、「文書の管理」オプションでは、すべてのページがリストされるわけではありません。 22ページのみが掲載される(NPR-35086)。
* ポリシーが編集されると、テキストコンポーネントはポリシーの変更を保持しません(NPR-35070)。
* 番号付きリストで一部の項目をインデントする場合、すべての項目で同じ番号が維持されますが、インデントが同じ項目については、番号は1から開始する必要があります。(CQ-4313011)
* 縮小が有効な場合、ページやコンポーネントを編集できません。 問題は、AEM 6.5 Service Pack 7のインストール後に開始されました(CQ-431133)。
* オムニ検索とアセットフィルターが無関係な結果または結果を返さない(CQ-4312322、NPR-35793)。
* 複数のページが同時にクライアントライブラリにアクセスする場合、HTMLライブラリマネージャーはクライアントライブラリの読み込みに失敗します。 その結果、ページが正しくレンダリングされません(NPR-35538)。
* [!DNL Experience Manager](NPR-35294)でSSLを設定すると、コンテキストパスが自動的に削除されます。
* パッケージマネージャーは、「ログアウト」オプション(NPR-35160)をクリックした後でもユーザーをログアウトしません。

### [!DNL Assets] {#assets-6580}

[!DNL Adobe Experience Manager] 6.5.8.0では、次の問題が [!DNL Assets] 修正され、次の機能強化が行われました。

* アセットの以前のバージョンを復元すると、イベントDamEvent.Type RESTOREDはOSGiコンソール(NPR-35789)でトリガーされません。
* `IndexWriter.merge` を指定すると、スマートタグ機能によって大き `OutOfMemoryError` い `/oak:index/lucene` と `/oak:index/ntBaseLucene` インデックスが作成されるので、エラーが発生します(NPR-35651)。
* マルチバイト文字を名前に含む[!UICONTROL アセット貢献度]タイプのフォルダーを保存しようとすると、エラーメッセージが表示されます(NPR-35605)。
* カスケードメタデータのサブタイプフィールドを使用すると、誤った「このフィールドに入力してください」エラーが発生します(NPR-35643)。
* 既存のアセットを[!DNL Assets]ユーザーインターフェイスにドラッグして新しいバージョンを作成すると、メタデータの変更が永続的に行われません(NPR-34940)。
* カスケードメニュー用のメタデータスキーマエディターでルールを作成する場合、[!UICONTROL 依存オン]オプションは同じ名前を繰り返します(NPR-35596)。
* [!UICONTROL アセット管理者の検索レール]を編集した後、類似性検索が機能しない(NPR-35588)。
* フォルダー内から、左のナビゲーションバーの「フィルター]」をクリックしてアセット検索を開くと、[!UICONTROL ステータス]/[!UICONTROL チェックアウト]/[!UICONTROL チェックアウト]が機能しません(NPR-35530)。[!UICONTROL 
* アセットのすべてのスマートタグを削除して変更を保存しようとしても、タグは削除されません。 ただし、ユーザーインターフェイスは、変更が保存されると示します(NPR-35519)。
* 順序指定可能なフォルダー(NPR-35516)内のリスト表示で、アセットの並べ替えや並べ替えを行うことはできません。
* 初期設定のメタデータスキーマを編集すると、アセットの[!UICONTROL プロパティ]ページのタグフィールドがテキストフィールドに変わります。 この変更により、ユーザーがオンデマンドタグを追加できない状態になり、タグがリポジトリ(NPR-35478)に文字列として保存されます。
* アセットをダウンロードする際に、有効な電子メールアドレスを持たない名前を指定した場合、ダウンロードオプションは使用できません。 ただし、ダウンロードダイアログの別のオプションが選択されている場合は、このボタンは有効になりますが、電子メールは送信されません(NPR-35365)。
* ユーザーは、[!DNL Adobe InDesign]でアセットを編集した後にチェックインできず、権限がないことに関するエラーを受け取ることができません(NPR-35341)。
* ハンドルバーのJavaScriptライブラリがv4.7.6にアップグレードされました(NPR-35333)。
* バルクメタデータ編集から開始し、1つの項目が選択されたままになるまで項目の選択を解除すると、メタデータエディターインターフェイスが期待どおりに動作しなくなります(NPR-35144)。
* `assets.html`ページ内でクリックすると、グローバルナビゲーションで正しいコンソールが開かない(CQ-4312311)。
* [!DNL Assets] RGBレンディション(CQ-4310190)を持つアセットのRGBレンディションを表示しません。
* メニューの「[!UICONTROL 関連付け]」オプションは、[!UICONTROL プロパティ]ページ(CQ-4310188)に正しく表示されません。
* ドキュメントのfiletype filterを使用してアセットを検索し、スマートコレクションを作成する場合、コレクションにアクセスする際にフィルターは適用されません。 代わりに、すべてのタイプのアセットが検索に表示されます(NPR-35759)。
* [!DNL Assets]ユーザーインターフェイス(NPR-35901)からライトボックス内のアセットをドラッグして追加することはできません。
* 名前の競合を解決した後に既存のアセットの新しいバージョンを作成すると、元のアセットのメタデータが上書きされます(CQ-4313594)。
* 検索フィルターまたは述語を使用してアセット検索をフィルタリングする場合、表示するアセットを開くか編集し、検索結果ページに戻ると、フィルターは機能しません。 検索されたすべてのアセットがフィルタリングされずに一覧表示されます(NPR-35913)。

#### [!DNL Dynamic Media] {#dynamic-media-6580}

* RESS画像プリセットのURLオプションは、アセットの詳細ページで有効になります。 現在は、「動的レンディション」セクションでRESS画像プリセットを選択した場合に、アセットの詳細ページでURLとRESSの両方のオプションを使用できます。 (CQ-4311241)
* インタラクティブメディアコンポーネント — インタラクティブビデオは、ユーザーが選択的発行設定を使用する[!DNL Experience Manager]を持っている場合、機能しません。(CQ-4311054)
* アセットをフォルダー間で移動する場合、API経由の[!DNL Experience Manager]と[!DNL Dynamic Media–Scene7]の間の同期は非常に遅くなります(CQ-4310001)。
* Omnisearchを使用すると、ログのサイズが大幅に増えます。(CQ-4309153)
* 選択的な同期が有効で、アセットが同期フォルダーにコピー（移動されない）されると、期待どおりに同期されません(CQ-4307122)。
* アップロードしたアセットがDMに自動公開される場合、ステータスに「AEMで公開済み」は表示されません。 また、「Dynamic Media公開ステータス」列に正しい公開ステータスが表示されません(CQ-4306415)。
* アセットが[!DNL Experience Manager]に発行され、アクティベーション上の[!DNL Dynamic Media]に発行するように設定されている場合、`scene7FileStatus`メタデータ値は期待どおりに更新されません(CQ-4308269)。
* ビデオプロファイルを編集する場合、[!DNL Experience Manager]には、ビデオプリセットに設定された高さとビットレートの値は表示されません。 フィールドが空白で表示されます。(CQ-4311828)

### [!DNL Commerce] {#commerce-6580}

* コマースのすべての製品に対してカスタムタグを作成できません(CQ-4310682)。

* 製品アセット参照の更新により、ProductAssetListenerスレッドがJCRへのコミットを完了するまで、レプリケーションスレッドは待機状態になります(NPR-35269)。

### Platform {#platform-6580}

* タブのないCoral Tab表示コンポーネントを使用し、その後Foundationバリデーターをトリガーすると、次のエラーが発生します(NPR-35636)。

   ```TXT
    Uncaught TypeError: Cannot set property 'invalid' of undefined
     at enable (foundation.js:10703)
     at foundation.js:10710
   ```

* 名前にコンマが含まれるノード(NPR-35191)の削除イベントで、SCDの転送レプリケーションが失敗する。

* AEM 6.5.7にアップグレードすると、ビルド開始が失敗します。 理由は、古いバージョンであるか、jackson-coreがuber-jarに埋め込まれていない(GRANITE-33006)ためです。

### ユーザーインターフェイス {#ui-6580}

* アセットコンソール内のドキュメントのカード表示からリスト表示に切り替えると、並べ替えが適切に動作しません(NPR-35842)。

* テキストコンポーネント内のテキストをハイパーリンクする場合、検索機能では適切な結果が表示されません(NPR-35849)。

* 必須とマークされた非表示のフィールドに値が指定されない場合、コンポーネントの保存がブロックされます(NPR-35219)。

### 統合 {#integrations-6580}

* IMSテナントIDとターゲットクライアントコードに異なる値を使用すると、[!DNL Experience Manager]は[!DNL Adobe Target] (NPR-35342)との統合に失敗します。

### 翻訳プロジェクト{#translation-6580}

* 翻訳ジョブを[!DNL Experience Manager]で書き出しまたは読み込むときに発生する問題(NPR-35259)。

### Campaign {#campaign-6580}

* タッチUIの標準搭載されたキャンペーンを使用してテンプレートページを作成し、ページプロパティダイアログの「電子メール」タブを開くと、件名フィールドと本文フィールドのパーソナライズ変数は無効のままになります。(CQ-4312388)

### [!DNL Communities] {#communities-6580}

* コミュニティグループにページ構造を追加すると、パンくずリスト内の[!UICONTROL Group]タイトルが、最初の[!UICONTROL Page](NPR-35803)のタイトルに変更されます。
* モデレーターとは異なり、標準コミュニティのメンバーはドラフト投稿にアクセスして編集することができません(NPR-35339)。
* DSRPReindexServletを使用したアクセス制御とサービス拒否(DoS)。インデックス作成が完了するまでコミュニティのサイトを停止します(NPR-35591)。
* [!UICONTROL 管理者]フィールドから[!UICONTROL すべてのユーザー]を削除しても、実際にはバックエンド(NPR-35592、NPR-35611)からは削除されません。
* [!UICONTROL 構成メッセージ]コンポーネントは、入力されたテキストが部分一致の場合、結果を返しません(NPR-35666)。

### [!DNL Brand Portal] {#brandportal-6580}

* [!UICONTROL アセット貢献度]タイプのフォルダーにメンバーを追加すると、ユーザーインターフェイスに「[!UICONTROL 追加ユーザー」または「グループ]」のキャプションが表示されますが、ブランドポータルのアクティブユーザーのみがサポートされ、グループはサポートされません(NPR-35332)。

### [!DNL Forms] {#forms-6580}

>[!NOTE]
>
>[!DNL Experience Manager Forms] では、予定されている [!DNL Experience Manager] サービスパックリリース日の 1 週間後にアドオンパッケージをリリースします。

セキュリティ更新について詳しくは、[Experience Managerのセキュリティ速報ページ](https://helpx.adobe.com/security/products/experience-manager.html)を参照してください。

## 6.5.8.0 {#install}のインストール

**設定要件と詳細情報**

* Experience Manager6.5.8.0では、Experience Manager6.5が必要です。詳細な手順については、[アップグレードドキュメント](/help/sites-deploying/upgrade.md)を参照してください。
* Service Packのダウンロードは、Adobe[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)で入手できます。
* MongoDBと複数のインスタンスを使用するデプロイメントでは、Package Managerを使用して、いずれかの作成者インスタンスにExperience Manager6.5.8.0をインストールします。

>[!NOTE]
>
>[!DNL Adobe Experience Manager] 6.5.8.0パッケージの削除またはアンインストールは、Adobeにお勧めしません。

### サービスパック{#install-service-pack}をインストールします

[!DNL Adobe Experience Manager] 6.5インスタンスにService Packをインストールするには、次の手順に従います。

1. インスタンスが更新モードの場合（これは、インスタンスが以前のバージョンから更新された場合）、インストール前にインスタンスを再起動します。 Adobeでは、インスタンスの現在の稼働時間が長い場合は再起動を推奨します。

1. インストールする前に、[!DNL Experience Manager]インスタンスのスナップショットまたは新規バックアップを作成します。

1. [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.8.zip)からService Packをダウンロードします。

1. パッケージマネージャーを開き「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。詳しくは、[パッケージマネージャー](/help/sites-administering/package-manager.md)を参照してください。

1. パッケージを選択し、「**[!UICONTROL インストール]**」をクリックします。

1. S3コネクタを更新するには、Service Packのインストール後にインスタンスを停止し、既存のコネクタをinstallフォルダーに指定された新しいバイナリファイルに置き換えてから、インスタンスを再起動します。 [AmazonS3データストア](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)を参照してください。

>[!NOTE]
>
>Service Packのインストール中に、Package Manager UIのダイアログが閉じることがあります。 Adobeでは、エラーログが安定するのを待ってからデプロイメントにアクセスすることをお勧めします。 アップデーターバンドルのアンインストールに関連する特定のログが表示されるのを待ってから、インストールが成功したことを確認してください。 通常、これは[!DNL Safari]で起こりますが、どのブラウザーでも断続的に起こる可能性があります。

**自動インストール**

作業インスタンスにAdobe Experience Manager6.5.8.0を自動的にインストールするには、次の2つの方法があります。

A.サーバーがオンラインで使用できる状態で、パッケージを`../crx-quickstart/install`フォルダーに配置します。 パッケージが自動的にインストールされます。

B. Package Manager](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html)の[HTTP APIを使用します。 `cmd=install&recursive=true`を使用して、ネストされたパッケージをインストールします。

>[!NOTE]
>
>Adobe Experience Manager6.5.8.0は、Bootstrapのインストールをサポートしていません。

**インストールの検証**

1. 製品情報ページ(`/system/console/productinfo`)には、[!UICONTROL インストール済み製品]の下に、更新バージョン文字列`Adobe Experience Manager (6.5.8.0)`が表示されます。

1. すべてのOSGiバンドルは、OSGiコンソールで&#x200B;**[!UICONTROL ACTIVE]**&#x200B;または&#x200B;**[!UICONTROL FRAGMENT]**&#x200B;です(Webコンソールを使用：`/system/console/bundles`)。

1. OSGiバンドル`org.apache.jackrabbit.oak-core`はバージョン1.22.3以降です(Webコンソールを使用：`/system/console/bundles`)。

このリリースで動作が確認されたプラットフォームについて詳しくは、[技術要件](/help/sites-deploying/technical-requirements.md)を参照してください。

### UberJar {#uber-jar}

Experience Manager6.5.8.0のUberJarは、[Maven Centralリポジトリ](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.8/)で入手できます。

MavenプロジェクトでUberJarを使用するには、[UberJarの使用方法](/help/sites-developing/ht-projects-maven.md)を参照し、プロジェクトPOMに次の依存関係を含めます。

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
>UberJarおよびその他の関連アーティファクトは、AdobeのパブリックMavenリポジトリ(`repo.adobe.com`)ではなく、Maven Centralリポジトリで使用できます。 メインのUberJarファイルの名前が`uber-jar-<version>.jar`に変更されます。 したがって、`dependency`タグには`apis`を値として持つ`classifier`はありません。

## 非推奨（廃止予定）の機能 {#removed-deprecated-features}

以下は、[!DNL Experience Manager] 6.5.7.0で非推奨とマークされた機能と機能のリストです。機能は、最初は非推奨とされ、今後のリリースで削除されます。 通常は、代替オプションが提供されます。

機能または機能を配置で使用するかどうかを確認します。 また、別のオプションを使用するように実装を変更することを計画します。

| 領域 | 機能 | 代替手段 |
|---|---|---|
| 統合 | **[!UICONTROL AEMクラウドサービスのオプトイン]**&#x200B;画面は非推奨です。 Experience Manager6.5で更新されたExperience ManagerとAdobe Targetの統合により、AdobeIMSとI/Oを介した認証を使用するAdobe Target標準APIがサポートされ、分析とパーソナライゼーションのExperience Managerページの実装でAdobeの起動の役割が高まり、オプトインウィザードは機能的に無関係になりました。 | 各Experience Managerクラウドサービスを使用して、システム接続、AdobeIMS認証、[!DNL Adobe I/O]統合を設定します。 |
| コネクタ | Experience Manager6.5では、JCR Connector for Microsoft SharePoint 2010およびMicrosoft SharePoint 2013のAdobeは非推奨です。 | 該当なし |

## 既知の問題 {#known-issues}

* [!DNL Experience Manager]インスタンスを6.5から6.5.8.0バージョンにアップグレードする場合は、`RRD4JReporter`例外を`error.log`ファイルで表示できます。 インスタンスを再起動して問題を解決します。

* [!DNL Experience Manager] 6.5 Service Pack 5または以前のService Packを[!DNL Experience Manager] 6.5にインストールした場合、（`/var/workflow/models/dam`で作成した）アセットカスタムワークフローモデルのランタイムコピーが削除されます。
ランタイムコピーを取得する場合、Adobeでは、HTTP APIを使用して、カスタムワークフローモデルのデザイン時コピーをそのランタイムコピーと同期することを推奨します。
   `<designModelPath>/jcr:content.generate.json`

* [!UICONTROL AdobeメタデータスキーマFormsエディタ]および[!UICONTROL メタデータスキーマFormsエディタ]で、[!UICONTROL ルール]を定義ダイアログを使用してカスケードルールを編集および作成する際に問題が発生した場合は、カスタマーケアにお問い合わせください。 既に作成および保存されているルールは、期待どおりに動作しています。

* 階層内のフォルダーの名前が[!DNL Experience Manager Assets]に変更され、アセットを含むネストされたフォルダーが[!DNL Brand Portal]に発行された場合、ルートフォルダーが再度発行されるまで、フォルダーのタイトルは[!DNL Brand Portal]に更新されません。

* ユーザーがアダプティブフォームで初めてフィールドを設定することを選択した場合、設定を保存するオプションはプロパティブラウザーに表示されません。 同じエディターでアダプティブフォームの他のフィールドの設定を選択すると、問題が解決します。

* [!UICONTROL 接続されたアセットの構成]ウィザードがインストール後に404エラーメッセージを返す場合は、Package Managerを使用して`cq-remotedam-client-ui-content`および`cq-remotedam-client-ui-components`パッケージを手動で再インストールします。

* Experience Manager6.5.x.xのインストール中に、次のエラーおよび警告メッセージが表示される場合があります。
   * 「Target Standard API（IMS認証）を使用して、Adobe Target統合をExperience Managerで設定した場合、エクスペリエンスフラグメントをターゲットに書き出すと、誤ったオファータイプが作成されます。 Target では、「エクスペリエンスフラグメント」/source「Adobe Experience Manager」タイプではなく、「HTML」/source「Adobe Target Classic」タイプのオファーをいくつか作成します。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * SUM、MAX、MINなどの集計機能が使用されると、アダプティブフォームのサーバー側検証に失敗します。 CQ-4274424
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * 買い物かご可能なバナービューアでアセットをプレビューすると、Dynamic Mediaのインタラクティブ画像のホットスポットが表示されません。

## OSGiバンドルとコンテンツパッケージ（{#osgi-bundles-and-content-packages-included}に含まれています）

[!DNL Experience Manager] 6.5.8.0に含まれるOSGiバンドルとコンテンツパッケージに関する次のテキストドキュメントリスト。

* [Experience Manager6.5.8.0に含まれるOSGiバンドルのリスト](assets/6580_bundles.txt)

* [Experience Manager6.5.8.0に含まれるコンテンツパッケージのリスト](assets/6580_packages.txt)

## 制限付きWebサイト{#restricted-sites}

これらのWebサイトは、お客様のみ利用できます。 アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [Adobeカスタマーケアへのお問い合わせ方法](https://experienceleague.adobe.com/docs/customer-one/using/home.html)を参照してください。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5リリースノート](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] 製品ページ](https://www.adobe.com/marketing/experience-manager.html)
>* [[!DNL Experience Manager] 6.5ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=ja)
>* [Adobe Priority 製品アップデート](https://www.adobe.com/subscription/priority-product-update.html)のサブスクリプションを購入する

