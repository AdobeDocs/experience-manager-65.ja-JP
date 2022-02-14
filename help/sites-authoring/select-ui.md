---
title: 'UI の選択 '
seo-title: Selecting your UI
description: AEM で使用するインターフェイスを設定します
seo-description: Configure which interface you will use to work in AEM
uuid: ab127f2f-2f8a-4398-90dd-c5d48eed9e53
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: e418d330-f234-411d-8cad-3fd9906dcbee
docset: aem65
exl-id: 01cab3c3-4c0d-44d9-b47c-034de9a08cb1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '743'
ht-degree: 100%

---

# UI の選択 {#selecting-your-ui}

タッチ対応 UI が標準 UI になり、サイトの管理と編集はほぼ同等の機能を持つようになりましたが、[クラシック UI](/help/sites-classic-ui-authoring/classicui.md) に切り替えたくなることもあるでしょう。そのためのオプションがいくつか用意されています。

>[!NOTE]
>
>クラシック UI の機能の同一性の状況について詳しくは、[タッチ UI 機能の同一性](/help/release-notes/touch-ui-features-status.md)のドキュメントを参照してください。

様々な場所で、使用する UI を定義できます。

* [ユーザーのインスタンス用のデフォルト UI の設定](#configuring-the-default-ui-for-your-instance)
ユーザーのログイン時にデフォルトで表示する UI を設定します。ただし、ユーザーはこの設定を上書きしたり、自分のアカウントまたは現在のセッション用に別の UI を選択したりできます。

* [ユーザーのアカウント用のクラシック UI オーサリングの設定](/help/sites-authoring/select-ui.md#setting-classic-ui-authoring-for-your-account)
ページの編集時にデフォルトで使用する UI を設定します。ただし、ユーザーはこの設定を上書きしたり、自分のアカウントまたは現在のセッション用に別の UI を選択したりできます。

* [現在のセッションでのクラシック UI への切り替え](#switching-to-classic-ui-for-the-current-session)
現在のセッション用にクラシック UI に切り替えます。

* [ページのオーサリング時には、状況に応じて、UI が自動的に上書きされます](#ui-overrides-for-the-editor)。

>[!CAUTION]
>
>クラシック UI に切り替えるための様々なオプションは、そのまますぐに使用することはできません。使用しているインスタンス用に設定する必要があります。
>
>詳しくは、[クラシック UI へのアクセスの有効化](/help/sites-administering/enable-classic-ui.md)を参照してください。

>[!NOTE]
>
>以前のバージョンからアップグレードされたインスタンスでは、ページオーサリング用にクラシック UI が保持されます。
>
>アップグレード後、ページオーサリングが自動的にタッチ対応 UI に切り替わることはありませんが、**WCM オーサリング UI モードサービス**（`AuthoringUIMode` サービス）の [OSGi 設定](/help/sites-deploying/configuring-osgi.md)を使用すると、その切り替えを設定できます。[エディターの UI 上書き](#ui-overrides-for-the-editor)を参照してください。

## ユーザーのインスタンス用のデフォルト UI の設定 {#configuring-the-default-ui-for-your-instance}

システム管理者は、[ルートマッピング](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping)を使用して、起動時およびログイン時に表示される UI を設定できます。

この設定はユーザーデフォルトまたはセッション設定によって上書きできます。

## ユーザーのアカウント用のクラシック UI オーサリングの設定 {#setting-classic-ui-authoring-for-your-account}

各ユーザーは、[ユーザーの環境設定](/help/sites-authoring/user-properties.md#userpreferences)にアクセスして、ページオーサリング用に（デフォルト UI の代わりに）クラシック UI を使用するかどうかを定義できます。

この設定はセッション設定によって上書きできます。

## 現在のセッションでのクラシック UI への切り替え {#switching-to-classic-ui-for-the-current-session}

タッチ対応 UI を使用しているデスクトップユーザーは、必要に応じてクラシック UI（デスクトップ専用）に戻すことができます。現在のセッション用にクラシック UI に切り替えるには、複数の方法があります。

* **ナビゲーションリンク**

   >[!CAUTION]
   >
   >クラシック UI に切り替えるためのこのオプションは、そのまますぐに使用することはできません。使用しているインスタンス用に設定する必要があります。
   >
   >
   >詳しくは、[クラシック UI へのアクセスの有効化](/help/sites-administering/enable-classic-ui.md)を参照してください。

   この設定を有効にすると、該当するコンソールの上にマウスポインターを置くたびに、アイコン（モニターのシンボル）が表示され、これをタップ／クリックすると、適切な場所がクラシック UI で開きます。

   例えば、**Sites** から **siteadmin** へのリンクなどです。

   ![syui-01](assets/syui-01.png)

* **URL**

   クラシック UI には、`welcome.html` のようこそ画面の URL を使用してアクセスできます。例は次のとおりです。

   `https://localhost:4502/welcome.html`

   >[!NOTE]
   >
   >タッチ対応 UI には、`sites.html` 経由でアクセスできます。次に例を示します。
   >
   >
   >`https://localhost:4502/sites.html`

### ページ編集時のクラシック UI への切り替え {#switching-to-classic-ui-when-editing-a-page}

>[!CAUTION]
>
>クラシック UI に切り替えるためのこのオプションは、そのまますぐに使用することはできません。使用しているインスタンス用に設定する必要があります。
>
>詳しくは、[クラシック UI へのアクセスの有効化](/help/sites-administering/enable-classic-ui.md)を参照してください。

有効な場合は、**ページ情報**&#x200B;ダイアログで&#x200B;**クラシック UI を開く**&#x200B;が使用可能です。

![syui-02](assets/syui-02.png)

### エディターの UI 上書き {#ui-overrides-for-the-editor}

ページのオーサリング時には、ユーザーまたはシステム管理者が定義した設定がシステムによって上書きされることがあります。

* ページのオーサリング時には次のようになります。

   * URL で `cf#` を使用してページにアクセスする場合、クラシックエディターが強制的に使用されます。次に例を示します。
      `https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

   * URL で `/editor.html` を使用しているか、タッチデバイスを使用している場合、タッチ対応エディターが強制的に使用されます。次に例を示します。
      `https://localhost:4502/editor.html/content/geometrixx/en/products/triangle.html`

* 強制は一時的なものであり、ブラウザーセッションでのみ有効です。

   * Cookie は、タッチ対応（`editor.html`）とクラシック（`cf#`）のどちらが使用されているかに応じて設定されます。

* `siteadmin` を使用してページを開くと、以下が存在するかがチェックされます。

   * Cookie
   * ユーザーの環境設定
   * どちらも存在しない場合は、**WCM オーサリング UI モードサービス**（`AuthoringUIMode` サービス）の [OSGi 設定](/help/sites-deploying/configuring-osgi.md)で指定された定義がデフォルトで使用されます。

>[!NOTE]
>
>[ユーザーが既にページオーサリング用の環境設定を定義している](#settingthedefaultauthoringuiforyouraccount)場合は、OSGi プロパティの変更によってその設定が上書きされることはありません。

>[!CAUTION]
>
>既に説明したように、Cookie を使用しているので、次の操作はお勧めしません。
>
>* URL の手動編集 - 非標準の URL を使用すると予期しない状況となり、機能しなくなる可能性があります。
>* 両方のエディターを同時に開くこと - 例えば、別のウィンドウで開くなど。

