---
title: 設定ファイルの読み込みと書き出し
description: 設定ファイルを読み込んで書き出し、サーバーの環境設定を編集する方法、または別のAEM forms 製品インスタンスを設定する方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 225dbeb5-a21c-4338-98c7-e10c32973721
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 4%

---

# 設定ファイルの読み込みと書き出し {#importing-and-exporting-the-configuration-file}

手動設定ページを使用して、設定のコピーを XML 形式でダウンロードします。 このファイルの設定は、すべてのサーバの環境設定を制御します。 その後、ファイルを編集し、サーバーにアップロードし直すことができます。 また、このファイルを使用して、別のAEM forms 製品インスタンスを設定することもできます。

セキュリティ上の問題を回避するために、ディレクトリサーバーのバインドパスワード値は、書き出された設定ファイルに含まれません。 ファイルを新しいシステムに読み込む前に、XML ファイル内のパスワードを更新します。

>[!NOTE]
>
>設定ファイルを読み込むと、ファイル内の情報に基づいてAEM forms が再設定されます。 設定ファイルの変更を検討するのは、AEM forms 製品および XML に詳しいシステム管理者またはプロフェッショナルサービスコンサルタントのみです。 例えば、破損した設定を再構成する場合に、設定ファイルを編集する必要が生じる場合があります。

**設定情報の書き出し**

1. 管理コンソールで、設定/User Management/設定/設定ファイルの読み込みと書き出しをクリックします。
1. 「書き出し」をクリックします。 Microsoft Internet Explorer を使用している場合は、ファイルを保存する場所を指定するよう求められます。 Firefox を使用している場合、ファイルはデスクトップに保存されます。

**設定情報の読み込み**

1. 管理コンソールで、設定/User Management/設定/設定ファイルの読み込みと書き出しをクリックします。
1. 「参照」をクリックして設定ファイルを探し、「読み込み」をクリックして、「OK」をクリックします。
