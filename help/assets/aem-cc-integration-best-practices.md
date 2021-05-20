---
title: Adobe Creative Cloudとの統合のベストプラクティス
description: ' [!DNL Adobe Experience Manager] with [!DNL Adobe Creative Cloud] を統合し、アセット転送ワークフローを効率化し、高いコンテンツ速度を実現するためのベストプラクティス。'
contentOwner: AG
role: Business Practitioner, Administrator
feature: コラボレーション，Adobeアセットリンク，デスクトップアプリ
exl-id: c7d589a3-1c5f-4ff0-879e-15e1c556f6dc
source-git-commit: c4cfb709162ca8f8f6e8508516c39542347c6bc4
workflow-type: tm+mt
source-wordcount: '3254'
ht-degree: 54%

---

# [!DNL Adobe Experience Manager] と統合の [!DNL Creative Cloud] ベストプラクティス  {#aem-and-creative-cloud-integration-best-practices}

[!DNL Adobe Experience Manager Assets] は、と統合できるデジタルアセット管理(DAM)ソリューションで [!DNL Adobe Creative Cloud] す。DAMユーザーがクリエイティブチームと連携し、コンテンツ作成プロセスでのコラボレーションを効率化できます。

[!DNL Adobe Creative Cloud] は、デジタルアセットの作成を支援するソリューションとサービスのエコシステムをクリエイティブチームに提供します。デスクトップおよびモバイルアプリケーション、デスクトップ同期やWebエクスペリエンスを備えたストレージなどのクラウドサービス、[!DNL Adobe Stock]などのマーケットプレイスが含まれます。

使用例に基づいてデスクトップとエンタープライズクラスの DAM の間で選択すべき統合や、つながるワークフローに関連するベストプラクティスについては、このドキュメントで説明します。

>[!NOTE]
>
>[!DNL Experience Manager] をフォ [!DNL Creative Cloud] ルダー共有に変更することは廃止され、このガイドでは取り上げません。Adobeでは、[!DNL Experience Manager]で管理されたAdobeへのアクセス権をクリエイティブユーザーに与えるために、[Experience Managerアセットリンク](https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link.html)や[アセットデスクトップアプリケーション](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html)などの新しい機能を使用することをお勧めします。

## クリエイティブ、マーケター、DAMユーザーのコラボレーションニーズ{#collaboration-needs-of-creatives-marketers-and-dam-users}

| 要件 | 使用例 | 関係するサーフェス |
|---|---|---|
| デスクトップ上でクリエイティブプロフェッショナル向けのエクスペリエンスを簡素化する | クリエイティブプロフェッショナル、またはネイティブのアセット作成アプリケーションで作業するデスクトップユーザー向けに、DAM([!DNL Experience Manager Assets])からのアセットへのアクセスを合理化します。 [!DNL Experience Manager]を簡単かつ簡単に検出し、（開く）、編集し、変更をに保存し、新しいファイルをアップロードする方法が必要です。 | WindowsまたはMacデスクトップ[!DNL Creative Cloud]アプリ |
| [!DNL Adobe Stock]から高品質で使いやすいアセットを提供する | マーケティング担当者は、アセットの調達と検出を支援することでコンテンツ作成プロセスの促進に貢献します。クリエイティブプロフェッショナルは、承認されたアセットをクリエイティブツール内から直接使用します。 | [!DNL Experience Manager Assets]; [!DNL Adobe Stock] marketplace;メタデータフィールド |
| 組織でアセットを配布および共有する | 社内部門／支店および外部のパートナー、ディストリビューター、代理店は、親組織で共有されている承認済みアセットを使用します。組織では、作成したアセットを安全かつシームレスに共有して幅広く再利用したいと考えています。 | Brand Portal、Asset Share Commons |

## コラボレーションニーズをサポートするアドビ製品／サービス {#adobe-offerings-to-support-the-collaboration-need}

