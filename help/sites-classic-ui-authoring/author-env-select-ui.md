---
title: UI の選択
description: オーサリングユーザーが使用しやすいように、タッチ対応 UI は必要に応じてクラシック UI に切り替えることができます。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 57d45b06-e76e-420c-8cd0-389bd9f811af
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 100%

---

# UI の選択 {#selecting-your-ui}

タッチ操作向け UI はクラシック UI より優先されるので、クラシック UI の使用を続行するには、AEM インスタンスのユーザーまたは管理者が自発的に決定する必要があります。クラシック UI のサポートは既に終了しています。そのため、オーサリングユーザーはクラシック UI からタッチ対応 UI の同等の機能に簡単に切り替えることはできません。

オーサリングユーザーが使用しやすいように、タッチ対応 UI は必要に応じてクラシック UI に切り替えることができます。詳しくは、標準のオーサリングドキュメントの [UI の選択](/help/sites-authoring/select-ui.md)を参照してください。

>[!NOTE]
>
>以前のバージョンからアップグレードされたインスタンスでは、ページオーサリング用にクラシック UI が保持されます。
>
>アップグレード後、ページオーサリングが自動的にタッチ対応 UI に切り替わることはありませんが、**WCM オーサリング UI モードサービス**（`AuthoringUIMode` サービス）の [OSGi 設定](/help/sites-deploying/configuring-osgi.md)を使用して、これを設定できます。[エディターの UI の上書き](#uioverridesfortheeditor)を参照してください。

## 使用しているインスタンスへのデフォルト UI の設定 {#configuring-the-default-ui-for-your-instance}

システム管理者は、[ルートマッピング](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping)を使用して、起動時およびログイン時に表示される UI を設定できます。

この設定は、ユーザーのデフォルト設定またはセッション設定で上書きできます。
