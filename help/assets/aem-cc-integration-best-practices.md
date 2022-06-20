---
title: Adobe Creative Cloud ベストプラクティスとの統合
description: ' [!DNL Adobe Experience Manager] と [!DNL Adobe Creative Cloud] を統合してアセット転送ワークフローを効率化し高いコンテンツ速度を実現するためのベストプラクティスです。'
contentOwner: AG
mini-toc-levels: 1
role: User, Admin
feature: Collaboration,Adobe Asset Link,Desktop App
exl-id: c7d589a3-1c5f-4ff0-879e-15e1c556f6dc
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '3280'
ht-degree: 99%

---

# [!DNL Adobe Experience Manager] と [!DNL Creative Cloud] の統合のベストプラクティス {#aem-and-creative-cloud-integration-best-practices}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/aem-cc-integration-best-practices.html?lang=en) |
| AEM 6.5 | この記事 |
| AEM 6.4 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/aem-cc-integration-best-practices.html?lang=en) |

[!DNL Adobe Experience Manager Assets] は、[!DNL Adobe Creative Cloud] と統合できるデジタルアセット管理（DAM）ソリューションで、DAM ユーザーがクリエイティブチームと協力してコンテンツ作成プロセスでのコラボレーションを効率化できるようにサポートします。

[!DNL Adobe Creative Cloud] は、デジタルアセットの作成を支援するソリューションとサービスのエコシステムをクリエイティブチームに提供します。デスクトップアプリケーション、モバイルアプリケーション、デスクトップ同期機能や web エクスペリエンスを備えたストレージなどのクラウドサービスのほか、[!DNL Adobe Stock] などのマーケットプレイスも含まれます。

ユースケースに基づいてデスクトップとエンタープライズクラスの DAM の間で選択すべき統合や、つながるワークフローに関連するベストプラクティスについて、このドキュメントでは説明します。

>[!NOTE]
>
>[!DNL Experience Manager] から [!DNL Creative Cloud] へのフォルダー共有は非推奨で、このガイドでは扱われなくなりました。アドビでは、[Adobe Asset Link](https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link.html) または [Experience Managerデスクトップアプリケーション](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html?lang=ja)などの新しい機能を使用して、[!DNL Experience Manager]で管理されているアセットにクリエイティブユーザーがアクセスできるようにすることを推奨しています。

## クリエイター、マーケター、DAM ユーザーのコラボレーションニーズ {#collaboration-needs-of-creatives-marketers-and-dam-users}

| 要件 | 使用例 | 関係するサーフェス |
|---|---|---|
| デスクトップ上でクリエイティブプロフェッショナル向けのエクスペリエンスを簡素化する | クリエイティブプロフェッショナル（より広い意味では、ネイティブアセット作成アプリケーションで作業しているデスクトップユーザー）向けに、DAM（[!DNL Experience Manager Assets]）で管理されるアセットへのアクセスを効率化します。これらのユーザーには、新しいファイルをアップロードするだけでなく、変更を検出し、使用し（開き）、編集し、[!DNL Experience Manager] に保存するための簡単でわかりやすい方法が必要です。 | Win または Mac のデスクトップ、[!DNL Creative Cloud] アプリケーション |
| すぐに使用できる高品質なアセットを [!DNL Adobe Stock] から提供する | マーケターは、アセットの調達と検出を支援することでコンテンツ作成プロセスの促進に貢献します。クリエイティブプロフェッショナルは、承認されたアセットをクリエイティブツール内から直接使用します。 | [!DNL Experience Manager Assets]、[!DNL Adobe Stock] マーケットプレイス、メタデータフィールド |
| 組織でアセットを配布および共有する | 社内部門／支店および外部のパートナー、ディストリビューター、代理店は、親組織で共有されている承認済みアセットを使用します。組織では、作成したアセットを安全かつシームレスに共有して幅広く再利用したいと考えています。 | Brand Portal、Asset Share Commons |

## コラボレーションニーズをサポートするアドビ製品／サービス {#adobe-offerings-to-support-the-collaboration-need}

