---
title: ' [!DNL Adobe Experience Manager]  6.5 のリリースノート'
description: ' [!DNL Adobe Experience Manager] 6.5 のリリース情報、新機能、インストール方法、詳細な変更リストを確認します。'
mini-toc-levels: 4
source-git-commit: 210299acf9f853a19bd513c84c1678e44ba81729
workflow-type: tm+mt
source-wordcount: '2456'
ht-degree: 54%

---

# [!DNL Adobe Experience Manager] 6.5 の最新のサービスパックのリリースノート {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, November 30, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## リリース情報 {#release-information}

| 製品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| バージョン | 6.5.20.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| タイプ | サービスパックのリリース |
| 日付 | 2024 年 2 月 22 日木曜日 <!-- UPDATE FOR EACH NEW RELEASE --> |
| ダウンロード URL | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## [!DNL Experience Manager] 6.5.20.0 の内容 {#what-is-included-in-aem-6520}

[!DNL Experience Manager] 6.5.20.0 には、2019年4月の 6.5 の初公開以降にリリースされた新しい機能、お客様から要望のあった主な機能強化、バグ修正およびパフォーマンスや安定性、セキュリティの向上が含まれています。[!DNL Experience Manager] 6.5 で[このサービスパックをインストール](#install)します。

<!-- UPDATE FOR EACH NEW RELEASE -->

## 主な機能および機能強化

<!-- * _6.5.20.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

このリリースの主な機能と機能強化は次のとおりです。

* Dynamic Mediaは、Apple iOS/iPadOS の可逆 HEIC 画像形式をサポートするようになりました。 詳しくは、 [fmt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html?lang=en) (Dynamic Media Image Serving and Rendering API の )

* マルチサイトマネージャー (MSM) で、フォルダーやサブフォルダーを含むエクスペリエンスフラグメント構造がサポートされ、エクスペリエンスフラグメントをライブコピーに効率的に一括ロールアウトできるようになりました。

<!-- ### [!DNL Forms]

* text -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## サービスパック 20 で修正された問題 {#fixed-issues}

### [!DNL Sites]{#sites-6520}

<!--#### Accessibility{#sites-accessibility-6520}

* text -->

#### 管理ユーザーインターフェイス{#sites-adminui-6520}

* The `Workflow Title` 次の項目でマークされている `*` 必要に応じて検証されますが、検証はおこなわれません。 （SITES-16491）

<!--#### Classic UI{#sites-classicui-6520}

* text -->

#### [!DNL Content Fragments]{#sites-contentfragments-6520}

* ネストされた設定フォルダーはサポートされなくなり、AEM 6.5.18 またはAEM 6.5.19 にアップグレードした後、コンテンツフラグメントモデルフォルダーが表示されなくなりました。 （SITES-18110）
* 一部のサブフォルダーは、継承されたコンテンツフラグメントモデルから選択できません。 フォルダーをサポートするには、 `jcr:content` プロパティに含まれます。ユーザーインターフェイスを介して作成された DAM フォルダーにそのようなノードがある場合でも同様です。 （SITES-17943）

#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-6520}

<!-- REMOVED AS PER EMAIL FROM SAMEER DHAWAN FEBRUARY 19, 2024 * When upgrading AEM from 6.5.19.0 to 6.5.20.0, the path `/libs/cq/graphql/sites/graphiql` was getting deleted. (SITES-19530) CRITICAL -->
* GraphQLクエリを実行して [結果をフィルター](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#filtering) 特定の値が **not** オプションの変数に指定された場合、変数はフィルター評価で無視されます。 （SITES-17051）

<!--#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6520}

* text -->

#### [!DNL Content Fragments] - REST API{#sites-restapi-6520}

* のアップグレードに伴う `org.json` ライブラリでは、小数のデシリアル化方法が変更されました。 「デフォルトで」を「Double」に変換し、今後は BigDecimals に変換する前の手順です。 代わりに、REST API を介して保存されたメタデータプロパティの値が、BigDecimal から倍精度浮動小数点に変換されます。 （SITES-16857）

#### コアバックエンド{#sites-core-backend-6520}

* コンテンツフラグメントのクイック公開を使用すると、読み込みが続行され、公開されません。 つまり、サービスパックをAEM 6.5.7 からAEM 6.5.17 にアップグレードした後、クイック公開がコンテンツフラグメントで機能しない。ユーザーが管理公開を試みたときに機能しました。 ただし、クイック公開を試みると、公開されていませんでした。 特に、 `com.day.cq.wcm.core.impl.reference.ActivationReferenceSearchBuilder` システムがひねくれる原因となった。 （SITES-17311）
* Jackson エクスポーターでは、コンテンツフラグメントをシリアル化できません。ページ内で参照されているコンテンツフラグメント（Jackson エクスポーターコードを使用）とコンテンツフラグメントに追加されたタグがあると、ページ読み込みが中断します。 （SITES-18096）

#### コアコンポーネント{#sites-core-components-6520}

* AEMにCIFコアコンポーネントパッケージをインストールすると、原因がわかります `:type` 変更する既存のコンポーネントの値。 この変更により、ページが追加されたページではレンダリングされなくなります。 （SITES-17601）

#### Campaign 統合{#sites-campaign-integration-6520}

* AEMが許可リストに加える使用していた ( 別名： `whitelist` — 脆弱性の報告による。 この許可リストに加えるでは、お客様が必要な機能を使用できませんでした。 （SITES-16822）

#### エクスペリエンスフラグメント{#sites-experiencefragments-6520}

* MSM for Experience Fragments で、フォルダーやサブフォルダーを含むエクスペリエンスフラグメントコンテンツ構造への一括ロールアウトがサポートされるようになりました。 （SITES-16004）

<!--#### Foundation Components (Legacy){#sites-foundation-components-legacy-6520}

* text

#### Launches{#sites-launches-6520}

* text -->

#### MSM - ライブコピー{#sites-msm-live-copies-6520}

* An &quot;`Is not modifiable`コンポーネントのロールアウト時に「 」例外がスローされます。 特に、 `org.apache.sling.servlets.post.impl.operations.ModifyOperation` 応答の処理中に例外が発生しました。 （SITES-18809）
* エクスペリエンスフラグメントの特定のライブコピーに対して変更をロールアウトできない。 （SITES-17930）
* ユーザーがブループリントページのコンポーネントに注釈を追加してからロールアウトすると、ライブコピーの注釈数が正しく表示されない問題を修正しました。 （SITES-17099）
* タッチグラフィカルユーザーインターフェイスで、親ページから子ページへの MSM ロールアウトボタンが壊れます。選択すると、次のエラーが表示されます。 `Uncaught TypeError: _g.shared is undefined`. （SITES-16991）

#### ページエディター{#sites-pageeditor-6520}

* Formsテーマエディターのプレビューが壊れています。 「プレビュー」を選択すると、読み込みアイコンのみが表示されます。 （SITES-17164）

### [!DNL Assets]{#assets-6520}

* メタデータエディターヘルパーでルールベースのフィールドを検証できず、「必須フィールドが見つかりません」というエラーメッセージが表示される。 （ASSETS-31396）
* PDFを別の場所に移動した後、 **[!UICONTROL ページを表示]** オプションが表示されなくなります。 （ASSETS-30538）
* 読み取り権限を持つ画像を選択できません。 （ASSETS-32199）
* 表示設定でカードサイズを変更できません。 （ASSETS-31667）
* .oft ファイルタイプのアップロード中にアップロードが失敗しました。 （ASSETS-30109）
* カスタムメタデータフィールドをレポートに追加の列として追加しようとすると、チェックボックスがオンになりません。 （ASSETS-31671）
* Asset Service Pack 16 では、アセットの移動操作が適切にExperience Managerされません。 （ASSETS-30598）

#### [!DNL Dynamic Media]{#assets-dm-6520}

* アセットがAEMにアップロードされると、 `Update_asset` ワークフローがトリガーされます。 ただし、ワークフローは完了しません。 ワークフローは、製品のアップロードステップまで完了します。 次の手順はScene7のバッチアップロードですが、そのプロセスはAEMに取り込まれません。 （ASSETS-30443）
* Dynamic MediaコンポーネントでDynamic Media以外のビデオを適切に処理するための、より優れた方法が必要です。 この問題は、インスタンス化中に例外が発生していました `dynamicmedia_sly.js`. （ASSETS-31301）
* プレビューは、すべてのアセット、アダプティブビデオセットおよびビデオで機能します。 ただし、次の場合は 403 エラーがスローされます： `.m3u8` ファイル（ちなみに、まだパブリックリンクを通じて動作している） （ASSETS-31882）
* The `scene7SmartCropProcessingStatus` ステータスを修正しました。 成功した場合でも失敗を表示するために使用されるスマート切り抜きビデオメタデータ。 （ASSETS-31255）

### [!DNL Forms]{#forms-6520}

[!DNL Experience Manager] Forms の修正プログラムは、[!DNL Experience Manager] サービスパックリリース予定日の 1 週間後に、別のアドオンパッケージとして提供されます。この場合、AEM 6.5.20.0 Forms アドオンパッケージリリースは、2024年2月29日木曜日（PT）に予定されています。Formsの修正および機能強化のリストが、リリース後のこの節に追加されました。

<!-- #### [!DNL Adaptive Forms] -->

<!--LEFT BULLET LIST HERE IN CASE OF REUSE BY FORMS IN THE FUTURE 
* **Document Services**
  * text
* **Adaptive Forms** 
  * text
* **Accessibility**
  * text
* **Interactive Communications**
  * text -->

<!--### Commerce{#commerce-6520}

* text -->

### 基盤 {#foundation-6520}

#### Communities {#communities-6520}

* ユーザー同期を正常に構成した後、ユーザー同期診断が失敗しました。 （NPR-41693）

<!-- #### Content distribution{#foundation-content-distribution-6520}

* text -->

#### 統合{#integrations-6520}

* AEM 6.5 からAdobeSearch&amp;Promoteのすべてのコードと依存関係を削除します。 （NPR-40856）

#### ローカライゼーション{#localization-6520}

* Aria-label &quot;close&quot;が **[!UICONTROL Assets]** > **[!UICONTROL ファイル]**&#x200B;をクリックし、フォルダーを選択して、ツールバーで「 」を選択します。 **[!UICONTROL プロパティ]** > **[!UICONTROL 権限]** タブ/メンバー名。 （NPR-41705）
* ツールチップが切り捨てられ、 **[!UICONTROL キーストアのパスワード]** ロケール ENG、FRA、KOR、DEU、PTB の「SSL 設定」ページのフィールド。 （NPR-41367）

#### プラットフォーム{#foundation-platform-6520}

* /api サーブレットが href json に正しいスキームを返さないことが原因で、Campaign とAEMの統合に関する問題が発生しました。 これは、AEMが X-Forward-Proto ヘッダーを受信していなかったためで、このヘッダーにより、HTTPS ではなく HTTP スキームで要求の応答が強制されていました。 そのため、OSGi 設定に基づいてスキームの選択を切り替える機能を追加する必要があります。 (GRANITE-48454)

#### Sling{#foundation-sling-6520}

* The `org.apache.sling.resourceMerger` バンドル 1.4.2 では、AEM 6.5、Service Pack 17 以降で例外がスローされます。 Sling resource merger 1.4.4 は、Service Pack 20 に含まれる必要があります。 （NPR-41630）

#### 翻訳{#foundation-translation-6520}

* AEM 6.5 Service Pack 18 のデプロイ後、翻訳ルールエディターの「フィルター」タブに問題が発生しました。 「コンテキスト」を選択し、「編集」>「保存」をクリックすると、次に同じコンテキストを開いたときに、HTML文字として二重引用符が表示されます。 基本的に、翻訳ルールが正しく保存されていませんでした。 （NPR-41624）
* 翻訳後の文字列が翻訳プロバイダーからAEMに送り返されるコンテンツフラグメントの翻訳に関連する問題ですが、翻訳後の文字列が `/content/projects` レベルを変更し、コンテンツフラグメントを更新しない。 （NPR-41516）
* 言語コピーを作成すると、エラーメッセージが表示されます。 コンテンツフラグメントモデルを使用して、コンテンツフラグメントがページプロパティで参照されているページで発生します。 （NPR-41441）
* 言語コピー中に、エクスペリエンスフラグメント内のリンクが正しい言語に調整されない。 代わりに、エクスペリエンスフラグメントはプライマリロケールを指します。 （NPR-41343）

#### ユーザーインターフェイス{#foundation-ui-6520}

* AEM 6.5、Service Pack 18 へのアップグレード後にコンソールエラーが発生する。 エラーは、 `coralUI3.js` ファイルに含まれ、AEMで任意のドロップダウンを選択したときに発生します。 特に、 `onOverlayToggle` イベント。 エラー `Uncaught TypeError: Cannot read properties of null (reading 'innerText')` が表示されます。 （NPR-41467）
* AEMでは、 **[!UICONTROL ツール]** > **[!UICONTROL 一般]** > **[!UICONTROL タグ付け]** > **[!UICONTROL 作成]** > **[!UICONTROL タグを作成]**、に非ラテン文字を入力する **タイトル** フィールドによって、 **名前** ハイフン ( `-` ) をクリックします。 （NPR-41623）
* の著作権年が正しくありません `About Adobe Experience Manager` ダイアログボックス。 （NPR-41526）
* 未翻訳です **[!UICONTROL プロファイルのプロパティ]** 文字列を使用して設定を編集できます。 すべてのロケールで発生します。 （NPR-41365）

<!-- #### WCM{#wcm-6520}

* text

#### Workflow{#foundation-workflow-6520}

* text -->

## [!DNL Experience Manager] 6.5.20.0 のインストール{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.20.0 には [!DNL Experience Manager] 6.5 が必要です。手順について詳しくは、[アップグレードに関するドキュメント](/help/sites-deploying/upgrade.md)を参照してください。<!-- UPDATE FOR EACH NEW RELEASE -->
* サービスパックは、アドビの[ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip)からダウンロードできます。
* MongoDB と複数のインスタンスを含むデプロイメントでは、パッケージマネージャーを使用して、オーサーインスタンスの 1 つに [!DNL Experience Manager] 6.5.20.0 をインストールしてください。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> アドビでは、[!DNL Experience Manager] 6.5.20.0 パッケージを削除またはアンインストールすることを推奨しません。したがって、パッケージをインストールする前に、ロールバックする必要がある場合に備えて `crx-repository` のバックアップを作成する必要があります。<!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### [!DNL Experience Manager] 6.5 へのサービスパックのインストール{#install-service-pack}

1. インスタンスが更新モードの場合（インスタンスが以前のバージョンから更新された場合）、インストール前にインスタンスを再起動します。インスタンスの現在の稼動時間が長い場合、アドビは再起動することを推奨します。

1. インストールする前に、[!DNL Experience Manager] インスタンスのスナップショットまたは新しいバックアップを作成します。

1. 次の場所からサービスパックをダウンロードします。 [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. パッケージマネージャーを開き、「**[!UICONTROL パッケージをアップロード]**」を選択して、パッケージをアップロードします。詳しくは、[パッケージマネージャー](/help/sites-administering/package-manager.md)を参照してください。

1. パッケージを選択して、「**[!UICONTROL インストール]**」を選択します。

1. S3 コネクタを更新するには、サービスパックのインストール後にインスタンスを停止し、既存のコネクタをインストールフォルダーに用意されている新しいバイナリファイルに置き換えて、インスタンスを再起動します。[Amazon S3 データストア](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)を参照してください。

>[!NOTE]
>
>サービスパックのインストール中に、パッケージマネージャー UI のダイアログが終了することがあります。Adobeでは、エラーログが安定するのを待ってから、デプロイメントにアクセスすることをお勧めします。アップデーターバンドルのアンインストールに関連する特定のログが表示されるのを待ってから、インストールが成功したことを確認してください。この問題は、通常 [!DNL Safari] ブラウザーで発生しますが、どのブラウザーでも断続的に発生する場合があります。

**自動インストール**

[!DNL Experience Manager] 6.5.20.0 の自動インストールに使用できる方法は 2 つあります。<!-- UPDATE FOR EACH NEW RELEASE -->

* サーバーがオンラインで使用可能な場合、パッケージを `../crx-quickstart/install` フォルダーに配置します。パッケージが自動的にインストールされます。
* [パッケージマネージャーの HTTP API](/help/sites-administering/package-manager.md#package-share) を使用します。ネストされたパッケージがインストールされるように、`cmd=install&recursive=true` を使用します。

>[!NOTE]
>
>Experience Manager 6.5.20.0 では、Bootstrap のインストールをサポートしていません。<!-- UPDATE FOR EACH NEW RELEASE -->

**インストールの検証**

このリリースでの動作が認定されたプラットフォームについては、[技術要件](/help/sites-deploying/technical-requirements.md)を参照してください。

1. 製品情報ページ（`/system/console/productinfo`）の[!UICONTROL インストール済み製品]に、更新されたバージョン文字列 `Adobe Experience Manager (6.5.20.0)` が表示されます。<!-- UPDATE FOR EACH NEW RELEASE -->

1. すべての OSGi バンドルは、OSGi コンソールで **[!UICONTROL アクティブ]** または **[!UICONTROL フラグメント]** です（web コンソールを使用：`/system/console/bundles`）。

1. OSGi バンドル `org.apache.jackrabbit.oak-core` はバージョン 1.22.18 以降です（Web コンソールを使用：`/system/console/bundles`）。<!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### [!DNL Experience Manager] Forms へのサービスパックのインストール{#install-aem-forms-add-on-package}

AEM Forms にサービスパックをインストールする手順については、[AEM Forms サービスパックのインストール手順](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)を参照してください。

>[!NOTE]
>
>[AEM 6.5 クイックスタート](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/deploying/deploy.html)で使用できるアダプティブフォーム機能は、探索と評価のみを目的として設計されています。アダプティブフォームの機能には適切なライセンスが必要なので、実稼動環境で使用する場合は、AEM Forms の有効なライセンスを取得することが不可欠です。

### Experience Manager コンテンツフラグメント用の GraphQL インデックスパッケージのインストール{#install-aem-graphql-index-add-on-package}

GraphQL を使用しているお客様は、[Experience Manager コンテンツフラグメントと GraphQL インデックスパッケージ 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip) をインストールする必要があります。

これにより、実際に使用する機能に基づいて、必要なインデックス定義を追加できます。

このパッケージをインストールしないと、GraphQL クエリが遅くなったり失敗したりする場合があります。

>[!NOTE]
>
>このパッケージは、インスタンスごとに 1 度だけインストールします。サービスパックごとに再インストールする必要はありません。

### UberJar{#uber-jar}

[!DNL Experience Manager] 6.5.20.0 の UberJar は、[Maven Central リポジトリ](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.20/)で入手できます。<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Maven プロジェクトで UberJar を使用するには、[UberJar の使用方法](/help/sites-developing/ht-projects-maven.md)を参照し、プロジェクト POM に次の依存関係を含めます。<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.20</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar およびその他の関連アーティファクトは、Adobe のパブリック Maven リポジトリー （`repo.adobe.com`） ではなく、Maven Central リポジトリーで入手できます。メインの UberJar ファイルの名前は、「`uber-jar-<version>.jar`」に変更されます。そのため `classifier` が存在せず、`apis` が値として `dependency` タグに使用されます。

## 廃止される機能および削除された機能{#removed-deprecated-features}

[廃止される機能および削除された機能](/help/release-notes/deprecated-removed-features.md/)を参照してください。

## 既知の問題{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.-->

<!-- * **Page publishing not working in Page Editor after upgrading to Service Pack 18 (6.5.18.0)** -->

<!-- https://jira.corp.adobe.com/browse/SITES-15856 REMOVE FOR 6.5.19.0 -->
<!-- After you upgrade an instance of AEM 6.5.0.0&mdash;6.5.17.0 to AEM 6.5.19.0, when you click **Publish Page** inside the Page Editor, you are redirected to a URL that does not exist.

  To work around this issue, do one of the following:

  * Remove the following "path" property.

       `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/publish/granite:data`

  * Paste the correct URL directly into the browser.

       `http://localhost:4504/editor.html/libs/wcm/core/content/sites/publishpagewizard.html?item=/content/we-retail/language-masters/en/about-us.html` -->



* **Oak 関連**
サービスパック 13 以降で、永続性キャッシュに影響する次のエラーログが表示されるようになりました。

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

   1. 次の 2 つのフォルダーを `crx-quickstart/repository/` から削除する

      * `cache`
      * `diff-cache`

   1. サービスパックをインストールするか、Experience Manager as a Cloud Serviceを再起動します。
`cache` および `diff-cache` の新しいフォルダーが自動的に作成され、`error.log` 内で `mvstore` に関連する例外は発生しなくなりました。

* コンテンツモデルのカスタム API 名を使用していた可能性のある GraphQL クエリを、代わりにコンテンツモデルのデフォルト名を使用するように更新してください。

* GraphQL クエリでは、`fragments` インデックスの代わりに `damAssetLucene` インデックスを使用する場合があります。このアクションは結果的に、GraphQL クエリが失敗するか、実行に非常に長い時間がかかる可能性があります。

  問題を修正するには、`damAssetLucene` では、`/indexRules/dam:Asset/properties` に次の 2 つのプロパティを含むように設定する必要があります。

   * `contentFragment`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/contentFragment"`
      * `propertyIndex="{Boolean}true"`
      * `type="Boolean"`
   * `model`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/data/cq:model"`
      * `ordered="{Boolean}true"`
      * `propertyIndex="{Boolean}true"`
      * `type="String"`

  インデックス定義を変更した後、インデックス再作成が必要です（`reindex` = `true`）。

  これらの手順を行うと、GraphQL クエリの実行が高速化されます。

* コンテンツフラグメント、サイト、ページのいずれかを移動、削除または公開しようとすると、バックグラウンドクエリが失敗したため、コンテンツフラグメント参照が取得される際に問題が発生します。つまり、この機能が動作しなくなります。
正しく動作させるには、インデックス定義ノード `/oak:index/damAssetLucene` に次のプロパティを追加する必要があります（インデックスの再作成は不要です）。

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* [!DNL Experience Manager] インスタンスを 6.5.0～6.5.4 から Java™ 11 の最新のサービスパックにアップグレードすると、`error.log` ファイルに `RRD4JReporter` 例外が表示されます。例外を停止するには、[!DNL Experience Manager] のインスタンスを再起動します。<!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* ユーザーは、[!DNL Assets] の階層内のフォルダーの名前を変更し、ネストされたフォルダーを [!DNL Brand Portal] に公開できます。ただし、ルートフォルダーが再公開されるまで、[!DNL Brand Portal] でフォルダーのタイトルは更新されません。

* [!DNL Experience Manager] 6.5.x.x のインストール中に、次のエラーや警告メッセージが表示される場合があります。
   * 「Target Standard API（IMS 認証）を使用して [!DNL Experience Manager] に Adobe Target 統合を設定する場合、エクスペリエンスフラグメントを Target に書き出すと、間違ったオファータイプが作成されます。Target では、「エクスペリエンスフラグメント」／ソース「Adobe Experience Manager」タイプではなく、「HTML」／ソース「Adobe Target Classic」タイプのオファーをいくつか作成します。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * SUM、MAX、MIN などの集計関数が使用される場合、アダプティブフォームのサーバー側検証が失敗します （CQ-4274424）。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * ショッパブルバナービューアでアセットをプレビューしている間、Dynamic Media インタラクティブ画像のホットスポットは表示されません。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]`：登録状況を未登録に変更する処理が完了するのを待機中にタイムアウトになりました。

* AEM 6.5.15 以降、```org.apache.servicemix.bundles.rhino``` バンドルで提供される Rhino JavaScript Engine には、新しい巻上げ動作が追加されました。strict モード（```use strict;```）を使用するスクリプトでは、変数を正しく宣言する必要があります。宣言しない場合、変数は実行されず、代わりにランタイムエラーが発生します。

### AEM Forms の既知の問題

の既知の問題 [!DNL Experience Manager] Formsは、スケジュールされた [!DNL Experience Manager] サービスパックのリリース日です。 この場合、AEM 6.5.20.0 Forms アドオンパッケージリリースは、2024年2月29日木曜日（PT）に予定されています。リリース後のこの節には、フォームに関する既知の問題のリストが追加されます。

<!--

#### Supported platforms 

* JDK 11.0.20 is not supported to install AEM Forms on JEE Installer. Only JDK 11.0.19 or earlier versions are supported to install AEM Forms on JEE Installer. (FORMS-10659)

#### Installation 

* On JBoss&reg; 7.1.4 platform, when user installs Experience Manager 6.5.16.0 or later service pack, `adobe-livecycle-jboss.ear` deployment fails. (CQ-4351522, CQDOC-20159)

<!-- 
* After upgrading to AEM Forms 6.5.18.0 JBoss&reg; Turnkey full installer environment on Windows Server 2022, when compiling Output client application code using Java&trade; 11, the following compilation error may occur:
  
  ```
  error: error reading [AEM_Forms_Installation_dir]\sdk\client-libs\common\adobe-output-client.jar; java.net.URISyntaxException: 
  Illegal character in path at index 70: file:/[AEM_Forms_Installation_dir]/sdk/client-libs/common/${clover.jar.name} 1 error
  
  ```
  
  To resolve the issue, perform the following steps:
    1. Navigate to `[AEM_Forms_Installation_dir]\sdk\client-libs\common\` and unzip `adobe-output-client.jar` to extract the `Manifest.mf` file.
    1. Update the `Manifest.mf` file by removing the entry `${clover.jar.name}` from the class-path attribute. 

        >[!NOTE]
        >
        > You can also use an in-place editing tool, for example, 7-zip, to update the `Manifest.mf` file.  

    1. Save the updated the `Manifest.mf` in the `adobe-output-client.jar` archive. 
    1. Save the modified `adobe-output-client.jar` file and rerun the setup. (CQDOC-20878) 

* After installing AEM Service Pack 6.5.20.0 full installer, the EAR deployment fails on JEE using JBoss&reg; Turnkey. UPDATE FOR EACH NEW RELEASE To resolve the issue, locate the AEM_Forms_Installation_dir\jboss\bin\standalone.bat file and update `Adobe_Adobe_JAVA_HOME` to `Adobe_JAVA_HOME` for all occurrences before running the configuration manager. (CQDOC-20803).

#### Install the servlet fragment (AEM Service Pack 6.5.14.0 or earlier)

* If you are upgrading to AEM Service Pack 6.5.15.0 or higher, and your AEM instance is operating on Tomcat 8.5.88, it is mandatory that you install the servlet fragment. Do this install *before* you proceed with the installation of Service Pack 6.5.15.0 or higher.
* It is mandatory that you install the servlet fragment for all application servers except those running on JBoss&reg; EAP 7.4.0.

**To install the servlet fragment:**

1. Download the servlet fragment from [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).
1. Start the application server. 
1. Wait for the logs to stabilize and check the bundle state.
1. Open Web Console Bundles. The default URL is `http://[Server]:[Port]/system/console/bundles`.
1. Select **[!UICONTROL Install]** or **[!UICONTROL Update]**. 
1. Select the downloaded fragment 
`org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar` 
1. Select **[!UICONTROL Install]** or **[!UICONTROL Update]**. 
1. Wait for the application server to stabilize.
1. Stop the application server.

#### Adaptive Forms

* When an Adaptive Form is published, all its dependencies, including policies, get republished, even if no modifications have been made to them. (FORMS-10454)
* When a user selects to configure a field for the first time in an adaptive form, the option to save a configuration does not display in Properties Browser. Selecting to configure some other field of the Adaptive Form in the same editor resolves the issue. 
* When users perform the submit action, the submission fails with an error: 
`javax.servlet.ServletException: java.lang.NoSuchMethodError`
To resolve the issue, [recompile the Sling scripts such as JSP, Java&trade;, and Sightly](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16543.html#resolution). (FORMS-8542)
* After installing AEM Service Pack 6.5.14.0 and onwards, users are unable to select a font from the JEE Admin UI for PDF documents when navigating to `Home` > `Services` > `PDF Generator` > `Adobe PDF Settings`, as the font list appears empty. (FORMS-12095)
 When a form is signed using the OOTB Scribble Signature component, it appears in the image dialogue but does not preview and appears blank when you click on it. (FORMS-12073). A hotfix is available for this issue. To download and install the hotfix, see [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md) 
* On AEM Forms on JEE, the HTML5 Forms that use the context path, fail to render. (FORMS-12485, FORMS-12691). A hotfix is available for this issue. To download and install the hotfix, see [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md).
* Adaptive Forms let you use custom functions with ECMAScript version 5 or earlier. When a custom function uses ECMAScript version 6 or later, like 'let', 'const', or arrow functions, the rule editor might not open properly.

#### AEM Forms on JEE 

* Critical security vulnerabilities have been reported for Struts 2 RCE, a popular and open-source web application framework for developing Java&trade; EE web applications. Adobe has released [AEM 6.5 Service Pack 19.1 (6.5.19.1)](/help/forms/using/mitigating-struts-2-rce-vulnerabilities-for-experience-manager-manager-form.md) to address the vulnerability in AEM Forms on JEE. 

The font enumeration fails due to the missing Ps2Pdf service file.-->

## 含まれている OSGi バンドルとコンテンツパッケージ{#osgi-bundles-and-content-packages-included}

以下のテキストドキュメントでは、このドキュメントに含まれる OSGi バンドルとコンテンツパッケージの一覧を示します [!DNL Experience Manager] 6.5 Service Pack リリース：

* [Experience Manager 6.5.20.0 に含まれている OSGi バンドルのリスト](/help/release-notes/assets/65200-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5.20.0 に含まれているコンテンツパッケージのリスト](/help/release-notes/assets/65200-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 制限付き Web サイト{#restricted-sites}

以下の web サイトはお客様のみが参照できます。アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [アドビカスタマーサポートに連絡](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=ja)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 製品ページ](https://business.adobe.com/jp/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=ja)
>* [アドビ製品アップデートの優先通知に登録する](https://www.adobe.com/subscription/priority-product-update.html)
