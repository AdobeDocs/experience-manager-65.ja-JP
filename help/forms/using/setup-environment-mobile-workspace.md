---
title: AEM Forms アプリケーションの環境設定
description: AEM Formsアプリを構築しデプロイするためのハードウェア、ソフトウェア、ライセンス。
uuid: 4123a6b7-5766-476c-9afb-f57029b148ad
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e6b01ade-7ea3-42a7-872d-cc35a3d2782a
docset: aem65
exl-id: 1d1f9db2-83cf-4612-ac8c-d2638c3bbaea
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 22%

---

# AEM Forms アプリケーションの環境設定{#set-up-environment-for-aem-forms-app}

AEM Formsアプリを構築してデプロイするには、次のハードウェア、ソフトウェア、ライセンスが必要です。

## Windows デバイスの場合 {#for-windows-devices}

* Microsoft® Windows 10
* Microsoft® Visual Studio 2015
* Microsoft® Visual Studio Tools for Apache Cordova

## iOSデバイスの場合 {#for-ios-devices}

* macOS X 10.9.5 以降を実行するインテルベースのApple Mac
* iOS SDK 8.4 以降
* Xcode バージョン：OS X 以降の Xcode 6.4
* iOS Developer Enterprise プログラムのメンバーシップ
* 社内iOSアプリを配布するためのエンタープライズ証明書
* Apple iPadとiOS 8.4 以降

## Android™デバイスの場合 {#for-android-devices}

* Android™ Development Toolkit （ADT バンドル）。 [https://developer.android.com/studio](https://developer.android.com/studio)
* 環境がMacシステムに設定されている場合、ADT は Applications フォルダーにインストールされている必要があります。
* ADT がMacの他の場所にインストールされている場合、または環境が Windows システムに設定されている場合は、ADT SDK のパスを `local.properties` ファイル。 このファイルは、 `src\android` 抽出されたソースアーカイブ内のフォルダー `mobileworkspace-src.zip`. このファイルで、`sdk.dir` 変数をデスクトップ上の ADT SDK の場所を指すようにします。

>[!NOTE]
>
>adobe-lc-mobileworkspace-src.zip には PhoneGap SDK 5.0 が含まれています。PhoneGap SDK が事前にインストールされていないことを確認してください。
