---
title: 期限切れのReader拡張サービス証明書を更新しています
description: 'Readerの拡張ドキュメントが機能しません。証明書を更新してください '
source-git-commit: 5f2fc6a32f67cfed3bc4b09b63bcf9689659a99d
workflow-type: tm+mt
source-wordcount: '1572'
ht-degree: 24%

---


# 期限切れのReader拡張サービス証明書を更新しています {#Updating-expired-Reader-Extension-service-certificates}

Adobe Experience Manager Forms(AEM Forms) をご利用のお客様は、Adobe Managed Services またはオンプレミスの Enterprise Base ライセンスを持っている場合、Reader拡張サービスを使用する資格があります。 このサービスを使用すると、追加の使用権限でAdobe Readerの機能を拡張し、組織がインタラクティブなPDFドキュメントを簡単に共有できます。 このサービスは、PDFドキュメントに使用権限を追加し、ドキュメントへのコメントの追加、フォームへの入力、ドキュメントの保存など、Adobe Acrobat Reader DCを使用してPDFドキュメントを開いた場合に通常使用できない機能をアクティブにします。 サードパーティユーザーは、使用権限を付与されたドキュメントを扱うためにソフトウェアまたはプラグインを追加する必要はありません。使用権限が追加された PDF ドキュメントは、「使用権限を付与されたドキュメント」と呼ばれます。使用権限を付与された PDF ドキュメントを Adobe Reader で開いたユーザーは、そのドキュメントで有効になっている操作を実行できます。

Adobeでは、PKI（公開鍵インフラストラクチャ）を活用して、ライセンスや機能のイネーブルメントに使用する電子証明書を発行します。 Adobeは、証明機関「Adobeルート CA」に基づいて証明書を発行しており、2023 年 1 月 7 日に期限が切れる予定です。 この認証局に基づいて発行されたすべての証明書の有効期限が切れます。 証明書の有効期限が切れると、証明書に依存するすべての機能は機能しなくなります。 例えば、Adobe Acrobat Readerを使用してコメントを追加できる読者用に拡張されたPDFドキュメントは、2023 年 1 月 7 日以降に、お客様に対して機能しなくなります。 この問題を解決するには、Reader拡張サービスの管理者は、古い証明書を使用して、新しいAdobeルート CA G2 が発行した新しい証明書を取得し、PDFドキュメントに再適用する必要があります (reader は、新しい証明書でPDFドキュメントを拡張します )。

証明書の有効期限は、JEE 上のAEM Formsと OSGi スタック上のAEM Formsの両方に影響します。 両方のスタックには、異なる命令のセットがあります。 スタックに応じて、次のパスのいずれかを選択します。

* JEE 環境上のAEM Formsの証明書の更新
* OSGi 環境でのAEM Formsの証明書の更新

>[!NOTE]
>
>このドキュメントでは、用語の証明書と秘密鍵証明書が同じ意味で使用されています。

## 前提条件 {#Pre-requisites}

証明書を更新するには、AEM Forms管理者コンソールで使用できるアクションと、AEM Formsが提供するReader拡張 API を使用する必要があります。 このドキュメントは、Adobe Experience Manager Forms API の使用に関する知識を持つユーザーおよび管理者を対象としています。 開始する前に、次の点を確認します。

* ユーザーには、基になるAEM Forms環境の管理者権限があります。
* ユーザーが [開発環境](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/howto-projects-eclipse.html) そしてそれにアクセスできる
* 証明書を取得します。

### 証明書を取得する {#obtain-the-certificates}

使用権限秘密鍵証明書は、公開鍵と秘密鍵の両方を含んでいる電子証明書、および秘密鍵証明書にアクセスするためのパスワードとして提供されます。

組織が実稼動版のReader拡張機能を購入した場合、実稼動版の権限資格情報はAdobeライセンス Web サイト (LWS) によって配信されます。 実稼働環境用の使用権限秘密鍵証明書は、会社に固有のものであり、必要とする特定の使用権限を有効にすることができます。

Reader拡張機能をソフトウェアに統合したパートナーまたはソフトウェアプロバイダーからReader拡張機能を取得した場合、そのAdobeからこの資格情報を受け取ったパートナーから権限資格情報が提供されます。

