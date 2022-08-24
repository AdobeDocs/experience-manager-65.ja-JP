---
title: Designer のインストールと設定
seo-title: Installing and configuring Designer
description: 'WorkBench にバンドルされている Designer は、スタンドアロンのインストーラーとして使用することができます。ここでは、スタンドアロンの Designer をインストールする方法について説明します。  '
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
source-git-commit: a3cf926bde4a4b3a0810058e84ac01012a4a3a57
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 100%

---

# Designer のインストールと設定{#installing-and-configuring-designer}

## 前提条件 {#pre-requisites}

AEM Forms Designer インストーラーを実行するには、32 ビット版の [Visual C++ 再頒布可能ランタイムパッケージ 2012](https://support.microsoft.com/ja-jp/topic/the-latest-supported-visual-c-downloads-2647da03-1eea-4433-9aff-95f26a218cc0) と [Visual C++ 再頒布可能ランタイムパッケージ 2013](https://support.microsoft.com/ja-jp/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package) が必要です。インストールを開始する前に、前述の再頒布可能ランタイムパッケージがインストールされていることを確認してください。

Designer をインストールまたはアンインストールするには、管理者権限が必要です。

## Designer のインストール {#install-designer}

WorkBench にバンドルされている Designer は、スタンドアロンのインストーラーとして使用することができます。Designer でスタンドアロンのインストーラーを使用する場合は、以下の手順を実行します。

1. アドビ[ライセンス web サイト](https://licensing.adobe.com/)から Designer をダウンロード してください。

   >[!NOTE]
   >
   >旧バージョンの Designer がインストールされている場合は、そのバージョンをアンインストールしてから、以下の手順を実行してください。

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


