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
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# アダプティブフォームのローカリゼーション用に新しいロケールをサポート{#supporting-new-locales-for-adaptive-forms-localization}

## ロケールの辞書について {#about-locale-dictionaries}

アダプティブフォームのローカリゼーションは、次の 2 種類のロケールの辞書に基づいています。

**フォーム固有の辞書** ：アダプティブフォームで使用される文字列を含みます。 例えば、ラベル、フィールド名、エラーメッセージ、ヘルプの説明文などです。It is managed as a set of XLIFF files for each locale and you can access it at `https://<host>:<port>/libs/cq/i18n/translator.html`.

**グローバル辞書** 2つのグローバル辞書があり、JSONオブジェクトとしてAEMクライアントライブラリで管理されます。 これらの辞書にはデフォルトのエラーメッセージ、12 か月の名前、通貨シンボル、日付と時間のパターンなどが含まれます。これらの辞書は CRXDe Lite の /libs/fd/xfaforms/clientlibs/I18N にあります。これらの場所では、各ロケールごと別々のフォルダーが用意されています。グローバルの辞書は頻繁に更新されることはありません。各ロケールごとに別の JavaScript ファイルを保持することで、ブラウザーによりそれらがキャッシュされるため、同一サーバー上で異なるアダプティブフォームにアクセスする際に、ネットワーク帯域幅の使用量を減らすことができます。

### アダプティブフォームのローカリゼーションの仕組み {#how-localization-of-adaptive-form-works}

アダプティブフォームがレンダリングされるときは、指定された順序で以下のパラメーターが参照され、リクエストされたロケールが識別されます。

* Request parameter `afAcceptLang`
To override the browser locale of users, you can pass the `afAcceptLang` request parameter to force the locale. 例えば、次のURLは日本語ロケールでのフォームのレンダリングを強制します。
   `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* The browser locale set for the user, which is specified in the request using the `Accept-Language` header.

* AEM のユーザー指定の言語設定です。

ロケールが識別されると、アダプティブフォームはフォームに固有の辞書を参照します。リクエストされたロケールでフォームに固有の辞書が見つからない場合、代わりに英語辞書（en）が使用されます。

リクエストされたロケールでクライアントライブラリが存在しない場合、ロケールに含まれる言語コードがクライアントライブラリに存在しないかチェックします。例えば、リクエストされたロケールが `en_ZA`（南アフリカ英語）で`en_ZA`用のクライアントライブラリが存在しない場合、アダプティブフォームは、`en`（英語）言語が存在する場合、このクライアントライブラリを使用します。ただし、どちらも存在しない場合、アダプティブフォームでは`en`ロケールの辞書が使用されます。

## サポートされていないロケールにローカリゼーションのサポートを追加する {#add-localization-support-for-non-supported-locales}

AEM Formsでは、現在、英語(en)、スペイン語(es)、フランス語(fr)、イタリア語(it)、ドイツ語(de)、日本語(ja)、ポルトガル語(br)、中国語(zh-CN)、中国語(taiwan)ロケール(zh-TW)、韓国語(ko-KR)のアダプティブフォームコンテンツのローカライゼーションをサポートしています。.

アダプティブフォーム実行時に新しいロケールのサポートを追加するには、次を参照してください。

1. [GuideLocalizationService にロケールを追加する](../../forms/using/supporting-new-language-localization.md#p-add-a-locale-to-the-guide-localization-service-br-p)

1. [XFA クライアントライブラリをロケール用に追加する](../../forms/using/supporting-new-language-localization.md#p-add-xfa-client-library-for-a-locale-br-p)

1. [アダプティブフォームのクライアントライブラリをロケール用に追加する](../../forms/using/supporting-new-language-localization.md#p-add-adaptive-form-client-library-for-a-locale-br-p)
1. [辞書のロケールサポートを追加する](../../forms/using/supporting-new-language-localization.md#p-add-locale-support-for-the-dictionary-br-p)
1. [サーバーの再起動](../../forms/using/supporting-new-language-localization.md#p-restart-the-server-p)

### Add a locale to the Guide Localization service {#add-a-locale-to-the-guide-localization-service-br}

1. `https://'[server]:[port]'/system/console/configMgr` にアクセスします。
1. **Guide Localization Service**&#x200B;をクリックしてコンポーネントを編集します。
1. 追加するロケールを、サポート対象のロケールの一覧に追加します。

![GuideLocalizationSevice](assets/configservice.png)

### XFA クライアントライブラリをロケール用に追加する {#add-xfa-client-library-for-a-locale-br}

次のタイプのノードを、 `cq:ClientLibraryFolder` カテゴリ `etc/<folderHierarchy>`を含 `xfaforms.I18N.<locale>`むで作成し、クライアントライブラリに追加します。

* **の定義に従って** 、I18N.js `xfalib.locale.Strings` が `<locale>` を定義しています `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`。

* 以下を含む **js.txt** ファイル。

```
/libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js
```

### アダプティブフォームのクライアントライブラリをロケール用に追加する {#add-adaptive-form-client-library-for-a-locale-br}

の下にタイプのノードを作成し、の `cq:ClientLibraryFolder` ノードを、のノードと、の `etc/<folderHierarchy>`カテゴリと依存関係を `guides.I18N.<locale>` 持たせて `xfaforms.3rdparty`くださ `xfaforms.I18N.<locale>``guide.common`い。&quot;

クライアントライブラリに次のファイルを追加します。

* **i18n.js** , `guidelib.i18n`, &quot;calendarSymbols&quot;のパターンを持つ，,, `datePatterns`, `timePatterns`, `dateTimeSymbols`, `numberPatterns`, `numberSymbols`, `currencySymbols`, per `typefaces``<locale>`[](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf)xfa, locale setロケールset仕様を定義する， You can also see how it is defined for other supported locales in `/etc/clientlibs/fd/af/I18N/fr/javascript/i18n.js`.
* **とを定義するLogMessages** .js `guidelib.i18n.strings` （を参照）。とは、を参照してく `guidelib.i18n.LogMessages` ださい。LogMessages.jsは、とを定義してい `<locale>``/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`ます。
* 以下を含む **js.txt** ファイル。

```
i18n.js
LogMessages.js
```

### 辞書のロケールサポートを追加する {#add-locale-support-for-the-dictionary-br}

Perform this step only if the `<locale>` you are adding is not among `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`.

1. Create an `nt:unstructured` node `languages` under `etc`, if not present already.

1. すでに存在しない場合は、複数の値を持つ文字列プロパティ `languages` をノードに追加します。
1. デフ追加ォルト `<locale>` のロケール値， `de`, `es`, `fr`, `it`, , `pt-br`, `zh-cn``zh-tw``ja``ko-kr`notは既に存在します。

1. Add the `<locale>` to the values of the `languages` property of `/etc/languages`.

がに表 `<locale>` 示されま `https://'[server]:[port]'/libs/cq/i18n/translator.html`す。

### サーバーの再起動 {#restart-the-server}

追加したロケールを有効にするために AEM サーバーを再起動します。

## スペイン語サポートを追加する場合のサンプルライブラリ {#sample-libraries-for-adding-support-for-spanish}

スペイン語サポートを追加する場合のサンプルクライアントライブラリ

[ファイルを入手](assets/sample.zip)
