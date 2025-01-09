---
title: フォントを使用可能にする
description: フォーム内で使用されているフォントが、AEM Forms をホストする J2EE アプリケーションサーバーで使用できることを確認します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e9eae896-b1e4-4caa-b466-ac8c9e7416a4
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '228'
ht-degree: 100%

---

# フォントを使用可能にする {#make-fonts-available}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

フォーム内で使用されているフォントが、AEM Forms をホストする J2EE アプリケーションサーバーで使用できることを確認します。例えば、次のようなシナリオが考えられます。フォームデザイナーが、Designer で使用するフォントをフォントディレクトリに追加し、そのフォントを使用するフォームを別のコンピューターで作成します。Output サービスでそのフォントを使用するには、カスタマーフォントディレクトリにフォントを配置します。カスタマーフォントディレクトリが存在しない場合は、AEM Forms をホストする J2EE アプリケーションサーバー上にディレクトリを作成します。

その他のフォント設定について詳しくは、[一般的な AEM Forms の設定](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)を参照してください。

**カスタマーフォントディレクトリの場所の指定**

1. 管理コンソールで、設定／コアシステム設定／設定をクリックします。
1. システムフォントディレクトリの場所ボックスにカスタマーフォントディレクトリのパスを入力します。複数のディレクトリを追加する場合は、セミコロン **;** で区切って指定します。
1. 「OK」をクリックしてください。
1. AEM Forms がインストールされているシステムを再起動します。

>[!NOTE]
>
>フォントは Windows システムのフォントのキャッシュから選択されます。キャッシュを更新するにはシステムを再起動する必要があります。カスタマーフォントディレクトリを指定した後、AEM Forms をインストールしているシステムを再起動してください。
