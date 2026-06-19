---
title: AEM Forms JEEでのシリアル化の問題の軽減| Adobe Experience Manager
description: JDK 8で動作するAEM Forms JEEでJava デシリアライズの問題を軽減する方法について説明します。
solution: Experience Manager, Experience Manager Forms
feature: Security
version: Experience Manager 6.5
type: Documentation
role: Admin
source-git-commit: ec3941675081255879065c3be9d5af77474b2072
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 1%

---


# AEM Forms JEEでのシリアル化の問題の軽減 {#mitigating-serialization-issues-in-aem-forms-jee}

AEM Forms JEEには、オブジェクトのデシリアライズを試みる前にプリフライトチェックを追加するデシリアライゼーションファイアウォールが含まれています。 このチェックは、ファイアウォールスタイルのコース名に対してクラス名をテストし、Java™の逆シリアル化許可リストに加えるによって悪用されることが知られているクラスを拒否します。 基になるエージェントは、[Apache 2 ライセンス ](https://www.apache.org/licenses/LICENSE-2.0)の下でライセンスされているオープンソース [NotSoSerial](https://github.com/kantega/notsoserial) プロジェクトのAdobeによる変更済みディストリビューションです。

**JDK 11以降**&#x200B;を実行しているインストールでは、この保護はプラットフォームのネイティブのシリアル化フィルターによってアクティブ化され、手動の手順は必要ありません。 **JDK 8**&#x200B;を実行しているインストールでは、ネイティブのシリアル化フィルタリングは効果的ではないため、起動時にエージェントをJVMに明示的にアタッチする必要があります。 この記事では、その方法について説明します。

>[!NOTE]
>
>シリアル化解除フィルターのヘルスチェックで、サーバーでアクティブであることが既に報告されている場合（[ エージェントのアクティベーションの検証](#verifying-the-agents-activation)を参照）、アプリケーションサーバーは既に保護されており、このドキュメントの残りの手順をスキップできます。

## 開始する前に {#before-you-begin}

アプリケーションサーバーが実行するJava™ バージョンを確認します。

```shell
java -version
```

報告されたバージョンが`1.8.x` （JDK 8）の場合は、この記事の手順が適用されます。 11以降の場合、手動による操作は必要ありません。[ エージェントのアクティベーションの確認](#verifying-the-agents-activation)で説明されているヘルスチェックを使用して保護を確認します。

次の手順では、`<jee-installation-directory>`はAEM Forms JEE インストールのルートを指します。

## エージェントの適用 {#applying-the-agent}

>[!IMPORTANT]
>
>これらの手順では、アプリケーションサーバーを再起動する必要があります。 影響を受ける各インスタンスにそれらを適用します。

1. **現在の状態を検証します。** シリアル化解除フィルターのヘルスチェックを参照します。

   ```text
   https://<server>:<port>/system/console/healthcheck?tags=deserialization
   ```

   チェックがアクティブであると報告した場合、インスタンスは既に保護されており、追加のアクションは必要ありません。 失敗している場合は、次の手順に進みます。

1. **エージェント JARが既に存在するかどうかを確認します。** 次の場所の`notsoserial.jar`を確認してください：

   ```text
   <jee-installation-directory>/crx-quickstart/opt/notsoserial/
   ```

1. **見つからない場合はJARを追加します。** [`notsoserial.jar`](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/notsoserial.jar)をダウンロードし、各インスタンスの上記のフォルダーにコピーします。

   ```text
   <jee-installation-directory>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >この手順を、公開前に、エージェントのForms JEE ディストリビューション用のAdobeの公式ダウンロード場所に置き換えます。

1. **アプリケーションサーバーのJVM起動パラメーター**&#x200B;を更新して、エージェントを添付します。 Java™の実行行に次のオプションを追加します。

   ```shell
   -javaagent:<jee-installation-directory>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   Java™実行行の正確な場所は、アプリケーションサーバー（JBoss、WebLogic、WebSphere®など）によって異なります。 このオプションを、AEM Forms JEE アプリケーションサーバーの起動に使用するJVM オプションに追加します。

1. **JEE サーバー**&#x200B;を再起動して、エージェントがJVM起動時に読み込まれるようにします。

1. **再検証します。** ヘルスチェックをもう一度参照します。

   ```text
   https://<server>:<port>/system/console/healthcheck?tags=deserialization
   ```

   ヘルスチェックは正常と報告されるようになりました。

## エージェントのアクティベーションの確認 {#verifying-the-agents-activation}

デシリアライゼーションエージェントの設定は、次のURLを参照することで、いつでも確認できます。

```text
https://<server>:<port>/system/console/healthcheck?tags=deserialization
```

エージェントに関連するヘルスチェックのリストが表示されます。 チェックが通過した場合、エージェントは適切にアクティブ化されます。 JDK 8 インスタンスで失敗している場合、エージェントは読み込まれておらず、[ エージェントの適用](#applying-the-agent)の手順を使用して手動でアタッチする必要があります。

## エージェントの設定 {#configuring-the-agent}

次の手順は、アプリケーションサーバーのJava™ バージョンがJDK 8で実行されている場合に適用されます。 エージェントをアタッチして読み込んだ後、[ エージェントの適用](#applying-the-agent)の手順を使用してエージェントを設定できます。

ほとんどのインストールでは、デフォルト設定で十分です。 これには、既知のリモートで悪用可能なクラスのブロックリストに加えると、信頼できるデータのデシリアライズが安全なパッケージのシームレスなタイプが含まれます。 許可リストに加えるされたエントリの前に、のブロックリストが適用されます。

ファイアウォールの設定は動的であり、いつでも変更できます。

1. `https://<server>:<port>/system/console/configMgr`のWeb コンソールに移動します。

1. 「**Deserialization Firewall Configuration**」を検索してクリックします。

この設定には、許可リスト、ブロックリストに加える、診断ロギングオプションが含まれています。

* **リストの作成を許可** - クラスまたはパッケージのプレフィックスは逆シリアル化に許可されています。 独自のクラスをデシリアライズする場合は、ここに関連するクラスまたはパッケージを追加します。
* **ブロックリスト** - シリアル化解除が許可されていないクラス。 最初のセットは、リモート実行攻撃に対して脆弱であることが判明したクラスに限定されます。
* **診断ログ** - シリアル化解除時にログに記録するオプション。 デフォルトの&#x200B;**class-name-only**&#x200B;は、シリアル化解除されるクラスを報告します。 **full-stack** オプションは、最初のシリアル化解除試行に対してJava™ スタックをログに記録します。これは、使用時に信頼できないシリアル化解除を見つけて削除するのに役立ちます。 これらのオプションは、最初の使用時にのみログに記録されます。

## その他 {#other-considerations}

* エージェントは、現在知られている脆弱なクラスを軽減することを目的としています。 プロジェクトで信頼できないデータがデシリアライズされる場合でも、サービス拒否、メモリ不足、または不明な将来のデシリアライズ攻撃にさらされる可能性があります。
* JDK （Java™ Development Kit）ではなくJRE （Java™ Runtime Environment）で実行する場合、動的なエージェントの読み込みに必要なツールは使用できず、[ エージェントの適用](#applying-the-agent)で説明しているように、起動時にエージェントを手動で添付する必要があります。
* IBM® JVMで実行している場合は、Java™ Attach APIのサポートに関するドキュメントを参照してください。
