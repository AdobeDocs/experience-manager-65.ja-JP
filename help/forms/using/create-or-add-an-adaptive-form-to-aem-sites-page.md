---
title: アダプティブフォームを作成するか、AEM Sitesページに追加する
description: アダプティブフォームを容易に作成したり、シームレスにAEM Sitesページに追加したりする方法を学びます。 動的でカスタマイズ可能なフォームを Web サイトに統合し、デジタルエクスペリエンスを最適化して最大限の効果を得るための、順を追った手法とベストプラクティスについて説明します。
Keywords: AEM Forms in sites, AF in Sites editor, af in aem sites, aem sites af, add af to a sites page, af aem sites, af sites, create af in a sites page, adaptive form in aem sites, forms aem sites, add form to a sites page, adaptive forms aem sites, add adaptive forms to aem page, create forms in an aem sites page
feature: Adaptive Forms
exl-id: 1813ccfc-87ce-46fa-a1d5-5edffd91efb0
source-git-commit: 600dcc52829ff2c5e54176bda7631845ef24f986
workflow-type: tm+mt
source-wordcount: '2970'
ht-degree: 2%

---

# アダプティブフォームを作成するか、AEM Sitesページに追加する {#create-or-add-an-adaptive-form-to-aem-sites-page}

<span class="preview"> Adobeでは、最新の拡張可能なデータキャプチャを使用することをお勧めします [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja) 対象： [新しいアダプティブFormsの作成](/help/forms/using/create-an-adaptive-form-core-components.md) または [AEM SitesページへのアダプティブFormsの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). これらのコンポーネントは、アダプティブFormsの作成における大幅な進歩を表し、印象的なユーザーエクスペリエンスを実現します。 この記事では、基盤コンポーネントを使用してアダプティブFormsを作成する古い方法について説明します。 </span>

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | この記事 |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/create-or-add-an-adaptive-form-to-aem-sites-page.html) |

AEM Formsを使用すれば、アダプティブフォームを Web ページにシームレスに組み込むことができます。 これにより、訪問者は、ページを離れることなく、フォームに簡単に入力して送信できます。 これにより、Web サイト上の他の要素とのやり取りを容易に行いながら、フォームを積極的に操作することができます。

AEMページエディターを使用すると、複数のフォームをすばやく作成してAEM Sitesページに追加できます。 AEM Page Editor を使用すると、動的な動作、検証、データ統合、レコードのドキュメントの生成、ビジネスプロセスの自動化など、アダプティブフォームのコンポーネントを活用して、Sites ページ内にシームレスなデータ取得エクスペリエンスを作成できます。 また、バージョン管理、ターゲティング、翻訳、マルチサイトマネージャーなど、AEM Sitesページの様々な機能を使用できます。

AEM FormsにはアダプティブフォームコンテナとアダプティブForms — 埋め込みコンポーネントが用意されています。 アダプティブフォームコンテナを使用して、エクスペリエンスフラグメントまたはAEM Sitesページで新しいフォームを作成できます。アダプティブForms — 埋め込みコンポーネントでは、既存のアダプティブフォームを追加したり、アダプティブFormsエディターを使用して新しいフォームを作成できます。

![サイトページ内のアダプティブフォーム](/help/forms/using/assets/adaptive-form-in-sites-page.png)

## アダプティブフォームコンテナコンポーネントをAEMページエディターまたはエクスペリエンスフラグメントで使用するメリット

AEM Page Editor でアダプティブフォームコンテナを使用すると、動的な動作、検証、データ統合、レコードのドキュメントの生成、ビジネスプロセスの自動化など、アダプティブFormsコンポーネントを活用して、Sites ページ内にシームレスなデータ取得エクスペリエンスを作成できます。 また、バージョン管理、ターゲティング、翻訳、マルチサイトマネージャーなど、AEM Sitesページの様々な機能を使用して、フォームの全体的な作成と管理のエクスペリエンスを強化できます。 次の機能の一部を見てみましょう。

