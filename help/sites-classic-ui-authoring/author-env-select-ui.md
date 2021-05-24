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
exl-id: 57d45b06-e76e-420c-8cd0-389bd9f811af
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 60%

---

# UI の選択{#selecting-your-ui}

タッチ操作対応UIはクラシックUIより優先されるので、クラシックUIを引き続き使用するには、AEMインスタンスのユーザーまたは管理者がアクティブに決定する必要があります。 クラシックUIはメンテナンスされなくなったので、オーサリングユーザーは、タッチ操作対応UIでクラシックUIから同等のUIに切り替えるだけでは済みません。

オーサリングユーザーが使用しやすいように、タッチ対応 UI は必要に応じてクラシック UI に切り替えることができます。詳しくは、標準オーサリングのドキュメントの [UI の選択](/help/sites-authoring/select-ui.md)を参照してください。

>[!NOTE]
>
>以前のバージョンからアップグレードされたインスタンスでは、ページオーサリング用にクラシック UI が保持されます。
>
>アップグレード後、ページオーサリングはタッチ操作対応UIに自動的に切り替わりませんが、**WCMオーサリングUIモードサービス**（`AuthoringUIMode`サービス）の[OSGi設定](/help/sites-deploying/configuring-osgi.md)を使用して設定できます。 [エディターの UI 上書き](#uioverridesfortheeditor)を参照してください。

## ユーザーのインスタンス用のデフォルト UI の設定 {#configuring-the-default-ui-for-your-instance}

システム管理者は、[ルートマッピング](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping)を使用して、起動時およびログイン時に表示される UI を設定できます。

この設定はユーザーデフォルトまたはセッション設定によって上書きできます。
