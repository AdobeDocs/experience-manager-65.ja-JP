---
title: Adobe Experience Manager 6.5 リリースの累積的な主な機能および機能強化。
description: 以前の 8 つのサービスパックリリースから Adobe Experience Manager 6.5 に加えられた主な機能および機能強化の累積リストです。
content-type: reference
docset: aem65
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 01fe5b53-2244-445f-a4d0-bd58ea38b611
solution: Experience Manager
source-git-commit: 3d47b1e17a4500e5e68e1abe2e2d4ac86376f424
workflow-type: tm+mt
source-wordcount: '3122'
ht-degree: 74%

---

# 累積的な主な機能および機能強化

以前の 8 つのサービスパックリリースに対する Adobe Experience Manager 6.5 の主な機能および機能強化の累積リストです。

詳しくは、[Adobe Experience Manager 6.5 の最新のサービスパックリリースノート](/help/release-notes/release-notes.md)も参照してください。


## AEM 6.5 サービスパック 23 - 2025 年 5 月 22 日（Pt）

### Forms {#forms-sp23}

* [静的 PDF の混合テキストスタイルを用いたアクセシブルなハイパーリンク](https://helpx.adobe.com/content/dam/help/ja/experience-manager/6-5/forms/pdf/using-designer.pdf)：静的 PDF で混合テキストスタイルを含むハイパーリンクが、単一のアクセシブルな要素としてタグ付けされるようになりました。この機能強化では、タグツリー構造を簡素化、スクリーンリーダーのナビゲーションを改善、アクセシビリティコンプライアンスを向上します。

* [更新されたサポート対象プラットフォームのマトリックス](/help/forms/using/aem-forms-jee-supported-platforms.md)

  最新バージョンでは、サポート対象プラットフォームマトリックスのアップデートを行い、新しいテクノロジーとの互換性を確保します。

   * IBM® Content Manager クライアント 8.7

   * MongoDB Enterprise 7.0

   * MySQL 8.4

   * Microsoft® SQL Server 2022

   * Microsoft® SQL Server JDBC ドライバー 12.8

   * Red Hat® Enterprise Linux® 9 （Kernel 4.x、64 ビット）

* [強化されたファイル添付コンポーネント](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment)：セキュリティ対策として、許可されたファイルタイプのチェックを回避しようとする、拡張子が変更されたファイルの送信をコンポーネントが防ぐようになりました。有効なファイルタイプのみが受け入れられるように、このようなファイルは送信中にブロックされます。

## AEM 6.5 サービスパック 22 - 2024 年 11 月 21 日（Pt）

### Sites {#sites}

[ユニバーサルエディター](/help/sites-developing/universal-editor/introduction.md)が機能パックの適用により、AEM 6.5 でヘッドレスユースケースに使用できるようになりました。

### [!DNL Assets]

IPTC タブは、[!UICONTROL 代替テキスト]と[!UICONTROL 詳細な説明]テキストフィールドをサポートするようになりました。 （Assets-34918）

### Forms {#forms-sp22}

#### AEM Forms の新しい GA 機能 {#ga-aem-forms-sp22}

* [インタラクティブ通信の Batch API](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/interactive-communications/create-interactive-communication#output-format-print-channel) でフォント埋め込みを有効にするサポートの追加 - インタラクティブ通信には、Batch API で生成された PDF に Adobe Ming および Adobe Myungjo フォントを埋め込むサポートが含まれるようになりました。 この機能強化により、フォントサブセットを使用している場合でも、生成されたドキュメントで正確なテキストレンダリングが確保され、PDF 出力での多言語コンテンツのサポートが向上します。

* [PDF アクセシビリティに対する Table of Content API](/help/forms/using/aem-document-services-programmatically.md#auto-tag-pdf-documents-auto-tag-api) - OSGi 上の AEM Forms では、アクセシビリティ標準の PDF を強化する新しい TOC Tag API をサポートするようになりました。 これにより、支援テクノロジーを使用するユーザーが PDF にアクセスしやすくなります。

* [フラグメント XDP の解決](/help/forms/using/assembler-service.md#resolve-references-on-crx-repository-resolve-references-on-crx-repository) - OSGi 上の AEM Forms は、プライマリ XDP で参照され、AEM CRX リポジトリに保存されているフラグメント XDP を解決するようになりました。

* [PDF/A 準拠の機能強化](/help/forms/developing/pdf-a-documents.md#converting-documents-to-pdfa-documents-converting-documents-to-pdf-a-documents) - ユーザーは、アクセシビリティを確保し、これらの標準への準拠を検証しながら、アーカイブ目的で PDF を PDF/A 形式（1a、2a、3a）に変換できるようになりました。

* **静的 PDF ドキュメントのフォントの自動サイズ変更のサポート** - AEM Forms Designer、OutputService および FormsService は、静的 PDF のフォントの自動サイズ変更をサポートするようになりました。 ユーザーがテキスト、数値、パスワード、日時の各フィールドのフォントサイズを 0 に設定すると、フィールド全体のサイズは変更されずに、これらのフィールド内のフォントサイズが自動調整されます。 この機能を使用するには、ユーザーはカスタム XCI：`<behaviorOverride>patch-LC-3921991:1</behaviorOverride>` でフラグを渡します。

#### AEM Forms の新しいベータ版機能 {#beta-aem-forms-sp22}

ベータ版機能は、最先端のイノベーションに排他的にアクセスし、その開発に貢献できるユニークな機会を提供します。お使いの環境でベータ版機能を有効にすることに興味がありますか？興味のある機能のリストを添えて、公式アドレスから aem-forms-ea@adobe.com にメールを送信してください。

* [hCaptcha](/help/forms/using/integrate-adaptive-forms-hcaptcha.md) および [Cloudfare Turnstile CAPTCHA](/help/forms/using/integrate-adaptive-forms-turnstile.md) サービス：AEM Forms は、次の Captcha サービスをサポートします。
   * hCaptcha は、チェックボックスウィジェットを使用してユーザーに入力を要求し、ボット、スパム、自動化された不正使用からフォームを保護します。 これにより、人間のユーザーのみが続行でき、オンライントランザクションのセキュリティが強化されます。
   * Cloudflare Turnstile は、自動ボット、悪意のある攻撃、スパム、不要な自動トラフィックからフォームを保護することを目的としたセキュリティ対策を提供します。 フォームの送信を許可する前に、フォームの送信時にユーザーが人間であることを確認するチェックボックスが表示されます。

* アダプティブフォームのバージョン管理：
   * [アダプティブフォームの複数バージョンの作成](/help/forms/using/add-versioning-reviews-comments.md) - ユーザーは既存のフォームのバリエーションを簡単に管理できるようになりました。 このプロセスにより、合理化された単一のワークフロー内で、バージョン管理をシンプルに、フォーム最適化の比較を容易に行えるようになります。
   * [アダプティブフォームの比較](/help/forms/using/compare-forms-core-components.md)：ユーザーは 2 つのフォームを簡単に比較して、その違いを特定できるようになりました。 チームメンバーがリビジョンを比較し、変更を効率的に議論できるので、共同作業がスムーズになります。

## AEM 6.5 サービスパック 21 - 2024 年 6 月 6 日（Pt）

### [!DNL Assets]

#### 機能強化

IPTC タブは、[!UICONTROL 代替テキスト]と[!UICONTROL 詳細な説明]テキストフィールドをサポートするようになりました。 （Assets-34918）

#### アクセシビリティ

* アセットの処理ステータスが失敗またはメタデータが失敗の場合、キャプションとオーディオトラック UI が適切に機能するようになりました。 （Assets-37281）
* アセットのメタデータを保存して編集しようとすると、言語名が表示されるようになりました。 （Assets-37281）

### [!DNL Forms]

このリリースの主な機能と機能強化は次のとおりです。

* **OAuth 資格情報のサポート**：既存のサービスアカウント（JWT）資格情報に代わる、サーバー間認証用の新しく使いやすい資格情報。 （NPR-41994）
* [AEM Forms のルールエディターの機能強化](/help/forms/using/rule-editor-core-components.md)：
   * `When-then-else` 機能を使用したネストされた条件の実装のサポート。
   * パネルやフォーム（フィールドを含む）の検証またはリセット。
   * カスタム関数内の let 関数や arrow 関数（ES10 サポート）などの最新の JavaScript 機能をサポートします。
* [PDF アクセシビリティに対する AutoTag API](/help/forms/using/aem-document-services-programmatically.md#doc-utility-services-doc-utility-services)：OSGi 上の AEM Forms では、タグ（段落、リスト）を追加して、アクセシビリティ標準の PDF を強化する新しい AutoTag API をサポートするようになりました。 これにより、支援テクノロジーを使用するユーザーが PDF にアクセスしやすくなります。
* **16 ビット PNG のサポート**：PDF Generator の ImageToPDF サービスで、16 ビットの色深度を持つ PNG の変換をサポートするようになりました。
* **XDP 内の個々のテキストブロックにアーティファクトを適用**：Forms Designer では、XDP ファイル内の個々のテキストブロックを設定できるようになりました。 この機能を使用すると、作成された PDF でアーティファクトとして扱われる要素を制御できます。 これらの要素（ヘッダーやフッターなど）は、支援テクノロジーからアクセスできるようになります。 主な機能には、テキストブロックをアーティファクトとしてマークする機能と、これらの設定を XDP メタデータに埋め込む機能があります。 Forms Output サービスは、PDF の生成時にこれらの設定を適用し、適切な PDF/UA タグ付けを行います。
* **AEM Forms Designer は `GB18030:2022` 標準で認定されています**：`GB18030:2022` 認定により、Forms Designer では、中国語の Unicode 文字セットをサポートし、すべての編集可能なフィールドとダイアログボックスに漢字を入力できるようになりました。
* [JEE Server での WebToPDF ルートのサポート ](/help/forms/using/admin-help/configure-service-settings.md#generate-pdf-service-settings-generate-pdf-service-settings)PDF Generator サービスを使用して、HTML ファイルを JEE 上のPDF ドキュメントに変換するための WebToPDF ルートをサポートするようになりました。 このサポートは、既存の Webkit および WebCapture （Windows のみ）ルートに追加されます。 WebToPDF ルートは OSGi で既に使用可能で、JEE に拡張されています。 現在、JEE と OSGi の両方のプラットフォームで、PDF Generator サービスは、様々なオペレーティングシステム間で次のルートをサポートします。
   * **Windows**：Webkit、WebCapture、WebToPDF
   * **Linux®**：Webkit、WebToPDF


## AEM 6.5 サービスパック 20 - 2024 年 2 月 22 日（Pt）

### [!DNL Assets]

* Dynamic Media では、Apple iOS／iPadOS の可逆 HEIC 画像形式をサポートするようになりました。 Dynamic Media 画像サービングおよびレンダリング API の[fmt](https://experienceleague.adobe.com/ja/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt)を参照してください。
* マルチサイトマネージャー（MSM）では、エクスペリエンスフラグメントをライブコピーに効率的に一括ロールアウトするために、フォルダーやサブフォルダーを含むエクスペリエンスフラグメント構造をサポートするようになりました。

### [!DNL Forms]

* **JEE 上のAEM Formsにおけるトランザクションレポート**:JEE 上のAEM Formsにトランザクションレポート機能が導入されました。 コンバージョン、レンディション、送信など、ドキュメントトランザクションの包括的な記録が可能になります。 この機能強化により、効率が向上し、より適切な記録管理が簡単になります。 機能はデフォルトでは無効になっています。 管理 UI から有効化にできます。
* **ECDSA サポートによるセキュリティの強化**：AEM Forms では、JEE スタックと OSGi スタックの両方で楕円曲線デジタル署名アルゴリズム（ECDSA）の堅牢なサポートを提供するようになりました。 ユーザーは、セキュリティを強化して PDF ドキュメントの署名、認証および検証を行うことができるようになりました。 サポートされる EC 曲線アルゴリズムには、次が含まれます。
   * SHA256 ダイジェストアルゴリズムを使用した ECDSA 楕円曲線 P256
   * SHA384 ダイジェストアルゴリズムを使用した ECDSA 楕円曲線 P384
   * SHA512 ダイジェストアルゴリズムを使用した ECDSA 楕円曲線 P512
* **Forms Designer 用の Windows 11 とのシームレスな互換性**：AEM Forms Designer で Windows 11 をサポートするようになり、スムーズなインストールと操作が保証されます。 ユーザーは、Forms Designer を再インストールする手間や互換性の問題を心配することなく、自信を持って Windows 11 にアップグレードでき、中断のないワークフローが保証されます。
* **AEM Forms Designer のカスタム「キャプション」の役割によるアクセシビリティの強化**：AEM Forms Designer には「キャプション」と呼ばれるカスタムアクセシビリティの役割が含まれており、ユーザーはパーソナライズされたキャプション要素を含む XDP を作成できます。 この機能は、ユーザーがカスタムキャプションをドキュメントデザインに統合させることでアクセシビリティを強化し、包括性とユーザーエクスペリエンスを向上できます。

## AEM 6.5 サービスパック 19 - 2023 年 12 月 7 日（Pt）

* Sites ページエディター／画像コンポーネントユーザーがリモート Assets Cloud Service からアセットを参照できるようにしました。（Sites-13448、Sites-13433）
* AEMは、サーバーサイドの並べ替えをサポートし、リスト表示でのプロジェクトのナビゲーションを迅速化しました。 プロジェクトノードは、インターフェイスに表示される前に、ユーザーが選択した列に基づいて並べ替えられます。

### [!DNL Forms]

* **新しいアダプティブフォームコアコンポーネント**：垂直タブ、利用条件、チェックボックスが追加され、フォームのスケーラビリティが向上します。
   * **[チェックボックスコンポーネント](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox)**：コアコンポーネントに基づくアダプティブフォームにチェックボックスコンポーネントを含めることができるようになりました。これにより、ユーザーは特定のオプションを選択または選択解除する二者択一の選択を行うことができます。通常、小さなボックスとして表示され、クリックまたはタップすると、オンとオフの 2 つの状態を切り替えることができます。チェックボックスは、はい／いいえ、または真／偽の選択肢を提示するために使用される一般的なフォーム要素です。

   * **[利用条件コンポーネント ](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions)**：コアコンポーネントベースのアダプティブFormsに利用条件コンポーネントが含まれるようになりました。 フォーム作成者はこのセクションを追加して、サービス、製品、またはプラットフォームの利用条件、条件、法的契約をユーザーに表示します。 このコンポーネントは、フォームを送信することで同意するルール、規制、義務についてユーザーに通知するように設計されています。

     ![垂直タブ、利用条件およびチェックボックスコンポーネント](/help/forms/using/assets/forms-components.png)

   * **[垂直タブコンポーネント](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs)**：コアコンポーネントに基づくアダプティブフォームでは、フォームのコンテンツをタブの垂直リストに整理し、構造化されたナビゲートしやすいレイアウトを提供できるようになりました。フォーム内の垂直タブを使用すると、ナビゲーションとコンテンツの整理が簡単になり、ユーザーエクスペリエンスが向上します。 これらは、フォームに複数のセクションや複雑な情報が含まれている場合に特に役立ちます。

* **[64 ビット版の AEM Forms Designer](/help/forms/using/installing-configuring-designer.md)**：64 ビット版の AEM Forms Designer では、パフォーマンス、スケーラビリティ、メモリ管理が強化され、フォーム作成エクスペリエンスを支援します。64 ビットアーキテクチャを使用すると、さらに大規模で複雑なプロジェクトに簡単に取り組むことができ、シームレスな設計ワークフローと最適化された効率が保証されます。この最先端のリリースでフォームデザイン機能を強化し、AEM Forms Designer の未来を体現します。

* **[アダプティブフォームと Microsoft® SharePoint リストの接続](/help/forms/using/configuring-submit-actions.md#submit-to-microsoft&reg;-sharepoint-list)**：AEM Forms では、フォームデータを SharePoint リストに直接送信する標準の統合を提供し、SharePoint のリスト機能を使用できます。Microsoft® SharePoint リストをフォームデータモデルのデータソースとして設定し、「フォームデータモデルを使用して送信」送信アクションを使用して、アダプティブフォームを SharePoint リストに接続できます。

* **[アダプティブフォームフラグメント用のレコードのドキュメントプロパティの設定のサポート](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)**：アダプティブフォームエディターで、アダプティブフォームフラグメントとそのフィールドを簡単にカスタマイズできるようになりました。

* **64 ビット XMLFM**：64 ビット反復の XMLFM により、パフォーマンス、スケーラビリティ、洗練されたメモリ管理が導入されます。これは、サーバーサイドにデプロイされた最初の 64 ビットネイティブサービスです。XMLFM 64 ビットでは、32 ビット版と比較してより大きなメモリリソースにアクセスする固有の機能を利用することで、より大きなレンダリングワークロードをシームレスに処理できます。このマイルストーンは、パフォーマンスの飛躍的な向上を示すだけでなく、AEM Forms サーバー内のネイティブサービスフレームワークに重要な機能強化も導入します。このアップデートにより、AEM Forms Server は 64 ビットのネイティブサービスをシームレスにサポートできるようになります。

## AEM 6.5 サービスパック 18 - 2023年8月24日（PT）

* Assets、Dynamic Media - [Dynamic Media でのビデオの複数キャプションおよびオーディオトラックのサポート ](/help/assets/video.md#about-msma) – プライマリビデオに複数のサブタイトルと複数のオーディオトラックを簡単に追加できるようになりました。 この機能により、グローバルなオーディエンスがビデオにアクセスできるようになります。1 つの公開済みプライマリビデオを複数の言語でグローバルオーディエンスに向けてカスタマイズし、様々な地理的地域のアクセシビリティガイドラインに従うことができます。また、作成者は、ユーザーインターフェイスの 1 つのタブからサブタイトルとオーディオトラックを管理することもできます。
* Assets - 検索結果から、アセットが含まれるフォルダーの場所に移動でき、様々なアセット管理タスクを実行できるようになります。
* コンテンツフラグメントの Sites Polaris ピッカーのパフォーマンスが向上しました。
* Sites ページエディター／画像コンポーネントユーザーがリモート Assets Cloud Service からアセットを参照できるようにしました。
* システムに多数のプロジェクトがある場合に、リスト表示ですばやくプロジェクトを見つけるために、Adobeでは、サーバーサイドの並べ替えをサポートするようになりました。 プロジェクトノードは、ユーザーインターフェイスでレンダリングする前に、ユーザーが選択した列に基づいて、バックエンドで並べ替えられます。
* AEM 6.5.18.0 は、MongoDB 5.0～6.0 をサポートします。

### [!DNL Forms]

* **[ルールエディターでのカスタムエラーハンドラーによるエラー処理の強化](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms)** - 外部サービスから返されたエラーに応じて（クライアントライブラリを使用して）カスタム関数を呼び出すことができるようになりました。また、エンドユーザーに対してカスタマイズされた応答を提供できるようになりました。または、サービスから返されたエラーに対して特定のアクションを実行できます。例えば、特定のエラーコードに対してバックエンドでカスタムワークフローを呼び出したり、サービスが停止していることを顧客に通知したりできます

* **[Adobe Sign ワークフローステップの機能強化](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/workflows/aem-forms-workflow-step-reference#sign-document-step)** - AEM ワークフローの Adobe Sign ワークフローステップは、次の機能強化で使用可能になります。

   * **Adobe Sign の Government ID ベースの認証によるセキュリティの強化** - Adobe Acrobat Signの Government ID ベースの認証では、検証レイヤーが追加されました。 これにより、ユーザーは行政発行の ID（運転免許証、国民 ID、パスポート）を使用して身元を認証できます。この機能強化により、信頼できる ID ドキュメントを使用することで、署名プロセスの信頼性がさらに高まり、高度なセキュリティ、コンプライアンスおよびユーザー検証を必要とするシナリオに最適になります。

   * **Adobe Sign ドキュメントの監査記録を使用した透明性の向上** – 監査記録機能を使用すると、Adobe Sign ドキュメントのライフサイクルに関する詳細なインサイトを得ることができます。 監査記録を使用すると、ドキュメントに関連するすべてのアクションとインタラクションの包括的な記録を保持できるようになりました。 これらのアクションとインタラクションには、誰がドキュメントを閲覧、編集または署名したかと、各イベントのタイムスタンプが含まれます。 この機能強化は、コンプライアンスの保持、紛争の解決、デジタル契約の整合性を確保する上で重要です。


   * **署名者以外にも契約書受信者の役割を拡大** - Adobe Acrobat Signでは、ワークフロー要件に合わせて、署名者以外にも契約書受信者の役割を拡大できます。 有効にすると、契約の各受信者の役割を個別に設定でき、署名者がデフォルトになります。


* **[AEM Forms on JEE 完全インストーラー](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms)** - サービスパックには、AEM Forms on JEE 完全インストーラーが含まれており、以下を含む複数の新しいソフトウェアの組み合わせがサポートされます。
   * Microsoft® Windows Server 2022
   * Microsoft® Active Directory 2022
   * Oracle WebLogic 14C（Windows Server 2022）
   * Red Hat® JBoss® 7.4.10
   * MongoDB 6.0 <!-- it was previously MongoDB 4.4 -->
   * MySQL JDBC Connector 8

AEM 6.5 Forms on JEE 環境に最新ソフトウェアをインストールしている場合や、使用することを計画している場合は、AEM 6.5.18.0 Forms on JEE の完全なインストーラーを使用することをお勧めします。新しく追加されたソフトウェアと非推奨（廃止予定）のソフトウェアの完全なリストを確認するには、AEM Forms on JEE または AEM Forms on OSGi のドキュメントを参照してください。

## AEM 6.5 サービスパック 17 - 2023年5月25日（PT）

* **検索エクスペリエンスの強化** - 検索結果に表示されるアセットに対して、次の操作を素早く実行できるようになりました。
   * ワークフローの作成
   * バージョンを作成
   * アセットの関連付けまたは関連付けを解除

  これらの操作を実行する場合、アセットの場所に移動してアセットのプロパティを表示する必要はありません。

* **Dynamic Media _スナップショット_**&#x200B;では、テスト画像または Dynamic Media の URL を使用して、画像の修飾子とスマートイメージングの最適化（WebP または AVIF 出力、帯域幅対応の圧縮、デバイスピクセル比のスケーリングなど）をプレビューできます。 その後、各設定が画質とファイルサイズにどのように影響するかを即座に比較できます。
詳しくは、[Dynamic Media スナップショット](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot)を参照してください。
* **Dynamic Media での DASH ストリーミング** - Dynamic Media ビデオ配信でのアダプティブストリーミング用に新しいプロトコル（DASH - HTTP 経由の動的アダプティブストリーミング）が開始されました（CMAF が有効な場合）。 すべての地域で利用可能です。
* **Experience Manager SitesおよびコンテンツフラグメントとAssets次世代 Dynamic Media の統合** - Experience Manager Sites 6.5 でクラウドホスト型アセットを使用できるようになりました。オンプレミスインスタンスまたはManaged Services インスタンスで、これらのアセットを作成して配信できます。

### [!DNL Forms]

* **[AEM ページエディター内のアダプティブForms](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)** - AEM ページエディターを使用して、複数のフォームを作成し、サイトページにすばやく追加できるようになりました。 この機能を使用すると、コンテンツ作成者は、動的な動作、検証、データ統合、レコードのドキュメントの生成、ビジネスプロセスの自動化など、アダプティブフォームコンポーネントの機能を利用して、Sites ページ内にシームレスなデータキャプチャエクスペリエンスを作成できます。以下の操作を実行できます。
   * アダプティブフォームを作成するには、AEM Sites エディターまたはエクスペリエンスフラグメントで、フォームコンポーネントをアダプティブ Forms コンテナコンポーネントにドラッグ&amp;ドロップします。
   * AEM Sites Editor 内でアダプティブFormsウィザードを使用すると、Sites ページに依存しないフォームを作成でき、そのようなフォームを複数のページで自由に再利用できます。
   * 複数のフォームを Sites ページに追加し、ユーザーエクスペリエンスを合理化し、柔軟性を高めます。
* **[Experience Manager Formsでの reCAPTCHA Enterprise のサポート](/help/forms/using/captcha-adaptive-forms.md)** - Experience Manager Formsで reCAPTCHA Enterprise のサポートを追加しました。 この機能は、既存のGoogle reCAPTCHA v2 のサポートに加えて、不正なアクティビティやスパムに対する保護を強化します。
* **[Experience Manager Formsを使用したAdobe Acrobat Sign for Government のサポートを追加](/help/forms/using/adobe-sign-integration-adaptive-forms.md)** - AEM FormsがAdobe Acrobat Sign for Government と統合されました（FedRAMP 準拠）。 この統合により、政府関連のアカウント（政府機関および機関）に対するアダプティブフォーム送信による電子サインに、高度なコンプライアンスとセキュリティを提供します。Adobe Acrobat Sign for Government との統合により、Adobeのパートナーや政府機関のお客様は、アダプティブFormsで電子サインを使用して、最もミッションクリティカルで機密性の高い一部の事業部門を利用できます。 このセキュリティの強化により、すべての電子サインが FedRAMP Moderate コンプライアンスに完全に準拠し、アドビの政府機関のお客様に安心感を提供します。
* **データ交換用にExperience Manager FormsとSalesforceの統合を有効にする** - OAuth 2.0 クライアント資格情報フローを使用して、Experience Manager FormsとSalesforce アプリケーションの統合を設定します。 この機能により、アプリケーションの安全で直接の認証と承認が可能になり、ユーザーが関与しないシームレスな通信が可能になります。
* **ワークフローエンジンの最適化と機能強化**：ワークフローインスタンスの数を最小限に抑えて、ワークフローエンジンのパフォーマンスを向上させます。`COMPLETED` および `RUNNING` ステータス値に加えて、ワークフローは 3 つの新しいステータス値、`ABORTED`、`SUSPENDED` および `FAILED` もサポートします。

## AEM 6.5 サービスパック 16 - 2023年2月23日（PT）

CMAF（[共通メディアアプリケーション形式]）が有効な Dynamic Media ビデオ配信で、アダプティブビットレートストリーミング用の新しいプロトコル DASH（HTTP での動的アダプティブストリーミング）が開始しました。

* アダプティブストリーミング（DASH/HLS）により、エンドユーザーがビデオを視聴する際のエクスペリエンスが向上します。
* DASH はアダプティブビデオストリーミングの国際標準プロトコルであり、業界で広く採用されています。
* 現在、アジア太平洋および北米で利用可能です。ヨーロッパ中東アフリカではまもなく提供予定です。

### [!DNL Forms]

* [ヘッドレスアダプティブフォーム](https://experienceleague.adobe.com/ja/docs/experience-manager-headless-adaptive-forms/using/overview)を使用すると、デベロッパーは、従来のグラフィカルユーザーインターフェイスではなく、API を介してアクセスおよび操作できるインタラクティブなフォームを作成、公開、管理できます。

* [アダプティブフォームコアコンポーネント](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/introduction#features)は、Adobe Experience Manager WCM コアコンポーネントの基盤上に構築された、BEM に準拠した 24 個のオープンソースからなるコンポーネント群です。これらのコンポーネントはオープンソースなので、デベロッパーは組織の特定のニーズに合わせて簡単にカスタマイズおよび拡張できます。 [WCM コアコンポーネント](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/get-started/authoring)をカスタマイズできる既存のスキルがあれば、これらのコンポーネントを簡単にカスタマイズおよびスタイル設定できます。

* OSGi の Reader Extension サービスには、Adobe Acrobat Reader でデータを読み込みまたは書き出しするために、PDF の読み込みおよび書き出しの使用権限を有効化する個別のオプションが追加されました。
