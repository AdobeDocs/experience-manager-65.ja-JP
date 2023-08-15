---
title: AEM 6.5 における後方互換性
seo-title: Backward Compatibility in AEM 6.5
description: アプリと設定をAEM 6.5 と互換性を保つ方法を説明します。
seo-description: Learn how to keep your apps and configurations compatible with AEM 6.5
uuid: 81dc2771-f59b-4b24-8932-9e938cba05e0
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: f3b4ec1d-9054-47d4-afcb-0a0121b94190
docset: aem65
feature: Upgrading
exl-id: c432a014-2dab-4c49-a25b-e4f461d13f9b
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 45%

---

# AEM 6.5 における後方互換性{#backward-compatibility-in-aem}

## 概要 {#overview}

>[!NOTE]
>
>互換性パッケージの範囲に含まれないコンテンツと設定の変更のリストについては、 [AEMでのリポジトリの再構築](/help/sites-deploying/repository-restructuring.md).

AEM 6.5 では、すべての機能が後方互換性を念頭に置いて開発されています。

ほとんどの場合、AEM 6.3 を実行しているお客様は、アップグレードの際にコードやカスタマイズの修正をおこなう必要はありません。AEM 6.1 および 6.2 のお客様の場合、6.3 にアップグレードする際よりも大きい変更はありません。

例外的に機能の後方互換性を維持できない場合は、6.4 の互換パッケージをインストールすることで、バンドルおよびコンテンツの後方非互換性の問題を軽減できます（ダウンロード場所について詳しくは、以下の「設定方法」を参照してください）。この互換パッケージは、AEM 6.4 に準拠したアプリケーションのほとんどの場合で、互換性を回復するのに役立ちます。

互換性パッケージを使用すると、AEMを互換モードで実行し、新しいAEM機能に対するカスタム開発を延期できます。

>[!NOTE]
>
>互換性パッケージは、AEM 6.5 との互換性を維持するために必要な開発を遅らせるための一時的なソリューションに過ぎません。アップグレード後すぐに開発を通じて互換性の問題に対処できない場合にのみ、最後のオプションとして推奨されます。 6.5 ベースのカスタム開発を続行し、6.5 の機能をフルに利用できるようになったら、ネイティブモードに切り替えて、互換性パッケージをアンインストールすることを強くお勧めします。

![sase](assets/sase.png)

互換性パッケージには次の 2 つのモードがあります。 **ルーティング有効** および **ルーティング無効**.

これにより、AEM 6.5 を次の 3 つのモードで実行できます。

**ネイティブモード：**

ネイティブモードは、AEM 6.5 のすべての新機能を使用し、すべての新機能でカスタマイズ機能を動作させるために開発を行う準備が整っているお客様向けです。

つまり、アップグレード後すぐにアプリケーションで調整を行う必要が生じる場合があります。

**互換性モード：ルーティングが有効な互換性パッケージがインストールされました**

互換性モードは、後方互換性を維持できないインターフェイスのカスタマイズを持つお客様向けです。 これにより、AEMを互換性モードで実行し、一部のカスタムコードと互換性のない新しいAEM機能に対して必要なカスタム開発を遅らせることができます。

**レガシーモード：ルーティングが無効な状態で互換パッケージがインストールされました**

レガシーモードは、互換性パッケージから移動された、AEMのレガシーまたは廃止されたコードに基づくカスタムインターフェイスを持つお客様向けです。

![sapte](assets/sapte.png)

## 設定方法 {#how-to-set-up}

**6.5 用 AEM 6.4 互換性パック**&#x200B;は、パッケージマネージャーを使用してパッケージとしてインストールできます。[6.5 用 AEM 6.4 互換性パックは、ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=compat*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=20&amp;package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fcompatpack%2Faem-compat-cq65-to-cq64)サイトからダウンロードできます。

互換パッケージがインストールされると、次に示すように、OSGI 設定のスイッチを使用して、ルーティングを有効または無効にできます。

![互換スイッチ](assets/compat-switches.png)

互換パッケージがインストールされて設定されると、各機能は選択された互換モードに基づいて使用されるようになります。
