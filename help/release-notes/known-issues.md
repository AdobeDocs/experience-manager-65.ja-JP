---
title: 既知の問題
description: Adobe Experience Manager 6.5の既知の問題に関するリリースノート
uuid: 8fbdb167-833a-4179-aad1-0a26a4e5b3a7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: d11fc727-f23a-4cde-9fa6-97e2c81b4ad0
docset: aem65
translation-type: tm+mt
source-git-commit: 3d607217e3d66998a8463db3f527a626beaca769

---


# 既知の問題 {#known-issues}

このページは、2019 年 4 月にリリースされた Adobe Experience Manager 6.5 の既知の問題の一覧を示しています。

既知の問題について詳しくは、[サポートまでお問い合わせ](https://helpx.adobe.com/support/experience-manager.html)ください。

## プラットフォーム {#platform}

CRX-Quickstartとその内容が削除される問題が報告されます。

これらの各アクションで、「*htmllibmanager.fileSystemOutputCacheLocation」プロパティが空の文字列でないことを確認してください*。

1. &quot;*/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true*&quot;を呼び出します。
2. AEM 6.5 へのアップグレード.
3. AEM 6.5での「遅延コンテンツ移行」の実行。

ナレッジ [ベースの記事に](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) 、この問題の詳細と回避策が記載されています。

## Assets {#assets}

* **検索：** 検索文字列の先頭にスペースが含まれている場合、検索結果は返され[ません(OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **フォルダーメタデータスキーマ**：選択ボタンを追加すると、「ID」フィールドと「値」フィールドが期待どおりにレンダリングされず、削除機能が機能しない（CQ-4261144）
* アセット名の変更時に、アセット名に空白を使用できない（CQ-4266403）

## Forms {#forms}

* AEM Forms が Linux オペレーティングシステムにインストールされている場合、ハードウェアセキュリティモジュールを使用した電子署名が機能しない（CQ-4266721）
* (AEM Forms on WebSphere only) The **Forms Workflow **> **Task Search** option does not return any result if you search for an **Administrator** with **Username** as the search criteria. （CQ-4266457）

* AEM Forms で、JPEG 圧縮の .tif および.tiff ファイルを PDF ドキュメントに変換できない（CQ-4265972）
* **AEM Forms の移行**&#x200B;ページの「**AEM Forms アセットスキャナー**」オプションと「**レターからインタラクティブコミュニケーションへの移行**」オプションが機能しない（CQ-4266572）

* （JBoss 7のみ）以前のバージョンからAEM 6.5 Formsにアップグレードし、以前のバージョンでデフォルトの送信プロセスまたはデフォルトのレンダリングプロセスのコピーを作成して使用したプロセス(.lca)がある場合、このようなプロセス(.lca)を使用するHTML5 Formsは必要な操作を実行できません。 （CQ-4243928）
* アダプティブフォームで、ルールエディターからフォームデータモデルサービスを呼び出して画像選択コンポーネントの値を動的に更新する場合、画像選択コンポーネントの値が更新されない（CQ-4254754）
* AEM Forms Designer installer requires the 32-bit version of [Visual C++ redistributable runtime package 2012](https://support.microsoft.com/en-in/help/2977003/the-latest-supported-visual-c-downloads) and [Visual C++ redistributable runtime packages 2013](https://support.microsoft.com/en-in/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package). インストールを開始する前に、これらの再頒布可能ランタイムパッケージがインストールされていることを確認してください。（CQ-4265668）

* コンポーネントの値を動的に更新するようにアダプティブフォームが設定されていて、そのフォームをホストするパブリッシュインスタンスにディスパッチャーを通じてアクセスする場合、フィールドの値を動的に更新する機能が動作しなくなるこの問題を解決するには、パブリッシュインスタンスで CRXDE を開き、/libs/fd/af/runtime/clientlibs/guideChartReducer を探して、以下のプロパティを作成します。

   * 名前：allowProxy
   * タイプ：Boolean
   * 値：true
   * 保護：false
   * 必須：false
   * 複数：false
   * 自動作成：false

このプロパティを設定すると、ランタイムフォルダー内のクライアントライブラリからプロキシにアクセスできます。（CQ-4268679）

