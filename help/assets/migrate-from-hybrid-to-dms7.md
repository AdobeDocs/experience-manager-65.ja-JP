---
title: Dynamic Media — ハイブリッドモードからDynamic Media- S7モードへの移行
description: Dynamic Media — ハイブリッドモードのインスタンスをDynamic Media- S7モードに移行する方法を説明します。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
translation-type: tm+mt
source-git-commit: f466193a259d9e8869d7f79eafda1be20869e4af
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 2%

---


# Dynamic MediaハイブリッドからDynamic MediaScene7への移行について{#about-migrating}

Dynamic MediaハイブリッドはDynamic MediaとAdobe Experience Managerの統合の古いバージョンです。 ハイブリッドバージョンは、AEM (Adobe Experience Manager) 6.1で最初に導入されました。Adobeはハイブリッドモードを引き続きサポートしますが、推奨モードではありません(Dynamic MediaScene7が推奨モードです)。 また、スマート切り抜きやパノラマ画像などの新機能はサポートされません。 Dynamic Media・Scene7はそうだ。

Dynamic MediaハイブリッドとDynamic MediaScene7の主な違いは次のとおりです。

* URLの構造。
* ビデオの取り込み。
* 画像レンディションの作成とストレージ。
* クラウドの設定と資格情報（プロビジョニング）

Dynamic MediaハイブリッドからDynamic MediaScene7に移動する場合は、2つのオプションを使用できます。 1つ目の選択肢は、単にAEM上にDynamic MediaScene7の新しいインスタンスを提供することです。 2つ目の方法は、Dynamic Mediaハイブリッドの既存のインスタンスをDynamic MediaScene7に移行することです。 このオプションでは、移動中に行う手順と考慮事項を、表形式で下に説明します。

>[!IMPORTANT]
>
>Adobeでは、実稼働インスタンスでDynamic Mediaハイブリッド実装をDynamic MediaScene7に移行しないことをお勧めします。

## オプション1 - AEM {#provision-new-dms7}上のDynamic Media-Scene7の新しいインスタンスをプロビジョニングする

Adobe Experience ManagerのDynamic Media・Scene7の新しいプロビジョニングされた例から始めてみましょう Dynamic MediaCloud Serviceを通じたアセットの取り込みと処理に加えて、アセットの使用、ワークフロー、コンポーネントのAdobe監査も強くお勧めします。 多くの場合、カスタムコンポーネントとワークフローは、標準搭載された新しい機能で置き換えることができます。

## オプション2 -Dynamic Mediaハイブリッドの既存のインスタンスをDynamic MediaScene7に移行する{#process-for-migrating}

| ステップ | タスク | 検討事項 |
|---|---|---|
| 1 | Dynamic Mediaハイブリッド作成者インスタンスのコピー | この移行プロセスの残りの手順が正常に完了するまで、フォールバック用に、Dynamic Mediaハイブリッド作成者の既存のインスタンスを維持する必要があります。 |
| 2 | 開始で、Dynamic Media-Scene7モードでオーサーインスタンスを複製しました。 |  |
| 3 | Adobe Experience ManagerCloud Servicesで、Dynamic MediaScene7の資格情報を使用してDynamic Mediaを設定します。 | Adobeは、Dynamic Media・Scene7のプロビジョニングを承認する必要があります。 同時にサポートされるDynamic MediaM-Hybrid環境とDynamic Media-Scene7があります。 |
| 4 | 必要に応じてアセットを取り込む移行バンドルを作成します。<br>Dynamic Mediaハイブリッドへの初回取り込み時に作成されたローカルPTIFFを削除します。 | 現在、すべてのアセットがDynamic Mediaハイブリッドインスタンスで使用可能な場合、そのクローンには既にすべてのアセットが含まれています。 したがって、バンドルは必要ありません。 |
| 5 | アセット更新ワークフローを実行して、アセットをDynamic MediaCloud Serviceと同期します。 | Adobeでは、圧縮を可能にするために、更新ワークフローをバッチで実行することをお勧めします。 |
| 6 | ビューア、画像およびビデオプリセットを移行します。 |  |
| 7 | 各Webコンテンツ管理参照アセットを調べ、関連URLを更新します。 |  |
| 8 | 新しいDynamic MediaScene7モードをサポートするように、カスタムワークフローを移行します（手動アップデート）。 |  |
| 9 | Webコンテンツ管理のアップロードと設定を確認します。 |  |
| 10 | 検証後、Dynamic Mediaハイブリッド発言者を無効にする承認を取得します（フォールバックとして維持）。 |  |
| 11 | 約1か月のDynamic Media-Scene7の使用が成功した後、Dynamic Media — ハイブリッド作成者インスタンスを削除します。 |  |
