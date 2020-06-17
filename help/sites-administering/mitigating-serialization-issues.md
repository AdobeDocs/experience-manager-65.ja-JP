---
title: AEM でのシリアル化の問題の軽減
seo-title: AEM でのシリアル化の問題の軽減
description: AEM でのシリアル化の問題を軽減する方法について説明します。
seo-description: AEM でのシリアル化の問題を軽減する方法について説明します。
uuid: c3989dc6-c728-40fd-bc47-f8427ed71a49
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f3781d9a-421a-446e-8b49-40744b9ef58e
translation-type: tm+mt
source-git-commit: 3cbbad3ce9d93a353f48fc3206df989a8bf1991a
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 68%

---


# AEM でのシリアル化の問題の軽減{#mitigating-serialization-issues-in-aem}

## 概要 {#overview}

 アドビの AEM チームは、オープンソースプロジェクト [NotSoSerial](https://github.com/kantega/notsoserial) と緊密に連携して **CVE-2015-7501** に記載されている脆弱性の軽減に努めています。NotSoSerial は [Apache 2 ライセンス](https://www.apache.org/licenses/LICENSE-2.0)でライセンスが付与され、[BSD に似た独自のライセンス](https://asm.ow2.org/license.html)でライセンスが付与される ASM コードが含まれます。

このパッケージに含まれるエージェント JAR は、アドビが変更を加えて配布する NotSoSerial です。

  NotSoSerial は Java レベルの問題を解決する Java レベルのソリューションであり、AEM に固有のものではありません。これはオブジェクトのシリアル化を解除するときに、プリフライトのチェックを追加します。このチェックでは、クラス名をファイアウォール形式の許可リストやブロックリストに対してテストします。 デフォルトブロックリストのクラス数に制限があるので、システムやコードに影響を及ぼす可能性はありません。

デフォルトでは、エージェントは、現在の既知の脆弱なクラスに対してブロックリストチェックを実行します。 このブロックリストは、この種の脆弱性を使用する悪用の現在のリストからユーザーを保護することを目的としています。

The block list and allow list can be configured by following the instructions in the [Configuring the Agent](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent) section of this article.

エージェントの目的は、最新の既知のクラスの脆弱性を軽減することです。プロジェクトで信頼されないデータのシリアル化を解除している場合でも、サービス拒否攻撃、メモリ不足攻撃および未知のシリアル化解除による攻撃に対しては脆弱なままであることがあります。

  アドビは Java 6、7 および 8 を正式にサポートしていますが、NotSoSerial は Java 5 もサポートしています。

## エージェントのインストール {#installing-the-agent}

>[!NOTE]
>
>以前に AEM 6.1 向けのシリアル化のホットフィックスをインストールした場合は、Java を実行する行からエージェントの開始コマンドを削除してください。

1. **com.adobe.cq.cq-serialization-tester** バンドルをインストールします。

1. Go to the Bundle Web Console at `https://server:port/system/console/bundles`
1. シリアル化のバンドルを探して開始します。これにより、NotSoSerial エージェントが動的にオートロードされます。

## アプリケーションサーバーへのエージェントのインストール {#installing-the-agent-on-application-servers}

NotSoSerialエージェントは、アプリケーションサーバー用のAEMの標準配布物には含まれません。 ただし、それを AEM JAR 配布版から抽出して、アプリケーションサーバーの設定に使用できます。

1. まず、AEM クイックスタートファイルをダウンロードして展開します。

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. Go to the location of the newly unzipped AEM quickstart, and copy the `crx-quickstart/opt/notsoserial/` folder to the `crx-quickstart` folder of the AEM application server installation.

1. Change the ownership of `/opt` to the user running the server:

   ```shell
   chown -R opt <user running the server>
   ```

1. この記事の続きの節に示すようにエージェントを設定し、エージェントが正しくアクティベートされていることを確認してください。

## エージェントの設定 {#configuring-the-agent}

ほとんどのインストールにおいて、デフォルトの設定で十分機能します。これには、既知のリモート実行脆弱クラスのブロックリストと、信頼できるデータの逆シリアル化が比較的安全であるパッケージの許可リストが含まれます。

   ファイアウォールの設定は動的であり、次の手順でいつでも変更できます。

1. Going to the Web Console at `https://server:port/system/console/configMgr`
1. 「**Deserialization Firewall Configuration**」を探してクリックします

   >[!NOTE]
   >
   >次の URL から設定ページに直接アクセスすることもできます。
   >
   >* `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`


この設定には、許可リスト、ブロックリストおよびデシリアル化のログが含まれます。

**リストを許可**

許可一覧セクションでは、これらは、デシリアル化を許可するクラスまたはパッケージプレフィックスです。 独自のクラスをデシリアライズする場合は、この許可リストにクラスまたはパッケージを追加する必要があることに注意してください。

**ブロック一覧**

ブロック一覧セクションには、非シリアライズを許可するクラスが含まれます。 これらのクラスの初期セットは、リモート実行の攻撃に脆弱であると見なされるクラスに限定されています。このブロックリストは、許可されたエントリの一覧の前に適用されます。

**診断ログ**

 この診断ログのセクションでは、シリアル化の解除が実行されているときにログに記録する内容を、複数のオプションから選択できます。これらは最初の使用時にログに記録され、後続の使用では記録されません。

  デフォルトの **class-name-only** は、シリアル化が解除されるクラスを示します。

**full-stack** オプションを選択すると、最初にシリアル化の解除が試行されたときの Java スタックがログに記録され、シリアル化の解除がおこなわれている場所を示します。これは、自身の環境からシリアル化が解除されたクラスを探して削除するときに便利です。

## エージェントのアクティベートの検証 {#verifying-the-agent-s-activation}

次の URL にアクセスしてシリアル化を解除するエージェントの設定を確認できます。

* `https://server:port/system/console/healthcheck?tags=deserialization`

URL にアクセスすると、エージェントに関連するヘルスチェックのリストが表示されます。ヘルスチェックに合格しているかを確認することで、エージェントが正しくアクティベートされているか判断できます。不合格の場合は、エージェントを手動で読み込む必要がある場合があります。

エージェントの問題のトラブルシューティングについて詳しくは、以下の[動的なエージェントの読み込みによるエラー処理](#handling-errors-with-dynamic-agent-loading)を参照してください。

>[!NOTE]
>
>If you add `org.apache.commons.collections.functors` to the allow list, the health check will always fail.

## 動的なエージェントの読み込みによるエラー処理 {#handling-errors-with-dynamic-agent-loading}

ログにエラーがある場合や、検証ステップでエージェントの読み込み時に問題が検出された場合は、エージェントを手動で読み込む必要がある場合があります。これは、JDK（Java Development Toolkit）ではなく、動的な読み込みをおこなうツールがない JRE（Java Runtime Environment）を使用している場合にも推奨されます。

エージェントを手動で読み込むには、以下の手順に従います。

1. 次のオプションを追加して、CQ JAR の JVM スタートアップパラメーターを変更します。

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >エージェントはフォークされた JVM では有効にできないので、CQ／AEM の -nofork オプションを、適切な JVM メモリ設定で使用する必要があります。

   >[!NOTE]
   >
   >The Adobe distribution of the NotSoSerial agent jar can be found in the `crx-quickstart/opt/notsoserial/` folder of your AEM installation.

1. JVM を停止して再開します。

1. 前述の[エージェントのアクティベートの検証](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation)のステップに従って、エージェントのアクティベートをもう一度検証します。

## その他の考慮事項 {#other-considerations}

IBM JVM 上で実行している場合は、[こちら](https://www.ibm.com/support/knowledgecenter/SSSTCZ_2.0.0/com.ibm.rt.doc.20/user/attachapi.html)の Java Attach API のサポートに関するドキュメントを参照してください。