| 関係するユーザーに対する価値提案 | アドビ製品／サービス | 関係するサーフェス |
|---|---|---|
| クリエイティブユーザーは、[!DNL Experience Manager] からアセットを見つけ、開いて使用し、編集して変更を [!DNL Experience Manager] にアップロードするほか、[!DNL Creative Cloud] アプリケーションから離れずに、[!DNL Experience Manager] に新しいファイルをアップロードします。 | [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) | [!DNL Adobe Photoshop]、[!DNL Adobe Illustrator] および [!DNL Adobe InDesign] です。 |
| ビジネスユーザーは、アセットのオープンと使用、編集と [!DNL Experience Manager] への変更内容のアップロード、[!DNL Experience Manager] への新しいファイルのアップロードをデスクトップ環境から簡単に行えます。汎用の統合を使用して、アドビ以外のアセットも含め、あらゆるアセットタイプをネイティブデスクトップアプリケーションで開きます。 | [Experience Manager デスクトップアプリ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja) | Windows および Mac デスクトップ上の [!DNL Experience Manager] デスクトップアプリケーション |
| マーケターとビジネスユーザーは、[!DNL Experience Manager] の中から [!DNL Adobe Stock] アセットの検出、プレビュー、ライセンスの取得と保存、管理を行います。ライセンスを取得して保存したアセットは、ガバナンスの強化に役立つ、[!DNL Adobe Stock] の選ばれたメタデータを提供します。 | [Experience Manager と Adobe Stock の統合](aem-assets-adobe-stock.md) | [!DNL Experience Manager] Web インターフェイス |

ここでは、主に、コラボレーションニーズの最初の 2 つの側面に焦点を当てます。アセットの大規模な配布と調達については、使用例として簡単に説明します。そのようなニーズに対するソリューションとしては、Adobe Brand Portal または Asset Share Commons を検討してください。[Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html?lang=ja)、[Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) コンポーネントを基に構築できるソリューション、[リンク共有](/help/assets/link-sharing.md)、[Experience Manager Assets](/help/assets/manage-assets.md) の使用などの代替ソリューションについては、それぞれ固有の要件に基づいた検討が必要です。

![Experience Manager の Creative Cloud 接続、使用する機能の決定](assets/creative-connections-aem.png)

### ユースケースとアドビソリューションの対応関係 {#mapping-of-use-cases-and-adobe-solutions}

<!-- TBD: Add some info about XD integration and possibly info about DA v2.0.
-->

