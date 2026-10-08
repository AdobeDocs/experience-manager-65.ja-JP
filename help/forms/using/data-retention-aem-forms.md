---
title: AEM Formsでのデータ保持
description: Adobe Experience Manager（AEM）Formsは、デフォルトではパススルーサーバーとして機能し、フォームエンドユーザーデータを保存せず、データプライバシーをサポートする仕組みについて説明します。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin, User
solution: Experience Manager Forms
feature: Adaptive Forms
source-git-commit: ca1448119778a2bcfeca7189aab5b360d992d99d
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 2%
---
# AEM Formsにおけるデータ保持 {#data-retention-in-aem-forms}

AEM Formsはフォームデータを保存しますか？ デフォルトでは、いいえ。 Adobe Experience Manager（AEM） Formsは、アダプティブFormsを介してキャプチャされたデータのパススルーサーバーとして機能し、エンドユーザーデータをAEM リポジトリに保存しません。 代わりに、サーバーは送信されたデータを所有および設定する宛先に渡します。 このデフォルトの動作は、データプライバシーとコンプライアンスの目標を達成するのに役立ちます。これは、OSGi上のAEM FormsとJEE上のAEM Formsの両方に適用されます。

AEM Formsは拡張可能な基盤であるため、AEMをカスタマイズして、このデフォルトのビヘイビアーを変更できます。 アダプティブフォームを通じて送信されたデータをAEM リポジトリに保存したり、AEM ログに書き込んだりする場合は、そのようなデータが実稼動システムやステージングシステムに保持されないようにする必要があります。

## すぐに使用できる機能を備えたデフォルトの動作 {#default-behavior}

標準のアダプティブ Forms機能を使用する場合、AEM Formsにはエンドユーザーデータは保存されません。 サーバーは、送信されたデータを、所有および設定する宛先に直接渡します。

フォームを独自の宛先に接続するすぐに利用できるメカニズムには、フォームデータモデル（FDM）、すぐに利用できるコネクタ、送信アクションなどがあります。 これらは、それぞれが所有および設定する場所にデータを送信するので、AEM リポジトリには保持されません。 フォームは、ルールまたは送信アクションからREST APIなどの外部サービスまたはサードパーティサービスを呼び出し、AEMのデータを保持することなく、そのサービスにデータを転送することもできます。

