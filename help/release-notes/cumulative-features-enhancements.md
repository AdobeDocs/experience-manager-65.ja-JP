---
title: Adobe Experience Manager 6.5 リリースの累積主な機能および機能強化。
description: 以前の 8 つのサービスパックリリースからAdobe Experience Manager 6.5 でおこなわれた主な機能と機能強化の累積リストです。
content-type: reference
docset: aem65
feature: Release Information
role: User, Admin
source-git-commit: 0aa929021aa724e4ec18d49fea26f8c0b0538bdc
workflow-type: tm+mt
source-wordcount: '2334'
ht-degree: 59%

---


# 累積的な主な機能および機能強化

以前の 8 つのサービスパックリリース向けの、Adobe Experience Manager 6.5 の主な機能および機能強化の累積リストです。

関連トピック [Adobe Experience Manager 6.5 最新の Service Pack リリースノート](/help/release-notes/release-notes.md).

## AEM 6.5、Service Pack 18—2023 年 12 月 7 日

* Sites ページエディター／画像コンポーネントユーザーがリモート Assets Cloud Service からアセットを参照できるようにしました。（Sites-13448、Sites-13433）
* AEMでサーバー側の並べ替えがサポートされ、リスト表示でのプロジェクトのナビゲーションをより迅速におこなえるようになりました。 プロジェクトノードは、インターフェイスに表示される前に、ユーザが選択した列に基づいて並べ替えられます。

### [!DNL Forms]

* **新しいアダプティブフォームコアコンポーネント**：フォームのスケーラビリティを高めるために、縦並びのタブ、「利用条件」および「チェックボックス」が追加されました。
   * **[チェックボックスコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox.html)**：コアコンポーネントに基づくアダプティブFormsで、チェックボックスコンポーネントを含めることができるようになりました。 ユーザーは、特定のオプションの選択または選択解除を行い、バイナリ選択をおこなうことができます。 これは通常、小さなボックスとして表示され、クリックまたはタップすると、2 つの状態（チェック済みとオフ）を切り替えることができます。 このチェックボックスは、はい/いいえ、真/偽の選択肢を提示するために使用される一般的なフォーム要素です。

   * **[利用条件コンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions.html)**：コアコンポーネントに基づくアダプティブFormsで、利用条件コンポーネントを含めることができるようになりました。 Formsの作成者は、フォーム内に特定のセクションを導入し、サービス、製品、プラットフォームの使用に関連する利用条件、または法的契約をユーザーに提示できます。 このコンポーネントは、フォームを送信することで、同意するルール、規制、義務をユーザーに通知するように設計されています。

     ![垂直タブ、利用条件およびチェックボックスコンポーネント](/help/forms/using/assets/forms-components.png)

   * **[垂直タブコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs.html)**：コアコンポーネントに基づくアダプティブFormsで、フォームコンテンツをタブの縦並びのリストに整理でき、構造化されたナビゲーション可能なレイアウトが提供されるようになりました。 フォーム内で縦置きのタブを使用すると、ナビゲーションが簡単になり、フォームコンテンツの構成が改善され、特にフォームに複数のセクションや複雑な情報が含まれる場合に、ユーザーの操作性が向上します。

* **[64 ビット版のAEM Forms Designer](/help/forms/using/installing-configuring-designer.md)**: 64 ビット版のAEM Forms Designer では、パフォーマンス、拡張性、メモリ管理の機能が強化され、フォーム作成エクスペリエンスが強化されます。 64 ビットアーキテクチャを使用すると、より大規模で複雑なプロジェクトに簡単に取り組むことができ、シームレスな設計ワークフローと最適化された効率を確保できます。 フォームデザインの機能を向上させ、この最先端リリースでAEM Forms Designer の将来を受け入れます。

