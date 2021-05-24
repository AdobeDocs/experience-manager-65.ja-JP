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
feature: 設定
exl-id: 5ecd09a3-c4be-4361-9816-03106435346f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2014'
ht-degree: 59%

---

# OSGi の設定{#configuring-osgi}

[OSGi は、Adobe Experience Manager（AEM）の技術スタックにおける基本要素です。AEM の複合バンドルおよびそれらの設定を制御するために使用します。](https://www.osgi.org/)

OSGi は標準化されたプリミティブを提供し、小さく再利用が可能で連携機能に優れたコンポーネントを組み合わせてアプリケーションを構築することを可能にします。これらのコンポーネントからアプリケーションを作成し、デプロイすることができます。**

これにより、 バンドルの管理が容易になり、バンドルを個別に停止、インストール、開始できます。相互依存関係は自動的に処理されます。各OSGiコンポーネント（[OSGi仕様](https://www.osgi.org/Specifications/HomePage)を参照）は、様々なバンドルの1つに含まれています。

これらのバンドルの設定は、次のいずれかの方法で管理できます。

* [Adobe CQ Web コンソール](#osgi-configuration-with-the-web-console)を使用
* [設定ファイル](#osgi-configuration-with-configuration-files)を使用
* リポジトリ](#osgi-configuration-in-the-repository)での[content-nodes(`sling:OsgiConfig`)の設定

いずれの方法も使用できますが、主に[実行モード](/help/sites-deploying/configure-runmodes.md)に関連して、次のようなわずかな違いがあります。

* [Adobe CQ Web コンソール](#osgi-configuration-with-the-web-console)

   * Webコンソールは、OSGi設定用の標準インターフェイスです。様々なプロパティを編集するためのUIを提供し、定義済みのリストから使用可能な値を選択できます。

      そのため、最も簡単に使用できます。

   * Web コンソールでおこなわれた設定は、現在のインスタンスにすぐに適用されます。現在の実行モードや、今後の実行モードの変更には関係ありません。

* [設定ファイル](#osgi-configuration-with-configuration-files)

   * Web コンソールで定義される設定を含みます。
   * 他のインスタンスで使用できるよう、コンテンツパッケージに含めることができます。

* [リポジトリ内のコンテンツノード（sling:osgiConfig）](#osgi-configuration-in-the-repository)

   * CRXDE Lite を使用した手動による設定が必要です。
   * `sling:OsgiConfig`ノードの命名規則により、設定を特定の[実行モード](/help/sites-deploying/configure-runmodes.md)に関連付けることができます。 複数の実行モードの設定を同じリポジトリに保存することもできます。
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
>Webコンソールで行われた変更は、[設定ファイル](#osgi-configuration-with-configuration-files)としてリポジトリに保存されます。 このファイルをコンテンツパッケージに含めておき、将来のインストールで再利用することができます。

>[!NOTE]
>
>Web コンソールでは、デフォルト設定に言及している説明はすべて、Sling のデフォルトに関連しています。
>
>Adobe Experience Manager には独自のデフォルト値があり、設定されるデフォルト値は、コンソールに表示される値と異なる場合があります。

Web コンソールで設定を更新するには：

1. 次のいずれかの方法で、Web コンソールの「**設定**」タブにアクセスします。

   * **ツール／運営**&#x200B;メニューのリンクから Web コンソールを開きます。コンソールにログインした後、次のドロップダウンメニューを使用できます。

      **OSGi >**

   * ダイレクトURL例：

      `http://localhost:4502/system/console/configMgr`
   リストが表示されます。

1. 次のいずれかの方法で、設定するバンドルを選択します。

   * 該当するバンドルの「**編集**」アイコンをクリック
   * 該当するバンドルの&#x200B;**名前**&#x200B;をクリック

1. ダイアログが開きます。ここで、必要に応じて編集できます。例えば、**Log Level**&#x200B;を`INFO`に設定します。

   ![chlimage_1-140](assets/chlimage_1-140.png)

   >[!NOTE]
   >
   >更新内容は、[設定ファイル](#osgi-configuration-with-configuration-files)としてリポジトリ内に保存されます。後でこれらを探すには（例えば、別のインスタンスで使用するコンテンツパッケージに含める場合など）、永続的なID( `PID` )をメモしておく必要があります。

1. 「**保存**」をクリックします。

   変更内容は、関連する OSGi 設定にすぐに適用され、再起動は不要です。

   >[!NOTE]
   >
   >これで、関連する[設定ファイル](#osgi-configuration-with-configuration-files)が見つかります。例えば、別のインスタンスで使用するためにコンテンツパッケージに含める場合などです。

## 設定ファイルでの OSGi 設定 {#osgi-configuration-with-configuration-files}

Webコンソールを使用して行った設定の変更は、次の場所に設定ファイル( `.config` )としてリポジトリに保持されます。

`/apps`

これらの設定ファイルをコンテンツパッケージに含めて、他のインスタンスで再利用することができます。

>[!NOTE]
>
>設定ファイルの形式は非常に具体的です。詳しくは、[Sling Apacheのドキュメント](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format)を参照してください。
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

## リポジトリでの OSGi 設定  {#osgi-configuration-in-the-repository}

Web コンソールを使用するほかに、リポジトリで設定の詳細を定義することもできます。これにより、様々な実行モードを簡単に設定できます。

これらの設定は、リポジトリ内に`sling:OsgiConfig`ノードを作成し、システムが参照できるようにすることで行われます。 これらのノードはOSGi設定を反映し、OSGi設定に対するユーザーインターフェイスを形成します。 設定データを更新するには、ノードプロパティを更新します。

リポジトリ内の設定データを変更すると、Webコンソールを使用して変更がおこなわれた場合と同様に、変更は関連するOSGi設定に即座に適用されます。適切な検証と整合性チェックがおこなわれます。 これは、`/libs/`から`/apps/`に設定をコピーするアクションにも当てはまります。

同じ設定パラメーターが複数の場所に配置される場合があるので、システムでは次の処理がおこなわれます。

* `sling:OsgiConfig`型のすべてのノードを検索
* サービス名に従ってフィルター処理
* 実行モードに従ってフィルター処理

>[!NOTE]
>
>[特定のインスタンスのためだけにリポジトリベースの設定を定義する方法](https://helpx.adobe.com/experience-manager/kb/RunModeDependentConfigAndInstall.html)も参照してください。

### リポジトリへの新しい設定の追加  {#adding-a-new-configuration-to-the-repository}

#### 必要な知識 {#what-you-need-to-know}

新しい設定をリポジトリに追加するには、以下を知っておく必要があります。

1. サービスの&#x200B;**永続ID**(PID)。

   Webコンソールの&#x200B;**Configurations**&#x200B;フィールドを参照します。 この名前は、バンドル名の後（またはページの下部にある&#x200B;**設定情報**）に角括弧で囲まれて表示されます。

   例えば、`com.day.cq.wcm.core.impl.VersionManagerImpl.`ノードを作成して、**AEM WCM Version Manager**&#x200B;を設定します。

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. 特定の[実行モード](/help/sites-deploying/configure-runmodes.md)が必要かどうか。フォルダーの作成：

   * `config`  — すべての実行モード
   * `config.author`  — オーサー環境用
   * `config.publish`  — パブリッシュ環境用
   * `config.<run-mode>`  — 適宜

1. **設定**&#x200B;または&#x200B;**ファクトリ設定**&#x200B;が必要かどうか。
1. 設定する個々のパラメーター。再作成が必要な既存のパラメーター定義を含めます。

   Webコンソールの個々のパラメーターフィールドを参照します。 名前は、各パラメーターに対して角括弧で囲まれて表示されます。

   例えば、プロパティを作成するには、
   `versionmanager.createVersionOnActivation` をクリックし **て、「アクティベーション時にバージョンを作成」を設定**&#x200B;します。

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. `/libs`に既に設定が存在しますか？インスタンス内のすべての設定をリストするには、CRXDE Liteの&#x200B;**クエリ**&#x200B;ツールを使用して、次のSQLクエリを送信します。

   `select * from sling:OsgiConfig`

   その場合は、この設定を` /apps/<yourProject>/`にコピーし、新しい場所でカスタマイズできます。

#### リポジトリでの設定の作成 {#creating-the-configuration-in-the-repository}

新しい設定をリポジトリに実際に追加するには：

1. CRXDE Lite を使用して次の場所に移動します。

   ` /apps/<yourProject>`

1. 既存のフォルダーがない場合は、`config`フォルダー(`sling:Folder`)を作成します。

   * `config` - すべての実行モードに該当
   * `config.<run-mode>`  — 特定の実行モードに固有

1. このフォルダーの下に、次の設定でノードを作成します。

   * 型：`sling:OsgiConfig`
   * 名前：永続ID(PID)

      例えば、AEM WCM Version Managerの場合は、`com.day.cq.wcm.core.impl.VersionManagerImpl`を使用します。
   >[!NOTE]
   >
   >ファクトリ設定を作成する場合は、名前に`-<identifier>`を追加します。
   >
   >例：`org.apache.sling.commons.log.LogManager.factory.config-<identifier>`
   >
   >ここで、`<identifier>`は、インスタンスを識別するフリーテキストに置き換えます（この情報は省略できません）。例：
   >
   >`org.apache.sling.commons.log.LogManager.factory.config-MINE`

1. 設定するパラメーターごとに、このノードでプロパティを作成します。

   * 名前：Webコンソールに表示されるパラメーター名名前は、フィールドの説明の最後に括弧で囲んで表示されます。 例えば、`Create Version on Activation`の場合は、`versionmanager.createVersionOnActivation`を使用します。
   * タイプ：適宜。
   * 値：必要に応じて。

   プロパティを作成する必要があるのは、設定対象のパラメーターのみです。その他は、AEM で設定されているデフォルト値を引き続き使用します。

1. すべての変更を保存します。

   変更は、サービスを再起動することによってノードが更新されるとすぐに適用されます（Web コンソールでおこなった変更と同様）。

>[!CAUTION]
>
>`/libs` パス内のものは一切変更しないでください。

>[!CAUTION]
>
>起動時に設定を読み込むには、設定のフルパスを正しく指定する必要があります。

## 設定の詳細 {#configuration-details}

### 起動時の優先順位 {#resolution-order-at-startup}

次の優先順位を使用します。

1. `/apps/*/config...`.の下のリポジトリノードで、型`sling:OsgiConfig`またはプロパティファイルを使用します。

1. `/libs/*/config...`の下にタイプ`sling:OsgiConfig`のリポジトリノード。 （標準定義）

1. `<*cq-installation-dir*>/crx-quickstart/launchpad/config/...`の`.config`ファイル。 ローカル・ファイル・システム上で

つまり、`/libs`の汎用設定は、`/apps`のプロジェクト固有の設定でマスクできます。

### 実行時の優先順位 {#resolution-order-at-runtime}

システム実行中に設定変更をおこなうと、変更後の設定で再読み込みが開始されます。

その後、次の優先順位が適用されます。

1. Web コンソールでの設定変更が、実行時に優先されるので、すぐに有効になります。
1. `/apps`での設定の変更は直ちに有効になります。
1. `/libs`での設定の変更は、`/apps`の設定でマスクされていない限り、すぐに有効になります。

### 複数の実行モードの解決 {#resolution-of-multiple-run-modes}

実行モードに固有の設定に関しては、複数の実行モードを組み合わせることができます。例えば、設定フォルダーを次のスタイルで作成できます。

`/apps/*/config.<runmode1>.<runmode2>/`

このようなフォルダー内の設定は、起動時に定義されている実行モードにすべての実行モードが一致した場合に適用されます。

例えば、実行モード`author,dev,emea`でインスタンスが開始された場合、`/apps/*/config.emea`、`/apps/*/config.author.dev/`、`/apps/*/config.author.emea.dev/`の設定ノードが適用され、`/apps/*/config.author.asean/`および`/config/author.dev.emea.noldap/`の設定ノードは適用されません。

同じ PID に複数の設定が該当する場合は、一致する実行モードの数が最も大きい設定が適用されます。

例えば、インスタンスが実行モード`author,dev,emea`で起動され、`/apps/*/config.author/`と`/apps/*/config.emea.author/`の両方が
`com.day.cq.wcm.core.impl.VersionManagerImpl`の場合、`/apps/*/config.emea.author/`の設定が適用されます。

このルールの精度は PID レベルです。`/apps/*/config.author/`で同じPIDの一部のプロパティと、同じPIDの`/apps/*/config.emea.author/`でより具体的なプロパティを定義することはできません。
一致する実行モードの数が最も多い設定は、PID全体に対して有効です。

### 標準設定 {#standard-configurations}

以下のリストは、リポジトリで使用できる（標準インストールの）設定の一部を示しています。

* 作成者 — AEM WCMフィルター：

   `libs/wcm/core/config.author/com.day.cq.wcm.core.WCMRequestFilter`

* 公開 — AEM WCMフィルター：

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.WCMRequestFilter`

* 公開 — AEM WCMページ統計：

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.stats.PageViewStatistics`

>[!NOTE]
>
>これらの設定は`/libs`内に存在するので、直接編集するのではなく、カスタマイズ前にアプリケーション領域(`/apps`)にコピーする必要があります。

インスタンスに含まれるすべての設定ノードをリストするには、CRXDE Lite の&#x200B;**クエリ**&#x200B;機能を使用して、次の SQL クエリを送信します。

`select * from sling:OsgiConfig`

### 設定の永続性 {#configuration-persistence}

* Webコンソールを使用して設定を変更すると、（通常は）次の場所にリポジトリに書き込まれます。

   `/apps/{somewhere}`

   * デフォルトでは`{somewhere}`は`system/config`なので、設定は

      `/apps/system/config`

   * ただし、最初にリポジトリ内の別の場所から取得した設定を編集する場合は、次の手順を実行します。例：

      /libs/foo/config/someconfig

      その後、元の場所に更新された設定が書き込まれます。例：

      `/apps/foo/config/someconfig`

* `admin`によって変更された設定は、次の場所にある`*.config`ファイルに保存されます。

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
