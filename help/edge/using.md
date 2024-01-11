---
title: Edge 配信サービスの使用
description: Edge 配信サービスの使用
exl-id: 6c9178b0-c8f3-4fc7-8614-8e71ffc2f0b8
source-git-commit: d2c0dea636280c28e1d5a76d1c5375f21b6eb111
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 92%

---

# Edge 配信サービスの使用 {#usingedge}

Edge 配信を使用すると、作成者がコンテンツをすばやく更新および公開でき、新しいサイトを迅速に起動できる、迅速な開発環境を作成できます。そのため、同じ web サイト上で複数のコンテンツソースを操作でき、選択したソースに関係なく、シームレスに公開を効率化できます。したがって、編集からインターネット上のコンテンツが表示されるまでに、数秒しかかかりません。

## オーサリング {#authoring-edge}

Edge 配信を使用すると、オーサリングが簡単、迅速、柔軟に行えます。オーサリングには、Edge 配信サービスのコンテキスト内で 2 つの異なる方法を使用できます。

* ドキュメントベースのオーサリング（Microsoft Word や Google Docs など）について詳しくは、[こちらのリンクを参照してください。](https://www.hlx.live/docs/authoring)。
* ページエディター／ユニバーサルエディター - アドビ営業担当者にお問い合わせください。

ドキュメントベースのオーサリングがある場合は、Microsoft Word やGoogle Docs など、様々なソースを使用できます。 これらのソースからのドキュメントは、web サイト上のページになります。見出し、リスト、画像、フォント要素、ビデオはすべて、初期ソースから web サイトに転送できます。SEO 用にメタデータを追加したり、ブロックを使用して構造化コンテンツを操作したり、機能を追加したりできます。

## 公開 {#publishing-edge}

Edge 配信を使用すると、コンテンツソースに関係なく、コンテンツの公開をシームレスに行えます。プロセスは次のように行われます。[サイドキック拡張機能](#using-sidekick)を使用して公開メカニズムをトリガーすると、web サイト上でコンテンツが数秒で公開されます。

## Edge 配信サービスおよび GitHub {#github-edge}

Edge 配信では GitHub を使用するので、顧客は GitHub リポジトリから直接コードを管理およびデプロイできます。 例えば、Google Docs または Microsoft Word にコンテンツを書き込み、GitHub で CSS と JavaScript を使用してサイトの機能を開発できます。コンテンツのプレビューから実稼動環境まで、ブランチごとに web サイトが自動的に作成されます。GitHub リポジトリに配置したすべてのリソースは、ビルドプロセスなしで web サイト上で使用できます。

## Sidekick の使用 {#using-sidekick}

AEM Sidekick には、コンテキストに応じたオプションを備えたツールバーがあり、これを使用して、コンテンツの編集、プレビューおよび公開を簡単に行うことができます。AEM Sidekick 拡張機能の[インストール](https://www.hlx.live/docs/sidekick-extension)後、プロジェクト環境でまたはコンテンツの編集時（例えば、Google Docs 内）に使用できます。環境に応じて、プレビュー、リロード、編集および公開など、いくつかのアクションを使用できます。サイドキックを使用する場合、プレビュー環境から実稼動環境（その逆も同様）に環境をを切り替えることもできます。

**公開する**&#x200B;には、プレビューページでサイドキックを開き、公開アクションを使用します。「公開」をクリックした後、ページの現在のプレビューバージョンが公開され、実稼動環境で使用できるようになります。

## AEM Assets とドキュメントベースのオーサリングの統合 {#integrate-assets-edge}

Edge 配信を使用すると、Microsoft Word またはGoogle Docs でドキュメントをオーサリングする際に、AEM Assets リポジトリで使用可能な画像を使用できます。

ドキュメント内で画像を使用するオプションは、[AEM Assets Sidekick プラグインを設定](https://www.hlx.live/developer/configuring-aem-assets-sidekick-plugin)した後に使用できます。

AEM Assets Sidekick プラグインは、次へのアクセスをサポートしています。

* AEM Assets as a Cloud Service

* AEM Assets Essentials

AEM Assets Sidekick プラグインを設定した後、[Google Docs または Microsoft Word ドキュメント内で画像の使用を開始](https://www.hlx.live/docs/aem-assets-sidekick-plugin)できます。

## 参考情報 {#further-reading}

詳しくは、次のページを参照してください。

* Edge 配信の開始方法について詳しくは、Edge 配信ドキュメントの[ビルド](https://www.hlx.live/docs/#build)の節を参照してください。
* Edge 配信を使用してコンテンツをオーサリングおよび公開する方法について詳しくは、[セクションの公開](https://www.hlx.live/docs/authoring)を参照してください。
* サイドキック拡張機能の使用方法について詳しくは、[サイドキックの使用](https://www.hlx.live/docs/sidekick)のページを参照してください。
* AEMオーサリングの場合は、 [オーサリングの概念ページ](/help/sites-authoring/author.md))