* **[Microsoft® SharePointリストとのアダプティブFormsの接続](/help/forms/using/configuring-submit-actions.md#submit-to-microsoft&reg;-sharepoint-list)**:AEM Formsは、すぐに使用できる統合機能を備えており、フォームデータをSharePointリストに直接送信して、SharePointのリスト機能を使用できます。 Microsoft® SharePointリストをフォームデータモデルのデータソースとして設定し、「フォームデータモデルを使用して送信」送信アクションを使用して、アダプティブフォームをSharePointリストに接続することができます。

* **[アダプティブフォームフラグメントのレコードのドキュメントプロパティの設定をサポート](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)**：アダプティブフォームエディターで、アダプティブフォームフラグメントとそのフィールドを簡単にカスタマイズできるようになりました。

* **64 ビット XMLFM**:XMLFM の 64 ビット版では、パフォーマンス、拡張性、メモリ管理の改善が導入されています。 これは、サーバー側にデプロイされる最初の 64 ビットネイティブサービスです。 XMLFM 64 ビットは、32 ビット対応のメモリリソースに比べて大きなメモリリソースにアクセスする独自の機能を備えており、より大きなレンダリングワークロードをシームレスに処理できます。 このマイルストーンは、パフォーマンスの飛躍を表すだけでなく、AEM Forms Server 内のネイティブサービスフレームワークに対する主な機能強化も導入します。 このアップデートでは、AEM Forms Server が 64 ビットのネイティブサービスをシームレスにサポートするようになっています。

## AEM 6.5、Service Pack 18—2023 年 8 月 24 日

* Assets、Dynamic Media - [Dynamic Media のビデオに対するマルチサブタイトルとマルチオーディオトラックのサポート](/help/assets/video.md#about-msma) - プライマリビデオに複数のサブタイトルと複数のオーディオトラックを簡単に追加できるようになりました。この機能により、グローバルなオーディエンスがビデオにアクセスできるようになります。1 つの公開済みプライマリビデオを複数の言語でグローバルオーディエンスに向けてカスタマイズし、様々な地理的地域のアクセシビリティガイドラインに従うことができます。また、作成者は、ユーザーインターフェイスの 1 つのタブからサブタイトルとオーディオトラックを管理することもできます。
* アセット — 検索結果から、アセットが含まれるフォルダーの場所に移動して、様々なアセット管理タスクを実行できるようになりました。
* コンテンツフラグメントの Sites Polaris ピッカーは、パフォーマンスを向上させました。
* サイトのページエディター/画像コンポーネントユーザーがリモートアセットCloud Serviceーからアセットを参照できるようになりました。
* システム内に多数のプロジェクトが存在する可能性があるリスト表示でプロジェクトをすばやく見つけるために、アドビではサーバーサイドでの並べ替えをサポートするようになりました。プロジェクトノードは、ユーザーインターフェイスでレンダリングする前に、ユーザーが選択した列に基づいて、バックエンドで並べ替えられます。
* AEM 6.5.18.0 は、MongoDB 5.0～6.0 をサポートします。

### [!DNL Forms]

* **[ルールエディターでのカスタムエラーハンドラーによるエラー処理の強化](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms.html?lang=ja)** - 外部サービスから返されたエラーに応じて（クライアントライブラリを使用して）カスタム関数を呼び出すことができるようになりました。また、エンドユーザーに対してカスタマイズされた応答を提供できるようになりました。または、サービスから返されたエラーに対して特定のアクションを実行できます。例えば、特定のエラーコードに対してバックエンドでカスタムワークフローを呼び出したり、サービスが停止していることを顧客に通知したりできます

* **[Adobe Sign ワークフローステップの機能強化](https://experienceleague.adobe.com/docs/experience-manager-65/forms/workflows/aem-forms-workflow-step-reference.html?lang=ja#sign-document-step)** - AEM ワークフローの Adobe Sign ワークフローステップは、次の機能強化で使用可能になります。

   * **Adobe Sign の行政 ID に基づいた認証によるセキュリティの機能強化** - Adobe Acrobat Sign の行政 ID に基づいた認証は、追加の検証レイヤーを提供します。これにより、ユーザーは行政発行の ID（運転免許証、国民 ID、パスポート）を使用して身元を認証できます。この機能強化により、信頼できる ID ドキュメントを使用することで、署名プロセスの信頼性がさらに高まり、高度なセキュリティ、コンプライアンスおよびユーザー検証を必要とするシナリオに最適になります。

   * **Adobe Sign ドキュメントの監査証跡による透明性の機能強化** - 監査証跡機能を使用すると、Adobe Sign ドキュメントのライフサイクルに関する詳細なインサイトが得られます。監査証跡を使用すると、ドキュメントに関連するすべてのアクションとインタラクションの包括的な記録を保持できるようになります。これには、ドキュメントを表示、編集、署名したユーザーなどの詳細と、各イベントのタイムスタンプが含まれます。この機能強化は、コンプライアンスの保持、紛争の解決、デジタル契約の整合性を確保する上で重要です。


   * **契約受信者の役割を署名者以外にも拡張** - Adobe Acrobat Sign を使用すると、契約受信者の役割を署名者以外にも拡張して、ワークフロー要件にさらに適合させることができます。有効にすると、契約の各受信者の役割を個別に設定でき、署名者がデフォルトになります。


* **[AEM Forms on JEE 完全インストーラー](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms.html?lang=ja)** - サービスパックには、AEM Forms on JEE 完全インストーラーが含まれており、以下を含む複数の新しいソフトウェアの組み合わせがサポートされます。
   * Microsoft® Windows Server 2022
   * Microsoft® Active Directory 2022
   * Oracle WebLogic 14C（Windows Server 2022）
   * Red Hat® JBoss® 7.4.10
   * MongoDB 6.0 <!-- it was previously MongoDB 4.4 -->
   * MySQL JDBC Connector 8

AEM 6.5 Forms on JEE 環境に最新ソフトウェアをインストールしている場合や、使用することを計画している場合は、AEM 6.5.18.0 Forms on JEE 完全インストーラーを使用することをお勧めします。新しく追加されたソフトウェアと非推奨（廃止予定）のソフトウェアの完全なリストを確認するには、AEM Forms on JEE または AEM Forms on OSGi のドキュメントを参照してください。

## AEM 6.5、Service Pack 17—2023 年 5 月 26 日

* **検索エクスペリエンスの強化** - 検索結果に表示されるアセットに対して、次の操作を素早く実行できるようになりました。
   * ワークフローの作成
   * バージョンを作成
   * アセットの関連付けまたは関連付けを解除

  これらの操作を実行する場合、アセットの場所に移動してアセットのプロパティを表示する必要はありません。
* **Dynamic Media _スナップショット_**- テスト画像や Dynamic Media の URL を試して、様々な画像修飾子の出力や、ファイルサイズ（WebP および AVIF 配信による）、ネットワーク帯域幅およびデバイスのピクセル比を最適化するスマートイメージングを確認します。詳しくは、[Dynamic Media スナップショット](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html?lang=ja)を参照してください。
* **Dynamic Media での DASH ストリーミング** - CMAF が有効な Dynamic Media ビデオ配信で、アダプティブストリーミングをサポートする新しいプロトコル（DASH - HTTP での動的アダプティブストリーミング）が開始しました。すべての地域で利用可能で、[サポートチケットを通じて有効になります](/help/assets/video.md#enable-dash-on-your-account-enable-dash)。
* **Experience Manager Sites およびコンテンツフラグメントと Assets の次世代 Dynamic Media の統合** - Experience Manager Assets as a Cloud Service の次世代 Dynamic Media のユーザーは、これらのクラウドホストアセットを、Experience Manager Sites 6.5 のオンプレミスインスタンスまたは Managed Services インスタンスでのオーサリングと配信に使用できるようになりました。

### [!DNL Forms]

* **[AEM ページエディター内のアダプティブフォーム](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)**：AEM ページエディターを使用して、複数のフォームをすばやく作成し、Sites ページに追加できるようになりました。この機能を使用すると、コンテンツ作成者は、動的な動作、検証、データ統合、レコードのドキュメントの生成、ビジネスプロセスの自動化など、アダプティブフォームコンポーネントの機能を利用して、Sites ページ内にシームレスなデータキャプチャエクスペリエンスを作成できます。以下の操作を実行できます。
   * フォームコンポーネントを AEM サイトエディターまたはエクスペリエンスフラグメントのアダプティブフォームコンテナコンポーネントにドラッグ＆ドロップして、アダプティブフォームを作成します。
   * AEM サイトエディター内でアダプティブフォームウィザードを使用すると、任意の Sites ページとは独立したフォームを作成して、自由に複数のページでそのフォームを再利用できます。
   * 複数のフォームを Sites ページに追加し、ユーザーエクスペリエンスを合理化し、柔軟性を高めます。
* **[Experience Manager Forms での reCAPTCHA Enterprise のサポート](/help/forms/using/captcha-adaptive-forms.md)**：Experience Manager Forms での reCAPTCHA Enterprise のサポートを追加し、既存の Google reCAPTCHA v2 のサポートに加えて、不正なアクティビティやスパムに対する保護を強化しました。
* **[Adobe Acrobat Sign for Government との Experience Manager Forms のサポート](/help/forms/using/adobe-sign-integration-adaptive-forms.md)**：AEM Forms は、Adobe Acrobat Sign for Government（FedRAMP 準拠）と統合されました。この統合により、政府関連のアカウント（政府機関および機関）に対するアダプティブフォーム送信による電子サインに、高度なコンプライアンスとセキュリティを提供します。Adobe Acrobat Sign for Government との統合により、アドビのパートナーや政府のお客様は、Adaptive Forms で最もミッションクリティカルで機密性の高い業務の一部に電子サインを使用できるようになります。このセキュリティの強化により、すべての電子サインが FedRAMP Moderate コンプライアンスに完全に準拠し、アドビの政府機関のお客様に安心感を提供します。
* **データ交換用に Experience Manager Forms と Salesforce の統合が有効化**：OAuth 2.0 クライアント資格情報フローを使用して、Experience Manager Forms と Salesforce アプリケーションの統合を設定します。この機能により、アプリケーションの安全で直接の認証と承認が可能になり、ユーザーが関与しないシームレスな通信が可能になります。
* **ワークフローエンジンの最適化と機能強化**：ワークフローインスタンスの数を最小限に抑えて、ワークフローエンジンのパフォーマンスを向上させます。`COMPLETED` および `RUNNING` ステータス値に加えて、ワークフローは 3 つの新しいステータス値、`ABORTED`、`SUSPENDED` および `FAILED` もサポートします。

## AEM 6.5、Service Pack 16—2023 年 2 月 24 日

CMAF（[共通メディアアプリケーション形式]）が有効な Dynamic Media ビデオ配信で、アダプティブビットレートストリーミングをサポートする新しいプロトコル DASH（HTTP での動的アダプティブストリーミング）が開始しました。

* アダプティブストリーミング（DASH/HLS）により、エンドユーザーがビデオを視聴する際の操作性が向上します。
* DASH はアダプティブビデオストリーミングの国際標準プロトコルであり、業界で広く採用されています。
* アジア太平洋および北米で現在利用可能です（サポートチケットを通じて有効化できます）。ヨーロッパ中東アフリカではまもなく提供予定です。

詳しくは、[アカウントでの DASH の有効化](/help/assets/video.md#enable-dash)を参照してください。

### [!DNL Forms]

* [ヘッドレスアダプティブフォーム](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=jp)を使用すると、デベロッパーは、従来のグラフィカルユーザーインターフェイスではなく、API を介してアクセスおよび操作できるインタラクティブなフォームを作成、公開、管理できます。

* [アダプティブフォームコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja#features)は、Adobe Experience Manager WCM コアコンポーネントの基盤上に構築された、BEM に準拠した 24 個のオープンソースからなるコンポーネント群です。これらのコンポーネントはオープンソースなので、デベロッパーは組織の特定のニーズに合わせて簡単にカスタマイズおよび拡張できます。[WCM コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/authoring.html)をカスタマイズできる既存のスキルがあれば、これらのコンポーネントを簡単にカスタマイズおよびスタイル設定できます。

* OSGi 上のReader拡張サービスに、Adobe Acrobat ReaderでのデータのインポートまたはエクスポートをおこなうPDFに対する使用権限のインポートとエクスポートを可能にする個別のオプションが追加されました。

## AEM 6.5、Service Pack 15—2022 年 11 月 24 日

### [!DNL Forms]

* AEM Forms Designer が [スペイン語のロケール](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja).
* これで、 [Microsoft® Office 365 メールサーバープロトコル（SMTP および IMAP）で認証するための OAuth2](/help/forms/using/oauth2-support-for-mail-service.md).
* 次の設定が可能です。 [サーバーで再検証](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?lang=ja#enabling-server-side-validation-br) プロパティを true に設定すると、サーバー側のレコードのドキュメントから除外する非表示フィールドが識別されます。
* AEM Forms Designer には、Visual C++ 2019 再頒布可能パッケージ (x86) の 32 ビット版が必要です。

## AEM 6.5、Service Pack 14—2022 年 8 月 26 日

バグの修正のみ。

## AEM 6.5、Service Pack 13—2022 年 5 月 27 日

* アダプティブフォームで非表示の CAPTCHA を使用：不明なアクティビティがある場合にのみ、非表示の CAPTCHA を使用して CAPTCHA チャレンジを表示できるようになりました。 疑わしいアクティビティが検出されない場合、CAPTCHA チャレンジは表示されません。これにより、チェックボックス要件を使わずに人間がフォームを完成させたかどうかを評価し、カスタマイズ作業を軽減し、エンドユーザーエクスペリエンスを向上させることができます。

* REST エンドポイント用のフォームデータモデル後処理での応答ヘッダーの取得のサポートが追加されました。

* これで、アダプティブフォームの翻訳ファイルを生成する際に、生成される XLIFF ファイルと、対応するアダプティブフォーム内のコンポーネントのシーケンスが同じテキストのシーケンスになります。

* アダプティブフォームをローカライズして、ベース言語のテキストにわずかな変更を加えると、他のすべての言語において翻訳が完全に失われます。この問題は、 [!DNL Experience Manager] 6.5.13.0.

* Forms のアクセシビリティの強化：

   * テーブルのヘッダーと本文を継続エンティティと接続エンティティとして認識するためのスクリーンリーダーのサポートが追加されました。スクリーンリーダーでテーブルを適切に移動するのに役立ちます。 （NPR-37139）
   * ダイアログが開くまでHTMLワークスペース内を移動しないようにするスクリーンリーダーのサポートを追加しました。

## AEM 6.5、Service Pack 12—2022 年 2 月 24 日

* リモート DAM と Sites デプロイメント間の接続を設定すると、リモート DAM 上のアセットが Sites デプロイメントで使用できるようになります。これで、リモート DAM アセットまたはフォルダーに対して 更新、削除、名前変更、および移動操作を実行できます。更新は、Sites デプロイメントで自動的に（少し遅れて）利用できます。
* ブループリント設定を必要とせずに、ライブコピーソースを複数のライブコピーにプッシュロールアウトできるようになりました。
* ユーザーが同じパス上で誤って複数の非同期操作をトリガーするのを防ぐために、進行中の非同期操作のステータスがユーザーインターフェイスに表示されるようになりました。
* IMS ベースの認証のサポートは、Analytics 2.0 API で提供されます。
* JSON オファータイプのエクスペリエンスフラグメントの API サポート。
* IMS のオファーを削除（エクスペリエンスフラグメント API）用にオファーリクエストが提供されるようになりました。
* 組み込みリポジトリ（Apache Jackrabbit Oak）は、引き続き 1.22.9 にあります。
