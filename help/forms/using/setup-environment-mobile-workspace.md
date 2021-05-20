---
title: AEM Forms アプリケーションの環境設定
seo-title: AEM Forms アプリケーションの環境設定
description: AEM Forms アプリケーションを構築しデプロイするためのハードウェア、ソフトウェア、ライセンス。
seo-description: AEM Forms アプリケーションを構築しデプロイするためのハードウェア、ソフトウェア、ライセンス。
uuid: 4123a6b7-5766-476c-9afb-f57029b148ad
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e6b01ade-7ea3-42a7-872d-cc35a3d2782a
docset: aem65
exl-id: 1d1f9db2-83cf-4612-ac8c-d2638c3bbaea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 67%

---

# AEM Forms アプリケーションの環境設定{#set-up-environment-for-aem-forms-app}

AEM Forms アプリケーションを構築しデプロイするためには、次のハードウェア、ソフトウェア、ライセンスが必要です。

## Windows デバイスの場合  {#for-windows-devices}

* Microsoft Windows 10
* Microsoft Visual Studio 2015
* Apache Cordova 向け Microsoft Visual Studio Tools

## iOS デバイス用 {#for-ios-devices}

* Mac OS X 10.9.5 以上搭載の Intel ベース Apple Mac
* iOS SDK 8.4以降
* Xcode バージョン: Xcode 6.4 for OS X 以上
* iOS Developer Enterprise プログラムのメンバーシップ
* 社内の iOS アプリケーション配布のためのエンタープライズ証明書
* Apple iPad（iOS 8.4 以降搭載）

## Android デバイスの場合  {#for-android-devices}

* [https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html)からダウンロード可能なAndroid開発ツールキット（ADTバンドル）
* MAC システム上に環境が設定される場合は、Applications フォルダーに ADT をインストールする必要があります。
* ADTがMAC上の他の場所にインストールされている場合、または環境がWindowsシステム上に設定されている場合は、ADT SDKのパスを`src\android`フォルダー内の`local.properties`ファイルに更新する必要があります。このファイルは、抽出されたソースアーカイブ`mobileworkspace-src.zip`内のにあります。 このファイルで、`sdk.dir` 変数をデスクトップ上の ADT SDK の場所にポイントしてください。

>[!NOTE]
>
>adobe-lc-mobileworkspace-src.zipにはPhoneGap SDK 5.0が含まれています。PhoneGap SDKが事前にインストールされていないことを確認してください。
