---
title: アダプティブフォームのローカリゼーション用に新しいロケールをサポート
seo-title: アダプティブフォームのローカリゼーション用に新しいロケールをサポート
description: AEM Forms は、アダプティブフォームのローカライズ用に新しくロケールを追加できます。デフォルトでサポートされているロケールは、英語、フランス語、ドイツ語、日本語です。
seo-description: AEM Forms は、アダプティブフォームのローカライズ用に新しくロケールを追加できます。デフォルトでサポートされているロケールは、英語、フランス語、ドイツ語、日本語です。
uuid: 7f9fab6b-8d93-46bb-8c7c-7b723d5159ea
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: d4e2acb0-8d53-4749-9d84-15b8136e610b
docset: aem65
feature: アダプティブフォーム
role: Administrator
exl-id: 2ed4d99e-0e90-4b21-ac17-aa6707a3ba7d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 84%

---

# アダプティブフォームのローカリゼーション用に新しいロケールをサポート{#supporting-new-locales-for-adaptive-forms-localization}

## ロケールの辞書について {#about-locale-dictionaries}

アダプティブフォームのローカリゼーションは、次の 2 種類のロケールの辞書に基づいています。

**フォーム固有の辞書アダプティブ** フォームで使用される文字列を含みます。例えば、ラベル、フィールド名、エラーメッセージ、ヘルプの説明文などです。各ロケールごとに、XLIFF ファイルのセットの形で管理されています。`https://<host>:<port>/libs/cq/i18n/translator.html` からアクセスできます。

**グローバル辞書** 2 つのグローバル辞書があり、AEM クライアントライブラリで JSON オブジェクトの形で管理されています。これらの辞書にはデフォルトのエラーメッセージ、12 か月の名前、通貨シンボル、日付と時間のパターンなどが含まれます。これらの辞書は CRXDe Lite の /libs/fd/xfaforms/clientlibs/I18N にあります。これらの場所では、各ロケールごと別々のフォルダーが用意されています。グローバルの辞書は頻繁に更新されることはありません。各ロケールごとに別の JavaScript ファイルを保持することで、ブラウザーによりそれらがキャッシュされるため、同一サーバー上で異なるアダプティブフォームにアクセスする際に、ネットワーク帯域幅の使用量を減らすことができます。

### アダプティブフォームのローカリゼーションの仕組み {#how-localization-of-adaptive-form-works}

アダプティブフォームのロケールを識別する方法は2つあります。 アダプティブフォームがレンダリングされると、要求されたロケールがによって識別されます。

* アダプティブフォームURLの`[local]`セレクターを確認する。 URL の形式は、`http://host:port/content/forms/af/[afName].[locale].html?wcmmode=disabled` です。`[local]`セレクターを使用すると、アダプティブフォームをキャッシュできます。

* 指定した順序で次のパラメーターを確認します。

   * リクエストパラメーター`afAcceptLang`
ユーザーのブラウザ-ロケールを上書きするには、 
`afAcceptLang` リクエストパラメーターを渡して、ロケールを強制します。例えば、次の URL は日本語ロケールでのフォームのレンダリングを強制します。
      `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

   * ユーザー向けに設定されるブラウザーのロケールです。これは、`Accept-Language` ヘッダーを使用したリクエストで指定されます。

   * AEM のユーザー指定の言語設定です。

   * ブラウザ-のロケールはデフォルトで有効です。ブラウザーのロケール設定を変更するには
      * 設定マネージャーを開きます。URL は `http://[server]:[port]/system/console/configMgr` です。
      * 「**[!UICONTROL アダプティブフォームおよびインタラクティブ通信 Web チャネル]**」の設定を検索して開きます。
      * 「**[!UICONTROL ブラウザーロケールを使用]**」オプションのステータスを変更して設定を「**[!UICONTROL 保存]**」します。

ロケールが識別されると、アダプティブフォームはフォームに固有の辞書を参照します。要求されたロケールに対するフォーム固有の辞書が見つからない場合は、アダプティブフォームが作成された言語用の辞書が使用されます。

ロケール情報が存在しない場合、アダプティブフォームは元の言語でフォームに配信されます。 元の言語は、アダプティブフォームの開発時に使用される言語です。

リクエストされたロケールでクライアントライブラリが存在しない場合、ロケールに含まれる言語コードがクライアントライブラリに存在しないかチェックします。例えば、リクエストされたロケールが `en_ZA`（南アフリカ英語）で`en_ZA`用のクライアントライブラリが存在しない場合、アダプティブフォームは、`en`（英語）言語が存在する場合、このクライアントライブラリを使用します。ただし、どちらも存在しない場合、アダプティブフォームでは`en`ロケールの辞書が使用されます。

## サポートされていないロケールにローカリゼーションのサポートを追加する {#add-localization-support-for-non-supported-locales}

