---
title: Adobe Creative Cloudのベストプラクティスとの統合
description: アセット転送ワークフローを合理化し、高いコンテンツ速度を達成するための [!DNL Adobe Experience Manager] with [!DNL Adobe Creative Cloud] 統合のベストプラクティス。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '3248'
ht-degree: 53%

---


# [!DNL Adobe Experience Manager] および [!DNL Creative Cloud] 統合のベストプラクティス  {#aem-and-creative-cloud-integration-best-practices}

[!DNL Adobe Experience Manager Assets] は、DAMとの統合により、DAMユーザーがクリエイティブチームと連携し、コンテンツ作成プロセス [!DNL Adobe Creative Cloud] でのコラボレーションを効率化できるデジタルアセット管理(DAM)ソリューションです。

[!DNL Adobe Creative Cloud] は、デジタルアセットの作成を支援するソリューションとサービスのエコシステムをクリエイティブチームに提供します。デスクトップおよびモバイルアプリケーション、デスクトップ同期やWebエクスペリエンスとのストレージなどのクラウドサービス、[!DNL Adobe Stock]などのマーケットプレイスが含まれます。

使用例に基づいてデスクトップとエンタープライズクラスの DAM の間で選択すべき統合や、つながるワークフローに関連するベストプラクティスについては、このドキュメントで説明します。

>[!NOTE]
>
>[!DNL Experience Manager] を [!DNL Creative Cloud] フォルダー共有にすることは推奨されなくなり、このガイドでは説明しなくなりました。Adobeでは、[Adobeアセットリンク](https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link.html)や[Experience Managerデスクトップアプリ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html)などの新しい機能を使用して、[!DNL Experience Manager]で管理されるアセットへのアクセスをクリエイティブユーザーに提供することをお勧めします。

## クリエイティブ、マーケター、DAMユーザーのコラボレーションのニーズ{#collaboration-needs-of-creatives-marketers-and-dam-users}

| 要件 | 使用例 | 関係するサーフェス |
|---|---|---|
| デスクトップ上でクリエイティブプロフェッショナル向けのエクスペリエンスを簡素化する | クリエイティブプロフェッショナル、またはより幅広くネイティブのアセット作成アプリケーションで作業するデスクトップユーザーは、DAM([!DNL Experience Manager Assets])からアセットに簡単にアクセスできます。 [!DNL Experience Manager]を見つけ、使用（開く）、編集、保存、新しいファイルのアップロードを行う簡単でシンプルな方法が必要です。 | WinまたはMacデスクトップ。[!DNL Creative Cloud]アプリ |
| [!DNL Adobe Stock]から高品質で使いやすいアセットを提供 | マーケティング担当者は、アセットの調達と検出を支援することでコンテンツ作成プロセスの促進に貢献します。クリエイティブプロフェッショナルは、承認されたアセットをクリエイティブツール内から直接使用します。 | [!DNL Experience Manager Assets]; [!DNL Adobe Stock] marketplace;メタデータフィールド |
| 組織でアセットを配布および共有する | 社内部門／支店および外部のパートナー、ディストリビューター、代理店は、親組織で共有されている承認済みアセットを使用します。組織では、作成したアセットを安全かつシームレスに共有して幅広く再利用したいと考えています。 | Brand Portal、Asset Share Commons |

## コラボレーションニーズをサポートするアドビ製品／サービス {#adobe-offerings-to-support-the-collaboration-need}

