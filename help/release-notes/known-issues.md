---
title: 既知の問題
description: Adobe Experience Manager6.5の既知の問題に関するリリースノート
translation-type: tm+mt
source-git-commit: 8d60e064ab50f24016c049c8d5d0fceb784c99a3
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 47%

---


# 既知の問題 {#known-issues}

このページは、2019 年 4 月にリリースされた Adobe Experience Manager 6.5 の既知の問題の一覧を示しています。

既知の問題について詳しくは、[サポートまでお問い合わせ](https://helpx.adobe.com/jp/support/experience-manager.html)ください。

## プラットフォーム {#platform}

* CRX-Quickstartとその内容が削除された場所に問題が報告されます。

   次の各アクションで、プロパティが空の文字列でないこ `htmllibmanager.fileSystemOutputCacheLocation` とを確認します。

   1. Calling `/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`.
   2. AEM 6.5 へのアップグレード.
   3. AEM 6.5での「遅延コンテンツ移行」の実行

   ナレッジベース [の記事には](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) 、この問題の詳細と回避策が記載されています。

* AEM 6.5インスタンスでJDK 11を使用している場合、一部のパッケージをデプロイすると、一部のページが空白で表示される場合があります。 ログファイルには、次のエラーメッセージが表示されます。

   ```java
   *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
   java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
   ```

このエラーを解決するには：

1. AEM インスタンスを停止して に移動 `<aem_server_path_on_server>crx-quickstart\conf` し、 `sling.properties` ファイルを開きます。 Adobeでは、このファイルのバックアップを作成することをお勧めします。

1. `org.osgi.framework.bootdelegation=` を検索。結果を表示す追加るプロパティ。 `jdk.internal.reflect,jdk.internal.reflect.*`

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. ファイルを保存し、AEMインスタンスを再起動します。

## Assets {#assets}

* **検索：** 検索文字列の先頭にスペースが含まれる場合、検索結果は何も返されません([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **フォルダーメタデータスキーマ**：選択ボタンを追加すると、「ID」フィールドと「値」フィールドが期待どおりにレンダリングされず、削除機能が機能しない（CQ-4261144）
* アセット名の変更時に、アセット名に空白を使用できない（CQ-4266403）

## フォーム {#forms}

* AEM FormsがLinuxオペレーティングシステムにインストールされている場合、Digital Signature with Hardware Security Moduleは機能しません。 （CQ-4266721）
* （WebSphere 上のAEM Forms のみ）**ユーザー名**&#x200B;を検索条件として&#x200B;**管理者**&#x200B;を検索する場合、**Forms のワークフロー**／**タスクの検索**&#x200B;を実行しても結果が返されない（CQ-4266457）

* AEM Formsは、JPEG圧縮を使用したTIFおよびTIFFファイルをPDFドキュメントに変換できません。 （CQ-4265972）
* **AEM Forms の移行**&#x200B;ページの「**AEM Forms アセットスキャナー**」オプションと「**レターからインタラクティブコミュニケーションへの移行**」オプションが機能しない（CQ-4266572）

* （JBoss 7のみ）旧バージョンからAEM 6.5Formsにアップグレードし、旧バージョンでデフォルトの送信プロセスまたはデフォルトのレンダリングプロセスのコピーを作成して使用したプロセス(.lca)がある場合、これらのプロセス(.lca)を使用したHTML5Formsは必要な操作を実行できません。 （CQ-4243928）
* アダプティブフォームで、ルールエディターからフォームデータモデルサービスを呼び出して画像選択コンポーネントの値を動的に更新する場合、画像選択コンポーネントの値が更新されない（CQ-4254754）
* AEM Forms Designer installer requires the 32-bit version of [Visual C++ redistributable runtime package 2012](https://support.microsoft.com/ja-jp/help/2977003/the-latest-supported-visual-c-downloads) and [Visual C++ redistributable runtime packages 2013](https://support.microsoft.com/ja-jp/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package). インストールを開始する前に、これらの再頒布可能ランタイムパッケージがインストールされていることを確認してください。（CQ-4265668）

* PDF Generatorは、スマートカードベースの認証をサポートしていません。  管理者がWindowsサーバーでグループポリシーを有効にす `Interactive Logon: Require Smart card` ると、既存のPDF Generatorユーザーはすべて無効になります。

* コンポーネントの値を動的に更新するようにアダプティブフォームが設定されていて、そのフォームをホストするパブリッシュインスタンスにディスパッチャーを通じてアクセスする場合、フィールドの値を動的に更新する機能が動作しなくなるTo resolve the issue, on the publish instance, open CRXDE, navigate to `/libs/fd/af/runtime/clientlibs/guideChartReducer`, and create the property listed in below.

   * 名前：allowProxy
   * タイプ：Boolean
   * 値：true
   * 保護：false
   * 必須：false
   * 複数：false
   * 自動作成： False

   このプロパティを設定すると、ランタイムフォルダー内のクライアントライブラリからプロキシにアクセスできます。（CQ-4268679）

* AEM Formsが起動すると、 `SAX Security Manager could not be setup` 警告が表示されます。