承認手順を含む長期間有効なプロセスでAEM ワークフローを使用する場合、AEM Formsは、操作を完了するためにデータをメモリおよび一時的なストレージに保持する場合があります。 このデータがAEMに保存されないようにする方法について詳しくは、[長期間有効なワークフロープロセスのデータ &#x200B;](#long-lived-workflow-processes)の節を参照してください。

Forms ポータルの送信アクションでは、アダプティブ Formsを介してキャプチャまたは送信されたデータは保持されますが、データはAEM リポジトリやログではなく、指定して所有する保存場所に保存されます。 詳細については、「[&#x200B; フォームポータルによって保存されたデータの保護アクション &#x200B;](/help/forms/using/hardening-securing-aem-forms-environment.md#secure-data-saved-by-forms-portal-submit-action)」を参照してください。

## 転送中のデータ {#data-in-transit}

AEM Formsでは、デフォルトではエンドユーザーのデータは保存されませんが、エンドユーザー、AEM Forms、および設定した宛先の間でデータが移動します。 転送中にデータが暗号化されるように、Transport Layer Security （TLS）でこのトラフィックを保護します。

ブラウザーとAEM間の接続を保護するには、AEM インスタンスでHTTPSを有効にします。 手順については、「[SSL/TLS デフォルト設定](/help/sites-administering/ssl-by-default.md)」を参照してください。

さらに、クラウド設定、送信アクション URL、フォームデータモデルのデータソースなど、AEM Formsがデータを送信するエンドポイントが安全なHTTPS エンドポイントを使用していることを確認します。 AEM Formsは通過するデータを保存しないため、保存中の暗号化はそのデータに適用されません。 接続の保護に関する詳細なガイダンスについては、[&#x200B; トランスポート層の保護](/help/forms/using/hardening-securing-aem-forms-environment.md#secure-transport-layer)を参照してください。

## 外部データストアのフォームデータモデル {#form-data-model}

データストアにデータを読み書きするには、フォームデータモデル（FDM）を使用します。 FDMは、データベースやRESTful web サービスなど、所有および管理するデータソースにフォームを接続する際に推奨されるメカニズムです。

詳しくは、[AEM Forms Data Integrationの概要](/help/forms/using/data-integration.md)を参照してください。 FDMが処理するデータの保護に関するガイダンスについては、[&#x200B; フォームデータモデル（FDM）で処理されるデータの保護](/help/forms/using/hardening-securing-aem-forms-environment.md#secure-data-handled-by-form-data-model-fdm)を参照してください。

## 長期間有効なワークフロープロセスのデータ {#long-lived-workflow-processes}

長期間有効なワークフロープロセスを使用する場合、AEMは、ワークフローペイロードの一部としてデータを一時的に保存できます。 このペイロードを含むワークフロー変数は、AEM リポジトリのワークフローインスタンスのメタデータに保存され、アダプティブフォームの入力時にエンドユーザーから提供された個人情報（PII）または機密性の高い個人データ（SPD）を含めることができます。

このデータを、AEMではなくAzure Blob Storageなどの所有および管理できるリポジトリに保存するには、AEMのデータ外部化機能を使用します。 変数を外部化すると、データはAEM リポジトリに保存されず、代わりに独自のデータリポジトリに保存されます。

データを外部化する手順については、[機密データをワークフロー変数にパラメーター化し、外部データストアに保存する](/help/forms/using/aem-forms-workflow.md#externalize-wf-variables)を参照してください。

## カスタマイズとログ {#customization-and-logging}

AEMを利用すれば。 AEMをカスタマイズする場合は、AEM リポジトリまたはログにデータが保存されていないことを確認します。

デフォルトの機能を使用する場合、AEM Formsはフォームのエンドユーザーデータをログに書き込みません。

カスタムコードは、ログにデータを書き込むことができます。 開発中にトレースまたはログを追加する場合は、コードをステージング環境と実稼動環境にデプロイする前に、ログに送信されたトレースとデータを削除します。

## AEM Forms Data retentionに関するよくある質問 {#faq}

**AEM Formsはフォームデータを保存しますか？**

いいえ。 デフォルトでは、Adobe Experience Manager（AEM）Formsは、アダプティブFormsを通じてキャプチャされたデータのパススルーサーバーとして機能し、エンドユーザーデータをAEM リポジトリに保存しません。 サーバーは、送信されたデータを、フォームデータモデルデータソース、送信アクションターゲット、外部APIなど、所有および設定する宛先に渡します。 このデフォルトのビヘイビアーは、OSGi上のAEM FormsとJEE上のAEM Formsの両方に適用されます。

**アダプティブフォームデータはどこに保存されますか？**

送信されたアダプティブフォームデータは、Adobe Experience Manager（AEM）リポジトリではなく、所有および設定する宛先に保存されます。 フォームデータモデル（FDM）、コネクタ、送信アクションなど、すぐに利用できるメカニズムにより、データを独自の場所に送信できます。 フォームは、AEMにデータを保持することなく、REST APIなどの外部サービスにデータを転送することもできます。 Forms ポータルの送信アクションは、提供および所有する保存場所にもデータを保存します。

**長期間有効なワークフローはフォームデータを保存しますか？**

Adobe Experience Manager（AEM）の長期間有効なワークフロープロセス Formsでは、ワークフローペイロードの一部としてデータを一時的に保存できます。このデータは、AEM リポジトリのワークフローインスタンスのメタデータに保存されます。 このデータを、AEMではなくAzure Blob Storageなどの所有および管理するリポジトリに保存するには、ワークフロー変数[&#128279;](/help/forms/using/aem-forms-workflow.md#externalize-wf-variables)にAEM データ外部化機能を使用します。

**AEM Formsはデータをログに書き込みますか？**

いいえ。 デフォルトの機能では、Adobe Experience Manager（AEM）Formsはフォームのエンドユーザーデータをログに書き込みません。 AEMはカスタマイズ可能な基盤であるため、カスタムコードを使用してデータをログに書き込むことができます。 開発中にトレースまたはログを追加する場合は、ステージング環境と実稼動環境にデプロイする前に、これらのトレースとログに記録されたデータを削除します。 AEM リポジトリまたはログにデータを保存することはできません。

**転送中のデータはどのように保護されますか？**

転送中のデータは、Adobe Experience Manager（AEM）FormsのTransport Layer Security （TLS）で保護されています。 AEM インスタンスでHTTPSを有効にして、ブラウザーとAEM間の接続を保護します。 さらに、クラウド設定、送信アクション URL、フォームデータモデルのデータソースなど、AEM Formsがデータを送信するエンドポイントが安全なHTTPS エンドポイントを使用していることを確認します。 AEM Formsは通過したデータを保存しないため、保存中の暗号化はそのデータに適用されません。

## 関連リソース {#related-resources}

* [AEM Forms データ統合機能の概要](/help/forms/using/data-integration.md)
* [機密データをワークフロー変数にパラメーター化し、外部データストアに保存](/help/forms/using/aem-forms-workflow.md#externalize-wf-variables)
* [送信アクションの設定](/help/forms/using/configuring-submit-actions.md)
* [OSGi環境でのAEM Formsの強化と保護](/help/forms/using/hardening-securing-aem-forms-environment.md)
