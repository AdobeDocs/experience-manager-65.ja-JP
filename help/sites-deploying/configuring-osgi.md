---
title: OSGi の設定
seo-title: OSGi の設定
description: OSGi は、Adobe Experience Manager（AEM）の技術スタックにおける基本要素です。AEM の複合バンドルおよびそれらの設定を制御するために使用します。この記事では、このようなバンドルの設定を管理する方法について詳しく説明します。
seo-description: OSGi は、Adobe Experience Manager（AEM）の技術スタックにおける基本要素です。AEM の複合バンドルおよびそれらの設定を制御するために使用します。この記事では、このようなバンドルの設定を管理する方法について詳しく説明します。
uuid: b39059a5-dd61-486a-869a-0d7a732c3a47
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: d701e4ba-417f-4b57-b103-27fd25290736
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '2013'
ht-degree: 59%

---


# OSGi の設定{#configuring-osgi}

[OSGi は、Adobe Experience Manager（AEM）の技術スタックにおける基本要素です。AEM の複合バンドルおよびそれらの設定を制御するために使用します。](https://www.osgi.org/)

OSGi は標準化されたプリミティブを提供し、小さく再利用が可能で連携機能に優れたコンポーネントを組み合わせてアプリケーションを構築することを可能にします。これらのコンポーネントからアプリケーションを作成し、デプロイすることができます。**

これにより、 バンドルの管理が容易になり、バンドルを個別に停止、インストール、開始できます。相互依存関係は自動的に処理されます。各OSGiコンポーネント( [OSGi仕様を参照](https://www.osgi.org/Specifications/HomePage))は、様々なバンドルの1つに含まれています。

これらのバンドルの設定は、次のいずれかの方法で管理できます。

* [Adobe CQ Web コンソール](#osgi-configuration-with-the-web-console)を使用
* [設定ファイル](#osgi-configuration-with-configuration-files)を使用
* configuring [content-nodes ( `sling:OsgiConfig`) in the repository](#osgi-configuration-in-the-repository)

いずれの方法も使用できますが、主に[実行モード](/help/sites-deploying/configure-runmodes.md)に関連して、次のようなわずかな違いがあります。

* [Adobe CQ Web コンソール](#osgi-configuration-with-the-web-console)

   * Webコンソールは、OSGi設定用の標準インターフェイスです。様々なプロパティを編集するためのUIが提供されます。このUIでは、あらかじめ定義されたリストから可能な値を選択できます。

      そのため、使い方が簡単です。

   * Web コンソールでおこなわれた設定は、現在のインスタンスにすぐに適用されます。現在の実行モードや、今後の実行モードの変更には関係ありません。

* [設定ファイル](#osgi-configuration-with-configuration-files)

   * Web コンソールで定義される設定を含みます。
   * 他のインスタンスで使用できるよう、コンテンツパッケージに含めることができます。

* [リポジトリ内のコンテンツノード（sling:osgiConfig）](#osgi-configuration-in-the-repository)

   * CRXDE Lite を使用した手動による設定が必要です。
   * ノードの命名規則に従って、設定を特定の `sling:OsgiConfig` 実行モードに関連付けることができます [](/help/sites-deploying/configure-runmodes.md)。 同じリポジトリ内に複数の実行モードの設定を保存することもできます。
   * 適切な設定がすぐに適用されます（実行モードに依存）。

使用するメソッドに関わらず、次のことが可能です。

* リポジトリのコンテンツをコピーまたはレプリケートすることにより、同一の設定を再作成できます。
* セキュリティやさらなる更新のために、FileVault または Subversion に設定をチェックアウトできます。
* パッケージとして保存し、他のインスタンスを設定する際に使用できます。
* スクリプトを使用して設定の詳細を反映させることにより、設定のロールアウトを実行できます。

>[!NOTE]
>
>特定の重要な設定について詳しくは、[、OSGi 設定](/help/sites-deploying/osgi-configuration-settings.md)を参照してください。。

## Web コンソールでの OSGi 設定 {#osgi-configuration-with-the-web-console}

AEM の [Web コンソール](/help/sites-deploying/web-console.md)は、バンドルを設定するための標準化されたインターフェイスを提供します。「**設定**」タブは、OSGi バンドルの設定時に使用します。AEM システムパラメーターを設定するための基盤となるメカニズムです。

おこなった変更は、関連する OSGi 設定にすぐに適用されます。再起動の必要はありません。

>[!NOTE]
>
>Changes made in the web console are saved in the repository as [configuration files](#osgi-configuration-with-configuration-files). このファイルをコンテンツパッケージに含めておき、将来のインストールで再利用することができます。

>[!NOTE]
>
>Web コンソールでは、デフォルト設定に言及している説明はすべて、Sling のデフォルトに関連しています。
>
>Adobe Experience Manager には独自のデフォルト値があり、設定されるデフォルト値は、コンソールに表示される値と異なる場合があります。

Web コンソールで設定を更新するには：

1. 次のいずれかの方法で、Web コンソールの「**設定**」タブにアクセスします。

   * **ツール／運営**&#x200B;メニューのリンクから Web コンソールを開きます。コンソールにログインした後、次のドロップダウンメニューを使用できます。

      **OSGi >**

   * ダイレクトURL;例：

      `http://localhost:4502/system/console/configMgr`
   リストが表示されます。

1. 次のいずれかの方法で、設定するバンドルを選択します。

   * 該当するバンドルの「**編集**」アイコンをクリック
   * 該当するバンドルの&#x200B;**名前**&#x200B;をクリック

1. A dialog will open. Here you can edit as required; for example, set the **Log Level** to `INFO`:

   ![chlimage_1-140](assets/chlimage_1-140.png)

   >[!NOTE]
   >
   >更新内容は、[設定ファイル](#osgi-configuration-with-configuration-files)としてリポジトリ内に保存されます。To locate these afterwards, (e.g. to include in a content package for use on another instance) you should make a note of the persistent identity ( `PID`).

1. 「**保存**」をクリックします。

   変更内容は、関連する OSGi 設定にすぐに適用され、再起動は不要です。

   >[!NOTE]
   >
   >You can now locate the related [configuration file(s)](#osgi-configuration-with-configuration-files); for example, to include in a content package for use on another instance.

## 設定ファイルでの OSGi 設定 {#osgi-configuration-with-configuration-files}

Configuration changes made using the Web Console are persisted in the repository as configuration files ( `.config`) under:

`/apps`

これらの設定ファイルをコンテンツパッケージに含めて、他のインスタンスで再利用することができます。

>[!NOTE]
>
>The format of the configuration files are very specific - see the [Sling Apache documentation](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format) for full details.
>
>そのため、実際の変更は Web コンソールを使用しておこない、設定ファイルが作成、維持されるようにすることをお勧めします。

Web コンソールには、リポジトリのどの場所に変更が保存されたかは表示されませんが、次の手順で簡単に見つけることができます。

1. [Web コンソールで最初の変更をおこなう](#osgi-configuration-with-the-web-console)ことで、設定ファイルを作成します。
1. CRXDE Lite を開きます。
1. **ツール**&#x200B;メニューの「**クエリー**」を選択します。
1. **タイプ**&#x200B;が `SQL` のクエリーを送信して、更新した設定の PID を検索します。

   例えば、**Apache Felix OSGi Management Console** の永続識別子（PID）は次のとおりです。

   `org.apache.felix.webconsole.internal.servlet.OsgiManager`

   よって、SQL クエリーは次のようになります。

   ```shell
   select * from nt:base where jcr:path like '/apps/%' and contains(*, 'org.apache.felix.webconsole.internal.servlet.OsgiManager')
   ```

1. 設定ファイルのノードが表示されます。

   上の例では、次のようになります。

   `/apps/system/config/org.apache.felix.webconsole.internal.servlet.OsgiManager.config`

   >[!CAUTION]
   >
   >このファイルを開くと、変更内容を確認できます。ただし、タイプミスを防ぐために、実際の変更はコンソールでおこなうことをお勧めします。

1. このノードを含むコンテンツパッケージをビルドしておくと、必要に応じて他のインスタンスで使用できます。

## リポジトリでの OSGi 設定 {#osgi-configuration-in-the-repository}

Web コンソールを使用するほかに、リポジトリで設定の詳細を定義することもできます。これにより、様々な実行モードを簡単に設定できます。

これらの設定は、システムが参照できるように、リポジトリ内に `sling:OsgiConfig` ノードを作成することで行われます。 これらのノードはOSGi設定を反映し、それらのノードに対するユーザーインターフェイスを形成します。 設定データを更新するには、ノードのプロパティを更新します。

リポジトリ内の設定データを変更すると、Webコンソールを使用して変更が行われたかのように、該当する検証と整合性チェックを行った上で、変更が関連するOSGi設定に直ちに適用されます。 これは、からに設定をコピーする操作にも当てはま `/libs/` り `/apps/`ます。

同じ設定パラメーターが複数の場所に配置される場合があるので、システムでは次の処理がおこなわれます。

* searches for all nodes of type `sling:OsgiConfig`
* サービス名に従ってフィルター処理
* 実行モードに従ってフィルター処理

>[!NOTE]
>
>[特定のインスタンスのためだけにリポジトリベースの設定を定義する方法](https://helpx.adobe.com/experience-manager/kb/RunModeDependentConfigAndInstall.html)も参照してください。

### リポジトリへの新しい設定の追加 {#adding-a-new-configuration-to-the-repository}

#### 必要な知識 {#what-you-need-to-know}

新しい設定をリポジトリに追加するには、以下を知っておく必要があります。

1. サービスの **永続的なID** (PID)。

   Webコンソールの「 **Configurations** 」フィールドを参照します。 名前は、バンドル名の後ろに括弧で囲まれて表示されます(または、ページの下部にある **設定情報** )。

   例えば、AEM WCM Version Manager `com.day.cq.wcm.core.impl.VersionManagerImpl.` を設定するノードを作成し **ます**。

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. Whether a specific [run mode](/help/sites-deploying/configure-runmodes.md) is required. Create the folder:

   * `config`  — すべての実行モード
   * `config.author`  — 作成者環境用
   * `config.publish`  — 公開環境用
   * `config.<run-mode>`  — 適宜

1. Whether a **Configuration** or **Factory Configuration** is necessary.
1. 設定する個々のパラメータ再作成する必要がある既存のパラメーター定義を含めます。

   Webコンソールの個々のパラメーターフィールドを参照します。 名前は、各パラメーターで括弧で囲まれて表示されます。

   例えば、プロパティを作成します。
   `versionmanager.createVersionOnActivation` 」をクリックして、「アクティベーションでバージョンを **作成**」を設定します。

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. に既に設定が存在しま `/libs`すか？インスタンス内のすべての設定をリストするには、CRXDE Liteの **クエリ** ・ツールを使用して次のSQLクエリを送信します。

   `select * from sling:OsgiConfig`

   その場合は、この設定をにコピーし、新しい場所でカスタマイズす ` /apps/<yourProject>/`ることができます。

#### リポジトリでの設定の作成 {#creating-the-configuration-in-the-repository}

新しい設定をリポジトリに実際に追加するには：

1. CRXDE Lite を使用して次の場所に移動します。

   ` /apps/<yourProject>`

1. If not already existing, create the `config` folder ( `sling:Folder`):

   * `config` - すべての実行モードに該当
   * `config.<run-mode>`  — 特定の実行モードに固有

1. このフォルダーの下に、次の設定でノードを作成します。

   * 型：`sling:OsgiConfig`
   * 名前：永続的なID(PID);

      例えば、AEM WCM Version Managerで `com.day.cq.wcm.core.impl.VersionManagerImpl`
   >[!NOTE]
   >
   >When making a Factory Configuration append `-<identifier>` to the name.
   >
   >例： `org.apache.sling.commons.log.LogManager.factory.config-<identifier>`
   >
   >Where `<identifier>` is replaced by free text that you (must) enter to identify the instance (you cannot omit this information); for example:
   >
   >`org.apache.sling.commons.log.LogManager.factory.config-MINE`

1. 設定するパラメーターごとに、このノードでプロパティを作成します。

   * 名前：Webコンソールに表示されるパラメータ名名前は、フィールドの説明の末尾に括弧で囲まれて表示されます。 例えば、 `Create Version on Activation` `versionmanager.createVersionOnActivation`
   * タイプ：適宜。
   * 値：必要に応じて。

   プロパティを作成する必要があるのは、設定対象のパラメーターのみです。その他は、AEM で設定されているデフォルト値を引き続き使用します。

1. すべての変更を保存します。

   変更は、サービスを再起動することによってノードが更新されるとすぐに適用されます（Web コンソールでおこなった変更と同様）。

>[!CAUTION]
>
>`/libs` パス内の設定は一切変更しないでください。

>[!CAUTION]
>
>起動時に設定を読み込むには、設定のフルパスを正しく指定する必要があります。

## 設定の詳細 {#configuration-details}

### 起動時の優先順位 {#resolution-order-at-startup}

次の優先順位を使用します。

1. Repository nodes under `/apps/*/config...`.either with type `sling:OsgiConfig` or property files.

1. Repository nodes with type `sling:OsgiConfig` under `/libs/*/config...`. （標準定義）

1. の任意の `.config` ファイル `<*cq-installation-dir*>/crx-quickstart/launchpad/config/...`。 ローカルファイルシステム上。

This means that a generic configuration in `/libs` can be masked by a project specific configuration in `/apps`.

### 実行時の優先順位 {#resolution-order-at-runtime}

システム実行中に設定変更をおこなうと、変更後の設定で再読み込みが開始されます。

その後、次の優先順位が適用されます。

1. Web コンソールでの設定変更が、実行時に優先されるので、すぐに有効になります。
1. Modifying a configuration in `/apps` will take immediate effect.
1. Modifying a configuration in `/libs` will take immediate effect, unless it is masked by a configuration in `/apps`.

### 複数の実行モードの解決 {#resolution-of-multiple-run-modes}

実行モードに固有の設定に関しては、複数の実行モードを組み合わせることができます。例えば、設定フォルダーを次のスタイルで作成できます。

`/apps/*/config.<runmode1>.<runmode2>/`

このようなフォルダー内の設定は、起動時に定義されている実行モードにすべての実行モードが一致した場合に適用されます。

For example, if an instance was started with the run modes `author,dev,emea`, configuration nodes in `/apps/*/config.emea`, `/apps/*/config.author.dev/` and `/apps/*/config.author.emea.dev/` will be applied, while configuration nodes in `/apps/*/config.author.asean/` and `/config/author.dev.emea.noldap/` will not be applied.

同じ PID に複数の設定が該当する場合は、一致する実行モードの数が最も大きい設定が適用されます。

For example, if an instance was started with the run modes `author,dev,emea`, and both `/apps/*/config.author/` and `/apps/*/config.emea.author/` define a configuration for
`com.day.cq.wcm.core.impl.VersionManagerImpl`, the configuration in `/apps/*/config.emea.author/` will be applied.

このルールの精度は PID レベルです。You cannot define some properties for the same PID in `/apps/*/config.author/` and more specific ones in `/apps/*/config.emea.author/` for the same PID.
一致する実行モードの数が最も多い設定は、PID全体に対して有効です。

### 標準設定 {#standard-configurations}

以下のリストは、リポジトリで使用できる（標準インストールの）設定の一部を示しています。

* 作成者 — AEM WCMフィルタ：

   `libs/wcm/core/config.author/com.day.cq.wcm.core.WCMRequestFilter`

* 発行 — AEM WCMフィルタ：

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.WCMRequestFilter`

* 発行 — AEM WCMページ統計：

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.stats.PageViewStatistics`

>[!NOTE]
>
>As these configurations reside in `/libs` they must not be edited directly, but copied to your application area ( `/apps`) before customization.

インスタンスに含まれるすべての設定ノードをリストするには、CRXDE Lite の&#x200B;**クエリ**&#x200B;機能を使用して、次の SQL クエリを送信します。

`select * from sling:OsgiConfig`

### 設定の永続性 {#configuration-persistence}

* Webコンソールを使用して設定を変更した場合、（通常は）次の場所にリポジトリに書き込まれます。

   `/apps/{somewhere}`

   * By default `{somewhere}` is `system/config` so the configuration is written to

      `/apps/system/config`

   * ただし、最初にリポジトリの別の場所から来た設定を編集する場合は、次のようにします。例：

      /libs/foo/config/someconfig

      その後、更新された設定が元の場所に書き込まれます。例：

      `/apps/foo/config/someconfig`

* Settings that are changed by `admin` are saved in `*.config` files under:

   ```
      /crx-quickstart/launchpad/config
   ```

   * これは OSGi 設定管理者の非公開データ領域であり、システムへの入力方法にかかわらず、`admin` によって指定された設定の詳細がすべて保持されます。
   * これは実装の詳細であり、このディレクトリをユーザーが直接編集してはいけません。
   * しかし、バックアップや複数インストールのためにコピーを取れるように、これらの設定ファイルの場所を知っておくと便利です。

      * Apache Felix OSGi Management Console

         `../crx/org/apache/felix/webconsole/internal/servlet/OsgiManager.config`

      * CRX Slingクライアントリポジトリ

         `../com/day/crx/sling/client/impl/CRXSlingClientRepository/<pid-nr>.config`

>[!CAUTION]
>
>次の場所にあるフォルダーやファイルは、***決して***&#x200B;編集しないでください。
>
>`/crx-quickstart/launchpad/config`