AEM Formsでは、現在、英語(en)、スペイン語(es)、フランス語(fr)、イタリア語(it)、ドイツ語(de)、日本語(ja)、ポルトガル語(pt-BR)、中国語(zh-CN)、中国語 — 台湾(zh-TW)、韓国語(ko-KR)ロケールのアダプティブフォームコンテンツのローカライゼーションをサポートしています。

アダプティブフォーム実行時に新しいロケールのサポートを追加するには、次を参照してください。

1. [GuideLocalizationService にロケールを追加する](../../forms/using/supporting-new-language-localization.md#p-add-a-locale-to-the-guide-localization-service-br-p)

1. [XFA クライアントライブラリをロケール用に追加する](../../forms/using/supporting-new-language-localization.md#p-add-xfa-client-library-for-a-locale-br-p)

1. [アダプティブフォームのクライアントライブラリをロケール用に追加する](../../forms/using/supporting-new-language-localization.md#p-add-adaptive-form-client-library-for-a-locale-br-p)
1. [辞書のロケールサポートを追加する](../../forms/using/supporting-new-language-localization.md#p-add-locale-support-for-the-dictionary-br-p)
1. [サーバーの再起動](../../forms/using/supporting-new-language-localization.md#p-restart-the-server-p)

### ロケールを Guide Localization Service に追加する {#add-a-locale-to-the-guide-localization-service-br}

1. `https://'[server]:[port]'/system/console/configMgr` にアクセスします。
1. **Guide Localization Service** をクリックしてコンポーネントを編集します。
1. 追加するロケールを、サポート対象のロケールの一覧に追加します。

![GuideLocalizationSevice](assets/configservice.png)

### XFA クライアントライブラリをロケール用に追加する {#add-xfa-client-library-for-a-locale-br}

`etc/<folderHierarchy>`　の下にカテゴリ　`xfaforms.I18N.<locale>`　のタイプ　`cq:ClientLibraryFolder`　のノードを作成し、次のファイルをクライアントライブラリに追加します。

* `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`　で定義されている　`<locale>`　の　`xfalib.locale.Strings`　を定義している　**I18N.js**。

* 以下を含む **js.txt** ファイル。

```text
/libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js
```

### アダプティブフォームのクライアントライブラリをロケール用に追加する {#add-adaptive-form-client-library-for-a-locale-br}

`etc/<folderHierarchy>`　の下にタイプ　`cq:ClientLibraryFolder`　のノードを作成します。カテゴリは　`guides.I18N.<locale>`、依存関係は　`xfaforms.3rdparty`、`xfaforms.I18N.<locale>`、`guide.common`　です。 「

クライアントライブラリに次のファイルを追加します。

* **I18n.js　で** `guidelib.i18n`　を定義し、`<locale>` の「calendarSymbols」、`datePatterns`、`timePatterns`、`dateTimeSymbols`、`numberPatterns`、`numberSymbols`、`currencySymbols`、`typefaces`　のパターンを持つファイルです。これらは[ロケールセットの仕様](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf)に記載されている XFA 仕様に従ってください。また、サポート対象の他のロケールがどのように定義されているか、`/etc/clientlibs/fd/af/I18N/fr/javascript/i18n.js` で確認することができます。
* **LogMessages.js　で**　で `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js` で定義された `<locale>` の `guidelib.i18n.strings` と `guidelib.i18n.LogMessages` を定義します。
* 以下を含む **js.txt** ファイル。

```text
i18n.js
LogMessages.js
```

### 辞書のロケールサポートを追加する {#add-locale-support-for-the-dictionary-br}

追加する`<locale>`が、`en`、`de`、`es`、`fr`、`it`、`pt-br`、`zh-cn`、`zh-tw`、`ja`、`ko-kr`以外の場合にのみ、この手順を実行してください。

1. すでに存在しない場合は、`nt:unstructured` の下に、`languages`ノード`etc` を作成します。

1. すでに存在しない場合は、複数の値を持つ文字列プロパティ `languages` をノードに追加します。
1. すでに存在しない場合は、`<locale>`デフォルトのロケール値`de`、`es`、`fr`、`it`、`pt-br`、`zh-cn`、`zh-tw`、`ja`、`ko-kr` を追加します。

1. `<locale>` を `/etc/languages` の `languages` プロパティの値に追加します。

`<locale>` は `https://'[server]:[port]'/libs/cq/i18n/translator.html` に表示されます。

### サーバーの再起動 {#restart-the-server}

追加したロケールを有効にするために AEM サーバーを再起動します。

## スペイン語サポートを追加する場合のサンプルライブラリ {#sample-libraries-for-adding-support-for-spanish}

スペイン語サポートを追加する場合のサンプルクライアントライブラリ

[ファイルを入手](assets/sample.zip)
