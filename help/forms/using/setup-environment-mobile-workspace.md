---
title: AEM Forms アプリケーションの環境設定
description: AEM Forms アプリを構築しデプロイするためのハードウェア、ソフトウェアおよびライセンス。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 1d1f9db2-83cf-4612-ac8c-d2638c3bbaea
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 86%
---
# AEM Forms アプリケーションの環境設定{#set-up-environment-for-aem-forms-app}

>[!NOTE]
>
>AEM Forms アプリは現在、非推奨です。 質問またはヘルプについては、[aemformsapp-android@adobe.com](mailto:aemformsapp-android@adobe.com)までお問い合わせください。

AEM Forms アプリを構築してデプロイするには、次のハードウェア、ソフトウェアおよびライセンスが必要です。

## Windows デバイスの場合 {#for-windows-devices}

* Microsoft® Windows 10
* Microsoft® Visual Studio 2015
* Apache Cordova 向け Microsoft® Visual Studio Tools

## iOS デバイスの場合 {#for-ios-devices}

* macOS X 10.9.5 以上搭載の Intel ベース Apple Mac
* iOS SDK 8.4 以降
* Xcode バージョン：OS X 以降の Xcode 6.4
* iOS Developer Enterprise プログラムのメンバーシップ
* 社内の iOS アプリ配布のためのエンタープライズ証明書
* iOS 8.4 以降搭載の Apple iPad

## Android™ デバイスの場合 {#for-android-devices}

* [https://developer.android.com/studio](https://developer.android.com/studio) からダウンロードできる Android™ 開発ツールキット（ADT バンドル）
* Mac システム上に環境を設定する場合は、Applications フォルダーに ADT をインストールする必要があります。
* ADT がMacの他の場所にインストールされている場合、または環境が Windows システムに設定されている場合は、`local.properties` ファイルで ADT SDK のパスを更新する必要があります。 このファイルは、抽出されたソースアーカイブ内の `src\android` フォルダーで使用できます`mobileworkspace-src.zip`。 このファイルで、`sdk.dir` 変数をデスクトップ上の ADT SDK の場所を指すようにします。

>[!NOTE]
>
>adobe-lc-mobileworkspace-src.zipには、PhoneGap SDK 5.0が含まれています。 PhoneGap SDKがプリインストールされていないことを確認します。