>[!NOTE]
>
>使用権限秘密鍵証明書は、一般的なドキュメントの署名や識別情報のアサーションには使用できません。これらの場合は、自己署名証明書を使用するか、認証局（CA）から識別情報証明書を取得してください。

次のタイプの使用権限秘密鍵証明書を取得できます。

**顧客評価**:Reader拡張機能を評価するお客様に提供される、有効期間が短い資格情報。 この秘密鍵証明書を使用してドキュメントに適用されている使用権限は、証明書の有効期限が切れると失効します。この種類の秘密鍵証明書は、2 ～ 3 か月間のみ有効です。

**実稼動**:製品全体を購入したお客様に提供される、有効期間が長い資格情報。 Production（実稼働環境用）証明書は、ユーザーごとに固有ですが、複数のシステムにインストールできます。

Reader 用の証明書を既に使用してPDFファイルを拡張している場合は、本番用の証明書を [Adobeライセンス Web サイト (LWS)](https://licensing.adobe.com/).

## JEE 環境上のAEM Formsの証明書の更新と適用 {#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment}

JEE 上のAEM Formsスタックで新しい証明書を更新および適用するには、新しい資格情報の読み込み、既存のPDFドキュメントから使用権限の削除、使用権限の適用が必要です。 Admin Console を使用して資格情報を読み込み、AEM FormsReader拡張 API を使用して使用権限を削除および適用できます。

### 資格情報の読み込みと設定

Trust Store の管理ページを使用して、新しい資格情報や置き換え用の資格情報を読み込むことができます。 Trust Store には、複数の Extensions 証明書を含めることができます。Reader これらの証明書の 1 つを、デフォルトの Reader Extensions 証明書として指定する必要があります。デフォルトの証明書は、Workbench ユーザーがプロセス作成時に、どの証明書を使用するかを判断できない場合に使用されます。デフォルトの証明書には以下の規則が適用されます。

* Reader拡張資格情報を読み込んでも、Trust Store に他のReader拡張資格情報が含まれていない場合、その資格情報がデフォルトとして設定されます。
* 「デフォルト」オプションを選択してReader拡張の証明書を読み込むと、デフォルトの種類は既存のデフォルトの証明書から削除されます。 読み込まれた証明書がデフォルトになります。
* デフォルトの Extensions 証明書は削除できませんReader。 デフォルトの証明書を削除するには、最初に、他の証明書をデフォルトとして設定します。ただし、証明書が 1 つしかない場合は例外で、デフォルトの証明書でも削除できます。
* デフォルトの Extensions 証明書は更新できません。Reader

資格情報を読み込むには：

1. 管理コンソールで、設定／Trust Store の管理／ローカル秘密鍵証明書をクリックします。
1. 「読み込み」をクリックし、「Trust Store の種類」で「Acrobat Reader DC Extensions 証明書」を選択します。
1. （オプション）この証明書を Acrobat Reader DC Extensions のデフォルトの証明書として指定するには、「デフォルト」を選択します。
1. 「エイリアス」ボックスに、証明書の ID を入力します。この ID は、Acrobat Reader DC Extensions で証明書の表示名として使用されます。このエイリアスは、AEM Forms SDK を使用してプログラムから証明書にアクセスするときにも使用されます。
1. 「ファイルを選択」をクリックして証明書を探し、証明書のパスワードを入力して「OK」をクリックします。

「ファイル形式が正しくないか、パスワードが正しくないため、秘密鍵証明書を読み込めませんでした」というエラーメッセージが表示される場合は、パスワードが有効であることを確認します。

プログラムによって証明書を読み込んだり、削除したりすることもできます（「[AEM Forms によるプログラミング](../../developing/credentials.md)」を参照してください。）

### 既存の権限が有効なPDF文書から使用権限を削除

最新の資格情報を使用して使用権限を適用する前に、既存の権限が有効なPDFドキュメントから使用権限を削除します。 JEE 上のAEM Formsは、使用権限を削除する API を提供しています。 詳しい手順については、 [使用権限の削除 (PDF・ドキュメント )](../../developing/assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).

Workbench で開発された JEE 上のAEM Formsプロセスの使用権限を削除するには、 [Workbench ヘルプ](https://helpx.adobe.com/jp/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf).

### 使用権限をPDF文書に適用

新しい資格情報を読み込み、既存の権限を持つPDFドキュメントから使用権限を削除した後、新しい資格情報を使用してPDFドキュメントに使用権限を適用します。 Acrobat Reader DC拡張機能 Java Client API と Web サービスを使用して、PDFドキュメントに使用権限を適用できます。  詳しくは、 [使用権限のPDF・ドキュメントへの適用](../../developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).


## OSGi 環境でのAEM Formsの証明書の更新と適用 {#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment}

OSGi スタック上のAEM Formsで新しい証明書を更新および適用するには、新しい資格情報を読み込み、既存のPDFドキュメントから使用権限を削除し、使用権限を適用する必要があります。 Admin Console を使用して資格情報を読み込み、AEM FormsReader拡張 API を使用して使用権限を削除および適用できます。

### 認証情報の読み込み {#Import-credentials}

OSGi 環境のAEM Formsでは、Reader拡張資格情報が fd-service ユーザーに関連付けられます。 fd-user キーストアの資格情報を追加する前に、次の手順を実行してキーストアを作成します。

1. AEM オーサーインスタンスに管理者としてログインします。
1. ツール／セキュリティ／ユーザーに移動します。
1. fd-service ユーザーアカウントが見つかるまで、ユーザーのリストを下にスクロールします。
1. fd-service ユーザーをクリックします。
1. 「キーストア」タブをクリックします。
1. 「キーストアを作成」をクリックします。
1. キーストアアクセスパスワードを設定し、設定を保存してキーストアパスワードを作成します。

キーストアを作成した後、fd-service ユーザーに資格情報を追加します。

>[!VIDEO](https://images-tv.adobe.com/mpcv3/5577/8db8e554-f04b-4fae-8108-b9b5e0eb03ad_1627925794.854x480at800_h264.mp4)

次のコマンドは、pfx ファイルの詳細をリストします。 コマンドを実行する前に、.pfx ファイルを含むディレクトリに移動します。

`keytool -v -list -storetype pkcs12 -keystore <name of your .pfx file>`

例えば、keytool -v -list -storetype pkcs12 -keystore 1005566.pfx の場合、1005566.pfx は私の pfx ファイルの名前です。

### 既存の権限が有効なPDF文書から使用権限を削除

最新の資格情報を使用して使用権限を適用する前に、既存の権限が有効なPDFドキュメントから使用権限を削除します。 docAssuranceServiceAPI 内から removeUsageRights API を呼び出すことで、ドキュメントの使用権限を削除できます。 詳しくは、 [使用権限を削除](/help/forms/using/aem-document-services-programmatically.md#removing-usage-rights) 文書。

### 使用権限をPDF文書に適用

OSGi 環境上のAEM Formsで使用権限を適用するには、カスタム OSGi サービスを作成して、ドキュメントに使用権限を付与します。 また、POSTメソッドを使用してサーブレットを作成し、読み取り用の拡張PDFをユーザーに返すこともできます。 詳しい手順については、 [Reader拡張の適用](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/document-services/apply-reader-extension-rights-to-pdf.html).

## よくある質問

**他に質問がある場合、誰に問い合わせればよいですか？**

次の連絡先に： [Adobeサポート](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=ja#support) またはサポートチケットを発行します。

**2023 年 1 月 7 日より前に証明書を更新しない場合はどうなりますか？**

古い証明書でPDFドキュメントReader拡張を開こうとすると、エラーメッセージが表示され、読み取り用の拡張機能にアクセスできなくなります。 エラーの例はです。

`The document has been changed since it was created and use of extended features in no longer available. Please contact the author for the orignal version of this document.`

**新しい説明の名前に何か変更はありますか？**

新しいReader拡張証明書では、説明内でプログラム名としてG3-P24 が挙げられます。 古い証明書では、説明に P24 というプログラム名が記載されていました。