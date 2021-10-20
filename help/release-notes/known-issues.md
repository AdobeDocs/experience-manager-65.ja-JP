---
title: 既知の問題
description: リリースノート (Adobe Experience Manager 6.5 の既知の問題に固有 )
exl-id: 736037cf-af8c-4ce2-969e-c100a939a038
source-git-commit: e0f024c2e1dc9fc7908382d406844575b4b38363
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 48%

---

# 既知の問題 {#known-issues}

このページは、2019 年 4 月にリリースされた Adobe Experience Manager 6.5 の既知の問題の一覧を示しています。

既知の問題について詳しくは、[サポートまでお問い合わせ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=ja)ください。

## Platform {#platform}

* CRX-Quickstart とその内容が削除された場所に問題が報告されます。

   これらの各アクションで、 `htmllibmanager.fileSystemOutputCacheLocation` は空の文字列ではありません：

   1. 呼び出し `/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`.
   2. AEM 6.5 へのアップグレード.
   3. AEM 6.5 で「遅延コンテンツ移行」を実行します。

   A [ナレッジベース](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) この記事には、この問題の詳細と回避策が記載されています。

* AEM 6.5 インスタンスで JDK 11 を使用している場合、一部のパッケージをデプロイすると、一部のページが空白で表示されることがあります。 次のエラーメッセージがログファイルに表示されます。

   ```java
   *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
   java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
   ```

このエラーを解決するには：

1. AEM インスタンスを停止してに移動します。 `<aem_server_path_on_server>crx-quickstart\conf` をクリックし、 `sling.properties` ファイル。 Adobeは、このファイルのバックアップを作成することをお勧めします。

1. `org.osgi.framework.bootdelegation=` を検索。追加 `jdk.internal.reflect,jdk.internal.reflect.*` 結果を表示するプロパティ。

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. ファイルを保存し、AEMインスタンスを再起動します。

## Assets {#assets}

* **検索：** 検索文字列の先頭にスペース ([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **フォルダーメタデータスキーマ**：選択ボタンを追加すると、「ID」フィールドと「値」フィールドが期待どおりにレンダリングされず、削除機能が機能しない（CQ-4261144）
* アセット名の変更時に、アセット名に空白を使用できない（CQ-4266403）

## Forms {#forms}

* AEM Formsが Linux オペレーティングシステムにインストールされている場合、ハードウェアセキュリティモジュールを使用したデジタル署名は機能しません。 （CQ-4266721）
* （WebSphere 上のAEM Forms のみ）**ユーザー名**&#x200B;を検索条件として&#x200B;**管理者**&#x200B;を検索する場合、**Forms のワークフロー**／**タスクの検索**&#x200B;を実行しても結果が返されない（CQ-4266457）

* AEM Formsは、JPEG圧縮を含む TIF およびTIFFファイルをPDFドキュメントに変換できません。 （CQ-4265972）
* **AEM Forms の移行**&#x200B;ページの「**AEM Forms アセットスキャナー**」オプションと「**レターからインタラクティブコミュニケーションへの移行**」オプションが機能しない（CQ-4266572）

* （JBoss 7 のみ）以前のバージョンからAEM 6.5 Formsにアップグレードし、以前のバージョンで、デフォルトの送信プロセスまたはデフォルトのレンダリングプロセスのコピーを作成して使用したプロセス (.lca) がある場合、そのようなプロセス (.lca) を使用したHTML5 Formsは必要なアクションを実行できません。 （CQ-4243928）
* アダプティブフォームで、ルールエディターからフォームデータモデルサービスを呼び出して画像選択コンポーネントの値を動的に更新する場合、画像選択コンポーネントの値が更新されない（CQ-4254754）
* AEM Forms Designer インストーラーを使用するには、32 ビット版の [Visual C++再頒布可能ランタイムパッケージ 2012](https://support.microsoft.com/ja-jp/help/2977003/the-latest-supported-visual-c-downloads) および [Visual C++再頒布可能ランタイムパッケージ 2013](https://support.microsoft.com/ja-jp/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package). インストールを開始する前に、これらの再頒布可能ランタイムパッケージがインストールされていることを確認してください。（CQ-4265668）

* PDFジェネレーターは、スマートカードベースの認証をサポートしていません。  管理者がグループポリシーを有効にしたとき `Interactive Logon: Require Smart card` Windows サーバーでは、既存のすべてのPDF・ジェネレータ・ユーザーが無効化されます。

* コンポーネントの値を動的に更新するようにアダプティブフォームが設定されていて、そのフォームをホストするパブリッシュインスタンスにディスパッチャーを通じてアクセスする場合、フィールドの値を動的に更新する機能が動作しなくなるこの問題を解決するには、パブリッシュインスタンスで CRXDE を開き、に移動します。 `/libs/fd/af/runtime/clientlibs/guideChartReducer`をクリックし、次のプロパティを作成します。

   * 名前：allowProxy
   * タイプ：Boolean
   * 値：true
   * 保護：false
   * 必須：false
   * 複数：false
   * 自動作成：False

   このプロパティを設定すると、ランタイムフォルダー内のクライアントライブラリからプロキシにアクセスできます。（CQ-4268679）

* AEM Formsを起動すると、 `SAX Security Manager could not be setup` 警告が表示されます。
* Apple iOSまたはAdobe Acrobat Readerバージョン20.10.00を実行する iPadOS で、AEM Forms Document Security で保護されたPDFを開いたとき。
* 標準の HTML アップロードフィールドを含んだフォームを Apple iOS デバイスから送信すると、ファイルの内容が送信されず、送信先で 0 バイトのファイルを受信することがあります。Apple iOS 15.1 で問題の修正がおこなわれました。
