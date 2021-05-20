---
title: 既知の問題
description: リリースノート(Adobe Experience Manager 6.5の既知の問題に固有)
exl-id: 736037cf-af8c-4ce2-969e-c100a939a038
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 46%

---

# 既知の問題 {#known-issues}

このページは、2019 年 4 月にリリースされた Adobe Experience Manager 6.5 の既知の問題の一覧を示しています。

既知の問題について詳しくは、[サポートまでお問い合わせ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=ja)ください。

## プラットフォーム {#platform}

* CRX-Quickstartとその内容が削除された場合に発生する問題が報告されます。

   これらの各アクションで、プロパティ`htmllibmanager.fileSystemOutputCacheLocation`が空の文字列でないことを確認します。

   1. `/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`を呼び出しています。
   2. AEM 6.5 へのアップグレード.
   3. AEM 6.5で「遅延コンテンツ移行」を実行する。

   詳細とこの問題の回避策については、[ナレッジベース](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html)の記事を参照してください。

* AEM 6.5インスタンスでJDK 11を使用している場合、一部のパッケージをデプロイすると、一部のページが空白で表示されることがあります。 ログファイルには、次のエラーメッセージが表示されます。

   ```java
   *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
   java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
   ```

このエラーを解決するには：

1. AEM インスタンスを停止して `<aem_server_path_on_server>crx-quickstart\conf`に移動し、`sling.properties`ファイルを開きます。 Adobeは、このファイルのバックアップを作成することをお勧めします。

1. `org.osgi.framework.bootdelegation=` を検索。結果を表示する`jdk.internal.reflect,jdk.internal.reflect.*`プロパティを追加します。

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. ファイルを保存し、AEMインスタンスを再起動します。

## Assets {#assets}

* **検索：** 検索文字列の先頭にスペースが含まれている場合、検索結果が返されない([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **フォルダーメタデータスキーマ**：選択ボタンを追加すると、「ID」フィールドと「値」フィールドが期待どおりにレンダリングされず、削除機能が機能しない(CQ-4261144)
* アセット名の変更時に、アセット名に空白を使用できない(CQ-4266403)

## フォーム {#forms}

* AEM FormsがLinuxオペレーティングシステムにインストールされている場合、ハードウェアセキュリティモジュールを使用したデジタル署名は機能しません。 (CQ-4266721)
* （WebSphere 上のAEM Forms のみ）**ユーザー名**&#x200B;を検索条件として&#x200B;**管理者**&#x200B;を検索する場合、**Forms のワークフロー**／**タスクの検索**&#x200B;を実行しても結果が返されない(CQ-4266457)

* AEM Formsで、JPEG圧縮のTIFおよびTIFFファイルをPDFドキュメントに変換できない。 (CQ-4265972)
* **AEM Forms の移行**&#x200B;ページの「**AEM Forms アセットスキャナー**」オプションと「**レターからインタラクティブコミュニケーションへの移行**」オプションが機能しない(CQ-4266572)

* （JBoss 7のみ）以前のバージョンからAEM 6.5 Formsにアップグレードし、以前のバージョンで、デフォルトの送信またはデフォルトのレンダリングプロセスのコピーを作成して使用したプロセス(.lca)がある場合、このようなプロセス(.lca)を使用するHTML5 Formsは必要なアクションを実行できません。 (CQ-4243928)
* アダプティブフォームで、ルールエディターからフォームデータモデルサービスを呼び出して画像選択コンポーネントの値を動的に更新する場合、画像選択コンポーネントの値が更新されない(CQ-4254754)
* AEM Forms Designerのインストーラーには、32ビット版の[Visual C++再配布可能ランタイムパッケージ2012](https://support.microsoft.com/ja-jp/help/2977003/the-latest-supported-visual-c-downloads)と[Visual C++再配布可能ランタイムパッケージ2013](https://support.microsoft.com/ja-jp/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package)が必要です。 インストールを開始する前に、これらの再頒布可能ランタイムパッケージがインストールされていることを確認してください。(CQ-4265668)

* PDF Generatorはスマートカードベースの認証をサポートしていません。  管理者がWindowsサーバーでグループポリシー`Interactive Logon: Require Smart card`を有効にすると、既存のPDF Generatorユーザーはすべて無効化されます。

* コンポーネントの値を動的に更新するようにアダプティブフォームが設定されていて、そのフォームをホストするパブリッシュインスタンスにディスパッチャーを通じてアクセスする場合、フィールドの値を動的に更新する機能が動作しなくなるこの問題を解決するには、パブリッシュインスタンスでCRXDEを開き、`/libs/fd/af/runtime/clientlibs/guideChartReducer`に移動して、以下に示すプロパティを作成します。

   * 名前：allowProxy
   * タイプ：Boolean
   * 値：true
   * 保護：false
   * 必須：false
   * 複数：false
   * 自動作成：False

   このプロパティを設定すると、ランタイムフォルダー内のクライアントライブラリからプロキシにアクセスできます。(CQ-4268679)

* AEM Formsが起動すると、`SAX Security Manager could not be setup`警告が表示されます。
* Adobe AcrobatReaderバージョン20.10.00を実行するApple iOSまたはiPadOSで、AEM Forms Document Securityで保護されたPDFを開く場合。
