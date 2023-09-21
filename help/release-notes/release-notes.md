---
title: ' [!DNL Adobe Experience Manager]  6.5 のリリースノート'
description: ' [!DNL Adobe Experience Manager] 6.5 のリリース情報、新機能、インストール方法、詳細な変更リストを確認します。'
mini-toc-levels: 4
source-git-commit: ffda4927ddc8555564f33697fa81d1f8a0cd2cdc
workflow-type: tm+mt
source-wordcount: '4548'
ht-degree: 27%

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
| バージョン | 6.5.18.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| タイプ | サービスパックのリリース |
| 日付 | 2023 年 8 月 24 日木曜日 <!-- UPDATE FOR EACH NEW RELEASE --> |
| ダウンロード URL | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/jp/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.18.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## [!DNL Experience Manager] 6.5.18.0 の内容 {#what-is-included-in-aem-6518}

[!DNL Experience Manager] 6.5.18.0には、2019 年 4 月の 6.5 の初期リリース以降にリリースされた新機能、お客様からリクエストされた主な機能強化、バグ修正、パフォーマンス、安定性、セキュリティの改善が含まれています。 [このサービスパックを [!DNL Experience Manager] 6.5 にインストール](#install)。

<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

このリリースの主な機能および機能強化の一部を次に示します。

**主な機能**

* Assets、Dynamic Media - [Dynamic Mediaでのビデオのマルチサブタイトルおよびマルチオーディオトラックのサポート](/help/assets/video.md#about-msma) — プライマリビデオに複数のサブタイトルや複数のオーディオトラックを簡単に追加できるようになりました。 この機能を使用すると、ビデオにアクセスできるのは、全世界のオーディエンス全体です。 複数の言語でグローバルオーディエンスに対して 1 つの公開済みプライマリビデオをカスタマイズし、様々な地域のアクセシビリティガイドラインに従うことができます。 作成者は、ユーザーインターフェイスの 1 つのタブからサブタイトルやオーディオトラックを管理することもできます。

* アセット — 検索結果から、アセットが含まれるフォルダーの場所に移動して、様々なアセット管理タスクを実行できるようになりました。 （ASSETS-23182）

**主な機能強化**

* コンテンツフラグメントの Sites Polaris ピッカーは、パフォーマンスを向上させました。 （SITES-14092）

* サイトのページエディター/画像コンポーネントユーザーがリモートアセットCloud Serviceーからアセットを参照できるようになりました。 （Sites-13448、Sites-13433）

* リスト表示でプロジェクトをすばやく見つけるために、Adobeでは、サーバー側での並べ替えがサポートされるようになりました。 プロジェクトノードは、ユーザーインターフェイスでレンダリングする前に、ユーザーが選択した列に基づいて、バックエンドで並べ替えられます。 （NPR-41027）

* AEM 6.5.18.0は、MongoDB 5.0 から 6.0 をサポートしています。

**非推奨（廃止予定）の機能**

* AEMの ActiveMQ は非推奨です。 2 つのAEMパブリッシュインスタンス間の通信に ActiveMQ が使用されていました。 Adobeでは、現在ロードバランサーを使用することをお勧めします。

**Forms**

* **[ルールエディターでのカスタムエラーハンドラーによるエラー処理の強化](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms.html)**  — 外部サービスから返されたエラーに応じて、（クライアントライブラリを使用して）カスタム関数を呼び出せるようになりました。 また、エンドユーザーに合わせて適切な応答を提供できます。 または、サービスから返されたエラーに対して特定のアクションを実行できます。 例えば、特定のエラーコードに対してバックエンドでカスタムワークフローを呼び出したり、サービスが停止していることを顧客に通知したりできます

* **[Adobe Sign Workflow ステップの強化](https://experienceleague.adobe.com/docs/experience-manager-65/forms/workflows/aem-forms-workflow-step-reference.html#sign-document-step)** - AEM Workflows のAdobe Signワークフローステップは、次の機能強化で使用できます。

   * **Adobe Signの政府機関 ID ベースの認証によるセキュリティの強化** - Adobe Acrobat Signの政府 ID ベースの認証により、さらに多くの検証がおこなわれます。 これにより、ユーザーは政府発行の ID（運転免許証、国籍 ID、パスポート）を使用して ID を認証できます。 この機能強化は、信頼された識別ドキュメントを使用することで、署名プロセスに対する信頼性を高め、セキュリティ、コンプライアンス、およびユーザーの検証を強化する必要があるシナリオに最適です。

   * **Adobe Signドキュメントの監査証跡による透明性の向上**  — 監査記録機能を使用すると、Adobe Signドキュメントのライフサイクルに関する詳細なインサイトを得ることができます。 監査証跡を使用すると、ドキュメントに関連するすべてのアクションとインタラクションの包括的な記録を維持できるようになりました。 これには、ドキュメントの閲覧者、編集者、署名者、および各イベントのタイムスタンプなどの詳細が含まれます。 この強化は、コンプライアンスの維持、紛争の解決、およびデジタル契約の整合性の確保に不可欠です。


   * **署名者だけを超えて、契約受信者の役割を拡張しました。** - Adobe Acrobat Signを使用すると、署名者以外に、契約の受信者の役割を拡張して、ワークフロー要件に合わせることができます。 有効にすると、契約の各受信者の役割は個別に設定でき、署名者がデフォルトとなります。


* **[AEM Forms on JEE の完全インストーラー](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms.html)**  — このサービスパックでは、次のような新しいソフトウェアの組み合わせをサポートする、JEE 上のAEM Formsの完全なインストーラーが提供されます。
   * Microsoft® Windows Server 2022
   * Microsoft® Active Directory 2022
   * OracleWebLogic 14C（Windows Server 2022 上）
   * Red Hat® JBoss® 7.4.10
   * MongoDB 4.4
   * MySQL JDBC Connector 8

JEE 上のAEM 6.5 Forms環境に最新のソフトウェアをインストールする、または使用する予定がある場合、Adobeでは、JEE 上のAEM 6.5.18.0 Formsフルインストーラーを使用することをお勧めします。 新しく追加および廃止されたソフトウェアの完全なリストを確認するには、JEE 上のAEM Formsまたは OSGi 上のAEM Formsのドキュメントを参照してください。

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## Service Pack 18 の問題を修正しました {#fixed-issues}

### [!DNL Sites]{#sites-6518}

* バルクエディターを使用して、 `tsv` エクスポートし、変更をオフラインでおこない、 `tsv` Experience Managerに戻る ページが更新された場合でも、JCR プロパティは `cq:lastModified` が更新されず、タイムラインに表示されました。 （SITES-14072）
* エクスペリエンスフラグメントのライブコピーまたはロールアウトを作成する際に、エクスペリエンスフラグメント内でリンク参照が更新されない。 （SITES-14759）
* 既製のExperience Manager標準ロールアウト設定（「ページとサブページのロールアウト」）に親ページからワークフロー同期アクションが追加され、非同期ジョブが NullPointer 例外で失敗しました。 ソースの場所ページ (en-us) は親に存在しませんが、ターゲットの場所（ライブコピー）(en) に存在します。 （SITES-12207）
* 次を含む「en」ページがあります： `jcr:description` 翻訳するページを送信しました。 The `jcr:description` が翻訳され、プロパティが launch の下に存在する。 ただし、ローンチが昇格されると、 `jcr:description` はページで更新されていません。 （SITES-13146）
* ライブコピー上のローカライズされたコンテンツは、ブループリントのロールアウト後に失われます。 （SITES-12602）

#### 管理ユーザーインターフェイス{#sites-adminui-6518}

* ユーザーの削除権限が useradmin コンソールを通じて削除された場合、ユーザーは（ページの選択時に） sites.html コンソールに「プロパティ」ボタンを表示しなくなります。 ただし、ユーザーがページエディターを開くと、このオプションが表示されます。 （SITES-14341）
* フォルダーに多数のページがあり、各ページに多数のバージョンがある場合、バージョン比較機能を使用すると、インスタンスの負荷が高くなります。 複数のユーザーが同時にこの機能を使用する場合、インスタンスは停止する可能性があります。 （SITES-13026）

#### [!DNL Content Fragments]{#sites-contentfragments-6518}

* の例外処理で問題が見つかりました `RemoteAssetClientImpl`. メタデータのクエリ中に IOException または RuntimeException が発生した場合、現在のスレッドは共有 httpClient を閉じて再作成しようとしますが、その結果、スレッド内の他のエラーがカスケードされる可能性があります。 （SITES-14092）
* 作成者がコンテンツフラグメントのリッチテキストエディターフィールドに入力し、リンク内に画像を挿入すると、コンテンツフラグメントがGraphQL API を使用して照会されると、エラーメッセージが表示されます `Exception while fetching data (/genericContentByPath) : null` が返されます。 このエラーは、画像が含まれるリンクが存在する場合にのみ発生していました。 リンクから画像を削除すると、エラーメッセージが表示されなくなりました。 （SITES-13988）
* Experience Manager6.5 のGraphQL実装がマスターと同じではなく、いくつかの重要な修正が見つかりませんでした。 （SITES-13096）
* メタデータサービスエンドポイントにアクセスする場合は、必須の HTTP ヘッダーが必要です。 （SITES-13068）

#### コアコンポーネント{#sites-core-components-6518}

* アセットセレクターを閉じて再び開いたときに、更新されたアセットのリストが取得されません。 リポジトリに新しいアセットがアップロードされた場合、アセットセレクターを含むページが更新されるまで、アセットセレクターに表示されません。 （SITES-14828）
* サイトエディター (CS) に統合されたアセットセレクターのユーザーインターフェイスは、ウィンドウが縮小されるとレスポンシブになりません。 （SITES-14127）
* アセットセレクター統合用のAdobe IMS(Identity Managementシステム ) 設定で、間違った値が受け入れられていました。 （SITES-13962）
* アセットセレクターを Sites 画像コンポーネントに統合する場合、画像以外のアセットを選択できないようにする必要があります。 （SITES-13879）
* ログインに成功すると、ユーザーはページエディターにリダイレクトされます。 リモートアセットを選択するには、アセットセレクターを再度開く必要があります。 （SITES-13851）
* リモートアセットピッカーは、常にAdobe IMS(Identity Management System) ステージ環境にリダイレクトされます。 （Sites-13448、Sites-13433）

<!-- #### [!DNL Experience Fragments]{#sites-experiencefragments-6518}

* A -->

#### ページエディター{#sites-pageeditor-6518}

* 作成者がページのプロパティを開くと、ダイアログボックスの表示が正しくない。 つまり、余分な水平スクロールバーと余分な余白が表示されます。 （SITES-14502）
* アンカーおよび body タグ用のスタイルがExperience Manager6.5 の Service Pack 17 で追加され、CSS の問題が発生していました。 作成者で、アンカータグに下線が表示されなかった問題を修正しました。 （SITES-14261）

### [!DNL Assets]{#assets-6518}

* スクリーンリーダーは、 [!UICONTROL 切り抜きを開始] オプションを使用して設定できます。 （NPR-40593）
* AEM 6.5.17.0インスタンスでアセットをアップロードする際に、Experience Managerにエラーメッセージと警告メッセージが表示される。 （ASSETS-26232）
* 読み取り専用アクセス権を持つフォルダーからのアセットに対して完全アクセス権を持つExperience Managerーからのアセットを関連付けると、エラーメッセージが表示されますが、2 つのアセット間に部分的な関係が作成されます。 （ASSETS-25832）
* AMS インスタンスとCloud Serviceインスタンスの間で Connected Assets が機能しない。 （ASSETS-24930）
* メタデータスキーマFormsの編集中に、 [!UICONTROL オンタイム] および [!UICONTROL オフタイム] フィールドが正しく保存されません。 （ASSETS-24871）
* トレーニング済みタグのスマートタグレポートを生成する際に、信頼性スコアの低いタグが一覧に表示されません。 （ASSETS-24109）
* Experience Managerは、列表示で画像を編集および注釈を付ける際に、空白の画面を表示します。 （ASSETS-24108）
* スクリーンリーダーで、コレクションの作成時に「ユーザーを追加」フィールドの目的が読み上げられない。 （ASSETS-21736）
* The **コレクション** ラベルがコレクションのプロパティページにローカライズされていない。 （ASSETS-21102）
* デフォルトのメタデータスキーマフォームを使用してルールを追加したり、既存のルールを編集したりする場合、ドロップダウンリストの言語はローカライズされません。 （ASSETS-21026）
* Experience Managerで、メタデータスキーマに JSON パスを追加すると、ローカライズされていないエラーメッセージが表示される。 （ASSETS-21025）
* 左側のナビゲーションの「タイムライン」オプションには、適切なコントラスト比が表示されません。 （ASSETS-17348）
* カレンダー要素では、必要な ARIA 属性は使用されません。 （ASSETS-17282）
* 左側のナビゲーションテキストには、適切なコントラスト比が表示されません。 （ASSETS-17268）
* Lightbox 画像は、スクリーンリーダーユーザーに対して非表示にはなりません。 （Assets-17263、Assets-17242）
* アクティブなユーザーインターフェイスの状態では、背景に関する適切なコントラスト比が提供されません。 （ASSETS-17260）
* アセットに注釈を追加する際に、スクリーンリーダーが [!UICONTROL バージョンとして保存] または [!UICONTROL ワークフローを開始] ボタンをクリックし、キーボードの矢印キーを使用して移動する。 （ASSETS-17253）
* 特定の ARIA ロールでは、Assets ホームページに適切な子ロールが含まれていません。 （ASSETS-17248）
* キーボードを使用して画像タイプのアセットの編集オプションに移動すると、 [!UICONTROL ローンチマップ] オプションが認識されず、キーボードフォーカスが代わりにキャンセルボタンに移動する。 （ASSETS-17238）

#### [!DNL Dynamic Media]{#assets-dm-6518}

* VTT のダウンロードに失敗した場合、ビデオは表示されません。 空白の画面が表示され、ビデオスクラバは前に進んでいます。 （ASSETS-21909）
* キーボードの Tab キーを使用して移動する際に、ビデオの下に表示される複数のコントロールにフォーカスが移動しない。 したがって、アクセスできません。 インタラクティブビデオのキーボードナビゲーションが改善されました。 （ASSETS-25749）
* Dynamic Mediaコンポーネントに表示される、無効になったビューアプリセットを修正しました。 （ASSETS-22922）
* 一般設定の「セキュリティ」タブから「画像サービング」を削除しました。 （ASSETS-24618）
* アセットがDynamic Mediaおよび StringIndexOutOfBoundsException にアップロードできない問題を修正しました。 （ASSETS-25787）
* 「基本」タブの必須の「幅」編集フィールドに視覚的なアスタリスクを追加しました。 （ASSETS-25741）
* 透かしのDynamic Mediaレンディションのダウンロードを修正しました。 （ASSETS-26173）
* ビデオ以外のアセット名の 127 文字の制限を復元しました。 （ASSETS-26074）

### [!DNL Forms]{#forms-6518}

<!-- Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.18.0 Forms add-on packages release is scheduled for Thursday, August 31, 2023. A list of Forms fixes and enhancements would be added to this section post the release. -->

* **Document Services**
   * ユーザーが transformPDF サービスを使用すると、次の例外が発生して失敗します。 `java.lang.ClassNotFoundException: default task-158Class name com.adobe.internal.afml.AFMLExceptionInvalidParameter from package com.adobe.internal.afml` (FORMS-9957)
   * サーバードキュメントの生成中にPDFがシャットダウンされた場合、サーバー起動後のジョブ処理エラーがスローされます。 引数 —Dcom.adobe.livecycle.dsc.deferServiceStart=true は、サーバーの起動中に追加する必要があります。 （FORMS-9836）
   * ユーザーが AssemblerService.Invoke メソッドを使用してPDFを結合しようとすると、アセンブラはタスクを実行できません。 （FORMS-9550）
   * OSGI および JEE 環境でAEM 6.5.15.0 Service Pack にアップグレードすると、特定のテンプレートを使用する Assembler サービスが動作しなくなります。 (FORMS-9355、FORMS-9445、FORMS-9408)
   * XMLFormService の Global Timeout が適切な値に設定されていないので、Java™ガベージコレクションはAEM Forms OSGi サーバー上の古い生成ヒープをクリアできません。 （FORMS-9384、FORMS-9035）
   * アダプティブフォームのPDFプレビューをレンダリングする際に、不要な Java™スタックダンプがエラーログに表示されます。 （FORMS-8865）
   * ユーザーがドキュメントの詳細セクションでドキュメントのドキュメントステータスを確認すると、正しく表示されません。 （FORMS-8946、FORMS-10424）
   * ユーザーがAEM Formsにアップグレードし、sendToPrinter サービスを使用すると、ヒープ使用率が継続的に増加します。 （FORMS-10148）
   * JBoss® 7.4 EAP サーバーでは、電子メール機能は次の条件で失敗します。 `java.io.IOException`. （FORMS-10138）
   * ユーザーが transformPDF サービスを使用すると、次のエラーで失敗します。 `java.lang.ClassNotFoundException: default task-158Class name com.adobe.internal.afml.AFMLExceptionInvalidParameter from package com.adobe.internal.afml`(FORMS-9957)
   * AEM Service Pack 6.5.14.0にアップグレードした後、特定のテンプレートを使用すると、Assembler サービスで問題が発生します。 （FORMS-9445、FORMS-9408）
  <!-- *  When a user configures the watched folder endpoint for PDF Generator, it fails to pick documents on JDK 11. (FORMS-10152) -->
* **アダプティブフォーム**
   * ユーザーがフィールドを変更せずにカスタム関数を呼び出そうとすると（例えば、別のフィールドの値を設定しようとする）、失敗します。 （FORMS-9921）
   * アダプティブフォーム内のルールエディターのカスタムエラー機能を使用する際に、次のエラーが発生します。
      * ユーザーが@paramを使用しようとしたとき{boolean} 関数を使用する場合、ルールエディターではブール値を関数に渡すことはできません。
      * ユーザーが@paramを使用しようとしたとき{string} 関数を使用すると、ルールエディターはオプションの値を渡せず、不完全なルールの警告を表示します。 （FORMS-9816、FORMS-9815）
   * forms-user グループが、アダプティブフォーム内でルールエディターを 2 回呼び出せません。 （FORMS-9051）
   * ビジュアルエディターでは、ユーザーがフォームオブジェクトを選択すると、フィールドの値だけでなく、フィールドインスタンスオブジェクト全体がカスタム関数に渡されます。 （FORMS-10015）
   * ユーザーがコアコンポーネントベースのアダプティブフォームを作成し、テキスト入力コンポーネントを追加した場合、 `Is Empty` および `Is Not Empty` ルールエディターでは作業しないでください。 （FORMS-10098）
   * コアコンポーネントベースのアダプティブフォームで、フィールドが無効とマークされている場合は、フィールド上で変更イベントが開始されます。 （FORMS-10087）
   * ユーザーが複雑な JSON スキーマを使用してアダプティブフォームを作成しようとすると、失敗します。 エラーは次のように発生します。
     `GET /content/forms/af/katezeroone/testaf1.html HTTP/1.1] com.adobe.aemds.guide.service.impl.JsonObjectCreatorImpl Could not emit JSON with context java.lang.ArrayIndexOutOfBoundsException:0` で使用される様々なキャッシュに分散されます。（FORMS-9639）
   * アダプティブフォームでは、ユーザーが「利用条件に同意します」チェックボックスを無効にすると、ユーザーがスクロールダウンすると再び有効になります。 （FORMS-9458）
   * ユーザーがGoogle Chrome/Firefox を使用して Android™デバイスでアダプティブフォームを開き、最大許容文字数をテキストボックスに入力すると、テキストボックス内の値がクリアされません。 （FORMS-9354）
   * チェックボックスのラベルに「、」、「/」、「。」などの特殊文字が含まれる場合、テキスト/ラベルをクリックしても、それぞれのチェックボックスは選択されません。 （FORMS-9313）
   * ユーザーが利用条件コンポーネントの検証を試みると、他のコンポーネントが検証される間、コンポーネントがフォーカスされていないかどうかの検証に失敗します。 （FORMS-8725、FORMS-8913）
   * AEM 6.5.16.0 Service Pack にアップグレードした後にアダプティブフォームが再読み込みされると、ファイル添付ファイルの取得に失敗します。 （FORMS-8906）
   * XDP に基づくアダプティブフォームで、チェックボックスコンポーネントにテキストタイトルが数値で割り当てられている場合、テキストタイトルは切り捨てられ、割り当てられた値と一致しません。 （FORMS-8743）
   * オーサー環境のアダプティブフォームに埋め込まれたフラグメントに遅延読み込みを実装しようとしても、フラグメントに対して定義されたルールやロジックはフォームに反映されません。 （FORMS-8554、FORMS-9182）
   * AEM 6.5.16.0 Service Pack で任意の Coral ダイアログを開こうとすると、 `error.log: cannot render resource` 例外です。 （FORMS-8942）
   * ユーザーがアダプティブフォーム内の 1 つのオプションを含むチェックボックスを翻訳しようとすると、失敗します。 （FORMS-10181）
   * すべてのレコードのドキュメント (DoR) テンプレートが公開に失敗しました。 英語のロケールベースの DoR テンプレートと、それに関連するFormsベースの DoR テンプレートのみが公開されます。 （FORMS-10535）

* **アクセシビリティ**
   * アダプティブフォームで手書き署名コンポーネントを使用すると、次のエラーが発生します。
      * 手書き署名コンポーネントの後に、コンポーネントが他にある場合は、Tab キーを押しても署名ダイアログボックスに移動せず、代わりに次のコンポーネントに移動します。 すべてのコンポーネントを走査した後にのみ、最終的に署名ダイアログボックスに移動します。
      * ユーザーがブラシやキーボードを使用して署名ダイアログボックスにサインインした場合、Enter キーを押してもダイアログボックスは閉じません。
      * 明確な署名の確認ダイアログには、キーボードを使用してアクセスできません。
      * スクリーンリーダーが、ダイアログボックスに入力された情報を読み取れない。
      * マウスを使用せずに署名をクリアすることはできません。 （FORMS-9317）
   * ユーザーがアダプティブフォームを送信すると、スクリーンリーダーは必須フィールドのエラーメッセージを読み取れません。 （FORMS-9316）
   * スクリーンリーダーがHTMLフォームを読み取ると、カーニング付き（間隔）でテキストを読み取る際に問題が発生します。 （FORMS-9258）
   * アダプティブフォームでは、テキストにリンクされた参照や脚注は、スクリーンリーダーを使用して呼び出されません。 （FORMS-8920）
   * 最新の Designer では、アクセシビリティタグが正しく認識されません。 （FORMS-10139）
* **インタラクティブコミュニケーション**
   * Correspondence Management では、ローカライゼーションは機能しません。 （FORMS-8926）
   * publishAll サービスを使用すると、ドラフトレターが開けません。 （FORMS-8589）
   * Experience Manager後、サーバーに Service Pack 16 がインストールされ、これらのレターを編集しようとすると、すべてのインタラクティブ通信レターがクロックを開始します。 プロパティページをプレビューまたは表示または編集するためのサンプルペイロードが用意されている場合は、機能します。 ただし、レターを編集することはできません。 （FORMS-9067）


<!-- ### [!DNL Commerce]{#commerce-6518}

* A -->

### 基盤{#foundation-6518}

#### コンテンツの配布{#foundation-content-distribution-6518}

* アセットの削除キューはブロックしないでください。また、ログファイルにエラーは発生しません。 （NPR-40570）

<!-- #### Integrations{#integrations-6518}

* A -->

<!-- #### Oak{#oak-6518}

* A -->

#### プラットフォーム{#foundation-platform-6518}

* バニラExperience Manager、Service Pack 17 のインストール後、 `stderr.log`. Vanilla のインストール時にエラーが発生しないようにする。 （CQ-4353637）
* ACL（アクセス制御リスト）に従わないタグ付け画面の「作成」ボタン。 （NPR-40973）
* Experience Manager上の ContextHub のキャッシュノードを作成、アクセス、またはその両方を行うことができません。 （NPR-40515）

#### レプリケーション{#foundation-replication-6518}

* レプリケーションフラッシュは、要求されたパスのすべての子孫を削除します。 （NPR-40569）

#### Sling{#foundation-sling-6518}

* リンク共有レポートが生成されると、リンク列に正しい値が含まれていません。 （NPR-40798）
* AEM 6.5.15.0では、AEMの再起動後、すべてのバニティー URL、Sling エイリアス、Sling マッピングが壊れます。 （NPR-40420）

#### 翻訳プロジェクト{#foundation-translation-6518}

* 翻訳 `rules.xml` 翻訳設定のユーザーインターフェイスからルールが追加された場合、ソートの品質が低くなりました。 （NPR-40431）
* 翻訳時にクエリパラメーターを使用したリンクをサポートします。 （NPR-40339）
* 追加のコンテキストルートを更新した後、辞書のユーザーインターフェイスが顧客に対して読み込まれません。 （NPR-40650）
* アセットの 1 つが、ReferenceFragment または ContentFragment タイプを持つ複数フィールドを含むコンテンツフラグメントの場合、言語コピーの作成中にエラーが発生しました。 （NPR-40892）

#### ユーザーインターフェイス{#foundation-ui-6518}

* 詳しくは、 [設定ブラウザーのドキュメント](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/configurations.html?lang=en#using-configuration-browser), _「名前」は、リポジトリ内のノード名になります。_. ただし、設定ブラウザーでは、CRXDE Liteのパスに設定タイトルが使用され、設定の名前は無視されます。 （NPR-40607）

<!-- #### WCM{#wcm-6518}

* A -->

#### ワークフロー{#foundation-workflow-6518}

* アセットのバージョンを元に戻しても、アセットのステータスは処理モードのままになります。 （NPR-41029）
* アセットおよびプロジェクトユーザーインターフェイスの並べ替えの問題。 ビジネス要件に従って、アセットとプロジェクトユーザーインターフェイスのカスタム列をオーバーレイしたものもあります。 標準のプロパティを使用して並べ替えを実装しています。 `sortable=true`. ただし、プロジェクトまたはアセットユーザーインターフェイスに多数のエントリがある場合、並べ替えで不整合が生じています。 （NPR-41027）
* ログに次の情報が入力されています： `NullPointerException` （内） `EMailNotificationService`、および送信するワークフローが設定された電子メールは送信されません。 （NPR-40898）
<!-- REMOVED BY ENGINEERING FROM TOTAL RELEASE CANDIDATE LIST  * The timeline is not providing references to the selected content. (NPR-40806) -->

## [!DNL Experience Manager] 6.5.18.0 のインストール{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.18.0 には [!DNL Experience Manager] 6.5 が必要です。手順について詳しくは、[アップグレードに関するドキュメント](/help/sites-deploying/upgrade.md)を参照してください。<!-- UPDATE FOR EACH NEW RELEASE -->
* サービスパックは、アドビの[ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/jp/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.18.0.zip)からダウンロードできます。
* MongoDB と複数のインスタンスを含むデプロイメントでは、パッケージマネージャーを使用して、オーサーインスタンスの 1 つに [!DNL Experience Manager] 6.5.18.0 をインストールしてください。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> アドビでは、[!DNL Experience Manager] 6.5.18.0 パッケージを削除またはアンインストールすることを推奨しません。したがって、パッケージをインストールする前に、ロールバックする必要がある場合に備えて `crx-repository` のバックアップを作成する必要があります。<!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### [!DNL Experience Manager] 6.5 へのサービスパックのインストール{#install-service-pack}

1. インスタンスが更新モードの場合（インスタンスが以前のバージョンから更新された場合）、インストール前にインスタンスを再起動します。インスタンスの現在の稼動時間が長い場合、アドビは再起動することを推奨します。

1. インストールする前に、[!DNL Experience Manager] インスタンスのスナップショットまたは新しいバックアップを作成します。

1. [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/jp/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.18.0.zip)からサービスパックをダウンロードします。 <!-- UPDATE FOR EACH NEW RELEASE -->

1. パッケージマネージャーを開き、「**[!UICONTROL パッケージをアップロード]**」を選択して、パッケージをアップロードします。詳しくは、[パッケージマネージャー](/help/sites-administering/package-manager.md)を参照してください。

1. パッケージを選択して、「**[!UICONTROL インストール]**」を選択します。

1. S3 コネクタを更新するには、サービスパックのインストール後にインスタンスを停止し、既存のコネクタをインストールフォルダーに用意されている新しいバイナリファイルに置き換えて、インスタンスを再起動します。[Amazon S3 データストア](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)を参照してください。

>[!NOTE]
>
>サービスパックのインストール中に、パッケージマネージャー UI のダイアログが終了することがあります。Adobeでは、エラーログが安定するのを待ってから、デプロイメントにアクセスすることをお勧めします。アップデーターバンドルのアンインストールに関連する特定のログが表示されるのを待ってから、インストールが成功したことを確認します。 通常、この問題は [!DNL Safari] ブラウザーは断続的に使用されますが、どのブラウザーでも発生する場合があります。

**自動インストール**

[!DNL Experience Manager] 6.5.18.0. の自動インストールに使用できる方法は 2 つあります<!-- UPDATE FOR EACH NEW RELEASE -->

* サーバーがオンラインで使用可能な場合、パッケージを `../crx-quickstart/install` フォルダーに配置します。パッケージが自動的にインストールされます。
* [パッケージマネージャーの HTTP API](/help/sites-administering/package-manager.md#package-share) を使用します。ネストされたパッケージがインストールされるように、`cmd=install&recursive=true` を使用します。

>[!NOTE]
>
>Experience Manager 6.5.18.0 では、Bootstrap のインストールをサポートしていません。<!-- UPDATE FOR EACH NEW RELEASE -->

**インストールの検証**

このリリースでの動作が認定されたプラットフォームについては、[技術要件](/help/sites-deploying/technical-requirements.md)を参照してください。

1. 製品情報ページ（`/system/console/productinfo`）の[!UICONTROL インストール済み製品]に、更新されたバージョン文字列 `Adobe Experience Manager (6.5.18.0)` が表示されます。<!-- UPDATE FOR EACH NEW RELEASE -->

1. すべての OSGi バンドルは、OSGi コンソールで **[!UICONTROL アクティブ]** または **[!UICONTROL フラグメント]** です（web コンソールを使用：`/system/console/bundles`）。

1. OSGi バンドル `org.apache.jackrabbit.oak-core` はバージョン 1.22.16 以降です（web コンソールを使用：`/system/console/bundles`）。<!-- NPR-41010 for 6.5.18.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### [!DNL Experience Manager] Forms へのサービスパックのインストール{#install-aem-forms-add-on-package}

AEM Forms にサービスパックをインストールする手順については、[AEM Forms サービスパックのインストール手順](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)を参照してください。

### Experience Manager コンテンツフラグメント用の GraphQL インデックスパッケージのインストール{#install-aem-graphql-index-add-on-package}

GraphQL を使用しているお客様は、[Experience Manager コンテンツフラグメントと GraphQL インデックスパッケージ 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip) をインストールする必要があります。

これにより、実際に使用する機能に基づいて、必要なインデックス定義を追加できます。

このパッケージをインストールしないと、GraphQL クエリが遅くなったり失敗したりする場合があります。

>[!NOTE]
>
>このパッケージは、インスタンスごとに 1 度だけインストールします。サービスパックごとに再インストールする必要はありません。

### UberJar{#uber-jar}

[!DNL Experience Manager] 6.5.18.0 の UberJar は、[Maven Central リポジトリ](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.18/)で入手できます。<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Maven プロジェクトで UberJar を使用するには、[UberJar の使用方法](/help/sites-developing/ht-projects-maven.md)を参照し、プロジェクト POM に次の依存関係を含めます。<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.18</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar およびその他の関連アーティファクトは、Adobe のパブリック Maven リポジトリー （`repo.adobe.com`） ではなく、Maven Central リポジトリーで入手できます。メインの UberJar ファイルの名前は、「`uber-jar-<version>.jar`」に変更されます。そのため `classifier` が存在せず、`apis` が値として `dependency` タグに使用されます。

## 廃止される機能および削除された機能{#removed-deprecated-features}

詳しくは、 [非推奨（廃止予定）の機能と削除された機能](/help/release-notes/deprecated-removed-features.md/).

## 既知の問題{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->
<!-- REMOVED AS PER CQDOC-20022, JANUARY 23, 2023 * If you install [!DNL Experience Manager] 6.5 Service Pack 10 or a previous service pack on [!DNL Experience Manager] 6.5, the runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) is deleted.
To retrieve your runtime copy, Adobe recommends to synchronize the design-time copy of the custom workflow model with its runtime copy using the HTTP API:
`<designModelPath>/jcr:content.generate.json`. -->

* **Service Pack 18 にアップグレードした後、ページパブリッシングがページエディターで機能しない (6.5.18.0)**

  <!-- https://jira.corp.adobe.com/browse/SITES-15856 REMOVE FOR 6.5.19.0--> AEM 6.5.0.0 のインスタンスをAEM 6.5.17.0にアップグレードした後、「 **ページを公開** ページエディター内に、存在しない URL にリダイレクトされます。

  この問題を回避するには、次のいずれかの操作を行います。

   * 次の「path」プロパティを削除します。

     `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/publish/granite:data`

   * 正しい URL をブラウザーに直接貼り付けます。

     `http://localhost:4504/editor.html/libs/wcm/core/content/sites/publishpagewizard.html?item=/content/we-retail/language-masters/en/about-us.html`



* **Oak に関連**
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

   1. 次の 2 つのフォルダーを `crx-quickstart/repository/` から削除する

      * `cache`
      * `diff-cache`

   1. サービスパックをインストールするか、Experience Manager as a Cloud Serviceを再起動します。
`cache` および `diff-cache` の新しいフォルダーが自動的に作成され、`error.log` 内で `mvstore` に関連する例外は発生しなくなりました。

* コンテンツモデルのカスタム API 名を使用した可能性のあるGraphQLクエリを更新し、代わりにコンテンツモデルのデフォルト名を使用します。

* GraphQL クエリでは、`fragments` インデックスの代わりに `damAssetLucene` インデックスを使用する場合があります。このアクションは結果的に、GraphQL クエリが失敗するか、実行に非常に長い時間がかかる可能性があります。

  問題を修正するには、`damAssetLucene` は、次の 2 つのプロパティを含むように設定する必要があります。

   * `contentFragment`
   * `model`

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

* のインストール中に、次のエラーおよび警告メッセージが表示される場合があります。 [!DNL Experience Manager] 6.5.x.x:
   * 「Target Standard API（IMS 認証）を使用して [!DNL Experience Manager] に Adobe Target 統合を設定する場合、エクスペリエンスフラグメントを Target に書き出すと、間違ったオファータイプが作成されます。Target では、「エクスペリエンスフラグメント」／ソース「Adobe Experience Manager」タイプではなく、「HTML」／ソース「Adobe Target Classic」タイプのオファーをいくつか作成します。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * SUM、MAX、MIN などの集計関数が使用される場合、アダプティブフォームのサーバー側検証が失敗します （CQ-4274424）。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * ショッパブルバナービューアでアセットをプレビューすると、Dynamic Mediaのインタラクティブ画像のホットスポットが表示されません。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : 登録状況を未登録に変更する処理が完了するのを待機中にタイムアウトになりました。

* AEM 6.5.15 以降、```org.apache.servicemix.bundles.rhino``` バンドル で提供される Rhino JavaScript Engine には、新しい巻上げ動作が追加されました。strict モード (```use strict;```) は、変数を正しく宣言する必要があります。そうしない場合は、実行されず、代わりにランタイムエラーが発生します。

### AEM Formsの既知の問題

#### サポートされているプラットフォーム

* 1.8.0_281 より高い JDK バージョンは、WebLogic JEE サーバーではサポートされていません。 (FORMS-8498、CQDOC-20383)
* [!DNL Microsoft® Windows Server 2019] は [!DNL MySQL 5.7] および [!DNL JBoss® EAP 7.1] をサポートしていないため、[!DNL Microsoft® Windows Server 2019] は [!DNL Experience Manager Forms 6.5.10.0] の自動インストールをサポートしていません。（CQDOC-18312）
* JDK 11.0.20 は、JEE 上のAEM Formsインストーラーのインストールをサポートしていません。 JEE 上のAEM Formsインストーラーのインストールには、JDK 11.0.19 以前のバージョンのみがサポートされています。 （FORMS-10659）

#### インストール

* JBoss® 7.1.4 プラットフォームで、Experience Manager 6.5.16.0 以降のサービスパックをインストールすると、`adobe-livecycle-jboss.ear` デプロイメントが失敗します。(CQ-4351522、CQDOC-20159)
* AEM Service Pack 6.5.18.0フルインストーラーをインストールした後、JEE で JBoss® Turnkey(CQDOC-20803) を使用して EAR デプロイメントが失敗します。
問題を解決するには、 `<AEM_Forms_Installation_dir>\jboss\bin\standalone.bat` ファイルと更新 `Adobe_Adobe_JAVA_HOME` から `Adobe_JAVA_HOME` を設定してから、configuration manager を実行する必要があります。

#### アダプティブフォーム

* アダプティブフォームが発行されると、変更が加えられていない場合でも、ポリシーを含むすべての依存関係が再発行されます。 （FORMS-10454）
* アダプティブフォームでユーザーが初めてフィールドを設定する場合、設定を保存するオプションはプロパティブラウザーに表示されません。同じエディターでアダプティブフォームの他のフィールドを設定するように選択すると、問題が解決します。
* アダプティブフォームのガイドコンテナでリダイレクト URL が設定されると、インライン署名が機能しなくなります。 （FORMS-10493）
* すべてのレコードのドキュメント (DoR) テンプレートが公開に失敗しました。 英語のロケールベースの DoR テンプレートと、それに関連するFormsベースの DoR テンプレートのみが公開されます。 （FORMS-10535）

#### インタラクティブコミュニケーション

* AEM Service Pack 18 にアップグレードした後は、インタラクティブ通信レターを編集できません。 (FORMS-10578) 問題を解決するには、次の手順を実行します。

   1. ダウンロード [Hotfix-FORMS-10578](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja) SD リンクから。
   1. ホットフィックスアーカイブファイルを展開して、Experience Managerパッケージ (.zip) ファイルとバンドル (.jar) ファイルを取得できるようにします。
   1. パッケージマネージャーからパッケージ (.zip) をアップロードしてインストールします。
   1. Configuration Manager バンドルを開きます。 `https://server:host/system/console/bundles`バンドル (.jar) をアップロードし、インストールします。

## 含まれている OSGi バンドルとコンテンツパッケージ{#osgi-bundles-and-content-packages-included}

次のテキストドキュメントには、[!DNL Experience Manager] 6.5.18.0 に含まれている OSGi バンドルとコンテンツパッケージの一覧が記載されています。<!-- UPDATE FOR EACH NEW RELEASE -->

* [Experience Manager 6.5.18.0 に含まれている OSGi バンドルの一覧](/help/release-notes/assets/65180_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5.18.0 に含まれているコンテンツパッケージの一覧](/help/release-notes/assets/65180_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 制限付き Web サイト{#restricted-sites}

以下の web サイトはお客様のみが参照できます。アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [アドビカスタマーサポートに連絡](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=ja)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 製品ページ](https://business.adobe.com/jp/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=ja)
>* [アドビ製品アップデートの優先通知に登録する](https://www.adobe.com/subscription/priority-product-update.html)
