---
title: UI の選択
seo-title: UI の選択
description: オーサリングユーザーが使用しやすいように、タッチ対応 UI は必要に応じてクラシック UI に切り替えることができます。
seo-description: オーサリングユーザーが使用しやすいように、タッチ対応 UI は必要に応じてクラシック UI に切り替えることができます。
uuid: 755e513e-990c-4dba-8316-623f17bf5c33
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: dcac2a3a-3241-47de-96ce-982ab0bc05eb
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 60%

---


# UI の選択{#selecting-your-ui}

タッチ対応UIはクラシックUIより優先されるので、AEMインスタンスのユーザーまたは管理者は、クラシックUIを使用し続けるためにアクティブな決定を行う必要があります。 従来のUIは維持されなくなったので、オーサリングユーザーがタッチ操作対応UIで従来のUIから同等のUIに切り替える方法はありません。

オーサリングユーザーが使用しやすいように、タッチ対応 UI は必要に応じてクラシック UI に切り替えることができます。詳しくは、標準オーサリングのドキュメントの [UI の選択](/help/sites-authoring/select-ui.md)を参照してください。

>[!NOTE]
>
>以前のバージョンからアップグレードされたインスタンスでは、ページオーサリング用にクラシック UI が保持されます。
>
>After upgrade, page authoring will not be automatically switched to the touch-enabled UI, but you can configure this usingthe[OSGi configuration](/help/sites-deploying/configuring-osgi.md) of the **WCM Authoring UI Mode Service** ( `AuthoringUIMode` service). [エディターの UI 上書き](#uioverridesfortheeditor)を参照してください。

## ユーザーのインスタンス用のデフォルト UI の設定 {#configuring-the-default-ui-for-your-instance}

システム管理者は、[ルートマッピング](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping)を使用して、起動時およびログイン時に表示される UI を設定できます。

この設定はユーザーデフォルトまたはセッション設定によって上書きできます。