| 関係するユーザーに対する価値提案 | アドビ製品／サービス | 関係するサーフェス |
|---|---|---|
| クリエイティブユーザーは、[!DNL Experience Manager]からアセットを検出し、開いて使用し、[!DNL Experience Manager]に対する変更を編集してアップロードし、[!DNL Creative Cloud]アプリを残さずに[!DNL Experience Manager]に新しいファイルをアップロードします。 | [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) | .[!DNL Adobe Photoshop]、[!DNL Adobe Illustrator]、[!DNL Adobe InDesign] です。 |
| ビジネスユーザーは、アセットの開封と使用、編集と[!DNL Experience Manager]への変更のアップロード、デスクトップ環境から[!DNL Experience Manager]への新しいファイルのアップロードを簡単におこなえます。 汎用の統合を使用して、アドビ以外のアセットも含め、あらゆるアセットタイプをネイティブデスクトップアプリケーションで開きます。 | [Experience Manager デスクトップアプリ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | [!DNL Experience Manager]Windows および Mac デスクトップ上の デスクトップアプリケーション |
| マーケターとビジネスユーザーは、[!DNL Experience Manager]内から[!DNL Adobe Stock]アセットを検出、プレビュー、ライセンス、保存および管理します。 ライセンスが必要なアセットと保存されたアセットは、ガバナンスを向上させるための[!DNL Adobe Stock]メタデータを提供します。 | [Adobe Experience Manager と Adobe Stock との連携](aem-assets-adobe-stock.md) | [!DNL Experience Manager] webインターフェイス |

ここでは、主に、コラボレーションニーズの最初の 2 つの側面に焦点を当てます。アセットの大規模な配布と調達については、使用例として簡単に説明します。そのようなニーズに対するソリューションとしては、Adobe Brand Portal または Asset Share Commons を検討してください。代替ソリューション([Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html)、[Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)コンポーネントに基づいて構築できるソリューション、[Link Share](/help/assets/link-sharing.md)、[Experience Managerアセット](/help/assets/manage-assets.md)の使用など)については、特定の要件に基づいて検討する必要があります。

![Creative CloudのExperience Manager接続、使用する機能の決定](assets/creative-connections-aem.png)

### 使用例とアドビソリューションの対応関係        {#mapping-of-use-cases-and-adobe-solutions}

<!-- TBD: Add some info about XD integration and possibly info about DA v2.0.
-->

| 使用例 | [!DNL Adobe Asset Link] | [!DNL Experience Manager] デスクトップアプリケーション | 備考／その他のソリューション |
|---|---|---|---|
| 検出 — DAMフォルダーの参照 | 可 | [!DNL Experience Manager] Webインターフェイスとデスクトップアクション |  |
| Discover - DAMコレクションにアクセス | 可 | [!DNL Experience Manager] Webインターフェイスとデスクトップアクション |  |
| 検出 — DAMからアセットを検索 | 可 | [!DNL Experience Manager] Webインターフェイスとデスクトップアクション |  |
| 使用 - アセットを開く | はい | はい | 「[Web インターフェイスから開く](manage-assets.md#previewing-assets)」またはファインダーから開く |
| を使用 — DAMのアセットをドキュメントに配置する | 対応 - 埋め込み | 対応 - リンクまたは埋め込み | [!DNL Experience Manager] デスクトップアプリケーションでは、ローカルファイルシステム上のファイルとしてアセットにアクセスできます。ネイティブアプリでは、これらのリンクはローカルパスで表されます。 |
| 編集 - 編集用に開く | 対応 - チェックアウトアクション | 対応 - 「開く」アクション（ネットワーク共有内） | 「[AAL でチェックアウト](https://helpx.adobe.com/jp/enterprise/using/manage-assets-using-adobe-asset-link.html)」の場合は、デフォルトでは、アセットをユーザーの Creative Cloud ストレージアカウント（Creative Cloud アプリで同期）に保存します。 |
| 編集 — DAM外で作業中 | 対応 - デスクトップに同期しているユーザーの Creative Cloud ストレージアカウントでアセットが入手可能です。 | 対応 |  |
| 編集 - 変更をアップロードする | 対応 - [チェックインアクション](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)（オプションコメント付き） | 対応 |  |
| アップロード - 単一ファイル | 対応 - 現在のアクティブなドキュメントをアップロードします | 対応 | [Web インターフェイスを使用してアップロード](manage-assets.md#uploading-assets) |
| アップロード - 複数ファイル／階層フォルダー構造 | 非対応 | 可 | [Web インターフェイスを使用してアップロード](manage-assets.md#uploading-assets) またはカスタムスクリプティングまたはツールを使用します。 |
| その他 - ユーザーとログイン | Creative Cloud デスクトップアプリケーションにログインした Creative Cloud ユーザーが認識されます（SSO） | [!DNL Experience Manager] ユーザーと資格情報 | 両方のソリューションのユーザーは、[!DNL Experience Manager]ユーザークォータにカウントされます。 |
| その他 - ネットワークとアクセス | ネットワークを介してユーザーのデスクトップから[!DNL Experience Manager]デプロイメントにアクセスする必要がある | ネットワークを介してユーザーのデスクトップから[!DNL Experience Manager]デプロイメントにアクセスする必要がある | [!DNL Adobe Asset Link] はネットワークプロキシ環境を共有しません。 |
| その他 - 多数のアセットを移行する | 不可 | 不可 | [アセット移行ガイド](assets-migration-guide.md) |

アセット配布使用例をサポートするには、他のソリューションを考慮に入れる必要があります。

* [Brand Portalを使](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) 用すれば、に設定可能なSaaSアドオンを使用し [!DNL Experience Manager Assets] て、アセットを公開できます。
* カスタムソリューションは [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) のコードベースに基づいて作成される。
* [!DNL Experience Manager][ リンク共有](/help/assets/link-sharing.md)：リンクを使用してアドホックでアセットを共有する。
* [Experience ManagerAssets Webイン](/help/assets/manage-assets.md) ターフェイス：外部ユーザーがにアクセスできるようにする、アクセス制御の設定によって保護された外部の関係者向けのエリア [!DNL Experience Manager] と、必要なIT/ネットワーク設定の調整機能を備えて [!DNL Experience Manager]います。

## 主な概念と使用例 {#key-concepts-and-use-cases}

### よく使用される用語 {#glossary-of-common-terms}

* **作業中（WIP）またはクリエイティブ WIP：**&#x200B;アセットライフサイクルのフェーズ。アセットに対してまだ複数の変更がおこなわれている最中であり、通常は、より広範なチームと共有するための準備がまだできていない状態。
* **クリエイティブレディアセット：** [!DNL Assets] 様々なチームと共有する準備ができているアセット。または、クリエイティブチームがマーケティングチームやLOBチームとの共有用に選択または承認済みのアセット。
* **アセット承認：** 既に DAM にアップロードされているアセットに対して実行される承認プロセス。通常、ブランド承認および法的承認などが含まれます。
* **最終アセット：**&#x200B;すべての                      承認／メタデータタグ付けが完了し、より広範なチームに使用される準備ができているアセット。このようなアセットは DAM に保存され、すべてのユーザー（またはすべての関係者）が使用できるようになっています。マーケティングチャネルで使用したり、クリエイティブチームがデザインの作成に使用したりできます。
* **アセットの小規模な更新／変更：**&#x200B;デジタルアセットに対する迅速で小規模な変更。多くの場合、リタッチ作業や小規模な編集の要求、アセットレビューまたは承認に対応するためにおこなわれます（例えば、再配置、テキストサイズの変更、彩度／明るさ、色などの調整）。
* **アセットの大規模な更新／変更：**&#x200B;デジタルアセットに加えられる、大規模な作業が必要な変更。その変更作業は比較的長期にわたる場合もあります。通常は複数の変更が含まれます。アセットは、更新中、複数回保存する必要があります。アセットの大規模な更新により、ほとんどの場合、アセットのステージは WIP になります。
* **DAM：**&#x200B;デジタルアセット管理。このドキュメントでは、特に断りのない限り、[!DNL Experience Manager Assets]と同義です。
* **クリエイティブユーザー：** Creative Cloud のアプリケーションとサービスを使用してデジタルアセットを作成するクリエイティブプロフェッショナル。クリエイティブチームに所属し、Creative Cloud を使用するが、デジタルアセットの作成はおこなわないメンバー（クリエイティブディレクターやクリエイティブチームマネージャーなど）を含む場合もあります。
* **DAM ユーザー：** DAM システムの一般的な利用者。組織によっては、マーケティング分野のユーザーもマーケティング以外の分野のユーザーも含まれます（例えば、事業部門（LOB）ユーザー、ライブラリアン、販売担当者など）。

### [!DNL Experience Manager]と[!DNL Creative Cloud]の統合{#considerations-when-using-aem-and-creative-cloud-integration}を使用する際の考慮事項

* [デスクトップアプリケーションのベストプラクティス](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html?lang=en#best-practices-to-prevent-troubles)を参照してください。
* [Adobe Stock統合](aem-assets-adobe-stock.md)を参照
* [Adobeアセットリンク](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)を参照

これは、[!DNL Experience Manager]と[!DNL Creative Cloud]の統合に関するベストプラクティスの概要です。 以下のそれぞれの項目の詳細は、このドキュメントで後述されています。

* **Photoshop、InDesignまたはIllustratorで作業しているクリエイティブユーザーの場合：** Adobeアセットリンクは、からチェックアウトされたアセットの更新の適切な処理など、最適なユーザーエクスペリエンスを提供し [!DNL Experience Manager]ます。
* **任意の汎用ファイル形式またはアプリケーションについてデスクトップからアセットへのアクセスを簡素化する場合：** デスクトップアプリ [!DNL Experience Manager] ケーションを使用します。
* **アセットをDAMに保存する理由とタイミングを理解する：** 更新を組織内の広範なチームで利用できるようにする必要があります。
* **共有するアセットの量に注意を払う：**&#x200B;アセットを配布する場合、ガバナンスとセキュリティが最も重要な要素になる可能性があります。Brand Portal のように、大規模なアセット配布を想定したツールの使用を検討してください。
* **アセットのライフサイクルを理解する：**&#x200B;組織内のそれぞれのチームでアセットがどのように処理されるかを理解します。
* **アセットへの頻繁な保存を慎重に処理する：** Adobe Asset Link では、PS、AI、ID を使用して自動的に処理します。他のアプリケーションの場合は、すべての変更が DAM で必要な場合を除き、マップされたフォルダーや共有フォルダーでは WIP 状態のタスクを実行しないでください。

### [!DNL Assets] {#access-to-adobe-stock-assets-from-aem-assets}からの[!DNL Adobe Stock]アセットへのアクセス

[Experience ManagerとAdobe Stock](/help/assets/aem-assets-adobe-stock.md) の統 [!DNL Experience Manager] 合により、からにアセットを検索、プレビュー、ライセンス、保存で [!DNL Adobe Stock] きま [!DNL Experience Manager]す。ライセンスが付与され、保存された[!DNL Stock]アセットでは、追加のフィルターで検索できる[!DNL Stock]メタデータが選択されています。

この統合に関するいくつかの重要な点を以下に示します。

* Adobe在庫のアセットが[!DNL Experience Manager]に保存されると、通常の[!DNL Assets]になり、バイナリが[!DNL Experience Manager]リポジトリに保存されます。 [!DNL Adobe Stock]に関連するメタデータの一部は、[!DNL Experience Manager]内のアセット用に保存されます。それ以外の場合、取り込みプロセスは他のファイルの場合と同じように見えます。 例えば、スマートタグがアクティブな場合、保存時にこれらのアセットにタグが追加されます。
* [!DNL Experience Manager]に保存されたアセットはコピーであり、[!DNL Adobe Stock]へのリンクではありません。

**からに保存されたアセ [!DNL Adobe Stock] ット [!DNL Experience Manager] の操[!DNL Creative Cloud]**&#x200B;作この統合は[!DNL Adobe Asset Link]とは独立していますが、[!DNL Adobe Asset Link]は[!DNL Stock]から保存されたアセットを認識し、[!DNL Photoshop]、[!DNL Illustrator]または[!DNL InDesign]の[!DNL Adobe Asset Link]拡張機能のUIに、追加のメタデータと[!DNL Adobe Stock]ロゴを表示します。 ファイルは[!DNL Experience Manager]に保存すると通常のアセットになるので、参照や開くなどに使用できます。
拡張子が[!DNL Adobe Asset Link]の[!DNL Creative Cloud]アプリで作業しているクリエイティブユーザーは、[!DNL Adobe Stock]から[!DNL Experience Manager]へのライセンスが既に必要なアセットにアクセスできるほか、 [!DNL Creative Cloud]ライブラリパネルを使用して[!DNL Adobe Stock]アセットの検索、プレビュー、ライセンス取得を行えます。
[!DNL Assets] ライセンス [!DNL Adobe Stock] が付与され、に保存されたの [!DNL Experience Manager] は、デプロイメントにアクセスするより広範なチームが利用できるようになります。一方、ライブラリパネルを介してからのクリエイティブライセンスアセット [!DNL Experience Manager Assets] は、デフォルトでアカウントでのみ利用で [!DNL Adobe Stock]  [!DNL Creative Cloud]  [!DNL Creative Cloud] きます。

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM introduction article.
-->

## DAM へのアセットの保存について {#about-storing-assets-in-a-dam}

クリエイティブチームとマーケティング／事業部門（LOB）チームの間の効率的なワークフローをデザインし、最適なサポート機能を選択するには、アセットを DAM に保存するタイミングと理由を理解することが重要です。

### アセットを DAM に保存する理由  {#why-assets-are-stored-in-dam}

アセットを DAM に保存すると、アクセスおよび検索がしやすくなります。これにより、組織またはエコシステムの多数のユーザー（パートナー、顧客などを含む）が、アセットを活用できるようになります。

ほとんどの組織は、ダウンストリームのマーケティング/LOBプロセスに関連するアセット([!DNL Experience Manager Sites]を介したWebチャネルや、Adobe Experience Cloud(Marketing Cloud、Advertising Cloud、Analytics Cloudが提供し、ユーザーやパートナーに提供するなど)のみを保存します。 また、レビュー／承認プロセスを受ける可能性のあるアセットも DAM に保存します。このように、DAM に保存されるアセットのほとんどは活用される可能性の高いアセットであり、活用の予定がないアセットの保存が防止されます。

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
* 特定の契約または契約に応じて、マーケティングで使用または要求できる特定のアセット形式（例えば、RAWファイルから変換されたJPGファイル、PSDオリジナルのTIFF/画像）。

#### アセットの更新を DAM に保存するタイミング {#when-updates-to-assets-are-stored-in-dam}

原則として、より広範な DAM ユーザーに関連するアセットの更新のみを DAM に保存するようにしてください。それにより、（マーケティングおよび類似の部門の）ユーザーの DAM アセットのタイムラインには、関連するバージョンのみが表示されます。

代表的な例としては、アセットのライフサイクルで主要なマイルストーンに関連する変更があります。例えば、最初のマーケティング用アセットや、クリエイティブチームからの要求／レビューに基づいた公式の更新などは、DAM に保存してバージョン管理する必要があります。

DAM の既存アセットに対する変更要求が出された後、マーケティングチームのレビューのためにクリエイティブチームがおこなった更新も、関連する更新の一例です。この更新は、今後の参考にしたり、以前のバージョンに戻したりするために、DAM に保存してバージョン管理する必要があります。

以下は、通常、関係がないと見なされる更新の例です。

* マーケティングレビューの準備が完了する前に、アセットの最終版以外のバージョンがアップロードされた場合
* アセットの準備ができたとクリエイティブチームおよびマーケティングチームが判断する前に、WIP フェーズのアセットにクリエイティブの変更が頻繁に加えられた場合

### DAM へのユーザーアクセス権 {#user-access-to-dam}

[!DNL Assets] は、デプロイメントへのアクセスに基づいて、2種類のユーザーをサポー [!DNL Assets] トします。通常、エンタープライズネットワーク（ファイアウォール）の内側にいるユーザーは、DAM に直接アクセスできます。エンタープライズネットワークの外側にいるその他のユーザーは、直接アクセスすることはできません。このユーザータイプにより、技術的観点から、どの統合を使用できるかが決定されます。

#### DAM への直接アクセス権を持つクリエイティブユーザー  {#creative-users-with-direct-access-to-dam}

通常、社内ネットワークにオンボーディングされた社内クリエイティブチームやエージェンシー/クリエイティブプロフェッショナルは、[!DNL Experience Manager]ログインを含むDAMデプロイメントへのアクセス権を持ちます。 [!DNL Experience Manager] また、ネットワークインフラストラクチャを設定して、外部の関係者（通常はクライアントで働く代理店などの信頼できる組織）に直接アクセスし、VPNやIP許可リストなどを介し [!DNL Experience Manager] て、ネットワーク経由でアクセスできるようにします。

このような場合、Adobeアセットリンクまたは[!DNL Experience Manager]デスクトップアプリケーションを使用すると、最終/承認済みアセットに簡単にアクセスし、クリエイティブレディアセットをDAMに保存できます。

#### DAM へのアクセス権を持たないクリエイティブユーザー {#creative-users-without-access-to-dam}

DAMデプロイメントに直接アクセスできない外部のエージェンシーやフリーランサーは、承認済みアセットへのアクセスが必要な場合や、新しいデザインをDAMに追加する場合があります。

以下の戦略で最終／承認済みアセットへのアクセスを提供します。

* Asset Link が機能しない場合は、デスクトップアプリケーションを使用します。
* 外部パートナーに安全にExperience Managerを配布するには、[アセットAssets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html)を使用します。
* [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) に基づいた、配布および調達用ポータルのカスタム実装を使用します。
* [!DNL Experience Manager]に設定されたアクセス制御と、必要なネットワークインフラストラクチャ(VPNやIP許可リストなど)を使用して、外部の関係者がDAM内のコンテンツの専用領域にアクセスできるようにします。 [!DNL Experience Manager] Web UIを使用してアセットを取得し、新しいコンテンツをDAMにアップロードできます。

####  内のアセットの更新 [!DNL Experience Manager]{#work-in-progress-on-assets-from-aem}

このドキュメントで説明するように、ローカルファイルに保存したすべての編集内容を変更として[!DNL Experience Manager]にアップロードすることなく、アセット（「作業中」とも呼ばれる）に対して大幅な更新を行うことをお勧めします。 これにより、デスクトップユーザーの作業がはかどり、使用されるネットワーク帯域幅が制限され、アセットのタイムラインが適切な状態に保たれ、管理された大規模な更新に集中するようになります。

Adobe Asset Link は、この使用例を適切にサポートしています。

* [!DNL Photoshop]、[!DNL InDesign]、または[!DNL Illustrator]のユーザーがファイルを編集しようとすると、指定されたアセットに対してチェックアウト操作が実行されます
* アセットはバックグラウンドでダウンロードされ、Creative CloudデスクトップアプリケーションによってCreative Cloudに同期されたユーザーアカウントに入れられ、編集上の競合を最小限に抑えるためにアセットの[!DNL Experience Manager]でチェックアウトフラグが切り替えられます
* それ以降、ユーザーは、同期した場所にローカルに保存されているファイルで作業をおこない、必要な変更を必要な頻度で継続的に作業し保存することができます。
* さらに、アセットは Creative Cloud アカウントにあるので、ユーザーが所有している他のデバイスでも使用でき（例えば、専用の Creative Cloud モバイルアプリで開いたり編集したりできます）、コラボレーション目的で他の Creative Cloud ユーザーと共有することもできます。
* クリエイティブユーザーが変更を完了すると、使用中の Creative Cloud アプリケーションで、そのファイルに対してチェックイン操作を実行できます。その際に、オプションでコメントを付けることもできます。[!DNL Experience Manager]内の対応するアセットは、新しいバイナリでバージョン管理され、に更新されます。 [!DNL Experience Manager]マーケティング担当者や LOB ユーザーなどの ユーザーは、 Assets のタイムライン UI を介して、アセットの大幅な変更やマイルストーンにアクセスできます。[!DNL Experience Manager]

[!DNL Experience Manager] デスクトップアプリケーションは、ネイティブアプリで開かれたアセットのネットワーク共有を提供します。デフォルトでは、ローカルでおこなわれたすべての変更は、しばらくすると自動的に[!DNL Experience Manager]にアップロードされます。 このような設定を使用すると、作業中の段階で頻繁に保存がすべて[!DNL Experience Manager]にアップロードされ、バージョン管理され、ネットワークトラフィックの多くが発生し、[!DNL Experience Manager]の不要なバージョンに限らず、拡張性に関する課題が発生します。

ここで推奨されるアプローチは、[!DNL Experience Manager]デスクトップアプリケーションのオプションを使用して自動更新をオフにし、デスクトップアプリケーションのAsset Status UIのアップロード変更操作を利用して、アセットに対する変更を[!DNL Experience Manager]に手動でアップロードすることです。

#### DAM への一括アップロード {#bulk-upload-to-dam}

同時に大量のファイルを DAM にアップロードする必要が生じることもあります。例えば、以下のような場合です。

* 撮影した大量の写真や 大きなプロジェクトを撮る
* クリエイティブエージェンシーから提供されたアセットのアップロード
* 大規模なアセットセットから選択したアセットのアップロード（選択が DAM の外部でおこなわれた場合）

説明とは、デスクトップユーザーのワークフローの通常の部分として、（例えば、毎週や写真を撮影するたびに）ファイルを操作的にアップロードすることを指します。 大規模なアセット移行については、ここでは説明しません。

次のアップロード機能を利用できます。

* 大きなフォルダーや階層フォルダーを一括でアップロードするには、[フォルダーアップロード](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=en#upload-and-add-new-assets-to-aem)機能を提供する[!DNL Experience Manager]デスクトップアプリケーションを使用します。 フォルダーの階層構造もアップロードできます。[!DNL Assets] はバックグラウンドでアップロードされるので、webブラウザーセッションに結び付けられることはありません
* 1つのフォルダーから少数のファイルをアップロードするには、ファイルを直接Webインターフェイスにドラッグするか、[!DNL Assets] Webインターフェイスの「作成」オプションを使用します。
* ビジネス要件によっては、カスタムアップローダーを使用することもできます。

#### デスクトップから直接デジタルアセットを管理する{#managing-digital-assets-directly-from-desktop}

ネットワークファイル共有を使用してデジタルアセットを管理する場合、[!DNL Experience Manager]デスクトップアプリケーションでマッピングされたネットワーク共有を使用するだけで、便利な方法と見なされます。 [!DNL Experience Manager] Webインターフェイスは、ネットワーク共有（検索、コレクション、メタデータ、コラボレーション、プレビューなど）で可能な限り多くのデジタルアセット管理機能を提供し、[!DNL Experience Manager]デスクトップアプリは、サーバー側DAMリポジトリをデスクトップ上の作業と接続します。

[!DNL Experience Manager]デスクトップアプリケーションを使用して[!DNL Assets]のネットワーク共有で直接アセットを管理することは避けてください。 例えば、[!DNL Experience Manager]デスクトップアプリケーションを使用して複数のファイルを移動/コピーしないでください。 代わりに、[!DNL Assets]インターフェイスを使用して、Finder/Explorerからネットワーク共有にフォルダーをドラッグするか、[!DNL Assets]フォルダーアップロード機能を使用します。

#### アセットの移行 {#asset-migration}

既存のシステムから新しいシステムへのアセットの移行や、サーバーに格納されている大量のアセットの移行を計画し実行するには、[移行ガイド](/help/assets/assets-migration-guide.md)を参照してください。[!DNL Experience Manager] デスクトップアプリケー [!DNL Experience Manager] ションと [!DNL Creative Cloud] 統合では、このような移行はサポートされません。大量のアセットを取り込む必要があり、メタデータのマッピング、変換および取り込みに関する様々な要件が多数あることから、移行には別のツールとアプローチを採用することをお勧めします。

>[!MORELIKETHIS]
>
>* [Adobeアセットリンク](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)
>* [Experience Managerデスクトップアプリケーションのベストプラクティス](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [Experience ManagerBrand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html?lang=ja)
>* [Adobe Experience Manager と Adobe Stock との連携](aem-assets-adobe-stock.md)