| ユースケース | [!DNL Adobe Asset Link] | [!DNL Experience Manager] デスクトップアプリケーション | 備考／その他のソリューション |
|---|---|---|---|
| 検出 - DAM フォルダーを参照する | 対応 | [!DNL Experience Manager] Web インターフェイスとデスクトップアクション |  |
| 検出 - DAM コレクションにアクセスする | 対応 | [!DNL Experience Manager] Web インターフェイスとデスクトップアクション |  |
| 検出 - DAM からアセットを検索する | 対応 | [!DNL Experience Manager] Web インターフェイスとデスクトップアクション |  |
| 使用 - アセットを開く | はい | はい | [Web インターフェイスから開く](manage-assets.md#previewing-assets)、または Finder から開く |
| 使用 - DAM からドキュメント内にアセットを配置する | 対応 - 埋め込み | 対応 - リンクまたは埋め込み | [!DNL Experience Manager] デスクトップアプリケーションでは、ローカルファイルシステム上のファイルとしてアセットにアクセスできます。ネイティブアプリでは、これらのリンクはローカルパスで表されます。 |
| 編集 - 編集用に開く | 対応 - チェックアウトアクション | 対応 - 「開く」アクション（ネットワーク共有内） | 「[AAL でチェックアウト](https://helpx.adobe.com/jp/enterprise/using/manage-assets-using-adobe-asset-link.html)」の場合は、デフォルトでは、アセットをユーザーの Creative Cloud ストレージアカウント（Creative Cloud アプリで同期）に保存します。 |
| 編集 - DAM の外部で作業を進行中 | 対応 - デスクトップに同期しているユーザーの Creative Cloud ストレージアカウントでアセットが入手可能です。 | 対応 |  |
| 編集 - 変更をアップロードする | 対応 - [チェックインアクション](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)（オプションコメント付き） | 対応 |  |
| アップロード - 単一ファイル | 対応 - 現在のアクティブなドキュメントをアップロードします | 対応 | [Web インターフェイスを使用してアップロード](manage-assets.md#uploading-assets) |
| アップロード - 複数ファイル／階層フォルダー構造 | 非対応 | はい | [Web インターフェイスを使用してアップロード](manage-assets.md#uploading-assets) またはカスタムスクリプティングやツールを使用します。 |
| その他 - ユーザーとログイン | Creative Cloud デスクトップアプリケーションにログインした Creative Cloud ユーザーが認識されます（SSO） | [!DNL Experience Manager] ユーザーと資格情報 | 両方のソリューションのユーザーが [!DNL Experience Manager] ユーザークォータに対してカウントされます。 |
| その他 - ネットワークとアクセス | ネットワークを介してユーザーのデスクトップから [!DNL Experience Manager] デプロイメントにアクセスできる必要があります | ネットワークを介してユーザーのデスクトップから [!DNL Experience Manager] デプロイメントにアクセスできる必要があります | [!DNL Adobe Asset Link] はネットワークプロキシ環境を共有しません。 |
| その他 - 多数のアセットを移行する | いいえ | 不可 | [Assets 移行ガイド](assets-migration-guide.md) |

アセット配布使用例をサポートするには、他のソリューションを考慮に入れる必要があります。

* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) は [!DNL Experience Manager Assets] への設定可能な SaaS アドオンでアセットの公開に使用されます。
* カスタムソリューションは [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) のコードベースに基づいて作成されます。
* [!DNL Experience Manager][ リンク共有](/help/assets/link-sharing.md)はリンクを使用してアドホックでアセットを共有します。
* [Experience Manager Assets web インターフェイス](/help/assets/manage-assets.md)は、[!DNL Experience Manager] アクセス制御のセットアップによって保護された外部関係者用の領域と、必要な IT／ネットワーク設定の調整を備えており、これらの外部ユーザーに [!DNL Experience Manager] へのアクセスを提供します。

## 主な概念と使用例 {#key-concepts-and-use-cases}

### よく使用される用語 {#glossary-of-common-terms}

* **作業中（WIP）またはクリエイティブ WIP：**&#x200B;アセットライフサイクルのフェーズ。アセットに対してまだ複数の変更が行われている最中であり、通常は、より広範なチームと共有するための準備がまだできていない状態。
* **クリエイティブレディアセット**：様々なグループと共有する準備ができている、またはクリエイティブチームによりマーケティングチームや LOB チームとの共有用に選択／承認されている [!DNL Assets]。
* **アセット承認**： 既に DAM にアップロードされているアセットに対して実行される承認プロセス。通常、ブランド承認および法的承認などが含まれます。
* **最終アセット：**&#x200B;すべての承認／メタデータタグ付けが完了し、より広範なチームで使用する準備ができているアセット。このようなアセットは DAM に保存され、すべてのユーザー（またはすべての関係者）が使用できるようになっています。マーケティングチャネルで使用したり、クリエイティブチームがデザインの作成に使用したりできます。
* **アセットの小規模な更新／変更：**&#x200B;デジタルアセットに対する迅速で小規模な変更。多くの場合、リタッチ作業や小規模な編集の要求、アセットレビューまたは承認に対応するために行われます（例えば、再配置、テキストサイズの変更、彩度／明るさや色の調整など）。
* **アセットの大規模な更新／変更：**&#x200B;デジタルアセットに加えられる、大規模な作業が必要な変更。その変更作業は比較的長期にわたる場合もあります。通常は複数の変更が含まれます。アセットは、更新中、複数回保存する必要があります。アセットの大規模な更新により、ほとんどの場合、アセットのステージは WIP になります。
* **DAM：**&#x200B;デジタルアセット管理。このドキュメントでは、特に断りのない限り [!DNL Experience Manager Assets] と同義です。
* **クリエイティブユーザー：** Creative Cloud のアプリケーションとサービスを使用してデジタルアセットを作成するクリエイティブプロフェッショナル。クリエイティブチームに所属し、Creative Cloud を使用するが、デジタルアセットの作成は行わないメンバー（クリエイティブディレクターやクリエイティブチームマネージャーなど）を含む場合もあります。
* **DAM ユーザー：** DAM システムの一般的な利用者。組織によっては、マーケティング分野のユーザーもマーケティング以外の分野のユーザーも含まれます（例えば、事業部門（LOB）ユーザー、ライブラリアン、販売担当者など）。

### [!DNL Experience Manager] と [!DNL Creative Cloud] の統合を使用する場合の考慮事項 {#considerations-when-using-aem-and-creative-cloud-integration}

* [デスクトップアプリケーションのベストプラクティス](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html?lang=ja#best-practices-to-prevent-troubles)を参照
* 詳しくは、[Adobe Stock 統合](aem-assets-adobe-stock.md)を参照
* 詳しくは、[Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) を参照

[!DNL Experience Manager] と [!DNL Creative Cloud] の統合に関するベストプラクティスの概要を説明します。以下のそれぞれの項目の詳細は、このドキュメントで後述されています。

* **Photoshop、InDesign、Illustrator のいずれかで作業しているクリエイティブユーザーの場合**：Adobe Asset Link は、[!DNL Experience Manager] からチェックアウトされたアセットの更新の適切な処理など、最適なユーザーエクスペリエンスを提供します。
* **任意の汎用ファイル形式またはアプリケーションについてデスクトップからアセットへのアクセスを簡素化する場合**：[!DNL Experience Manager] デスクトップアプリケーションを使用します。
* **アセットを DAM に保存する理由とタイミングを理解する：**&#x200B;更新を組織内の広範なチームで利用できるようにする必要があります。
* **共有するアセットの量に注意を払う：**&#x200B;アセットを配布する場合、ガバナンスとセキュリティが最も重要な要素になる可能性があります。Brand Portal のように、大規模なアセット配布を想定したツールの使用を検討してください。
* **アセットのライフサイクルを理解する：**&#x200B;組織内のそれぞれのチームでアセットがどのように処理されるかを理解します。
* **アセットへの頻繁な保存を慎重に処理する：** Adobe Asset Link では、PS、AI、ID を使用して自動的に処理します。他のアプリケーションの場合は、すべての変更が DAM で必要な場合を除き、マップされたフォルダーや共有フォルダーでは WIP 状態のタスクを実行しないでください。

### [!DNL Assets] から [!DNL Adobe Stock] のアセットにアクセスする {#access-to-adobe-stock-assets-from-aem-assets}

[Experience Manager と Adobe Stock の統合](/help/assets/aem-assets-adobe-stock.md)により、[!DNL Experience Manager] ユーザーは [!DNL Adobe Stock] から [!DNL Experience Manager] へのアセットの検索、プレビュー、ライセンス、保存ができるようになりました。ライセンス取得され保存された [!DNL Stock] アセットには、限定された [!DNL Stock] メタデータが付いており、このメタデータを使用してアセットをさらに絞り込むことができます。

この統合に関するいくつかの重要な点を以下に示します。

* Adobe Stock 内のアセットが [!DNL Experience Manager] に保存されると、それらは通常の [!DNL Assets] になり、バイナリが [!DNL Experience Manager] リポジトリに保存されます。[!DNL Adobe Stock] に関係する一部のメタデータが [!DNL Experience Manager] 内のアセットに保存されます。その他の点では、取り込みプロセスは他のあらゆるファイルの場合と同様です。例えば、スマートタグがアクティブな場合、保存時にこれらのアセットにタグが追加されます。
* [!DNL Experience Manager] に保存されたアセットはコピーであり、[!DNL Adobe Stock] へのリンクではありません。

**[!DNL Adobe Stock] から [!DNL Experience Manager] に保存されたアセットを[!DNL Creative Cloud]** で操作します。この統合は [!DNL Adobe Asset Link] とは独立していますが、[!DNL Adobe Asset Link] は [!DNL Stock] からそのように保存されたこれらのアセットを認識し、[!DNL Photoshop]、[!DNL Illustrator] または [!DNL InDesign] の [!DNL Adobe Asset Link] 拡張 UI でこれらのアセットに追加のメタデータと [!DNL Adobe Stock] ロゴを表示するようにします。[!DNL Experience Manager] に保存された時点で通常のアセットであるため、ファイルを閲覧したり開いたりすることができます。
[!DNL Adobe Asset Link] 拡張機能が存在する [!DNL Creative Cloud] アプリケーションで作業するクリエイティブ ユーザーは、[!DNL Adobe Stock] から [!DNL Experience Manager] へすでにライセンスを供与されているアセットにアクセスできるだけでなく、[!DNL Creative Cloud] ライブラリ パネルで [!DNL Adobe Stock] アセットの検索、プレビュー、ライセンスを供与できます。
[!DNL Adobe Stock] からライセンスを取得して [!DNL Experience Manager] に保存した [!DNL Assets] は、[!DNL Experience Manager Assets] デプロイメントにアクセスする幅広いチームで利用できるようになります。一方、[!DNL Creative Cloud] ライブラリパネルを介して [!DNL Adobe Stock] からアセットのライセンスを取得したクリエイターは、デフォルトでは自分たちの [!DNL Creative Cloud] アカウントでのみ利用できるようになっています。

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM introduction article.
-->

## DAM へのアセットの保存について {#about-storing-assets-in-a-dam}

クリエイティブチームとマーケティング／事業部門（LOB）チームの間の効率的なワークフローをデザインし、最適なサポート機能を選択するには、アセットを DAM に保存するタイミングと理由を理解することが重要です。

### アセットを DAM に保存する理由 {#why-assets-are-stored-in-dam}

アセットを DAM に保存すると、アクセスおよび検索がしやすくなります。これにより、組織またはエコシステムの多数のユーザー（パートナー、顧客などを含む）が、アセットを活用できるようになります。

ほとんどの組織は、下流のマーケティング／LOBプロセス（[!DNL Experience Manager Sites] 経由の Web チャネルや、Adobe Experience Cloud が提供する他のチャネル ー Marketing Cloud、Advertising Cloud および Analytics Cloud による測定などのチャネルへの公開、ユーザー／パートナーへの提供など）に関連するアセットのみを保存するように選択しています。また、レビュー／承認プロセスを受ける可能性のあるアセットも DAM に保存します。このように、DAM に保存されるアセットのほとんどは活用される可能性の高いアセットであり、活用の予定がないアセットの保存が防止されます。

また、アセットを保存する場合、技術上およびリソース使用上でも考慮すべき点があります。DAM では、保存されたアセット関連の追加サービスが用意されています（メタデータの抽出、バージョン管理、プレビュー／トランスコーディングの生成、参照の管理およびアクセス制御情報の追加など）。これらのサービスを使用すると、追加の時間リソースおよびインフラストラクチャリソースが消費されます。

多くの場合、アセットおよび更新をすべて保存することは推奨されません。例えば、特定のアセットの更新の質が低く、大量のリソースを消費するような場合、そのアセットは DAM に保存しないようにします。

#### アセットを DAM に保存するタイミング {#when-assets-are-stored-in-dam}

クリエイティブチーム（および組織）は、通常、アセットのライフサイクルのステージごとにアセットを保存しようとは考えません。例えば、以下のような場合、アセットは保存されません。

* アセットがまだ最終決定されていない、またはテストが予定されている場合。
* アセットがクリエイティブ／内部チームのレビューサイクルで不合格になった場合。
* 外部チームへの作業を示すのに、問題のアセットよりも適したアセットがある場合。

通常、以下のクラスのアセットが DAM に保存されます。

* 一定の成熟度に到達し、共有する準備ができたと判断されたアセット。
* クリエイティブチームが事前に選択したアセット。
* マーケティング部門が使用できる、または特定の契約や合意に応じて同部門から要求された、特定の形式のアセット（例えば、RAW ファイルから変換した JPG ファイル、PSD ファイルから作成した TIFF／画像ファイルなど）。

#### アセットの更新を DAM に保存するタイミング {#when-updates-to-assets-are-stored-in-dam}

原則として、より広範な DAM ユーザーに関連するアセットの更新のみを DAM に保存するようにしてください。それにより、（マーケティングおよび類似の部門の）ユーザーの DAM アセットのタイムラインには、関連するバージョンのみが表示されます。

代表的な例としては、アセットのライフサイクルで主要なマイルストーンに関連する変更があります。例えば、最初のマーケティング用アセットや、クリエイティブチームからの要求／レビューに基づいた公式の更新などは、DAM に保存してバージョン管理する必要があります。

DAM の既存アセットに対する変更要求が出された後、マーケティングチームのレビューのためにクリエイティブチームが行った更新も、関連する更新の一例です。この更新は、今後の参考にしたり、以前のバージョンに戻したりするために、DAM に保存してバージョン管理する必要があります。

以下は、通常、関係がないと見なされる更新の例です。

* マーケティングレビューの準備が完了する前に、アセットの最終版以外のバージョンがアップロードされた場合
* アセットの準備ができたとクリエイティブチームおよびマーケティングチームが判断する前に、WIP フェーズのアセットにクリエイティブの変更が頻繁に加えられた場合

### DAM へのユーザーアクセス権 {#user-access-to-dam}

[!DNL Assets] デプロイメントに対するアクセス権に基づいて、[!DNL Assets] では 2 つのタイプのユーザーをサポートしています。通常、エンタープライズネットワーク（ファイアウォール）の内側にいるユーザーは、DAM に直接アクセスできます。エンタープライズネットワークの外側にいるその他のユーザーは、直接アクセスすることはできません。このユーザータイプにより、技術的観点から、どの統合を使用できるかが決定されます。

#### DAM への直接アクセス権を持つクリエイティブユーザー {#creative-users-with-direct-access-to-dam}

通常、社内のクリエイティブチームや、社内ネットワークに接続している委託先やクリエイティブ担当者は、[!DNL Experience Manager] へのログインを含め、DAM デプロイメントへアクセスすることができます。外部の関係者（通常はクライアントのために働く委託先などの信頼できる組織）が、ネットワークを介して（例えば VPN や IP 許可リストを介して） [!DNL Experience Manager] に直接アクセスできるように、[!DNL Experience Manager] とネットワークインフラストラクチャを設定することができます。

その場合、Adobe Asset Link または [!DNL Experience Manager] デスクトップアプリケーションを使用すると、最終アセットや承認済みアセットに簡単にアクセスでき、クリエイティブ対応のアセットを DAM に保存することができます。

#### DAM へのアクセス権を持たないクリエイティブユーザー {#creative-users-without-access-to-dam}

DAM デプロイメントへの直接アクセス権を持たない外部の委託先やフリーランサーも、承認済みアセットにアクセスしたり、新しいデザインを DAM に追加したりする必要が生じることがあります。

次の方法を使用すると、最終アセットや承認済みアセットへのアクセス権を提供できます。

* Asset Link が機能しない場合は、デスクトップアプリケーションを使用します。
* 外部パートナーに安全にアセットを配布するには、[Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) を使用します。
* [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) に基づいた、配布および調達用ポータルのカスタム実装を使用します。
* [!DNL Experience Manager] に設定されたアクセス制御と必要なネットワークインフラストラクチャ（VPN や IP 許可リストなど）を使用して、DAM 内の専用のコンテンツ領域に外部の関係者がアクセスできるようにします。[!DNL Experience Manager] Web UI を使用してアセットを取得したり、新しいコンテンツを DAM にアップロードしたりできます。

#### [!DNL Experience Manager] からのアセットに対する処理中の作業 {#work-in-progress-on-assets-from-aem}

このドキュメントで説明しているように、アセットの大規模な更新（処理中の作業と呼ぶこともあります）を行うときは、ローカルファイルに保存したすべての編集内容を [!DNL Experience Manager] にも変更としてアップロードしないことをお勧めします。これにより、デスクトップユーザーの作業がはかどり、使用されるネットワーク帯域幅が制限され、アセットのタイムラインが適切な状態に保たれ、管理された大規模な更新に集中するようになります。

Adobe Asset Link は、この使用例を適切にサポートしています。

*  [!DNL Photoshop]、[!DNL InDesign]、[!DNL Illustrator] のいずれかでユーザーがファイルを編集しようとすると、指定されたアセットに対してチェックアウト操作が実行されます。
* そのアセットはバックグラウンドでダウンロードされ、Creative Cloud デスクトップアプリによりディスクに同期された Creative Cloud のユーザーアカウントに格納され、アセットに対するチェックアウトフラグが [!DNL Experience Manager] により切り替えられて編集の競合が最小限に抑えられます。
* それ以降、ユーザーは、同期した場所にローカルに保存されているファイルで作業を行い、必要な変更を必要な頻度で継続的に作業し保存することができます。
* さらに、アセットは Creative Cloud アカウントにあるので、ユーザーが所有している他のデバイスでも使用でき（例えば、専用の Creative Cloud モバイルアプリで開いたり編集したりできます）、コラボレーション目的で他の Creative Cloud ユーザーと共有することもできます。
* クリエイティブユーザーが変更を完了すると、使用中の Creative Cloud アプリケーションで、そのファイルに対してチェックイン操作を実行できます。その際に、オプションでコメントを付けることもできます。[!DNL Experience Manager] 内の対応するアセットに新しいバージョンが付けられ、新しいバイナリで更新されます。マーケターや LOB ユーザーなどの [!DNL Experience Manager] ユーザーは、[!DNL Experience Manager] のアセットタイムライン UI を介して、アセットの大幅な変更やマイルストーンにアクセスできます。

[!DNL Experience Manager] デスクトップアプリケーションを使用すると、ネイティブアプリで開かれたアセットをネットワークで共有できます。デフォルトでは、ローカルで行われたすべての変更は、しばらくすると自動的に [!DNL Experience Manager] にアップロードされます。このような設定では、処理中の作業フェーズで頻繁に保存を行うと、すべてが [!DNL Experience Manager] にアップロードされてバージョン管理されるので、不要なバージョンが [!DNL Experience Manager] に生成されるだけでなく、大量のネットワークトラフィックが発生し、スケーラビリティの問題が生じる可能性もあります。

[!DNL Experience Manager] デスクトップアプリケーションのオプションを使用して自動更新をオフにし、アプリのアセットステータス UI でアップロード変更アクションを利用して、アセットへの変更を手動で [!DNL Experience Manager] にアップロードすることをお勧めします。

#### DAM への一括アップロード {#bulk-upload-to-dam}

同時に大量のファイルを DAM にアップロードする必要が生じることもあります。例えば、以下のような場合です。

* 撮影した大量の写真や写真撮影プロジェクトや大規模なプロジェクト
* クリエイティブエージェンシーから提供されたアセットのアップロード
* 大規模なアセットセットから選択したアセットのアップロード（選択が DAM の外部で行われた場合）

この説明は、デスクトップユーザーが日常のワークフローとして、例えば毎週や写真撮影のたびに、運用上ファイルをアップロードすることを指しています。大規模なアセット移行については、ここでは説明しません。

次のアップロード機能を利用できます。

* 大きなフォルダーや階層フォルダーをまとめてアップロードするには、[フォルダーアップロード](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem?lang=ja)機能を提供する [!DNL Experience Manager] デスクトップアプリケーションを使用します。フォルダーの階層構造もアップロードできます。[!DNL Assets] はバックグラウンドでアップロードされるため、web ブラウザーのセッションに拘束されません。
* 1 つのフォルダーからいくつかのファイルをアップロードするには、ファイルを直接 web インターフェイスにドラッグするか、[!DNL Assets] web インターフェイスの「作成」オプションを使用します。
* ビジネス要件に応じて、カスタムアップローダーを使用することもできます。

#### デスクトップから直接実行するデジタルアセット管理 {#managing-digital-assets-directly-from-desktop}

ネットワークファイル共有を使用してデジタルアセットを管理している場合、[!DNL Experience Manager] デスクトップアプリケーションでマップされたネットワーク共有を使用するだけで、より便利になる可能性があります。ネットワークファイル共有から切り替える場合は、ネットワーク共有で可能な機能（検索、収集、メタデータ、コラボレーション、プレビューなど）に勝る豊富なデジタルアセット管理（DAM）機能が [!DNL Experience Manager] web インターフェイスに用意されています。また、[!DNL Experience Manager] デスクトップアプリケーションには、サーバー側の DAM リポジトリとデスクトップの作業を連携させるための便利なリンクもあります。

[!DNL Experience Manager] デスクトップアプリケーションを使用して [!DNL Assets] のネットワーク共有でアセットを直接管理することは避けてください。例えば、[!DNL Experience Manager] デスクトップアプリケーションを使用して複数のファイルを移動またはコピーしないでください。この場合は、[!DNL Assets] インターフェイスを使用して、Finder／エクスプローラーからフォルダーをネットワーク共有にドラッグします。または、[!DNL Assets] のフォルダーアップロード機能を使用します。

#### アセットの移行 {#asset-migration}

既存のシステムから新しいシステムへのアセットの移行や、サーバーに格納されている大量のアセットの移行を計画し実行するには、[移行ガイド](/help/assets/assets-migration-guide.md)を参照してください。[!DNL Experience Manager] デスクトップアプリケーションと [!DNL Experience Manager] から [!DNL Creative Cloud] への統合では、そのような移行をサポートしていません。大量のアセットを取り込む必要があり、メタデータのマッピング、変換および取り込みに関する様々な要件が多数あることから、移行には別のツールとアプローチを採用することをお勧めします。

>[!MORELIKETHIS]
>
>* [Adobeアセットリンク](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)
>* [Experience Manager デスクトップアプリケーションのベストプラクティス](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/archive/best-practices-for-v1.html?lang=ja)
>* [Experience Manager Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html?lang=ja)
>* [Experience Manager と Adobe Stock との連携](aem-assets-adobe-stock.md)

