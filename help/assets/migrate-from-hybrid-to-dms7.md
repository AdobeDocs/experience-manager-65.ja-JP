---
title: Dynamic Media — ハイブリッドモードからDynamic Media - S7モードへの移行
description: Dynamic Media — ハイブリッドモードからDynamic Media - S7モードへのインスタンスの移行方法を説明します
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
feature: Scene7モード，ハイブリッドモード
exl-id: 07f0803c-4ec4-4745-8214-63370e9d0282
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 2%

---

# Dynamic Media — ハイブリッドからDynamic Media-Scene7への移行について {#about-migrating}

Dynamic Media — ハイブリッドは、Dynamic MediaとAdobe Experience Managerの古いバージョン統合です。 ハイブリッドAdobeは、Adobe Experience Manager 6.1で初めて導入されました。ハイブリッドモードは引き続きサポートされますが、推奨モードではありません。Dynamic Media-Scene7を使用するのが推奨モードです。 また、ハイブリッドモードでは、スマート切り抜きやパノラマ画像などの新機能はサポートされませんが、Dynamic Media-Scene7ではサポートされています。

Dynamic Media — ハイブリッドとDynamic Media-Scene7間のその他の主な違いを次に示します。

* URLの構造。
* ビデオの取り込み。
* 画像レンディションの作成と保存。
* クラウド設定と資格情報（プロビジョニング）。

Dynamic Media — ハイブリッドからDynamic Media-Scene7に移行する場合、2つのオプションを使用できます。 1つ目のオプションは、Dynamic Media-Scene7の新しいインスタンスをExperience Manager上でプロビジョニングするだけです。 2つ目の方法は、Dynamic Mediaハイブリッドの既存のインスタンスをDynamic Media-Scene7に移行することです。 このオプションでは、移動中におこなう手順と考慮事項を以下に示す表形式の概要を説明します。

>[!IMPORTANT]
>
>Adobeでは、Dynamic Mediaハイブリッド実装を実稼動インスタンス上のDynamic Media-Scene7に移行しないことをお勧めします。

## オプション1 -Experience ManagerでのDynamic Media-Scene7の新しいインスタンスのプロビジョニング {#provision-new-dms7}

Adobe Experience Manager上のDynamic Media-Scene7の新しいプロビジョニング済みインスタンスを使用して、新規に作成することを検討します。 Dynamic MediaCloud Serviceを通じたアセットの取り込みと処理に加えて、アセットの使用状況、ワークフロー、コンポーネントのAdobe監査を強くお勧めします。 多くの場合、新しい標準搭載機能を使用して、カスタムコンポーネントやワークフローを置き換えることができます。

## オプション2 - Dynamic Mediaハイブリッドの既存のインスタンスをDynamic Media-Scene7に移行する {#process-for-migrating}

| ステップ | タスク | 検討事項 |
|---|---|---|
| 1 | Dynamic Media — ハイブリッドオーサーインスタンスのクローンを作成します。 | この移行プロセスの残りの手順が正常に完了するまで、フォールバック用にDynamic Media — ハイブリッドオーサーの既存のインスタンスを維持します。 |
| 2 | Dynamic Media - Scene7モードで、複製されたオーサーインスタンスを起動します。 |  |
| 3 | Adobe Experience ManagerCloud Servicesで、Dynamic Media-Scene7資格情報を使用してDynamic Mediaを設定します。 | Adobeは、Dynamic MediaとScene7のプロビジョニングを承認する必要があります。 そのため、同時Dynamic MediaMハイブリッド環境とDynamic Media-Scene7環境があり、これらはAdobeでサポートされますが、期間は限られています。 |
| 4 | 移行バンドルを作成して、必要に応じてアセットを取り込むことができます。<br>Dynamic Media — ハイブリッドへの最初の取り込み時に作成されたローカルPTIFFを削除します。 | すべてのアセットが現在Dynamic Media — ハイブリッドインスタンスで使用可能な場合は、そのすべてのアセットを既に含むのクローンです。 したがって、バンドルは不要です。 |
| 5 | アセットの更新ワークフローを実行して、アセットをDynamic MediaCloud Serviceに同期します。 | Adobeでは、圧縮を可能にするために、更新ワークフローをバッチで実行することをお勧めします。 |
| 6 | ビューア、画像およびビデオプリセットを移行します。 |  |
| 7 | 各Webコンテンツ管理で参照されるアセットを調べ、関連するURLを更新します。 |  |
| 8 | 新しいDynamic Media - Scene7モードをサポートするカスタムワークフローを移行します（手動更新）。 |  |
| 9 | Webコンテンツ管理のアップロードと設定を確認します。 |  |
| 10 | 検証後、Dynamic Media — ハイブリッドオーサーを無効にする承認を取得します（フォールバックとして維持）。 |  |
| 11 | Dynamic Media-Scene7を正常に使用してから約1か月後に、Dynamic Media — ハイブリッドオーサーインスタンスを削除します。 |  |
