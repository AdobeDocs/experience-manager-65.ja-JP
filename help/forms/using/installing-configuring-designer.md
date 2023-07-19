---
title: Designer のインストールと設定
seo-title: Installing and configuring Designer
description: WorkBench にバンドルされている Designer は、スタンドアロンのインストーラーとして使用することができます。スタンドアロン Designer のインストール方法を説明します。
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
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 96%

---

# Designer のインストールと設定{#installing-and-configuring-designer}

## 前提条件 {#pre-requisites}

* 32 ビット版の [Visual C++ 2019 再頒布可能パッケージ（x86）](https://learn.microsoft.com/ja-jp/cpp/windows/latest-supported-vc-redist?view=msvc-170)をインストールします。インストールを開始する前に、前述の再頒布可能ランタイムパッケージがインストールされていることを確認してください。
* AEM Forms Designer をインストールまたはアンインストールするには、管理者権限を持っている必要があります。

## AEM Forms Designer のインストール {#install-designer}

WorkBench にバンドルされている Designer は、スタンドアロンのインストーラーとして使用することができます。AEM Forms Designer でスタンドアロンのインストーラーを使用する場合は、以下の手順を実行します。

1. AEM Forms Designer の以前のバージョンが既にインストールされている場合は、そのバージョンをアンインストールします。
1. [アドビライセンス web サイト](https://licensing.adobe.com/)から Designer をダウンロードします。

   >[!NOTE]
   >
   > * Adobe Experience Manager 6.5 Forms サービスパック 15（6.5.15.0）以降の Forms Designer バージョンには、サービスパックバージョンも含まれています。例えば、サービスパック 15 の場合、バージョン番号は 6.5.15.20221112.1.0 です。この例では、6.5.15 がサービスパックのバージョンです。

1. setup.exe をダブルクリックして、AEM Forms Designer のインストーラーを起動します。
1. 続行して、「パーソナライズ機能」画面で詳細とシリアル番号を入力します。
1. 使用許諾契約に同意する場合は、「次へ」をクリックして先に進みます。
1. （オプション）Designer を選択した場所にインストールする場合は、既定のインストールパスを変更します。「次へ」をクリックします。
1. 設定を変更するには、「戻る」をクリックします。Designer をインストールするには、「インストール」をクリックします。
1. インストールが完了したら、「完了」をクリックします。

または、コマンドラインからパッシブモードもしくはサイレントモードを使用して AEM Forms Designer をインストールすることもできます。

* パッシブコマンドラインインストール：インストーラーにインストールが進行中であることを示す進行状況バーが表示されますが、プロンプトやエラーメッセージは表示されません。起動後は、インストールをキャンセルできません。

```shell
msiexec /i "<absolute path>\Designer.msi" /passive SERIALNUMBER=****-****-****-****-****-****
```

* サイレントコマンドラインインストール：インストーラーは、ユーザーインターフェイスを表示せずにインストールを実行します。プロンプト、メッセージ、ダイアログボックスは表示されません。起動後は、インストールをキャンセルできません。

```shell
msiexec /i "<absolute path>\Designer.msi" /quiet SERIALNUMBER=****-****-****-****-****-****
```

## AEM Forms Designer の更新 {#update-forms-designer}

AEM Forms Designer 6.5.16.0 の最新バージョンの更新する場合、次の 2 つのケースがあります。

* **ケース 1**：ユーザーの AEM Forms Designer バージョンが 6.5.15.0 より前の場合。
* **ケース 2**：ユーザーの AEM Forms Designer のバージョンが 6.5.15.0 の場合。

+++**ユーザーの AEM Forms Designer のバージョンが 6.5.15.0 より前の場合。**

AEM Forms Designer でスタンドアロンのインストーラーを使用する場合は、以下の手順を実行します。

1. **AEM Forms Designer 6.5.16.0** をインストールする前に、以前のバージョンをアンインストールする必要があります。
1. AEM Form のリリースページから [AEM Forms Designer 6.5.15.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja) をダウンロードしてインストールします。
1. **AEM Forms Designer 6.5.15.0** のインストールが完了したら、[AEM Forms Designer 6.5.16.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja) をダウンロードし、ダウンロードしたインストーラーファイルをダブルクリックしてインストールします。

+++

+++**ユーザーの AEM Forms Designer のバージョンが 6.5.15.0 の場合**

AEM Forms Designer でスタンドアロンのインストーラーを使用する場合は、以下の手順を実行します。
1. [ソフトウェア配布ポータル](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja)から最新バージョンの AEM Forms Designer をダウンロードします。
1. ダウンロードしたインストーラーファイルをダブルクリックして、最新バージョンのAEM Forms Designer をインストールします。

+++