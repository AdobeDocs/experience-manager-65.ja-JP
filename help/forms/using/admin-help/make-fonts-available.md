---
title: フォントを使用可能にする
description: フォーム内で使用されるフォントが、AEM forms をホストする J2EE アプリケーションサーバーで使用できることを確認します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e9eae896-b1e4-4caa-b466-ac8c9e7416a4
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 25%

---

# フォントを使用可能にする {#make-fonts-available}

フォーム内で使用されるフォントが、AEM forms をホストする J2EE アプリケーションサーバーで使用できることを確認します。 例えば、次のシナリオについて考えてみます。 フォームデザイナーが、Designer が使用するフォントディレクトリにフォントを追加し、別のコンピューター上でそのフォントを使用するフォームを作成します。 Output サービスでこのフォントを使用するには、このフォントを Customer fonts ディレクトリに配置します。 カスタマーフォントディレクトリが存在しない場合は、AEM Forms をホストする J2EE アプリケーションサーバー上にディレクトリを作成します。

その他のフォント設定については、 [一般的なAEM forms の設定](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).

**カスタマーフォントディレクトリの場所を指定します**

1. 管理コンソールで、設定/コアシステム設定/設定をクリックします。
1. 「システムフォントディレクトリの場所」ボックスに、カスタマーフォントディレクトリのパスを入力します。 複数のディレクトリを追加する場合は、セミコロン **;** で区切って指定します。
1. 「OK」をクリックしてください。
1. AEM forms がインストールされているシステムを再起動します。

>[!NOTE]
>
>フォントは Windows システムのフォントキャッシュから選択され、キャッシュを更新するにはシステムを再起動する必要があります。 カスタマーフォントディレクトリを指定した後、AEM Forms をインストールしているシステムを再起動してください。
