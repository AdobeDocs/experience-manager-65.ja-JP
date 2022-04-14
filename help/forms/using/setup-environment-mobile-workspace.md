---
title: AEM Forms アプリケーションの環境設定
seo-title: Set up environment for AEM Forms app
description: AEM Forms アプリケーションを構築しデプロイするためのハードウェア、ソフトウェア、ライセンス。
seo-description: Hardware, software, and licenses to build and deploy the AEM Forms app.
uuid: 4123a6b7-5766-476c-9afb-f57029b148ad
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e6b01ade-7ea3-42a7-872d-cc35a3d2782a
docset: aem65
exl-id: 1d1f9db2-83cf-4612-ac8c-d2638c3bbaea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '209'
ht-degree: 100%

---

# AEM Forms アプリケーションの環境設定{#set-up-environment-for-aem-forms-app}

AEM Forms アプリケーションを構築しデプロイするためには、次のハードウェア、ソフトウェア、ライセンスが必要です。

## Windows デバイスの場合 {#for-windows-devices}

* Microsoft Windows 10
* Microsoft Visual Studio 2015
* Apache Cordova 向け Microsoft Visual Studio Tools

## iOS デバイスの場合 {#for-ios-devices}

* Mac OS X 10.9.5 以上搭載の Intel ベース Apple Mac
* iOS SDK 8.4 以降
* Xcode バージョン: Xcode 6.4 for OS X 以上
* iOS Developer Enterprise プログラムのメンバーシップ
* 社内の iOS アプリケーション配布のためのエンタープライズ証明書
* Apple iPad（iOS 8.4 以降搭載）

## Android デバイスの場合 {#for-android-devices}

* [https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html) からダウンロードできる Android 開発ツールキット（ADT バンドル）
* MAC システム上に環境を設定する場合は、Applications フォルダーに ADT をインストールする必要があります。
* ADT が MAC 上のそれ以外の場所にインストールされている場合、あるいは環境が Window システム上に設定される場合、ADT SDK パスは、展開されたソースアーカイブ `mobileworkspace-src.zip` の `src\android` フォルダーにある `local.properties` ファイルでアップデートする必要があります。このファイルで、`sdk.dir` 変数をデスクトップ上の ADT SDK の場所を指すようにします。

>[!NOTE]
>
>adobe-lc-mobileworkspace-src.zip には PhoneGap SDK 5.0 が含まれています。PhoneGap SDK が事前にインストールされていないことを確認してください。
