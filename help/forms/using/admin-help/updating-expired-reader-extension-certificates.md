---
title: 期限切れの Reader Extension サービス証明書を更新しています
description: Reader 用の拡張ドキュメントが機能しません。証明書を更新してください
exl-id: 4e14e0dc-f248-4f6e-a075-6012b6792d9d
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 100%

---

# 期限切れの Reader Extension サービス証明書を更新しています {#Updating-expired-Reader-Extension-service-certificates}

Adobe Experience Manager Forms（AEM Forms）をご利用のお客様で、Adobe Managed Services またはオンプレミスの Enterprise Base ライセンスをお持ちの場合、Reader Extension サービスを使用する資格があります。サービスを使用すると、追加の使用権限を付与して Adobe Reader の機能を拡張することで、組織内でインタラクティブ PDF ドキュメントを簡単に共有できます。このサービスは、PDF ドキュメントに使用権限を追加し、ドキュメントへのコメントの追加、フォームへの入力、ドキュメントの保存など、Adobe Acrobat Reader DC を使用して PDF ドキュメントを開いた場合には通常使用できない機能をアクティブにします。サードパーティユーザーは、使用権限を付与されたドキュメントを扱うためにソフトウェアまたはプラグインを追加する必要はありません。使用権限が追加された PDF ドキュメントは、「使用権限を付与されたドキュメント」と呼ばれます。使用権限を付与された PDF ドキュメントを Adobe Reader で開いたユーザーは、そのドキュメントで有効になっている操作を実行できます。

アドビは PKI（公開鍵インフラストラクチャ）を活用して、ライセンスやイネーブルメント機能に使用する電子証明書を発行します。アドビは、認証機関「Adobe ルート CA」に基づいて証明書を発行しており、2023 年 1 月 7 日に期限が切れる予定です。この認証機関の下で発行されたすべての証明書の有効期限が切れます。証明書の有効期限が切れると、証明書に依存するすべての機能は機能しなくなります。例えば、Adobe Acrobat Reader を使用してコメントを追加できる Reader 用の拡張 PDF ドキュメントは、2023 年 1 月 7 日以降、機能しなくなります。この問題を解決するには、Reader Extension サービスの管理者は、古い証明書を使用して、新しい Adobe Root CA G2 が発行した新しい証明書を取得し、PDF ドキュメントに再適用する必要があります（Reader は、新しい証明書で PDF ドキュメントを拡張します）。