* **バージョン管理：** AEM Sites Pages オファー [堅牢なバージョン管理機能](/help/sites-authoring/working-with-page-versions.md)を使用して、様々なバージョンのフォームを追跡および管理できます。 これにより、必要に応じて以前のバージョンにロールバックする機能を維持しながら、フォームに変更や機能強化を加えることができます。 バージョン管理により、フォームの開発と進化に対する制御された整理されたアプローチが実現します。
* **ターゲティング (Adobe Targetとの統合 ):** AEM Sitesのページのターゲティング機能を使用して、 [様々なオーディエンス向けにフォームエクスペリエンスをパーソナライズする](/help/sites-administering/target.md). ユーザーセグメントとターゲット条件を活用することで、特定のユーザーグループに合わせてフォームのコンテンツ、デザインまたは動作を調整できます。 これにより、パーソナライズされた関連性の高いフォームエクスペリエンスを提供し、エンゲージメント率とコンバージョン率を高めることができます。
* **翻訳：** AEM Sites [翻訳サービスとのシームレスな統合](/help/sites-administering/translation.md)を使用すると、フォームを複数の言語に簡単に翻訳できます。 この機能により、ローカライゼーションプロセスが簡素化され、グローバルな閲覧者がフォームに確実にアクセスできるようになります。 AEM翻訳プロジェクト内で翻訳を効率的に管理できるので、多言語フォームのサポートに必要な時間と労力を削減できます。 翻訳について詳しくは、「考慮事項」の節を参照してください。
* **マルチサイト管理とライブコピー：** AEM Sitesは堅牢 [マルチサイト管理およびライブコピー機能](/help/sites-administering/msm.md)を使用すると、1 つの環境内で複数の web サイトを作成および管理できます。 この機能を使用すると、異なるサイト間でフォームを再利用できるようになり、一貫性を確保し、重複作業を減らすことができます。 一元管理により、複数の Web サイトにわたってフォームの管理と更新を効率的におこなうことができます。
* **テーマ：** AEM Sitesページには、複数の Web ページをまたいで一貫したビジュアルスタイルをデザインし、維持するためのフレームワークが用意されています。 これらは、Web サイトの全体的なルックアンドフィールに貢献する色、フォント、スタイルシート、その他の視覚要素を定義します。 [アダプティブフォームでAEM Sitesページ用に設計されたテーマを使用すると、時間と労力を節約できます](/help/sites-authoring/style-system.md).
* **タグ付け：** AEM Sitesのページでは、次の操作を実行できます。 [ページ、アセットまたは他のコンテンツへのタグやラベルの割り当て](/help/sites-authoring/tags.md). タグは、特定の条件に基づいてコンテンツを分類および整理する方法を提供するキーワードまたはメタデータラベルです。 AEM内のページやアセットなどのコンテンツ項目にタグを 1 つ以上割り当てて、アセットを検索や分類できるようにします。
* **コンテンツのロックとロック解除：** AEM Sitesでユーザーが [ページへのアクセスと変更の制御](/help/sites-authoring/editing-content.md#locking-a-page-locking-a-page) AEM Sites環境内で使用できます。 ページがロックされている場合、他のユーザーによる不正な変更や編集から保護されています。 コンテンツをロックしたユーザーまたは指定された管理者のみが、ロックを解除して変更を許可できます。


## アダプティブフォームをAEM Page Editor に追加するための様々なオプション

次のオプションを使用すると、この機能を最大限に活用できます。

* **[カスタムアダプティブフォームをAEM Sitesページに追加します。](#create-an-adaptive-form-in-sites-editor)** 要件やデザインの好みに合わせてカスタマイズし、新規フォームをゼロから作成します。

* **[エクスペリエンスフラグメントにカスタムアダプティブフォームを追加する：](#create-an-adaptive-form-in-experience-fragment)** AEMエクスペリエンスフラグメントにフォームを追加して、フォームのリーチを拡張し、複数のページやサイトでシームレスに再利用できます。

* **[アダプティブフォームをエクスペリエンスフラグメントに変換する：](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)** AEM Sitesページに追加されたアダプティブフォームをエクスペリエンスフラグメントに変換して、複数のAEM Sitesページでフォームを再利用することができます。

* **承認済みのテンプレートに基づいてフォームを作成し、AEM Sitesページに追加します。** 事前に承認されたテンプレートを活用して、組織のブランディングガイドラインやデザイン標準に合ったフォームをすばやく作成できます。 このオプションは、アダプティブFormsエディターまたはアダプティブForms — 埋め込みコンポーネントで作成されたアダプティブFormsでのみ使用できます。

* **既存のフォームをAEM Sitesページに追加する：** 作成済みのフォームを Web サイトに簡単に統合し、訪問者が直接操作できるようにします。 このオプションは、アダプティブFormsエディターまたはアダプティブForms — 埋め込みコンポーネントで作成されたアダプティブFormsでのみ使用できます。

* **複数のフォームをAEM Sitesページまたはエクスペリエンスフラグメントに追加する：**  複数のフォームをページに追加して、ユーザーの環境設定や要件に基づいて複数のフォームをユーザーに提供します。 新規フォームと既存フォームを組み合わせることができます。

## 検討事項 {#consideration}

* アダプティブフォームコンテナを使用してフォームを作成または追加する場合、フォームはAEM Sites翻訳フローを通じて翻訳およびローカライゼーションされます。 言語ごとに、サイトページと対応するフォームの個別のコピー（言語コピー）が生成され、コンテンツ作成者が親ページのフォームのルールを変更する場合は、フォームのすべての言語コピーで同じ変更を行う必要があります。 アダプティブフォームコンテナでは、AEM Sitesページの様々な機能（バージョン管理、ターゲティング、翻訳、マルチサイトマネージャーなど）を使用できます。

* アダプティブフォームの埋め込みコンポーネントを使用してフォームを作成または追加する場合、そのフォームはAEM Formsの翻訳フローを使用して翻訳およびローカライゼーションされます。 この場合、1 つのフォームが維持され、Sites ページのすべての言語コピーで参照されます。 アダプティブフォーム埋め込みコンポーネントでは、バージョン管理、ターゲティング、翻訳、マルチサイトマネージャーなど、AEM Sitesページの様々な機能にアクセスできません。


## 事前準備 {#before-you-start}

+++  環境でのアダプティブFormsコアコンポーネントの有効化

次の点を確認します。 [アダプティブFormsコアコンポーネントがお使いの環境で有効になっていること](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/quick-setup/enable-headless-adaptive-forms-and-core-components.html?lang=ja).

+++

+++  AEM SitesページおよびエクスペリエンスフラグメントページコンポーネントへのアダプティブFormsクライアントライブラリの追加

アダプティブFormsコンテナコンポーネントの完全な機能を有効にするには、デプロイメントパイプラインを使用して、Customheaderlibs および Customfooterlibs クライアントライブラリをAEM Sitesページに追加します。 ライブラリを追加するには：

1. AEM オーサーインスタンスにログインし、CRX DE を開きます。 ローカルで実行されるオーサーインスタンスのデフォルト URL は次のとおりです。 `http://localhost:4502/crx/de`.

1. を開きます。 `/apps/[your-sites-project]/components/page/customheaderlibs.html` ファイルを開き、次のコードをファイルに追加します。

       &quot;&#39;
       //Customheaderlibs.html
       &lt;sly data-sly-use.clientlib=&quot;core/wcm/components/commons/v1/templates/clientlib.html&quot;>
       &lt;sly data-sly-call=&quot;${clientlib.css @ categories=&amp;#39;core.forms.components.runtime.all&amp;#39;}&quot; />
       &lt;/sly>
       
       &quot;&#39;
   
1. を開きます。 `/apps/[your-sites-project]/components/page/customfooterlibs.html` ファイルを開き、次のコードをファイルに追加します。

       &quot;&#39;
       
       //customfooterlibs.html
       &lt;sly data-sly-use.clientlib=&quot;core/wcm/components/commons/v1/templates/clientlib.html&quot;>
       &lt;sly data-sly-test=&quot;${!wcmmode.edit}&quot; data-sly-call=&quot;${clientlib.js @ categories=&amp;#39;core.forms.components.runtime.all&amp;#39;, async=true}&quot; />
       &lt;/sly>
       &quot;&#39;
   
1. を開きます。 `/apps/[your-sites-project]/components/xfpage/customheaderlibs.html` ファイルを開き、次のコードをファイルに追加します。

       &quot;&#39;
       //Customheaderlibs.html
       &lt;sly data-sly-use.clientlib=&quot;core/wcm/components/commons/v1/templates/clientlib.html&quot;>
       &lt;sly data-sly-call=&quot;${clientlib.css @ categories=&amp;#39;core.forms.components.runtime.all&amp;#39;}&quot; />
       &lt;/sly>
       
       &quot;&#39;
   
1. を開きます。 `/apps/[your-sites-project]/components/customfooterlibs.html` ファイルを開き、次のコードをファイルに追加します。

       &quot;&#39;
       
       //customfooterlibs.html
       &lt;sly data-sly-use.clientlib=&quot;core/wcm/components/commons/v1/templates/clientlib.html&quot;>
       &lt;sly data-sly-test=&quot;${!wcmmode.edit}&quot; data-sly-call=&quot;${clientlib.js @ categories=&amp;#39;core.forms.components.runtime.all&amp;#39;, async=true}&quot; />
       &lt;/sly>
       &quot;&#39;
   
1. 環境内のすべてのオーサーインスタンスとパブリッシュインスタンスで、上記の手順を繰り返します。

+++

+++ アダプティブFormsコンテナの有効化

テンプレートのポリシーで[!UICONTROL アダプティブフォームコンテナ]コンポーネントを有効にするには、次の手順を実行します。

1. AEM Sitesページまたはエクスペリエンスフラグメントを編集用に開きます。 ページを編集用に開くには、ページを選択して「編集」をクリックします。
1. Sites ページまたはエクスペリエンスフラグメントページのテンプレートを開きます。 テンプレートを開くには、 [!UICONTROL ページ情報] ![ページ情報](/help/forms/using/assets/Smock_Properties_18_N.svg) > [!UICONTROL テンプレートを編集]. 対応するテンプレートがテンプレートエディターで開きます。
1. 構造ビューで、 **[!UICONTROL ポリシー]** ![ポリシー](/help/forms/using/assets/Smock_FeedManagement_18_N.svg) アイコンをクリックします。 Adobe Analytics の **[!UICONTROL 許可されたコンポーネント]** リストを表示し、 **[!UICONTROL アダプティブFormsコンテナ]**  の下のチェックボックス **[AEM Archetype プロジェクト名]  — アダプティブフォーム**.
1. 「**[!UICONTROL 完了]**」をクリックします。

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++

## アダプティブフォームの作成 {#create-an-adaptive-form-in-sites-editor-or-experience-fragment}

新しいフォームを最初から作成し、要件やデザインの環境設定に合わせて、AEM Sitesページまたはエクスペリエンスフラグメント内で直接新しいフォームを作成できます。 単一使用フォームの場合は、AEM Sitesページへの直接オーサリングをお勧めします。一方、エクスペリエンスフラグメントは、Web サイトの複数のページで再利用する必要があるフォームに最適です。

* [AEM Sitesページでのフォームの作成](#create-an-adaptive-form-in-sites-editor)
* [エクスペリエンスフラグメント内にフォームを作成する](#create-an-adaptive-form-in-experience-fragment)
* [AEM Sitesページ内のアダプティブフォームをエクスペリエンスフラグメントに変換する](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)

### AEM Sitesページでのフォームの作成 {#create-an-adaptive-form-in-sites-editor}

AEMページエディターのアダプティブフォームコンテナコンポーネントを使用して、カスタムフォームを作成できます。 このコンポーネントを使用すると、フォームコンポーネントをドラッグ&amp;ドロップしてフォームを作成できます。 フォームコンポーネントは、コアコンポーネントに基づいています。 これらは、組織の要件に応じて簡単にカスタマイズできます。

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

Sites ページでアダプティブフォームを作成するには：

1. AEM Sites ページを編集モードで開きます。
1. 次をドラッグ&amp;ドロップ： **[!UICONTROL アダプティブFormsコンテナ]** コンポーネントをコンポーネントブラウザーからサイトページに移動します。 ページ上にフォーム用のスペースが作成されます。 レイアウトモードを使用して、コンテナスペースのサイズを変更できます。
1. アダプティブフォームのコアコンポーネントをコンテナスペースにドラッグ&amp;ドロップしてフォームを作成します。
1. 「送信」ボタンを追加します。

次に、 [送信アクションの設定](#configure-submit-action-for-form) および詳細プロパティ。

### エクスペリエンスフラグメント内にフォームを作成する {#create-an-adaptive-form-in-experience-fragment}

フォームをAEMエクスペリエンスフラグメントに追加することで、フォームのリーチを拡大して、複数のページやサイトでシームレスに再利用できます。 例えば、エクスペリエンスフラグメント内にニュースレターのサインアップフォームを含めることができます。 これにより、Web サイトの複数のページでフラグメントを簡単に再利用できるので、フォームを繰り返し再作成する必要がなくなります。 エクスペリエンスフラグメント内のニュースレターサインアップフォームに加えた更新や変更は、そのニュースレターを利用するすべてのページに自動的に反映されます。 これにより、プロセスが合理化され、シームレスなユーザーエクスペリエンスを確保しながら、Web サイトのフォームの管理をシンプル化します。

エクスペリエンスフラグメント内にアダプティブフォームを作成するには：

1. エクスペリエンスフラグメントを開きます。
1. 次をドラッグ&amp;ドロップ： **[!UICONTROL アダプティブFormsコンテナ]** コンポーネントをコンポーネントブラウザーからエクスペリエンスフラグメントにドラッグします。
1. アダプティブフォームのコアコンポーネントをエクスペリエンスフラグメントのコンテナスペースにドラッグ&amp;ドロップして、フォームを作成します。
1. 「送信」ボタンを追加します。

次に、 [送信アクションの設定](#configure-submit-action-for-form) および詳細プロパティ。

### AEM Sitesページ内のアダプティブフォームをエクスペリエンスフラグメントに変換する {#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment}

複数のページまたはサイトでフォームを再利用するには、 Sites ページエディター内の既存のアダプティブフォームをエクスペリエンスフラグメントに変換します。

アダプティブフォームをAEM Sitesページからエクスペリエンスフラグメントに変換するには：

1. アダプティブフォームを含むAEM Sitesページを ( アダプティブFormsコンテナコンポーネントで ) 編集モードで開きます。
1. コンテンツツリーを開き、 **[!UICONTROL アダプティブFormsコンテナ]** アダプティブフォームをホストする 1 つのAEM Sitesページで複数のアダプティブFormsをホストできます。 したがって、適切なアダプティブFormsコンテナを慎重に選択してください。
1. メニューバーで、 ![エクスペリエンスフラグメントバリエーションに変換アイコン](/help/forms/using/assets/Smock_FilingCabinet_18_N.svg) エクスペリエンスフラグメントバリエーションに変換アイコン。
   ![Sites ページ内のフォームをエクスペリエンスフラグメントに変換する](/help/forms/using/assets/convert-form-in-sites-page-to-an-experience-fragment.png)

   アダプティブフォームコンテナを新しいエクスペリエンスフラグメントに変換するか、既存のエクスペリエンスフラグメントに追加するためのダイアログボックスが表示されます
1. エクスペリエンスフラグメントバリエーションに変換ダイアログボックスで、次のオプションの値を設定します。

   * **アクション：** 新しいエクスペリエンスフラグメントを作成する場合は「 」を選択し、既存のエクスペリエンスフラグメントに追加する場合は「 」を選択します。
   * **親パス：** エクスペリエンスフラグメントをホストするフォルダーのパスを指定します。 このオプションは、新しいエクスペリエンスフラグメントを作成する場合にのみ使用できます。
   * **テンプレート：** エクスペリエンスフラグメントテンプレートのパスを指定します。 エクスペリエンスフラグメントテンプレートがない場合は、 [作成する](/help/sites-developing/experience-fragments.md). このオプションは、既存のエクスペリエンスフラグメントにアダプティブフォームを追加する場合にのみ使用できます。
   * **フラグメントのタイトル：** エクスペリエンスフラグメントのタイトルを指定します。 タイトルは、エクスペリエンスフラグメントを一意に識別します


## フォームの送信アクションを設定する {#configure-submit-action-for-form}

送信アクションを使用すると、アダプティブフォームから取り込んだデータの送信先を選択できます。 これは、ユーザーがアダプティブフォーム上の「送信」ボタンをクリックするとトリガーされます。 アダプティブフォームには、すぐに使用できる送信アクションがいくつか含まれています。 デフォルトの送信アクションを拡張して、独自のカスタム送信アクションを作成することもできます。 フォームの送信アクションを設定するには、次の手順を実行します。

1. アダプティブフォームを含むAEMページエディターまたはエクスペリエンスフラグメントを開きます。
1. コンテンツツリーを開き、 **[!UICONTROL アダプティブFormsコンテナ]** アダプティブフォームをホストする 1 つのAEM Sitesページで複数のアダプティブFormsをホストできます。 したがって、適切なアダプティブFormsコンテナを慎重に選択してください。
1. アダプティブフォームコンテナのプロパティをクリックします。 ![アダプティブフォームコンテナのプロパティ](/help/forms/using/assets/configure-icon.svg) アイコン。 送信アクションを設定するアダプティブフォームコンテナダイアログボックスが開きます。
   ![アダプティブフォームコンテナ](/help/forms/using/assets/adaptive-forms-container.png)
1. 必要に応じて、送信アクションを選択して設定します。 送信アクションについて詳しくは、 [アダプティブフォーム送信アクション](configuring-submit-actions.md)


## フォームのスキーマまたはフォームデータモデルの設定 {#configure-schema-or-data-model-for-form}

フォームデータモデルを使用して、フォームをデータソースに接続し、ユーザーの操作に基づいてデータを送受信することができます。 また、フォームを JSON スキーマに接続して、送信済みデータを事前定義済みの形式で受け取ることもできます。

フォームをスキーマまたはフォームデータモデルに接続する前に

* [JSON スキーマを作成し、環境にアップロードする](adaptive-form-json-schema-form-model.md)
* [フォームデータモデルを作成する](create-form-data-models.md)

フォームの JSON スキーマまたはフォームデータモデルを設定するには、次の手順を実行します。

1. アダプティブフォームを含むAEMページエディターまたはエクスペリエンスフラグメントを開きます。
1. コンテンツツリーを開き、 **[!UICONTROL アダプティブFormsコンテナ]** アダプティブフォームをホストする 1 つのAEM Sitesページで複数のアダプティブFormsをホストできます。 したがって、適切なアダプティブFormsコンテナを慎重に選択してください。
1. アダプティブフォームコンテナのプロパティをクリックします。 ![アダプティブフォームコンテナのプロパティ](/help/forms/using/assets/configure-icon.svg) アイコン。 データモデルを設定するためのアダプティブフォームコンテナダイアログボックスが開きます。
   ![フォームデータモデルのアダプティブフォームコンテナ](/help/forms/using/assets/form-data-model-adaptive-forms-container.png)
1. 必要に応じて、JSON スキーマまたはフォームデータモデルを選択し、設定します。 送信アクションについて詳しくは、 [アダプティブフォーム送信アクション](configuring-submit-actions.md).

   * 次の項目を選択した場合： **[!UICONTROL フォームモデル]** オプションを選択する場合は、 **[!UICONTROL フォームデータモデルを選択]** 」オプションを使用して事前設定済みのフォームデータモデルを選択します。
   * 次の項目を選択した場合： **[!UICONTROL スキーマ]** オプションを選択する場合は、 **[!UICONTROL スキーマ]** オプションを使用して、フォームの JSON スキーマを選択します。

1. 「**[!UICONTROL 完了]**」をクリックします。

## フォームの事前入力サービスを設定する {#configure-prefill-service-for-form}

事前入力サービスを使用すると、既存のデータを使用してアダプティブフォームのフィールドに自動入力することができます。 ユーザーがフォームを開くと、これらのフィールドの値は事前入力されています。以下の操作を実行できます。

* [カスタム事前入力サービスの作成](prepopulate-adaptive-form-fields.md)
* [フォームデータモデルの事前入力サービスを使用する](#fdm-prefill-service)

### フォームデータモデルの事前入力サービスを使用する {#fdm-prefill-service}

フォームデータモデルの事前入力サービスを使用すると、設定済みのフォームデータモデルを使用してフォームのフィールドに事前入力することができます。 フォームデータモデルの事前入力サービスでは、 [設定済みのフォームデータモデルのサービスを取得する](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) データを取得します。 アダプティブフォームでフォームデータモデルの事前入力サービスを使用するには、次の手順を実行します。

1. アダプティブフォームを含むAEMページエディターまたはエクスペリエンスフラグメントを開きます。
1. コンテンツツリーを開き、 **[!UICONTROL アダプティブFormsコンテナ]** アダプティブフォームをホストする 1 つのAEM Sitesページで複数のアダプティブFormsをホストできます。 したがって、適切なアダプティブFormsコンテナを慎重に選択してください。
1. アダプティブフォームコンテナのプロパティをクリックします。 ![アダプティブフォームコンテナのプロパティ](/help/forms/using/assets/configure-icon.svg) アイコン。 データモデルを設定するためのアダプティブフォームコンテナダイアログボックスが開きます。
   ![サービス fdm aem サイトページエディターの事前入力](/help/forms/using/assets/prefill-service-fdm-aem-sites-page-editor.png)
1. フォームデータモデルを選択. を開きます。 **[!UICONTROL 基本]** タブをクリックします。 事前入力サービスで、「 」を選択します。 **[!UICONTROL Forms Portal Draft Prefill Service]**.
1. 「**[!UICONTROL 完了]**」をクリックします。

## フォームの送信時または「ありがとうございます」メッセージの表示時に、ユーザーを新しいユーザーにリダイレクトします

フォームの送信時に、別の Web ページまたはメッセージにユーザーをリダイレクトできます。 ユーザーをリダイレクトするか、「ありがとうございます」メッセージを設定するには、次の手順を実行します。

1. アダプティブフォームを含むAEMページエディターまたはエクスペリエンスフラグメントを開きます。
1. コンテンツツリーを開き、 **[!UICONTROL アダプティブFormsコンテナ]** アダプティブフォームをホストする 1 つのAEM Sitesページで複数のアダプティブFormsをホストできます。 したがって、適切なアダプティブFormsコンテナを慎重に選択してください。
1. アダプティブフォームコンテナのプロパティをクリックします。 ![アダプティブフォームコンテナのプロパティ](/help/forms/using/assets/configure-icon.svg) アイコン。 データモデルを設定するためのアダプティブフォームコンテナダイアログボックスが開きます。
1. を開きます。 **[!UICONTROL 送信]** タブをクリックします。

   * リダイレクト URL を設定するには、「送信時に URL にリダイレクト」オプションを選択し、絶対アドレス、リダイレクト URL、またはAEM Sitesページの相対パスを指定します。

   * カスタムメッセージまたはありがとうございますメッセージを設定するには、「送信」オプションで「メッセージを表示」オプションを選択し、「メッセージコンテンツ」ボックスにメッセージを指定します。 これはリッチテキストボックスで、全画面表示オプションを使用して、使用可能なすべてのリッチテキスト項目を表示できます。