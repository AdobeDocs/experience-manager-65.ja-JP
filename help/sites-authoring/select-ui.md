---
title: AEM でのユーザーインターフェイスの選択
description: AEM での作業に使用するインターフェイスを設定します。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 01cab3c3-4c0d-44d9-b47c-034de9a08cb1
source-git-commit: 4e2ee7da5424ac6677eaa2392de7803e7543d13c
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 43%

---

# UI の選択 {#selecting-your-ui}

Adobe Experience Manager(AEM) のタッチ操作対応 UI が標準 UI になり、サイトの管理と編集はほぼ同等の機能を備えています。 ただし、ユーザーが [クラシック UI](/help/sites-classic-ui-authoring/classicui.md). そのためのオプションがいくつか用意されています。

>[!NOTE]
>
>クラシック UI の機能の同一性の状況について詳しくは、[タッチ UI 機能の同一性](/help/release-notes/touch-ui-features-status.md)のドキュメントを参照してください。

使用する UI を様々な場所で定義できます。

* [インスタンスのデフォルト UI の設定](#configuring-the-default-ui-for-your-instance)
これにより、ユーザーのログイン時に表示されるデフォルトの UI が設定されます。 ユーザーは、これを上書きして、自分のアカウントまたは現在のセッションに別の UI を選択できます。

* [お使いのアカウント用のクラシック UI オーサリングの設定](/help/sites-authoring/select-ui.md#setting-classic-ui-authoring-for-your-account)
これにより、ページの編集時に UI がデフォルトに設定されますが、ユーザーはこれを上書きして、自分のアカウントまたは現在のセッション用に別の UI を選択できます。

* [現在のセッションのクラシック UI への切り替え](#switching-to-classic-ui-for-the-current-session)
現在のセッションのクラシック UI に切り替えます。

* の場合 [ページオーサリング時に、UI に関連して特定の上書きがおこなわれます。](#ui-overrides-for-the-editor).

>[!CAUTION]
>
>クラシック UI に切り替えるための様々なオプションをすぐに使用することはできません。その場合は、インスタンスに対して設定する必要があります。
>
>詳しくは、[クラシック UI へのアクセスの有効化](/help/sites-administering/enable-classic-ui.md)を参照してください。

>[!NOTE]
>
>以前のバージョンからアップグレードされたインスタンスは、ページオーサリング用にクラシック UI を保持します。
>
>アップグレード後、ページオーサリングは自動的にはタッチ操作対応 UI に切り替わりませんが、次のページで設定できます： [OSGi 設定](/help/sites-deploying/configuring-osgi.md) の **WCM オーサリング UI モードサービス** ( `AuthoringUIMode` サービス )。 [エディターの UI 上書き](#ui-overrides-for-the-editor)を参照してください。

## 使用しているインスタンスへのデフォルト UI の設定 {#configuring-the-default-ui-for-your-instance}

システム管理者は、[ルートマッピング](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping)を使用して、起動時およびログイン時に表示される UI を設定できます。

この設定は、ユーザーのデフォルト設定またはセッション設定で上書きできます。

## アカウントのクラシック UI オーサリングの設定 {#setting-classic-ui-authoring-for-your-account}

各ユーザーは、独自の [ユーザーの環境設定](/help/sites-authoring/user-properties.md#userpreferences) を定義して、ページオーサリングにデフォルトの UI ではなくクラシック UI を使用するかどうかを定義します。

この設定は、セッション設定で上書きできます。

## 現在のセッションのクラシック UI への切り替え {#switching-to-classic-ui-for-the-current-session}

タッチ操作対応 UI を使用する場合、デスクトップユーザーはクラシック（デスクトップのみ）UI に戻すことが望ましいことがあります。 現在のセッションでクラシック UI に切り替える方法はいくつかあります。

* **ナビゲーションリンク**

  >[!CAUTION]
  >
  >クラシック UI に切り替えるためのこのオプションは、すぐに使用できる状態にはなっていません。お使いのインスタンスに対して設定する必要があります。
  >
  >
  >詳しくは、[クラシック UI へのアクセスの有効化](/help/sites-administering/enable-classic-ui.md)を参照してください。

  このオプションが有効になっている場合は、該当するコンソールにマウスを移動するたびに、アイコン（モニタの記号）が表示されます。 これをタップまたはクリックすると、適切な場所がクラシック UI で開きます。

  例えば、 **Sites** から **siteadmin**:

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
>クラシック UI に切り替えるためのこのオプションは、すぐに使用できる状態にはなっていません。お使いのインスタンスに対して設定する必要があります。
>
>詳しくは、[クラシック UI へのアクセスの有効化](/help/sites-administering/enable-classic-ui.md)を参照してください。

有効な場合は、**ページ情報**&#x200B;ダイアログで&#x200B;**クラシック UI を開く**&#x200B;が使用可能です。

![syui-02](assets/syui-02.png)

### エディターの UI のオーバーライド {#ui-overrides-for-the-editor}

ページオーサリングがある場合、ユーザーまたはシステム管理者が定義した設定をシステムで上書きできます。

* ページのオーサリング時：

   * URL で `cf#` を使用してページにアクセスする場合、クラシックエディターが強制的に使用されます。次に例を示します。
     `https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

   * URL で `/editor.html` を使用しているか、タッチデバイスを使用している場合、タッチ対応エディターが強制的に使用されます。次に例を示します。
     `https://localhost:4502/editor.html/content/geometrixx/en/products/triangle.html`

* 強制は一時的なものであり、ブラウザーセッションでのみ有効です。

   * Cookie の設定は、タッチ操作対応 ( `editor.html`) または classic ( `cf#`) が使用されます。

* ページを開くとき `siteadmin`が設定され、次の値が存在するかがチェックされます。

   * Cookie
   * ユーザーの環境設定
   * どちらも存在しない場合は、 [OSGi 設定](/help/sites-deploying/configuring-osgi.md) の **WCM オーサリング UI モードサービス** ( `AuthoringUIMode` サービス )。

>[!NOTE]
>
>次の場合 [ユーザーが既にページオーサリングの環境設定を定義しています](#settingthedefaultauthoringuiforyouraccount)の値を上書きする必要はありません。OSGi プロパティの変更によって上書きされることはありません。

>[!CAUTION]
>
>既に説明したように、Cookie の使用により、次の操作はお勧めしません。
>
>* URL を手動で編集 - 非標準の URL を使用すると、不明な状況が発生し、機能が不足する場合があります。
>* 両方のエディターを同時に開くこと - 例えば、別のウィンドウで開くなど。