| 関係するユーザーに対する価値提案 | アドビ製品／サービス | 関係するサーフェス |
|---|---|---|
| クリエイティブユーザーは、[!DNL Experience Manager]からアセットを検出し、それを開いて使用し、変更を[!DNL Experience Manager]に編集してアップロードするほか、[!DNL Creative Cloud]アプリを閉じることなく、新しいファイルを[!DNL Experience Manager]にアップロードします。 | [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) | [!DNL Adobe Photoshop], [!DNL Adobe Illustrator], および [!DNL Adobe InDesign]. |
| ビジネスユーザーは、アセットの開き方と使用方法を簡単にし、変更を[!DNL Experience Manager]に編集およびアップロードし、デスクトップ環境ーから[!DNL Experience Manager]に新しいファイルをアップロードします。 汎用の統合を使用して、アドビ以外のアセットも含め、あらゆるアセットタイプをネイティブデスクトップアプリケーションで開きます。 | [Experience Managerデスクトップアプリ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | [!DNL Experience Manager]Windows および Mac デスクトップ上の デスクトップアプリケーション |
| マーケティング担当者とビジネスユーザーは、[!DNL Experience Manager]内から[!DNL Adobe Stock]アセットを発見、プレビュー、ライセンスを取得し、保存および管理します。 ライセンス済みおよび保存済みのアセットは、管理を強化するために[!DNL Adobe Stock]メタデータを選択します。 | [Adobe Experience Manager と Adobe Stock との連携](aem-assets-adobe-stock.md) | [!DNL Experience Manager] ウェブインターフェース |

ここでは、主に、コラボレーションニーズの最初の 2 つの側面に焦点を当てます。アセットの大規模な配布と調達については、使用例として簡単に説明します。そのようなニーズに対するソリューションとしては、Adobe Brand Portal または Asset Share Commons を検討してください。[ブランドポータル](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html)、[アセット共有コモンズ](https://adobe-marketing-cloud.github.io/asset-share-commons/)コンポーネント、[リンク共有](/help/assets/link-sharing.md)、[Experience Managerアセット](/help/assets/manage-assets.md)を使用して構築できるソリューションなど、別のソリューションは、特定の要件に基づいて検討する必要があります。

![Experience Manager用のCreative Cloud接続、使用する機能を決定](assets/creative-connections-aem.png)

### 使用例とアドビソリューションの対応関係     {#mapping-of-use-cases-and-adobe-solutions}

<!-- TBD: Add some info about XD integration and possibly info about DA v2.0.
-->

| 使用例 | [!DNL Adobe Asset Link] | [!DNL Experience Manager] デスクトップアプリ | 備考／その他のソリューション |
|---|---|---|---|
| Discover - DAMフォルダーを参照 | 可 | [!DNL Experience Manager] Webインターフェイスとデスクトップアクション |  |
| Discover - DAMコレクションにアクセス | 可 | [!DNL Experience Manager] Webインターフェイスとデスクトップアクション |  |
| Discover - DAMからのアセットの検索 | 可 | [!DNL Experience Manager] Webインターフェイスとデスクトップアクション |  |
| 使用 - アセットを開く | 可 | 可 | 「[Web インターフェイスから開く](manage-assets.md#previewing-assets)」またはファインダーから開く |
| 使用 — DAMからドキュメントにアセットを配置 | 対応 - 埋め込み | 対応 - リンクまたは埋め込み | [!DNL Experience Manager] デスクトップアプリケーションでは、ローカルファイルシステム上のファイルとしてアセットにアクセスできます。ネイティブアプリでは、これらのリンクはローカルパスで表されます。 |
| 編集 - 編集用に開く | 対応 - チェックアウトアクション | 対応 - 「開く」アクション（ネットワーク共有内） | 「[AAL でチェックアウト](https://helpx.adobe.com/jp/enterprise/using/manage-assets-using-adobe-asset-link.html)」の場合は、デフォルトでは、アセットをユーザーの Creative Cloud ストレージアカウント（Creative Cloud アプリで同期）に保存します。 |
| 編集 — DAM外で作業を進めています | 対応 - デスクトップに同期しているユーザーの Creative Cloud ストレージアカウントでアセットが入手可能です。 | 対応 |  |
| 編集 - 変更をアップロードする | 対応 - [チェックインアクション](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)（オプションコメント付き） | 対応 |  |
| アップロード - 単一ファイル | 対応 - 現在のアクティブなドキュメントをアップロードします | 対応 | [Web インターフェイスを使用してアップロード](manage-assets.md#uploading-assets) |
| アップロード - 複数ファイル／階層フォルダー構造 | 非対応 | 可 | [Web インターフェイスを使用してアップロード](manage-assets.md#uploading-assets) またはカスタムスクリプティングやツールを使用します。 |
| その他 - ユーザーとログイン | Creative Cloud デスクトップアプリケーションにログインした Creative Cloud ユーザーが認識されます（SSO） | [!DNL Experience Manager] ユーザーと資格情報 | 両方のソリューションのユーザーは、[!DNL Experience Manager]ユーザーの割り当てにカウントされます。 |
| その他 - ネットワークとアクセス | ネットワーク経由でユーザーのデスクトップから[!DNL Experience Manager]展開にアクセスする必要がある | ネットワーク経由でユーザーのデスクトップから[!DNL Experience Manager]展開にアクセスする必要がある | [!DNL Adobe Asset Link] ネットワークプロキシ環境を共有しません。 |
| その他 - 多数のアセットを移行する | 不可 | 不可 | [アセット移行ガイド](assets-migration-guide.md) |

アセット配布使用例をサポートするには、他のソリューションを考慮に入れる必要があります。

* [Brand ](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) Portalを使用して、アセットを発行するための設定可能なSaaSアドオン [!DNL Experience Manager Assets] を提供します。
* カスタムソリューションは [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) のコードベースに基づいて作成される。
* [!DNL Experience Manager][ リンク共有](/help/assets/link-sharing.md)：リンクを使用してアドホックでアセットを共有する。
* [Experience ManagerアセットWeb](/help/assets/manage-assets.md) インターフェイス。 [!DNL Experience Manager] アクセス制御の設定と必要なIT/ネットワーク構成の調整によって保護される外部のユーザー向けの領域を使用し、外部ユーザーに対するアクセスを提供 [!DNL Experience Manager]します。

## 主な概念と使用例 {#key-concepts-and-use-cases}

### よく使用される用語 {#glossary-of-common-terms}

* **作業中（WIP）またはクリエイティブ WIP：**&#x200B;アセットライフサイクルのフェーズ。アセットに対してまだ複数の変更がおこなわれている最中であり、通常は、より広範なチームと共有するための準備がまだできていない状態。
* **クリエイティブなアセット：様々なチーム** [!DNL Assets] と共有できる状態、またはクリエイティブチームがマーケティングチームやLOBチームと共有するために選択または承認した状態。
* **アセット承認：** 既に DAM にアップロードされているアセットに対して実行される承認プロセス。通常、ブランド承認および法的承認などが含まれます。
* **最終アセット：**&#x200B;すべての                承認／メタデータタグ付けが完了し、より広範なチームに使用される準備ができているアセット。このようなアセットは DAM に保存され、すべてのユーザー（またはすべての関係者）が使用できるようになっています。マーケティングチャネルで使用したり、クリエイティブチームがデザインの作成に使用したりできます。
* **アセットの小規模な更新／変更：**&#x200B;デジタルアセットに対する迅速で小規模な変更。多くの場合、リタッチ作業や小規模な編集の要求、アセットレビューまたは承認に対応するためにおこなわれます（例えば、再配置、テキストサイズの変更、彩度／明るさ、色などの調整）。
* **アセットの大規模な更新／変更：**&#x200B;デジタルアセットに加えられる、大規模な作業が必要な変更。その変更作業は比較的長期にわたる場合もあります。通常は複数の変更が含まれます。アセットは、更新中、複数回保存する必要があります。アセットの大規模な更新により、ほとんどの場合、アセットのステージは WIP になります。
* **DAM：**&#x200B;デジタルアセット管理。このドキュメントでは、特に特に言及がない限り、[!DNL Experience Manager Assets]と同義です。
* **クリエイティブユーザー：** Creative Cloud のアプリケーションとサービスを使用してデジタルアセットを作成するクリエイティブプロフェッショナル。クリエイティブチームに所属し、Creative Cloud を使用するが、デジタルアセットの作成はおこなわないメンバー（クリエイティブディレクターやクリエイティブチームマネージャーなど）を含む場合もあります。
* **DAM ユーザー：** DAM システムの一般的な利用者。組織によっては、マーケティング分野のユーザーもマーケティング以外の分野のユーザーも含まれます（例えば、事業部門（LOB）ユーザー、ライブラリアン、販売担当者など）。

### [!DNL Experience Manager]と[!DNL Creative Cloud]統合{#considerations-when-using-aem-and-creative-cloud-integration}を使用する場合の考慮事項

* [デスクトップアプリのベストプラクティス](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html?lang=en#best-practices-to-prevent-troubles)を参照
* [Adobe Stock統合](aem-assets-adobe-stock.md)を参照
* 「[Adobeアセットリンク](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)」を参照

これは、[!DNL Experience Manager]と[!DNL Creative Cloud]の統合のベストプラクティスの概要です。 以下のそれぞれの項目の詳細は、このドキュメントで後述されています。

* **クリエイティブユーザーは、Photoshop、InDesignまたはIllustratorで作業する場合、** Adobeアセットリンクを使用すると、チェックアウト元のアセットに対する作業中のクリーンな処理など、最高のユーザーエクスペリエンスを実現でき [!DNL Experience Manager]ます。
* **任意の汎用ファイル形式またはアプリケーションで、デスクトップからのアセットへのアクセスを簡略化するため：デスクトップアプリ** を [!DNL Experience Manager] 使用します。
* **DAMにアセットを保存する理由とタイミングを理解します。** 更新を行い、組織内の様々なチームが利用できるようにします。
* **共有するアセットの量に注意を払う：**&#x200B;アセットを配布する場合、ガバナンスとセキュリティが最も重要な要素になる可能性があります。Brand Portal のように、大規模なアセット配布を想定したツールの使用を検討してください。
* **アセットのライフサイクルを理解する：**&#x200B;組織内のそれぞれのチームでアセットがどのように処理されるかを理解します。
* **アセットへの頻繁な保存を慎重に処理する：** Adobe Asset Link では、PS、AI、ID を使用して自動的に処理します。他のアプリケーションの場合は、すべての変更が DAM で必要な場合を除き、マップされたフォルダーや共有フォルダーでは WIP 状態のタスクを実行しないでください。

### [!DNL Assets] {#access-to-adobe-stock-assets-from-aem-assets}から[!DNL Adobe Stock]アセットへのアクセス

[Experience ManagerとAdobe Stockの](/help/assets/aem-assets-adobe-stock.md) 統合により、からにアセットを検索、プレビュー、ライセンス、保存す [!DNL Experience Manager] る機能が [!DNL Adobe Stock] 提供され [!DNL Experience Manager]ます。ライセンスを取得し、保存した[!DNL Stock]アセットで[!DNL Stock]メタデータが選択されました。これは、追加のフィルターで検索するために使用できます。

この統合に関するいくつかの重要な点を以下に示します。

* Adobeストックのアセットが[!DNL Experience Manager]に保存されると、アセットは通常の[!DNL Assets]となり、バイナリは[!DNL Experience Manager]リポジトリに保存されます。 [!DNL Adobe Stock]に関連するメタデータの一部は、[!DNL Experience Manager]内のアセット用に保存されます。それ以外の場合は、取り込み処理は他のファイルと同じように見えます。 例えば、スマートタグがアクティブな場合、保存時にこれらのアセットにタグが追加されます。
* [!DNL Experience Manager]に保存されたアセットはコピーであり、[!DNL Adobe Stock]に戻るリンクではありません。

**からに保存されたアセット [!DNL Adobe Stock] の操作」 [!DNL Experience Manager] を参照してくだ[!DNL Creative Cloud]**&#x200B;さい。この統合は[!DNL Adobe Asset Link]とは独立していますが、[!DNL Adobe Asset Link]は[!DNL Stock]から保存されたこれらのアセットをこのように認識し、[!DNL Photoshop]、[!DNL Illustrator]、または[!DNL InDesign]の[!DNL Adobe Asset Link]拡張機能UIに追加のメタデータと[!DNL Adobe Stock]ロゴを表示します。 ファイルは[!DNL Experience Manager]に保存する際の通常のアセットなので、参照や開くなどに使用できます。
[!DNL Adobe Asset Link]拡張子が存在する[!DNL Creative Cloud]アプリで作業するクリエイティブユーザーは、[!DNL Adobe Stock]から[!DNL Experience Manager]に既にライセンスを取得しているアセットにアクセスできるほか、[!DNL Creative Cloud]ライブラリパネルを使用して[!DNL Adobe Stock]アセットを検索、プレビュー、ライセンスを取得できます。
[!DNL Assets] に [!DNL Adobe Stock] ライセンスされ、に保存さ [!DNL Experience Manager] れたアセットは、 [!DNL Experience Manager Assets] デプロイメントにアクセスする様々なチームが利用できるようになります。一方、 [!DNL Adobe Stock] ライブラリパネル [!DNL Creative Cloud] を [!DNL Creative Cloud] 介したクリエイティブのライセンスアセットは、アカウント内でのみ自分で利用できます。

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM introduction article.
-->

## DAM へのアセットの保存について {#about-storing-assets-in-a-dam}

クリエイティブチームとマーケティング／事業部門（LOB）チームの間の効率的なワークフローをデザインし、最適なサポート機能を選択するには、アセットを DAM に保存するタイミングと理由を理解することが重要です。

### アセットを DAM に保存する理由  {#why-assets-are-stored-in-dam}

アセットを DAM に保存すると、アクセスおよび検索がしやすくなります。これにより、組織またはエコシステムの多数のユーザー（パートナー、顧客などを含む）が、アセットを活用できるようになります。

ほとんどの組織は、下流のマーケティング/LOBプロセスに関連するアセット([!DNL Experience Manager Sites]経由のWebチャネルや、Adobe Experience Cloudが提供する他のチャネル(Marketing Cloud、Advertising Cloud、Analytics Cloudが測定し、ユーザー/パートナーなど)にのみ保存するよう選択します。 また、レビュー／承認プロセスを受ける可能性のあるアセットも DAM に保存します。このように、DAM に保存されるアセットのほとんどは活用される可能性の高いアセットであり、活用の予定がないアセットの保存が防止されます。

また、アセットを保存する場合、技術上およびリソース使用上でも考慮すべき点があります。DAM では、保存されたアセット関連の追加サービスが用意されています（メタデータの抽出、バージョン管理、プレビュー／トランスコーディングの生成、参照の管理およびアクセス制御情報の追加など）。これらのサービスを使用すると、追加の時間リソースおよびインフラストラクチャリソースが消費されます。

多くの場合、アセットおよび更新をすべて保存することは推奨されません。例えば、特定のアセットの更新の質が低く、大量のリソースを消費するような場合、そのアセットは DAM に保存しないようにします。

#### アセットを DAM に保存するタイミング  {#when-assets-are-stored-in-dam}

クリエイティブチーム（および組織）は、通常、アセットのライフサイクルのステージごとにアセットを保存しようとは考えません。例えば、以下のような場合、アセットは保存されません。

* アセットがまだ最終決定されていない、またはテストが予定されている場合。
* アセットがクリエイティブ／内部チームのレビューサイクルで不合格になった場合.
* 問題のアセットに比べ、外部チームへの作業の説明に、より適したアセットがある場合.

通常、以下のクラスのアセットが DAM に保存されます。

* 一定の成熟度に到達し、共有する準備ができたと判断されたアセット。
* クリエイティブチームが事前に選択したアセット.
* 特定の契約または契約に応じて、マーケティングで使用または要求される特定のアセット形式（例えば、RAWファイルから変換されたJPGファイル、TIFF/画像、PSDオリジナルのファイル）。

#### アセットの更新を DAM に保存するタイミング {#when-updates-to-assets-are-stored-in-dam}

原則として、より広範な DAM ユーザーに関連するアセットの更新のみを DAM に保存するようにしてください。それにより、（マーケティングおよび類似の部門の）ユーザーの DAM アセットのタイムラインには、関連するバージョンのみが表示されます。

代表的な例としては、アセットのライフサイクルで主要なマイルストーンに関連する変更があります。例えば、最初のマーケティング用アセットや、クリエイティブチームからの要求／レビューに基づいた公式の更新などは、DAM に保存してバージョン管理する必要があります。

DAM の既存アセットに対する変更要求が出された後、マーケティングチームのレビューのためにクリエイティブチームがおこなった更新も、関連する更新の一例です。この更新は、今後の参考にしたり、以前のバージョンに戻したりするために、DAM に保存してバージョン管理する必要があります。

以下は、通常、関係がないと見なされる更新の例です。

* マーケティングレビューの準備が完了する前に、アセットの最終版以外のバージョンがアップロードされた場合
* アセットの準備ができたとクリエイティブチームおよびマーケティングチームが判断する前に、WIP フェーズのアセットにクリエイティブの変更が頻繁に加えられた場合

### DAM へのユーザーアクセス権 {#user-access-to-dam}

[!DNL Assets] では、 [!DNL Assets] デプロイメントへのアクセスに基づいて2種類のユーザーをサポートしています。通常、エンタープライズネットワーク（ファイアウォール）の内側にいるユーザーは、DAM に直接アクセスできます。エンタープライズネットワークの外側にいるその他のユーザーは、直接アクセスすることはできません。このユーザータイプにより、技術的観点から、どの統合を使用できるかが決定されます。

#### DAM への直接アクセス権を持つクリエイティブユーザー  {#creative-users-with-direct-access-to-dam}

通常、社内ネットワークに接続している社内クリエイティブチームまたはエージェンシー/クリエイティブプロフェッショナルは、[!DNL Experience Manager]ログインを含むDAM展開にアクセスできます。 [!DNL Experience Manager] また、ネットワークインフラストラクチャは、外部パーティ（通常はクライアントで働く機関などの信頼できる組織）への直接アクセスを、VPNやIP許可リストなどを介してネットワーク経由で [!DNL Experience Manager] アクセスできるように設定できます。

このような場合、Adobeアセットリンクまたは[!DNL Experience Manager]デスクトップアプリを使用すると、最終的な/承認済みのアセットに簡単にアクセスでき、クリエイティブに対応したアセットをDAMに保存できます。

#### DAM へのアクセス権を持たないクリエイティブユーザー {#creative-users-without-access-to-dam}

DAMデプロイメントに直接アクセスできない外部のエージェンシーやフリーランサーは、承認されたアセットへのアクセス権が必要な場合や、DAMに新しいデザインを追加する必要がある場合があります。

以下の戦略で最終／承認済みアセットへのアクセスを提供します。

* Asset Link が機能しない場合は、デスクトップアプリケーションを使用します。
* 外部パートナーに安全にアセットを配布するには、[Experience Managerアセットブランドポータル](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html)を使用します
* [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) に基づいた、配布および調達用ポータルのカスタム実装を使用します。
* [!DNL Experience Manager]に設定されたアクセス制御と必要なネットワークインフラストラクチャ(VPNやIP許可リストなど)を使用して、外部パーティにDAMのコンテンツの専用領域へのアクセスを与えます。 ユーザーは[!DNL Experience Manager] Web UIを使用してアセットを取得し、新しいコンテンツをDAMにアップロードできます。

####  内のアセットの更新 [!DNL Experience Manager]{#work-in-progress-on-assets-from-aem}

このドキュメントで説明されているように、進行中の作業と呼ばれるアセットに対して大幅な更新を行うことをお勧めします。ローカルファイルに保存した編集内容はすべて[!DNL Experience Manager]にも変更としてアップロードされません。 これにより、デスクトップユーザーの作業がはかどり、使用されるネットワーク帯域幅が制限され、アセットのタイムラインが適切な状態に保たれ、管理された大規模な更新に集中するようになります。

Adobe Asset Link は、この使用例を適切にサポートしています。

* [!DNL Photoshop]、[!DNL InDesign]、または[!DNL Illustrator]内のユーザーがファイルを編集しようとすると、指定されたアセットに対してチェックアウト操作が実行されます
* アセットはバックグラウンドでダウンロードされ、Creative CloudのデスクトップアプリケーションによってCreative Cloudに同期されたユーザーアカウントに送信され、編集の競合を最小限に抑えるためにアセットの[!DNL Experience Manager]でチェックアウトフラグが切り替えられます
* それ以降、ユーザーは、同期した場所にローカルに保存されているファイルで作業をおこない、必要な変更を必要な頻度で継続的に作業し保存することができます。
* さらに、アセットは Creative Cloud アカウントにあるので、ユーザーが所有している他のデバイスでも使用でき（例えば、専用の Creative Cloud モバイルアプリで開いたり編集したりできます）、コラボレーション目的で他の Creative Cloud ユーザーと共有することもできます。
* クリエイティブユーザーが変更を完了すると、使用中の Creative Cloud アプリケーションで、そのファイルに対してチェックイン操作を実行できます。その際に、オプションでコメントを付けることもできます。[!DNL Experience Manager]内の対応するアセットは、新しいバイナリでバージョン付けされ、に更新されます。 [!DNL Experience Manager]マーケティング担当者や LOB ユーザーなどの ユーザーは、 Assets のタイムライン UI を介して、アセットの大幅な変更やマイルストーンにアクセスできます。[!DNL Experience Manager]

[!DNL Experience Manager] デスクトップアプリケーションは、ネイティブアプリで開かれたアセットのネットワーク共有を提供します。デフォルトでは、ローカルで行われたすべての変更は、しばらくすると自動的に[!DNL Experience Manager]にアップロードされます。 このような設定では、作業中の頻繁な保存はすべて[!DNL Experience Manager]にアップロードされ、[!DNL Experience Manager]の不要なバージョンに言及することなく、ネットワークトラフィックや拡張性に関する課題が多く発生します。

ここで推奨される方法は、[!DNL Experience Manager]デスクトップアプリのオプションを使用して自動更新を無効にし、アプリのアセットステータスUIのアップロードの変更操作を利用して手動で[!DNL Experience Manager]に変更をアップロードすることです。

#### DAM への一括アップロード {#bulk-upload-to-dam}

同時に大量のファイルを DAM にアップロードする必要が生じることもあります。例えば、以下のような場合です。

* 撮影した大量の写真や 写真や大きなプロジェクト
* クリエイティブエージェンシーから提供されたアセットのアップロード
* 大規模なアセットセットから選択したアセットのアップロード（選択が DAM の外部でおこなわれた場合）

説明は、デスクトップユーザーのワークフローの通常の部分として、操作上（毎週、写真撮影時など）にファイルをアップロードすることを指します。 大規模なアセット移行については、ここでは説明しません。

次のアップロード機能を利用できます。

* 大きい/階層のフォルダーを一括してアップロードするには、[フォルダーアップロード](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=en#upload-and-add-new-assets-to-aem)機能を提供する[!DNL Experience Manager]デスクトップアプリを使用します。 フォルダーの階層構造もアップロードできます。[!DNL Assets] がバックグラウンドでアップロードされるので、webブラウザーセッションに関連付けられません
* 1つのフォルダーから数個のファイルをアップロードするには、ファイルを直接Webインターフェイスにドラッグするか、[!DNL Assets] Webインターフェイスの「作成」オプションを使用します。
* ビジネス要件によっては、カスタムアップローダーを使用することもできます。

#### デスクトップからデジタルアセットを直接管理{#managing-digital-assets-directly-from-desktop}

ネットワークファイル共有を使用してデジタルアセットを管理する場合、[!DNL Experience Manager]デスクトップアプリでマッピングされたネットワーク共有を使用するだけで便利です。 [!DNL Experience Manager] Webインターフェイスは、ネットワーク共有(検索、コレクション、メタデータ、コラボレーション、プレビューなど)に対して可能な限り多くのDigital Asset Management機能を提供し、[!DNL Experience Manager]デスクトップアプリは、サーバー側DAMリポジトリをデスクトップ上の作業と接続する便利なリンクです。

[!DNL Experience Manager]デスクトップアプリを使用して[!DNL Assets]のネットワーク共有内でアセットを直接管理するのは避けてください。 例えば、[!DNL Experience Manager]デスクトップアプリを使用して複数のファイルを移動/コピーしないでください。 代わりに、[!DNL Assets]インターフェイスを使用してFinder/Explorerからネットワーク共有にフォルダをドラッグするか、[!DNL Assets]フォルダアップロード機能を使用します。

#### アセットの移行 {#asset-migration}

既存のシステムから新しいシステムへのアセットの移行や、サーバーに格納されている大量のアセットの移行を計画し実行するには、[移行ガイド](/help/assets/assets-migration-guide.md)を参照してください。[!DNL Experience Manager] デスクトップアプリケ [!DNL Experience Manager] ーションと [!DNL Creative Cloud] 統合では、このような移行はサポートされません。大量のアセットを取り込む必要があり、メタデータのマッピング、変換および取り込みに関する様々な要件が多数あることから、移行には別のツールとアプローチを採用することをお勧めします。

>[!MORELIKETHIS]
>
>* [Adobeアセットリンク](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)
>* [Experience Managerデスクトップアプリのベストプラクティス](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [Experience Managerブランドポータル](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
>* [Adobe Experience Manager と Adobe Stock との連携](aem-assets-adobe-stock.md)

