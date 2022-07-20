---
title: Dynamic Media - ハイブリッドモードから Dynamic Media - S7 モードへの移行
description: Dynamic Media - ハイブリッドモードから Dynamic Media - S7 モードに移行する方法を説明
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
feature: Scene7 Mode,Hybrid Mode
exl-id: 07f0803c-4ec4-4745-8214-63370e9d0282
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: ht
source-wordcount: '524'
ht-degree: 100%

---

# Dynamic Media - ハイブリッドから Dynamic Media - Scene7 への移行について {#about-migrating}

Dynamic Media - ハイブリッドは、Dynamic Media と Adobe Experience Manager の統合の古いバージョンです。ハイブリッドバージョンは、Adobe Experience Manager 6.1 で初めて導入されました。ハイブリッドモードは引き続きサポートされますが、推奨モードではありません。Dynamic Media - Scene7 を使用することをお勧めします。また、ハイブリッドモードでは、スマート切り抜きやパノラマ画像などの新機能はサポートされませんが、Dynamic Media - Scene7 ではサポートされています。

Dynamic Media - ハイブリッドと Dynamic Media - Scene7 のその他の主な違いは次の通りです。

* URL の構造。
* ビデオの取り込み。
* 画像レンディションの作成と保存。
* クラウド設定と資格情報（プロビジョニング）。

Dynamic Media - ハイブリッドから Dynamic Media - Scene7 に移行する際には、2 つのオプションを使用できます。1 つ目のオプションは、Dynamic Media - Scene7 の新しいインスタンスを Experience Manager 上でシンプルにプロビジョニングすることです。2 つ目のオプションは、Dynamic Media - ハイブリッドの既存のインスタンスを Dynamic Media - Scene7 に移行することです。このオプションでは、移動時に行う手順と考慮事項について（以下に示す表形式で）概要を説明します。

>[!IMPORTANT]
>
>アドビでは、ライブの実稼働インスタンスで Dynamic Media - ハイブリッドの実装を Dynamic Media - Scene7 に移行しないことをお勧めします。

## オプション 1 - Experience Manager で Dynamic Media - Scene7 の新しいインスタンスをプロビジョニング {#provision-new-dms7}

Adobe Experience Manager 上で Dynamic Media - Scene7 をプロビジョニングした新しいインスタンスで、新たに始めることを検討してください。Dynamic Media Cloud Service によるアセットの取り込みと処理に加え、アセットの使用状況、ワークフロー、コンポーネントに関するアドビの監査を強くお勧めします。多くの場合、標準搭載の新しい機能を使用して、カスタムコンポーネントやワークフローを置き換えることができます。

## オプション 2 - Dynamic Media - ハイブリッドの既存のインスタンスを Dynamic Media - Scene7 に移行 {#process-for-migrating}

| 手順 | タスク | 検討事項 |
|---|---|---|
| 1 | Dynamic Media - ハイブリッドオーサーインスタンスのクローンを作成します。 | この移行プロセスの残りの手順が正常に完了するまで、フォールバック用に Dynamic Media - ハイブリッドオーサーの既存のインスタンスを維持します。 |
| 2 | Dynamic Media - Scene7 モードで、複製されたオーサーインスタンスを開始します。 |  |
| 3 | Adobe Experience Manager Cloud Services で、Dynamic Media - Scene7 資格情報を使用して Dynamic Media を設定します。 | アドビは、Dynamic Media - Scene7 のプロビジョニングを承認する必要があります。そのため、Dynamic Media - ハイブリッド環境と Dynamic Media - Scene7 環境は同時に存在し、アドビがサポートしていますが、その期間は限られています。 |
| 4 | 移行バンドルを作成して、必要に応じてアセットを取り込むことができます。<br>Dynamic Media - ハイブリッドへの初回取り込み時に作成したローカル PTIFF を削除します。 | すべてのアセットが Dynamic Media - ハイブリッドインスタンスで現在使用可能な場合、そのクローンにはすでにすべてのアセットが含まれています。したがって、バンドルは必要ありません。 |
| 5 | アセット更新ワークフローを実行して、アセットを Dynamic Media Cloud Service に同期します。 | アドビは、圧縮を可能にするために、更新ワークフローをバッチで実行することをお勧めします。 |
| 6 | ビューア、画像およびビデオプリセットを移行します。 |  |
| 7 | Web コンテンツ管理で参照される各アセットを調べ、関連する URL を更新します。 |  |
| 8 | 新しい Dynamic Media - Scene7 モード（手動更新）をサポートするカスタムワークフローを移行します。 |  |
| 9 | Web コンテンツ管理のアップロードと設定を確認します。 |  |
| 10 | 検証後、Dynamic Media - ハイブリッドオーサーを無効にする承認を得ます（フォールバックとして維持）。 |  |
| 11 | Dynamic Media – Scene7 が正常に使用されてから約 1 か月後に、Dynamic Media - ハイブリッドオーサーインスタンスを削除します。 |  |