証明書の有効期限は、JEE 上の AEM Forms と OSGi スタック上の AEM Forms の両方に影響します。両方のスタックには、異なる手順のセットがあります。[前提条件](#Pre-requisites)および[新しい証明書の取得](#obtain-the-certificates)を満たした後、スタックに応じて、次のパスのいずれかを選択します。

* [JEE 環境上の AEM Forms の証明書の更新](#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment)
* [OSGi 環境上の AEM Forms の証明書の更新](#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment)

>[!NOTE]
>
>このドキュメントでは、用語の証明書と資格情報が互換的に使用されています。

## 前提条件 {#Pre-requisites}

証明書を更新するには、AEM Forms 管理者コンソールで使用できるアクションと、AEM Forms が提供する Reader Extension API を使用する必要があります。このドキュメントは、Adobe Experience Manager Forms API の使用に関する知識を持つユーザーおよび管理者を対象としています。開始する前に、次のことを確認します。

* ユーザーには、基になる AEM Forms 環境の管理者権限があります。
* ユーザーが[開発環境](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/howto-projects-eclipse.html?lang=ja)を設定し、それにアクセスできます。
* 証明書を取得できます。

### 証明書を取得する {#obtain-the-certificates}

使用権限秘密鍵証明書は、公開鍵と秘密鍵の両方を含んでいる電子証明書、および秘密鍵証明書にアクセスするためのパスワードとして提供されます。

Reader Extensions 製品版を購入した場合、実稼働環境用の使用権限秘密鍵証明書は、アドビライセンス web サイト（LWS）によって配信されます。実稼働環境用の使用権限秘密鍵証明書は、組織に固有のものであり、必要とする特定の使用権限を有効にすることができます。

Reader Extensions を各自のソフトウェアに統合したパートナーまたはソフトウェアプロバイダーを通じて Reader Extensions を入手した場合、使用権限秘密鍵証明書は、アドビからパートナーに提供され、その後パートナーからお客様に提供されます。

>[!NOTE]
>
>使用権限秘密鍵証明書は、一般的なドキュメントの署名や識別情報のアサーションには使用できません。これらの場合は、自己署名証明書を使用するか、認証局（CA）から識別情報証明書を取得してください。

次のタイプの使用権限秘密鍵証明書を取得できます。

**Customer Evaluation（カスタマー評価用）**：Reader Extensions を評価するお客様に提供される、有効期限が短い秘密鍵証明書。この秘密鍵証明書を使用してドキュメントに適用されている使用権限は、証明書の有効期限が切れると失効します。この種類の秘密鍵証明書は、2 ～ 3 か月間のみ有効です。

**Production（実稼働環境用）**：フル製品を購入したお客様に提供される、有効期間が長い秘密鍵証明書。Production（実稼働環境用）証明書は、ユーザーごとに固有ですが、複数のシステムにインストールできます。

Reader 用の証明書を既に使用して PDF ファイルを拡張している場合は、実稼働用の証明書を[アドビライセンス web サイト（LWS）](https://licensing.adobe.com/)からダウンロードできます。

## JEE 環境上の AEM Forms の証明書の更新と適用 {#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment}

JEE スタック上の AEM Forms で新しい証明書を更新および適用するには、新しい資格情報の読み込み、既存の PDF ドキュメントからの使用権限の削除、使用権限の適用が必要です。Admin Console を使用して資格情報を読み込み、AEM Forms Reader Extension API を使用して使用権限を削除および適用できます。

### 資格情報のインポートと設定

Trust Store の管理ページを使用して、新しい資格情報や置き換え用の資格情報をインポートすることができます。Trust Store には複数の Reader Extensions 証明書が含まれることがあります。これらの証明書の 1 つを、デフォルトの Reader Extensions 証明書として指定する必要があります。デフォルトの証明書は、Workbench ユーザーがプロセス作成時に、どの証明書を使用するかを判断できない場合に使用されます。デフォルトの証明書には以下の規則が適用されます。

*  Reader エクステンション証明書をインポートする際に、Trust Store に Reader Extensions 証明書が 1 つしか含まれていない場合は、その証明書がデフォルトとして設定されます。
* 「デフォルト」オプションを選択して Reader Extensions 証明書をインポートすると、既存のデフォルトの証明書からデフォルトタイプが削除されます。読み込まれた証明書がデフォルトになります。
* デフォルトの Reader Extensions 証明書は削除できません。デフォルトの証明書を削除するには、最初に、他の証明書をデフォルトとして設定します。ただし、証明書が 1 つしかない場合は例外で、デフォルトの証明書でも削除できます。
* デフォルトの Reader Extensions 証明書は更新できません。

資格情報をインポートするには、以下の手順に従います：

1. 管理コンソールで、設定／Trust Store の管理／ローカル秘密鍵証明書をクリックします。
1. 「読み込み」をクリックし、「Trust Store の種類」で「Acrobat Reader DC Extensions 証明書」を選択します。
1. （オプション）この証明書を Acrobat Reader DC Extensions のデフォルトの証明書として指定するには、「デフォルト」を選択します。
1. 「エイリアス」ボックスに、証明書の ID を入力します。この ID は、Acrobat Reader DC Extensions で証明書の表示名として使用されます。このエイリアスは、AEM Forms SDK を使用してプログラムから証明書にアクセスするときにも使用されます。
1. 「ファイルを選択」をクリックして証明書を探し、証明書のパスワードを入力して「OK」をクリックします。

「形式が正しくないか、パスワードが正しくないため、証明書を読み込めませんでした」というエラーメッセージが表示される場合は、パスワードが有効であることを確認してください。

プログラムによって証明書を読み込んだり、削除したりすることもできます（「[AEM Forms によるプログラミング](../../developing/credentials.md)」を参照してください。）

### 使用権限を付与された既存の PDF ドキュメントから使用権限を削除

最新の資格情報を使用して使用権限を適用する前に、使用権限を付与された既存の PDF ドキュメントから使用権限を削除してください。JEE 上の AEM Forms は、使用権限を削除する API を提供します。詳しい手順については、[PDF ドキュメントから使用権限の削除](../../developing/assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)を参照してください。

Workbench で開発した JEE プロセス上の AEM Forms の使用権限を削除するには、[Workbench ヘルプ](https://helpx.adobe.com/content/dam/help/ja/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf)を参照してください。

### 使用権限を PDF ドキュメントに適用する

新しい資格情報を読み込み、既存の権限が付与された PDF ドキュメントから使用権限を削除した後、新しい資格情報を使用して PDF ドキュメントに使用権限を適用してください。Acrobat Reader DC エクステンション Java クライアント API および web サービスを使用すると、PDF ドキュメントに使用権限を適用することができます。詳しくは、[PDF ドキュメントへの使用権限の適用](../../developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)を参照してください。


## OSGi 環境での AEM Forms の証明書の更新と適用 {#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment}

OSGi スタック上の AEM Forms で新しい証明書を更新および適用するには、新しい資格情報の読み込み、既存の PDF ドキュメントからの使用権限の削除、使用権限の適用が必要です。Admin Console を使用して資格情報を読み込み、AEM Forms Reader Extension API を使用して使用権限を削除および適用できます。

### 認証情報の読み込み {#Import-credentials}

OSGi 環境の AEM Forms では、Reader Extension 資格情報が fd-service ユーザーに関連付けられます。fd-user キーストアの資格情報を追加する前に、次の手順を実行してキーストアを作成してください。

1. AEM オーサーインスタンスに管理者としてログインします。
1. **[!UICONTROL ツール]**／**[!UICONTROL セキュリティ]**／**[!UICONTROL ユーザー]**&#x200B;に移動します。
1. fd-service ユーザーアカウントが見つかるまで、ユーザーのリストを下にスクロールします。
1. **[!UICONTROL fd-service]** ユーザーをクリックします。
1. 「キーストア」タブをクリックします。
1. **[!UICONTROL キーストアを作成]**&#x200B;をクリックします。
1. キーストアアクセスパスワードを設定し、設定を保存してキーストアパスワードを作成してください。

キーストアを作成した後、fd-service ユーザーに資格情報を追加してください。次のビデオでは、手順を説明しています。

>[!VIDEO](https://images-tv.adobe.com/mpcv3/5577/8db8e554-f04b-4fae-8108-b9b5e0eb03ad_1627925794.854x480at800_h264.mp4)

次のコマンドは、pfx ファイルの詳細を一覧表示します。コマンドを実行する前に、.pfx ファイルを含むディレクトリに移動します。

`keytool -v -list -storetype pkcs12 -keystore <name of your .pfx file>`

例えば、keytool -v -list -storetype pkcs12 -keystore 1005566.pfx の場合、1005566.pfx はご使用の pfx ファイルの名前です。

### 使用権限を付与された既存の PDF ドキュメントから使用権限を削除

最新の資格情報を使用して使用権限を適用する前に、使用権限を付与された既存の PDF ドキュメントから使用権限を削除してください。docAssuranceServiceAPI から removeUsageRights API を呼び出すことによって、ドキュメントの使用権限を削除できます。詳しくは、[使用権限の削除](/help/forms/using/aem-document-services-programmatically.md#removing-usage-rights)ドキュメントを参照してください。

### 使用権限を PDF ドキュメントに適用する

OSGi 環境上の AEM Forms で使用権限を適用するには、カスタム OSGi サービスを作成して、ドキュメントに使用権限を付与してください。また、POST メソッドを使用してサーブレットを作成し、Reader 用の拡張 PDF をユーザーに返すこともできます。詳しい手順については、 [Reader Extensions の適用](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/document-services/apply-reader-extension-rights-to-pdf.html?lang=ja)を参照してください。

## よくあるご質問

**他に質問がある場合、誰に問い合わせればよいですか？**

[アドビサポート](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=ja#support)に連絡するか、またはサポートチケットを発行してください。

**2023 年 1 月 7 日より前に証明書を更新しない場合はどうなりますか？**

古い証明書で Reader 用の拡張 PDF ドキュメントを開こうとすると、エラーメッセージが表示され、読み取り用の拡張機能にアクセスできなくなります。エラーの例です。

`The document has been changed since it was created and use of extended features in no longer available. Please contact the author for the orignal version of this document.`

**新しい説明の名前に何か変更はありますか？**

新しい Reader Extension の証明書では、説明内でプログラム名として G3-P24 が挙げられています。古い証明書では、説明内に P24 というプログラム名が記載されていました。
