---
title: マルチスレッドファイル変換を有効にする
description: マルチスレッドファイル変換を有効にする方法を説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 402c1fd4-c6c8-494e-b452-b56a91c4a397
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 4a55f87d3b8aa9944f0b32760aa645c42efd93e8
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 3%
---
# マルチスレッドファイル変換を有効にする {#enabling-multi-threaded-file-conversions}

PDF Generatorでは、複数のファイル変換を同時に実行して、変換スループットを向上させることができます。 該当するコンバージョンモードを選択します。

| コンバージョンモード | 同時変換をサポートするアプリケーション | ユーザーアカウントモデル |
|---|---|---|
| マルチユーザーモード | OpenOffice | 各OpenOffice インスタンスは、個別のユーザーアカウントで実行されます。 |
| シングルユーザーモード | Microsoft® WordおよびMicrosoft® Excel | 1つのユーザーアカウントで複数のWordおよびExcel インスタンスを実行します。 PowerPoint変換はシリアル化されたままです。 |

いずれかのモードを有効にする前に、使用しているアプリケーションとオペレーティングシステムの[PDF Generatorのプレインストール設定](/help/forms/using/install-configure-document-services.md#preinstallationconfigurations)を完了してください。 サポートされているアプリケーションのバージョンについては、[PDF Generatorのソフトウェアサポート &#x200B;](/help/forms/using/aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator)を参照してください。

## マルチユーザーモード {#multi-user-mode}

マルチユーザーモードでは、PDF Generatorは個別のユーザーアカウントの下で各OpenOffice インスタンスを起動します。 必要な同時コンバージョン数に対して十分な有効な管理ユーザーアカウントを設定します。 クラスター内で、各ノードで同じアカウントを設定します。

Windowsでは、PDF Generator ユーザーに[Replace a process level token権限](/help/forms/using/install-configure-document-services.md#grant-the-replace-a-process-level-token-privilege)が付与されていることを確認し、[Configure Document Services](/help/forms/using/install-configure-document-services.md#disable-user-account-control-uac)で説明されている該当するユーザーアカウント管理設定を完了してください。

### OpenOffice コンバージョン {#openoffice-conversions}

同時に実行できる各OpenOffice インスタンスに1つのPDF Generator ユーザーアカウントを設定します。 すべての設定済みユーザーがアクセスできる場所にOpenOfficeをインストールし、各ユーザーの初期OpenOffice アクティベーションダイアログを閉じます。

UNIX ベースのシステムの場合は、[Document Servicesの設定](/help/forms/using/install-configure-document-services.md#preinstallationconfigurations)でOpenOfficeのインストールとユーザー権限の要件を完了してください。

## Windowsのシングルユーザーモード {#single-user-mode-on-windows}

シングルユーザーモードでは、PDF Generatorで1つの設定されたユーザーアカウントで同時コンバージョンを実行できます。

このモードでは、Microsoft® Word （DOCおよびDOCX）とExcel （XLSおよびXLSX）の複数のインスタンスが同じユーザーで実行されます。 Microsoft® PowerPoint （PPTおよびPPTX）は、シングルユーザーモードをサポートしていません。 PDF Generatorは一度に1つのPowerPoint インスタンスのみを起動するので、PowerPoint コンバージョンはシリアル化されます。

WordとExcelの変換でシングルユーザーモードを有効にするには：

1. 管理コンソールで、**ホーム / サービス / アプリケーションとサービス / サービス管理**&#x200B;に移動します。
1. **PDF Generator**&#x200B;に対してフィルターを実行し、**GeneratePDFService**&#x200B;を選択します。
1. 「**設定**」タブで、次のオプションを設定します。

   * **Enable Single User Mode For PDFMaker**&#x200B;を&#x200B;**true**&#x200B;に設定します。
   * コンバージョンを同時に実行できるWord インスタンスの最大数に&#x200B;**PDFMaker プールサイズ**&#x200B;を設定します。
   * Native2PDF **の** Enable Single User Modeを&#x200B;**true**&#x200B;に設定します。
   * コンバージョンを同時に実行できるExcel インスタンスの最大数に&#x200B;**Native2PDF プール サイズ**&#x200B;を設定します。

1. AEM Forms サーバーを再起動します。
