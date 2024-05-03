---
title: AEM 翻訳ワークフローを使用したアダプティブフォームとレコードのドキュメントのローカライズ
description: AEM 翻訳ワークフローを使用してアダプティブフォームとレコードのドキュメントをローカライズする方法について説明します。
content-type: reference
topic-tags: develop
noindex: true
feature: Adaptive Forms, Foundation Components
exl-id: ebec03a3-67a0-4ecd-84bb-8580388e048a
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 100%

---

# AEM 翻訳ワークフローを使用したアダプティブフォームとレコードのドキュメントのローカライズ {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

<span class="preview">[アダプティブフォームの新規作成](/help/forms/using/create-an-adaptive-form-core-components.md)または [AEM Sites ページへのアダプティブフォームの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)には、最新の拡張可能なデータキャプチャ[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)を使用することをお勧めします。これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を表し、ユーザーエクスペリエンスの向上を実現します。この記事では、基盤コンポーネントを使用してアダプティブフォームを作成する古い方法について説明します。</span>

フォームのローカライズにより、様々な地域の幅広い対象者に向けてフォームを提供できるようになります。アダプティブフォームおよびレコードのドキュメントをローカライズするには、Adobe Experience Manager 翻訳ワークフローが役立ちます。アダプティブフォームのローカライズには、**機械翻訳**&#x200B;または&#x200B;**人間による翻訳**&#x200B;を使用できます。

この記事では、アダプティブフォームおよびレコードのドキュメントで AEM 翻訳ワークフローを使用する手順について説明します。

## 機械翻訳によるアダプティブフォームおよびレコードのドキュメントのローカライズ {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

機械翻訳サービスを使用すると、アダプティブフォームおよびレコードのドキュメントを即座に翻訳することができます。AEM Forms では、機械翻訳に Microsoft Translator の体験版を使用することが事前に定義されています。アダプティブフォームおよびレコードのドキュメントの機械翻訳を有効にするには、次の手順を実行します。

1. AEM Forms UI 上でフォームを選択し、「**辞書を追加**」オプションを選択します。
1. **辞書を翻訳プロジェクトに追加** 画面で、「**新しい翻訳プロジェクトを作成**」または「**既存の翻訳プロジェクトを追加**」オプションを選択します。
1. 「**プロジェクトタイトル**」フィールドでタイトルを指定します。例：`Government Reference Site - German locale.`
1. 「**ターゲット言語**」フィールドでロケールを指定し（例えば `German(de)` と入力します）、「**完了**」をクリックします。複数のロケールを指定できます。フォームは、**ターゲット言語**&#x200B;フィールドに指定されたすべてのロケールに翻訳されます。
1. 辞書が追加された際のダイアログボックスで、「**プロジェクトを開く**」をクリックします。プロジェクト画面で、新しく作成したプロジェクトを開きます。
1. 「**翻訳の概要**」タイルの下部にある&#x200B;**省略記号**&#x200B;をクリックします。翻訳の概要画面が開きます。
1. **翻訳の概要**&#x200B;の上部にある&#x200B;**編集**&#x200B;アイコンをクリックします。「**翻訳**」タブを開き、 **翻訳方法** 画面で機械翻訳を選択します。適切な **翻訳プロバイダー** と **クラウド設定** を選択します。画面の上部にある「**完了**」アイコンをクリックします。
1. **翻訳ジョブ**&#x200B;タイルで ![aem62forms_downarrow](assets/aem62forms_downarrow.png) アイコンをクリックし、「**開始**」をクリックします。タイルのステータスがドラフトに変わります。翻訳が完了すると、ステータスは「**レビューへの準備完了**」に変わります。数分後にページを更新し、ステータスを確認します。
1. **翻訳ジョブ**&#x200B;タイルのステータスが&#x200B;**レビューへの準備完了**&#x200B;に変わったことを確認できたら、ブラウザーウィンドウでフォームを開きます。フォームのローカライズ版が表示されます。

   >[!NOTE]
   >
   >* ブラウザーウィンドウでローカライズ版のフォームを開く前に、ブラウザーのロケールがフォームのロケールと一致するように設定されていることを確認します。例えば、フォームがドイツ語（de）に翻訳されている場合は、ブラウザーのロケールをドイツ語（de）に設定します。
   >* アダプティブフォームコンポーネントは、右から左に筆記する言語（RTL）をサポートしていません。例：ヘブライ語

   アダプティブフォームと共に、自動生成されるレコードのドキュメントもローカライズされます。

   レコードのドキュメントの設定と構成について詳しくは、以下を参照してください。

[レコードのドキュメントのテンプレート設定](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

[レコードのドキュメントの設定](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [レコードのドキュメントのブランディング情報をカスタマイズ](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)し、ブラウザーのロケールを、機械語を使用してアダプティブフォームをローカライズした言語と同じ言語に設定します。ブラウザーのロケールは、レコードのドキュメントにあるブランディング情報のローカライズに役立ちます。
1. ローカライズされたレコードのドキュメントを表示するには、「プレビューを生成」を選択します。レコードのドキュメントの PDF が生成され、ブラウザーの新しいタブに表示されます。

## 人間による翻訳を使用した、アダプティブフォームおよびレコードのドキュメントのローカライズ {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

人間による翻訳を使用すると、コンテンツは翻訳プロバイダーに送信され、専門の翻訳者によって翻訳が行われます。完了すると、翻訳コンテンツが返され、AEM に読み込まれます。翻訳プロバイダーが AEM と統合されると、AEM と翻訳プロバイダーとの間でコンテンツが自動的に送信されます。

翻訳では、XLIFF 形式のファイルを含む辞書が専門の翻訳者と共有されます。この辞書には、ロケールごとに個別の XLIFF ファイルが含まれます。各 XLIFF には、エンドユーザーに表示されるテキストと、対応するローカライズ済みのテキストのプレースホルダ―が含まれます。

人間による翻訳を使用してフォームとレコードのドキュメントをローカライズするには、次の手順を実行します。

1. [AEM を翻訳プロバイダーサービスに接続](/help/sites-administering/tc-tic.md)して、[翻訳統合フレームワーク設定を作成](/help/sites-administering/tc-tic.md)します。

1. 翻訳サービスとフレームワークの設定に[言語マスターのページを関連付け](/help/sites-administering/tc-tic.md)ます。

1. 翻訳する[コンテンツのタイプを特定](/help/sites-administering/tc-rules.md)します。

1. [翻訳するコンテンツを準備](/help/sites-administering/tc-prep.md)します。そのためには、言語マスターをオーサリングして、言語コピーのルートページを作成します。

1. [翻訳プロジェクトを作成](/help/sites-administering/tc-manage.md)して、翻訳するコンテンツを収集し、翻訳プロセスを準備します。

1. 翻訳プロジェクトを使用して、[コンテンツの翻訳プロセスを管理](/help/sites-administering/tc-manage.md)します。

>[!NOTE]
>
>* アダプティブフォームコンポーネントは、右から左に筆記する言語（RTL）をサポートしていません。例：ヘブライ語。
>
