---
title: AEM 6.5 における後方互換性
description: アプリと設定をAdobe Experience Manager(AEM)6.5 と互換性を保つ方法について説明します。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
docset: aem65
feature: Upgrading
exl-id: c432a014-2dab-4c49-a25b-e4f461d13f9b
source-git-commit: b66ec42c35b5b60804015d340b8194bbd6ef3e28
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 15%

---

# AEM 6.5 における後方互換性{#backward-compatibility-in-aem}

## 概要 {#overview}

>[!NOTE]
>
>互換性パッケージの範囲に属さないコンテンツおよび設定の変更のリストについては、 [AEMでのリポジトリの再構築](/help/sites-deploying/repository-restructuring.md).

Adobe Experience Manager(AEM)6.5 では、すべての機能が後方互換性を念頭に置いて開発されています。

通常、AEM 6.3 を実行しているお客様は、アップグレードの際にコードやカスタマイズを変更する必要はありません。 AEM 6.1 および 6.2 のお客様の場合、6.3 へのアップグレード時よりも重大な変更はありません。

機能の後方互換性を維持できない例外の場合、バンドルとコンテンツに対する後方非互換性の問題を軽減できます。 それには、6.4 用の互換性パッケージをインストールします（ダウンロード先の詳細については、以下のセットアップ方法を参照してください）。 この互換性パッケージは、AEM 6.4 に準拠しているアプリケーションで、通常は互換性を復元するのに役立ちます。

互換性パッケージを使用すると、AEMを互換モードで実行し、新しいAEM機能に対するカスタム開発を延期できます。

>[!NOTE]
>
>互換性パッケージは、AEM 6.5 との互換性を保つために必要な開発を遅らせるための一時的なソリューションに過ぎません。 Adobeでは、アップグレード直後に開発を通じて互換性の問題に対処できない場合にのみ、最後のオプションとしてのみお勧めします。 さらに、6.5 ベースのカスタム開発を続行し、6.5 の全機能を利用できるようになったら、Adobeはネイティブモードに切り替えて、互換性パッケージをアンインストールすることをお勧めします。

![sase](assets/sase.png)

互換性パッケージには次の 2 つのモードがあります。 **ルーティング有効** および **ルーティング無効**.

これにより、AEM 6.5 を次の 3 つのモードで実行できます。

**ネイティブモード：**

ネイティブモードは、AEM 6.5 のすべての新機能を使用し、すべての新機能でカスタマイズ機能を動作させるために開発を行う準備が整っているお客様向けです。

つまり、アップグレード後すぐにアプリケーションを調整する必要があります。

**互換性モード：ルーティングが有効な互換性パッケージがインストールされました**

互換性モードは、後方互換性を維持できないインターフェイスのカスタマイズを持つお客様向けです。 これにより、AEMを互換性モードで実行し、一部のカスタムコードと互換性のない新しいAEM機能に対して必要なカスタム開発を遅らせることができます。

**レガシーモード：ルーティングが無効な状態で互換パッケージがインストールされました**

レガシーモードは、互換性パッケージから移動された、AEMのレガシーまたは廃止されたコードに基づくカスタムインターフェイスを持つお客様向けです。

![sapte](assets/sapte.png)

## 設定方法 {#how-to-set-up}

The **6.5 用AEM 6.4 互換性パック** は、パッケージマネージャーを使用してパッケージとしてインストールできます。 次をダウンロード： [ソフトウェア配布版のAEM 6.4 Compatibility Pack （6.5 用）](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=compat*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=20&amp;package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fcompatpack%2Faem-compat-cq65-to-cq64) サイト。

互換パッケージがインストールされると、次に示すように、OSGI 設定のスイッチを使用して、ルーティングを有効または無効にできます。

![互換スイッチ](assets/compat-switches.png)

互換性パッケージをインストールして設定した後、選択した互換性モードに基づいて機能が使用されます。
