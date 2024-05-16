---
title: AEM 6.5 における後方互換性
description: お使いのアプリケーションおよび設定と、Adobe Experience Manager（AEM）6.5 との互換性を保つ方法について説明します。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
docset: aem65
feature: Upgrading
exl-id: c432a014-2dab-4c49-a25b-e4f461d13f9b
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: ht
source-wordcount: '485'
ht-degree: 100%

---

# AEM 6.5 における後方互換性{#backward-compatibility-in-aem}

## 概要 {#overview}

>[!NOTE]
>
>互換性パッケージの範囲に含まれないコンテンツおよび設定の変更のリストについては、[AEM におけるリポジトリの再構築](/help/sites-deploying/repository-restructuring.md)を参照してください。

Adobe Experience Manager（AEM）6.5 では、すべての機能が後方互換性を念頭に置いて開発されています。

ほとんどの場合、AEM 6.3 を実行しているお客様は、アップグレードの際にコードやカスタマイズの修正を行う必要はありません。AEM 6.1 および 6.2 のお客様の場合、6.3 にアップグレードする際よりも大きい変更はありません。

機能の後方互換性を維持できない例外に関して、バンドルとコンテンツに対する後方非互換性の問題を軽減できます。そのためには、6.4 用の互換性パッケージをインストールします（ダウンロード先の詳細については、以下のセットアップ方法を参照してください）。この互換性パッケージは、AEM 6.4 に準拠したアプリケーションのほとんどの場合で、互換性を回復するのに役立ちます。

互換性パッケージを使用すると、AEM を互換モードで実行でき、新しい AEM 機能に対するカスタム開発を先送りできます。

>[!NOTE]
>
>互換性パッケージは、AEM 6.5 との互換性を保つために必要な開発を遅らせるための一時的なソリューションに過ぎません。アップグレード直後の開発を通して互換性の問題に対処できない場合の最後の選択肢としてのみお勧めします。さらに、6.5 ベースのカスタム開発を続行し、6.5 の全機能を利用できるようになったら、ネイティブモードに切り替えて互換性パッケージをアンインストールすることをお勧めします。

![sase](assets/sase.png)

互換性パッケージには、**ルーティング有効**&#x200B;と&#x200B;**ルーティング無効**&#x200B;の 2 つのモードがあります。

これにより、AEM 6.5 は次の 3 つのモードで実行できます。

**ネイティブモード：**

ネイティブモードは、AEM 6.5 のすべての新機能を使用したいお客様、およびすべての新機能のカスタマイズ作業を行うための開発の準備ができているお客様用です。

つまり、アップグレード後すぐにアプリケーションの調整を行う必要があります。

**互換性モード：ルーティング有効で互換性パッケージをインストール**

互換性モードは、後方互換性のないインターフェイスのカスタマイズがあるお客様用です。これにより、AEM を互換性モードで実行し、一部のカスタムコードと互換性のない新しい AEM 機能に対して必要なカスタム開発を遅らせることができます。

**レガシーモード：ルーティング無効で互換性パッケージをインストール**

レガシーモードは、互換性パッケージで移行された AEM のレガシーコードまたは廃止されたコードに基づくカスタムインターフェイスを持つお客様用です。

![sapte](assets/sapte.png)

## 設定方法 {#how-to-set-up}

**6.5 用 AEM 6.4 互換性パック**&#x200B;は、パッケージマネージャーを使用してパッケージとしてインストールできます。[6.5 用 AEM 6.4 互換性パックは、ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=compat*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=20&amp;package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fcompatpack%2Faem-compat-cq65-to-cq64)サイトからダウンロードできます。

互換パッケージがインストールされると、次に示すように、OSGI 設定のスイッチを使用して、ルーティングを有効または無効にできます。

![互換スイッチ](assets/compat-switches.png)

互換性パッケージがインストールされて設定されると、各機能は選択された互換性モードに基づいて使用されるようになります。
