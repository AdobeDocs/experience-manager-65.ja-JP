---
title: OSGi の設定
seo-title: Configuring OSGi
description: OSGi は、Adobe Experience Manager（AEM）の技術スタックにおける基本要素です。AEM の複合バンドルおよびそれらの設定を制御するために使用します。この記事では、このようなバンドルの設定を管理する方法について詳しく説明します。
seo-description: OSGi is a fundamental element in the technology stack of Adobe Experience Manager (AEM). It is used to control the composite bundles of AEM and their configuration. This article details how you can manage the configuration settings for such bundles.
uuid: b39059a5-dd61-486a-869a-0d7a732c3a47
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: d701e4ba-417f-4b57-b103-27fd25290736
feature: Configuring
exl-id: 5ecd09a3-c4be-4361-9816-03106435346f
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1971'
ht-degree: 96%

---

# OSGi の設定{#configuring-osgi}

[OSGi](https://www.osgi.org/) は、Adobe Experience Manager（AEM）の技術スタックにおける基本要素です。AEM の複合バンドルおよびそれらの設定を制御するために使用します。

OSGi は「*標準化されたプリミティブを提供し、小さく再利用が可能で連携機能に優れたコンポーネントを組み合わせてアプリケーションを構築することを可能にします。これらのコンポーネントからアプリケーションを作成し、デプロイすることができます*」。

これにより、バンドルの管理が容易になり、バンドルの停止、インストール、開始を個別に実行できます。相互依存関係は自動的に処理されます。各 OSGi コンポーネント ( [OSGi の仕様](https://docs.osgi.org/specification/)を参照) は、様々なバンドルの 1 つに含まれています。

これらのバンドルの設定は、次のいずれかの方法で管理できます。

* [Adobe CQ web コンソール](#osgi-configuration-with-the-web-console)を使用
* [設定ファイル](#osgi-configuration-with-configuration-files)を使用
* [リポジトリ内のコンテンツノード（`sling:OsgiConfig`）](#osgi-configuration-in-the-repository)を設定

いずれの方法も使用できますが、主に[実行モード](/help/sites-deploying/configure-runmodes.md)に関連する、次のようなわずかな違いがあります。

* [Adobe CQ Web コンソール](#osgi-configuration-with-the-web-console)

   * Web コンソールは OSGi 設定の標準インターフェイスです。様々なプロパティを編集するための UI が提供されており、事前に定義されているリストから設定可能な値を選択できます。

     そのため、最も簡単に使用できます。

   * Web コンソールで行われた設定は、現在のインスタンスにすぐに適用されます。現在の実行モードや、今後の実行モードの変更には関係ありません。

* [設定ファイル](#osgi-configuration-with-configuration-files)

   * Web コンソールで定義される設定を含みます。
   * 他のインスタンスで使用できるよう、コンテンツパッケージに含めることができます。

* [リポジトリ内のコンテンツノード（sling:osgiConfig）](#osgi-configuration-in-the-repository)

   * CRXDE Lite を使用した手動による設定が必要です。
   * `sling:OsgiConfig` ノードの命名規則により、設定を特定の[実行モード](/help/sites-deploying/configure-runmodes.md)に関連付けることができます。同じリポジトリに複数の実行モードの設定を保存することもできます。
   * 適切な設定がすぐに適用されます（実行モードに依存）。

使用するメソッドに関わらず、次のことが可能です。

* リポジトリのコンテンツをコピーまたはレプリケートすることにより、同一の設定を再作成できます。
* セキュリティまたはその他の更新のために、FileVault または Subversion に設定をチェックアウトできます。
* パッケージとして保存し、他のインスタンスを設定する際に使用できます。
* スクリプトを使用して設定のロールアウトを実行し、設定の詳細を反映できます。

>[!NOTE]
>
>特定の重要な設定について詳しくは、[OSGi 設定の指定](/help/sites-deploying/osgi-configuration-settings.md)を参照してください。

## Web コンソールでの OSGi 設定 {#osgi-configuration-with-the-web-console}

AEM の [web コンソール](/help/sites-deploying/web-console.md)には、バンドルを設定するための標準化されたインターフェイスが搭載されています。「**設定**」タブは、OSGi バンドルの設定に使用します。AEM システムパラメーターを設定するための基盤となるメカニズムです。

行った変更は、関連する OSGi 設定にすぐに適用されます。再起動の必要はありません。

>[!NOTE]
>
>Web コンソールで加えた変更は、[設定ファイル](#osgi-configuration-with-configuration-files)としてリポジトリ内に保存されます。これらのファイルをコンテンツパッケージに含めておき、将来のインストールで再利用することができます。

>[!NOTE]
>
>Web コンソールでは、デフォルト設定に言及している説明はすべて、Sling のデフォルトに関連しています。
>
>Adobe Experience Manager には独自のデフォルト値があり、設定されるデフォルト値は、コンソールに表示される値と異なる場合があります。

Web コンソールで設定を更新するには：

1. 次のいずれかの方法で、web コンソールの「**設定**」タブにアクセスします。

   * **ツール／操作**&#x200B;メニューのリンクから web コンソールを開きます。コンソールにログインしたら、次のドロップダウンメニューを使用できます。

     **OSGi >**

   * ダイレクト URL 例：

     `http://localhost:4502/system/console/configMgr`

   リストが表示されます。

1. 次のいずれかの方法で、設定するバンドルを選択します。

   * 該当するバンドルの「**編集**」アイコンをクリック
   * 該当するバンドルの&#x200B;**名前**&#x200B;をクリック

1. ダイアログボックスが表示されます。必要に応じて、ここで編集できます。 例えば、以下のように&#x200B;**ログレベル**&#x200B;を `INFO` に設定します。

   ![chlimage_1-140](assets/chlimage_1-140.png)

   >[!NOTE]
   >
   >更新内容は、[設定ファイル](#osgi-configuration-with-configuration-files)としてリポジトリ内に保存されます。コンテンツパッケージに含めて別のインスタンスで使用する場合など、後で必要になったときにこれらのファイルを探し出せるように、永続 ID（`PID`）をメモしておく必要があります。

1. 「**保存**」をクリックします。

   変更内容は、実行しているシステムの関連する OSGi 設定にすぐに適用されます。再起動は不要です。

   >[!NOTE]
   >
   >これで、関連する[設定ファイル](#osgi-configuration-with-configuration-files)を探し出せるようになりました。例えば、コンテンツパッケージに含めて別のインスタンスで使用する場合に役立ちます。

## 設定ファイルでの OSGi 設定 {#osgi-configuration-with-configuration-files}

Web コンソールで行った設定変更は、設定ファイル（`.config`）としてリポジトリ内の次の場所に保存されます。

`/apps`

これらの設定ファイルをコンテンツパッケージに含めて、他のインスタンスで再利用することができます。

>[!NOTE]
>
>設定ファイルの形式は固有です。詳しくは、 Sling Apache のドキュメントを参照してください。
>* ～の詳細 [Apache Sling Provisioning Model と Apache SlingStart](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format).
>* のチュートリアルと例 [Sling でのリソースとプロパティの取得](https://sling.apache.org/documentation/tutorials-how-tos/getting-resources-and-properties-in-sling.html).
>
>そのため、実際の変更は web コンソールを使用して行い、設定ファイルが作成、維持されるようにすることをお勧めします。

Web コンソールには、リポジトリのどの場所に変更が保存されたかは表示されませんが、次の手順で簡単に見つけることができます。

1. [Web コンソールで最初の変更を行う](#osgi-configuration-with-the-web-console)ことで、設定ファイルを作成します。
1. CRXDE Lite を開きます。
1. **ツール**&#x200B;メニューの「**クエリ**」を選択します。
1. 更新した設定の PID を検索するには、**タイプ**&#x200B;が `SQL` のクエリを送信します。

   例えば、**Apache Felix OSGi マネージメントコンソール**&#x200B;の永続 ID（PID）は次のとおりです。

   `org.apache.felix.webconsole.internal.servlet.OsgiManager`

   よって、SQL クエリは次のようになります。

   ```shell
   select * from nt:base where jcr:path like '/apps/%' and contains(*, 'org.apache.felix.webconsole.internal.servlet.OsgiManager')
   ```

1. 設定ファイルのノードが表示されます。

   上の例では、次のようになります。

   `/apps/system/config/org.apache.felix.webconsole.internal.servlet.OsgiManager.config`

   >[!CAUTION]
   >
   >このファイルを開くと、変更内容を確認できます。ただし、タイプミスを防ぐために、実際の変更はコンソールで行うことをお勧めします。

1. このノードを含むコンテンツパッケージをビルドしておくと、必要に応じて他のインスタンスで使用できます。

## リポジトリでの OSGi 設定 {#osgi-configuration-in-the-repository}

Web コンソールを使用するほかに、リポジトリで設定の詳細を定義することもできます。これにより、様々な実行モードを簡単に設定できます。

これらの設定は、システムが参照するリポジトリ内の `sling:OsgiConfig` ノードを作成することによって行います。これらのノードは OSGi 設定を反映し、OSGi 設定に対するユーザーインターフェイスが形成されます。設定データを更新するには、ノードのプロパティを更新します。

リポジトリ内の設定データを変更すると、関連する OSGi 設定に変更が直ちに適用されます。この際、web コンソールで変更した場合と同様に、適切な検証と整合性チェックが行われます。このワークフローは、設定を `/libs/` から `/apps/` へコピーするアクションの場合にも適用されます。

同じ設定パラメーターが複数の場所に配置されるので、システムでは次の処理が行われます。

* タイプが `sling:OsgiConfig` のすべてのノードを検索
* サービス名に従ってフィルター処理
* 実行モードに従ってフィルター処理

>[!NOTE]
>
>[特定のインスタンスのためだけにリポジトリベースの設定を定義する方法](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17500.html?lang=ja)も参照してください。

### リポジトリへの新しい設定の追加 {#adding-a-new-configuration-to-the-repository}

#### 必要な知識 {#what-you-need-to-know}

設定をリポジトリに追加するには、以下を知っておく必要があります。

1. サービスの **永続 ID**（PID）。

   Web コンソールの「**設定** 」フィールドを参照します。この名前は、バンドル名の後に括弧でくくって（またはページの下部に向かって&#x200B;**設定情報**&#x200B;に）表示されます。

   例えば、`com.day.cq.wcm.core.impl.VersionManagerImpl.` ノードを作成して、**AEM WCM バージョンマネージャー**&#x200B;を設定します。

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. 特定の[実行モード](/help/sites-deploying/configure-runmodes.md)が必要かどうか。フォルダーを作成：

   * `config` - すべての実行モード用
   * `config.author` - オーサー環境用
   * `config.publish` - パブリッシュ環境用
   * `config.<run-mode>` - 適宜

1. **設定**&#x200B;または&#x200B;**ファクトリ設定**&#x200B;が必要かどうか。
1. 設定する個々のパラメーター。再作成が必要な既存のパラメーター定義を含めます。

   Web コンソールの個々のパラメーターフィールドを参照します。名前は、各パラメーターに対して角括弧で囲まれて表示されます。

   例えば、プロパティを作成します。
   `versionmanager.createVersionOnActivation` で **アクティベーション時にバージョンを作成**&#x200B;を設定します。

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. `/libs` に設定が存在するかどうか。インスタンスに含まれるすべての設定をリストするには、CRXDE Lite の&#x200B;**クエリ**&#x200B;ツールを使用して、次の SQL クエリを送信します。

   `select * from sling:OsgiConfig`

   その場合は、この設定を ` /apps/<yourProject>/` にコピーすると、新しい場所にカスタマイズされます。

#### リポジトリでの設定の作成 {#creating-the-configuration-in-the-repository}

新しい設定をリポジトリに実際に追加するには、次の手順を実行します。

1. CRXDE Lite を使用して次の場所に移動します。

   ` /apps/<yourProject>`

1. 存在しない場合は、`config` フォルダー（`sling:Folder`）を作成します。

   * `config` - すべての実行モードに該当
   * `config.<run-mode>` - 特定の実行モードに固有

1. このフォルダーの下に、次の設定でノードを作成します。

   * タイプ：`sling:OsgiConfig`
   * 名前：永続 ID（PID）

     例えば、AEM WCM Version Manager の場合は `com.day.cq.wcm.core.impl.VersionManagerImpl` を使用します

   >[!NOTE]
   >
   >ファクトリ設定を作成する場合は、`-<identifier>` を名前に付加します。
   >
   >例： `org.apache.sling.commons.log.LogManager.factory.config-<identifier>`
   >
   >`<identifier>` の部分は、インスタンスを識別するフリーテキストに置き換えます（この情報は省略できません）。次に例を示します。
   >
   >`org.apache.sling.commons.log.LogManager.factory.config-MINE`

1. 設定するパラメーターごとに、このノードでプロパティを作成します。

   * 名前：Web コンソールに表示される名前。名前は、フィールドの説明の最後に角括弧で囲んで表示されます。例： `Create Version on Activation` では `versionmanager.createVersionOnActivation` を使用
   * タイプ：適宜。
   * 値：必要に応じて。

   プロパティを作成する必要があるのは、設定対象のパラメーターのみです。その他は、AEM で設定されているデフォルト値を引き続き使用します。

1. すべての変更を保存します。

   変更は、サービスを再起動することによってノードが更新されるとすぐに適用されます（web コンソールで行った変更と同様）。

>[!CAUTION]
>
>`/libs` パス内は一切変更しないでください。

>[!CAUTION]
>
>起動時に設定を読み込むには、設定のフルパスを正しく指定する必要があります。

## 設定の詳細 {#configuration-details}

### 起動時の優先順位 {#resolution-order-at-startup}

次の優先順位が使用されます。

1. `/apps/*/config...` の下のリポジトリノード。タイプ `sling:OsgiConfig` またはプロパティファイル。

1. `/libs/*/config...` の下にある、タイプ `sling:OsgiConfig` のリポジトリノード。（標準定義）

1. `<*cq-installation-dir*>/crx-quickstart/launchpad/config/...` からの任意の `.config` ファイル。ローカルファイルシステム上。

`/libs` 内の汎用設定は、`/apps` 内のプロジェクト固有の設定によってマスクできます。

### 実行時の優先順位 {#resolution-order-at-runtime}

システム実行中に設定変更を行うと、変更後の設定で再読み込みが開始されます。

その後、次の優先順位が適用されます。

1. Web コンソールでの設定変更が、実行時に優先されるので、すぐに有効になります。
1. `/apps` での設定変更がすぐに有効になります。
1. `/apps` で設定によってマスクされない限り、`/libs` での設定変更は直ちに有効になります。

### 複数の実行モードの解決 {#resolution-of-multiple-run-modes}

実行モード固有の設定では、複数の実行モードを組み合わせることができます。例えば、次のスタイルで設定フォルダーを作成できます。

`/apps/*/config.<runmode1>.<runmode2>/`

このようなフォルダー内の設定は、すべての実行モードが起動時に定義されている実行モードと一致した場合に適用されます。

例えば、インスタンスが実行モード `author,dev,emea` で起動された場合は、`/apps/*/config.emea`、`/apps/*/config.author.dev/`、`/apps/*/config.author.emea.dev/` の設定ノードが適用され、`/apps/*/config.author.asean/` と `/config/author.dev.emea.noldap/` の設定ノードは適用されません。

同じ PID に複数の設定が該当する場合は、一致する実行モードの数が最も大きい設定が適用されます。

例えば、インスタンスが実行モード `author,dev,emea` で起動され、`/apps/*/config.author/` と `/apps/*/config.emea.author/` の両方で `com.day.cq.wcm.core.impl.VersionManagerImpl` の設定が定義されている場合は、
`/apps/*/config.emea.author/` の設定が適用されます。

このルールの精度は PID レベルです。
つまり、`/apps/*/config.author/` で同じ PID の一部のプロパティと、`/apps/*/config.emea.author/` で同じ PID のより具体的なプロパティを定義することはできません。
一致する実行モードの数が最も多い設定は、PID 全体で有効です。

### 標準設定 {#standard-configurations}

次のリストは、リポジトリで（標準インストールで）使用できる設定の一部を示しています。

* 作成者 - AEM WCM フィルター：

  `libs/wcm/core/config.author/com.day.cq.wcm.core.WCMRequestFilter`

* 公開 - AEM WCM フィルター：

  `libs/wcm/core/config.publish/com.day.cq.wcm.core.WCMRequestFilter`

* 公開 - AEM WCM ページ統計：

  `libs/wcm/core/config.publish/com.day.cq.wcm.core.stats.PageViewStatistics`

>[!NOTE]
>
>これらの設定は `/libs` 内にあるので、直接編集はせず、アプリケーション領域（`/apps`）にコピーしてからカスタマイズしてください。

インスタンスに含まれるすべての設定ノードをリストするには、CRXDE Lite の&#x200B;**クエリ**&#x200B;機能を使用して、次の SQL クエリを送信します。

`select * from sling:OsgiConfig`

### 設定の永続性 {#configuration-persistence}

* Web コンソールを使用して設定を変更した場合、（通常は）リポジトリの次の場所に書き込まれます。

  `/apps/{somewhere}`

   * デフォルトでは、`{somewhere}` は `system/config` なので、設定は次の場所に書き込まれます。

     `/apps/system/config`

   * ただし、最初にリポジトリ内の別の場所から取得した設定を編集する場合は、次のようにします。例：

     /libs/foo/config/someconfig

     その後、更新された設定が元の場所に書き込まれます。例：

     `/apps/foo/config/someconfig`

* `admin` によって変更された設定は、次の場所の下の `*.config` ファイルに保存されます。

  ```
     /crx-quickstart/launchpad/config
  ```

   * この領域には、OSGi 設定管理者の非公開データがあり、システムへの入力方法に関係なく、`admin` で指定されたすべての設定の詳細が保持されています。
   * この領域は実装の詳細であり、ユーザーがこのディレクトリを直接編集することはできません。
   * ただし、これらの設定ファイルの場所を把握しておくと、バックアップ、複数のインストール、またはその両方を目的としてコピーを作成する際に役立ちます。

      * Apache Felix OSGi Management Console

        `../crx/org/apache/felix/webconsole/internal/servlet/OsgiManager.config`

      * CRX Sling クライアントリポジトリ

        `../com/day/crx/sling/client/impl/CRXSlingClientRepository/<pid-nr>.config`

>[!CAUTION]
>
>次の場所にあるフォルダーやファイルは、決して編集しないでください。
>
>`/crx-quickstart/launchpad/config`
