---
title: 'UI の選択 '
seo-title: Selecting your UI
description: オーサリングユーザーが使用しやすいように、タッチ対応 UI は必要に応じてクラシック UI に切り替えることができます。
seo-description: For convenience to authoring users, the touch-enabled UI does allow for switching to the classic UI when necessary.
uuid: 755e513e-990c-4dba-8316-623f17bf5c33
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: dcac2a3a-3241-47de-96ce-982ab0bc05eb
exl-id: 57d45b06-e76e-420c-8cd0-389bd9f811af
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 100%

---

# UI の選択 {#selecting-your-ui}

タッチ操作向け UI はクラシック UI より優先されるので、クラシック UI の使用を続行するには、AEM インスタンスのユーザーまたは管理者が自発的に決定する必要があります。クラシック UI のサポートは既に終了しています。そのため、オーサリングユーザーはクラシック UI からタッチ対応 UI の同等の機能に簡単に切り替えることはできません。

オーサリングユーザーが使用しやすいように、タッチ対応 UI は必要に応じてクラシック UI に切り替えることができます。詳しくは、標準オーサリングのドキュメントの [UI の選択](/help/sites-authoring/select-ui.md)を参照してください。

>[!NOTE]
>
>以前のバージョンからアップグレードされたインスタンスでは、ページオーサリング用にクラシック UI が保持されます。
>
>アップグレード後、ページオーサリングが自動的にタッチ対応 UI に切り替わることはありませんが、**WCM オーサリング UI モードサービス**（`AuthoringUIMode` サービス）の [OSGi 設定](/help/sites-deploying/configuring-osgi.md)を使用して、これを設定できます。[エディターの UI の上書き](#uioverridesfortheeditor)を参照してください。

## ユーザーのインスタンス用のデフォルト UI の設定 {#configuring-the-default-ui-for-your-instance}

システム管理者は、[ルートマッピング](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping)を使用して、起動時およびログイン時に表示される UI を設定できます。

この設定はユーザーデフォルトまたはセッション設定によって上書きできます。
