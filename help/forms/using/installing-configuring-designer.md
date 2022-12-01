---
title: Designer のインストールと設定
seo-title: Installing and configuring Designer
description: WorkBench にバンドルされている Designer は、スタンドアロンのインストーラーとして使用することができます。ここでは、スタンドアロンの Designer をインストールする方法について説明します。
seo-description: Designer is available as a stand-alone installer and is also bundled with Workbench. Learn how to install stand-alone Designer.
uuid: c5b779d1-cb6a-48f4-87d6-48464753e516
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f3a5b5ce-2262-4d5d-a8ae-d59a3a4229e7
docset: aem65
role: Admin
exl-id: 90503d29-e079-43f4-a5dc-ce90ed7844c6
source-git-commit: 85189a4c35d1409690cbb93946369244e8848340
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 73%

---

# Designer のインストールと設定{#installing-and-configuring-designer}

## 前提条件 {#pre-requisites}

* 32 ビット版のをインストールする  [Visual C++ 2019 再頒布可能パッケージ (x86)](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170). インストールを開始する前に、前述の再頒布可能ランタイムパッケージがインストールされていることを確認してください。
* Designer をインストールまたはアンインストールするための管理者権限を持つユーザー。

## Designer のインストール {#install-designer}

WorkBench にバンドルされている Designer は、スタンドアロンのインストーラーとして使用することができます。Designer でスタンドアロンのインストーラーを使用する場合は、以下の手順を実行します。

1. AEM Forms Designer の以前のバージョンが既にインストールされている場合は、そのバージョンをアンインストールします。
1. 次から Designer をダウンロード： [Adobeライセンス Web サイト](https://licensing.adobe.com/).

   >[!NOTE]
   >
   > * Adobe Experience Manager 6.5 Forms Service Pack 15(6.5.15.0) 以降のForms Designer バージョンには、Service Pack バージョンも含まれています。 例えば、Service Pack 15 の場合、バージョン番号は 6.5.15.20221112.1.0です。この例では、6.5.15 が Service Pack のバージョンです。


1. setup.exe をダブルクリックして Designer のインストーラーを起動します。
1. 先に進んでユーザーの詳細とユーザー情報画面のシリアル番号を入力します。
1. 使用許諾契約に同意する場合は、「次へ」をクリックして先に進みます。
1. （オプション）Designer を選択した場所にインストールする場合は、既定のインストールパスを変更します。「次へ」をクリックします。
1. 設定を変更するには、「戻る」をクリックします。Designer をインストールするには、「インストール」をクリックします。
1. インストールが完了したら、「完了」をクリックします。

または、コマンドラインからパッシブモードまたはサイレントモードを使用して Designer をインストールすることもできます。

* パッシブコマンドラインインストール：インストーラーにインストールが進行中であることを示す進行状況バーが表示されますが、プロンプトやエラーメッセージは表示されません。起動後は、インストールをキャンセルできません。

```shell
msiexec /i "<absolute path>\Designer.msi" /passive SERIALNUMBER=****-****-****-****-****-****
```

* サイレントコマンドラインインストール：インストーラーは、ユーザーインターフェイスを表示せずにインストールを実行します。プロンプト、メッセージ、ダイアログボックスは表示されません。起動後は、インストールをキャンセルできません。

```shell
msiexec /i "<absolute path>\Designer.msi" /quiet SERIALNUMBER=****-****-****-****-****-****
```
