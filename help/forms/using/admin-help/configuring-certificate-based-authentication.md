---
title: 証明書ベースの認証の設定
seo-title: 証明書ベースの認証の設定
description: 証明書ベースの認証のために、認証局（CA）証明書を Trust Store に読み込み、証明書のマッピングを作成します。
seo-description: 証明書ベースの認証のために、認証局（CA）証明書を Trust Store に読み込み、証明書のマッピングを作成します。
uuid: 9802a969-6d29-4b80-a4ed-06eb6e66e046
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d958ae65-3008-4d68-9e11-4346e149827f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 94%

---


# 証明書ベースの認証の設定 {#configuring-certificate-based-authentication}

User Management は、通常、ユーザー名とパスワードを使用して認証を実行します。User Management では、証明書ベースの認証もサポートされています。この認証方式は、Acrobat 経由でのユーザーの認証、またはプログラムによるユーザーの認証に使用できます。プログラムによるユーザーの認証について詳しくは、「[AEM Forms によるプログラミング](https://www.adobe.com/go/learn_aemforms_programming_63)」を参照してください。

証明書ベースの認証を使用するには、信頼する認証局（CA）証明書を Trust Store に読み込み、証明書のマッピングを作成します。

## CA 証明書の読み込み  {#import-the-ca-certificate}

証明書を読み込むときに、「証明書認証で信頼」と「ID で信頼」のオプションと共に、必要な他のオプションを選択します。証明書の読み込みについて詳しくは、[証明書の管理](/help/forms/using/admin-help/certificates.md#managing-certificates)を参照してください。

## 証明書のマッピングの設定  {#configuring-certificate-mapping}

ユーザーに対して証明書ベースの認証を有効にするには、証明書のマッピングを作成します。「*証明書のマッピング*」では、証明書の属性とドメイン内のユーザーの属性の間のマップが定義されます。複数の証明書を同じドメインにマップすることができます。

証明書をテストすると、User Management では、証明書チェックをアップロードして、以下の要件を満たしているかどうかを確認します。

* 証明書が有効であること。
* 指定された発行者が証明書を検証できること。
* マッピングに必要な属性が証明書に含まれていること。
* 指定されたマッピングによって、証明書が AEM Forms データベース内の 1 人のユーザーにのみマッピングされること。マッピング条件に一致するかどうか判断するために、現在のユーザーと古い（削除された）ユーザーの両方がチェックされます。このため、古いユーザーを含む複数のユーザーに対象の属性がある場合、証明書テストは失敗します。

>[!NOTE]
>
>既存の証明書のマッピングを編集することはできません。

**証明書のマッピングの追加**

1. 管理コンソールで、設定／User Management／設定／証明書のマッピングをクリックします。
1. 「新しい証明書のマッピング」をクリックし、「発行者用」リストで、Trust Store の管理で設定されている証明書エイリアスを選択します。
1. 証明書の属性のいずれかをユーザーの属性にマップします。例えば、証明書の共通名をユーザーのログイン ID にマップできます。

   証明書の属性の内容が User Management データベース内のユーザーの属性の内容と異なる場合、Java の正規表現（regex）を使用して、2 つの属性をマッチさせることができます。例えば、証明書の共通名が「*Alex Pink (Authentication)*」や「*Alex Pink (Signing)*」などで、User Management データベースの共通名が「*Alex Pink*」である場合、regex を使用して、証明書の属性の必要な部分（この例では「*Alex Pink*」）を抽出できます。指定する正規表現は、Java regex 仕様に準拠している必要があります。

   「カスタムオーダー」ボックスでグループの順序を指定すると、正規表現を変換できます。カスタム注文は`java.util.regex.Matcher.replaceAll()`メソッドと共に使用されます。 結果の動作はこのメソッドの動作に対応するため、それに従って入力文字列（カスタムオーダー）を指定する必要があります。

   regex をテストするには、「テストパラメーター」ボックスに値を入力して、「テスト」をクリックします。

   regex では、以下の文字を使用できます。

   * ：（任意の文字）
   * &amp;ast;（0回以上の繰り返し）
   * () （グループを括弧で囲んで指定）
   * ¥ （regex 文字を正規文字にエスケープするために使用）
   * $n （n 番目のグループを表すために使用）

   正規表現の例：

   * 「Alex Pink (Authentication)」から「Alex Pink」を抽出するには

      **Regex:** (.&amp;ast;) \（認証\）

   * 「Alex (Authentication) Pink」から「Alex Pink」を抽出するには

      **Regex:** (.&amp;ast;)\（認証\） (.&amp;ast;)

   * 「Alex (Authentication) Pink」から「Pink Alex」を抽出するには

      **Regex:** (.&amp;ast;)\（認証\） (.&amp;ast;)

      カスタムオーダー：$2 $1（2 番目のグループを返し、最初のグループに連結、空白スペース文字で取得）

   * 「smtp:apink@sampleorg.com」から「apink@sampleorg.com」を抽出するには

      **Regex:** smtp:(.&amp;ast;)
   正規表現の使用方法について詳しくは、[Java Tutorials の正規表現に関するページ](https://java.sun.com/docs/books/tutorial/essential/regex/)を参照してください。

1. 「ドメイン用」リストで、ユーザーのドメインを選択します。
1. この設定をテストするには、「参照」をクリックしてサンプルのユーザー証明書をアップロードし、「証明書をテスト」をクリックします。次に、設定が正しいことを確認して、「OK」をクリックします。

**既存の証明書のマッピングの編集**

1. 管理コンソールで、設定／User Management／設定をクリックします。
1. 「証明書のマッピング」をクリックします。
1. 編集する証明書のマッピングを選択し、設定を編集します。正規表現およびカスタムオーダーを更新できます。
1. 変更をテストするには、「参照」をクリックしてサンプルの証明書をアップロードし、「証明書をテスト」をクリックして「OK」をクリックします。

**証明書のマッピングの削除**

1. 管理コンソールで、設定／User Management／設定／証明書のマッピングをクリックします。
1. 削除する証明書のマッピングのチェックボックスをオンにして「削除」をクリックし、「OK」をクリックします。

