---
title: AEM でのシリアル化の問題の軽減
seo-title: Mitigating serialization issues in AEM
description: AEMでのシリアル化の問題を軽減する方法について説明します。
seo-description: Learn how to mitigate serialization issues in AEM.
uuid: c3989dc6-c728-40fd-bc47-f8427ed71a49
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f3781d9a-421a-446e-8b49-40744b9ef58e
exl-id: 01e9ab67-15e2-4bc4-9b8f-0c84bcd56862
source-git-commit: 614c4c88f3f09feb5a400ade9f45f634ac4fbcd5
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 20%

---

# AEM でのシリアル化の問題の軽減{#mitigating-serialization-issues-in-aem}

## 概要 {#overview}

AdobeのAEMチームはオープンソースプロジェクトと密接に連携した [NotSoSerial](https://github.com/kantega/notsoserial) に記載されている脆弱性を軽減するために役立つ **CVE-2015-7501**. NotSoSerial は [Apache 2 ライセンス](https://www.apache.org/licenses/LICENSE-2.0)でライセンスが付与され、[BSD に似た独自のライセンス](https://asm.ow2.io/)でライセンスが付与される ASM コードが含まれます。

このパッケージに含まれるエージェント JAR は、アドビが変更を加えて配布する NotSoSerial です。

NotSoSerial は、Java™レベルの問題に対する Java™レベルのソリューションであり、AEM固有のソリューションではありません。 これはオブジェクトのシリアル化を解除するときに、プリフライトのチェックを追加します。このチェックは、ファイアウォールスタイルの、または許可リストその両方に対してクラス名をテスブロックリストトします。 デフォルトのクラス数は限られているのでブロックリスト、このテストがシステムやコードに影響を与える可能性は低くなります。

デフォルトでは、エージェントは、現在の既知の脆弱なクブロックリストラスに対してチェックを実行します。 このブロックリストは、このタイプの脆弱性を使用する現在の弱点のリストからユーザーを保護することを目的としています。

ブロックリストと許可リスト設定は、 [エージェントの設定](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent) 」の節を参照してください。

このエージェントは、最新の既知の脆弱なクラスを軽減するためのものです。 プロジェクトで信頼できないデータの逆シリアル化が行われている場合でも、サービス拒否攻撃、メモリ不足攻撃、未知の逆シリアル化攻撃に対する脆弱性が生じる可能性があります。

Adobeは、Java™ 6、7、8 を正式にサポートしています。 しかし、Adobeの理解では、NotSoSerial は Java™ 5 もサポートしています。

## エージェントのインストール {#installing-the-agent}

>[!NOTE]
>
>AEM 6.1 のシリアル化修正プログラムを以前にインストールしている場合は、Java™の実行行からエージェントの起動コマンドを削除します。

1. **com.adobe.cq.cq-serialization-tester** バンドルをインストールします。

1. Web コンソール（`https://server:port/system/console/bundles`）にアクセスします。
1. シリアル化バンドルを探し、起動します。 これにより、NotSoSerial エージェントが動的に自動ロードされます。

## アプリケーションサーバーへのエージェントのインストール {#installing-the-agent-on-application-servers}

NotSoSerial エージェントは、アプリケーションサーバーの AEM の標準配布版には含まれていません。ただし、AEM jar 配布から抽出して、アプリケーションサーバーの設定で使用することができます。

1. まず、AEM quickstart ファイルをダウンロードして抽出します。

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. AEM クイックスタートを展開した場所に移動し、`crx-quickstart/opt/notsoserial/` フォルダーを AEM アプリケーションサーバーのインストールの `crx-quickstart` フォルダーにコピーします。

1. `/opt` の所有者を、サーバーを実行しているユーザーに変更します。

   ```shell
   chown -R opt <user running the server>
   ```

1. この記事の後の節で示すように、エージェントが正しくアクティブ化されていることを設定および確認します。

## エージェントの設定 {#configuring-the-agent}

デフォルトの設定は、ほとんどのインストールで十分です。 この設定には、既知のリモート実行の脆弱なクブロックリストラスのと、信頼されたデータの逆シリアル化が安全なパッケージの許可リスト一部が含まれます。

ファイアウォールの設定は動的であり、次の手順でいつでも変更できます。

1. Web コンソール（`https://server:port/system/console/configMgr`）にアクセスします。
1. 検索とクリック **デシリアライゼーションファイアウォールの構成。**

   >[!NOTE]
   また、次の URL にアクセスして、設定ページに直接アクセスすることもできます。
   * `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`


この設定には、、シ許可リストリアル化ブロックリスト解除のログが含まれます。

**許可リストへの登録**

許可リストセクションでは、これらのリストはシリアル化解除を許可されるクラスまたはパッケージのプレフィックスです。 独自のクラスを逆シリアル化する場合は、クラスまたはパッケージをこのクラスに追加し許可リストます。

**Block Listing**

ブロックリストセクションには、シリアル化解除を許可しないクラスが含まれます。 これらのクラスの初期セットは、リモート実行の攻撃に脆弱であると見なされるクラスに限定されています。ブロックリストは、許可リストに登録されたエントリの前に適用されます。

**診断ログ**

診断ログのセクションでは、シリアル化解除の実行時にログに記録する複数のオプションを選択できます。 これらのオプションは、初回使用時にのみログオンし、以降の使用時には再ログは記録されません。

デフォルトの **class-name-only** は、デシリアライズされるクラスを通知します。

また、 **フルスタック** オプションを使用すると、最初のデシリアライゼーションの Java™スタックがログに記録され、デシリアライゼーションが行われている場所が通知されます。 このオプションは、使用状況からシリアル化解除を検索および削除する場合に役立ちます。

## エージェントのアクティベーションの確認 {#verifying-the-agent-s-activation}

シリアル化解除エージェントの設定は、次の URL を参照して確認できます。

* `https://server:port/system/console/healthcheck?tags=deserialization`

URL にアクセスすると、エージェントに関連するヘルスチェックのリストが表示されます。 エージェントが正しくアクティブ化されているかどうかは、ヘルスチェックが合格していることを確認することで確認できます。 エラーが発生した場合は、エージェントを手動で読み込む必要があります。

エージェントに関する問題のトラブルシューティングの詳細については、 [動的エージェントの読み込みでのエラーの処理](#handling-errors-with-dynamic-agent-loading) 下

>[!NOTE]
次を追加する場合： `org.apache.commons.collections.functors` に対し許可リストては、ヘルスチェックは常に失敗します。

## 動的エージェントの読み込みでのエラーの処理 {#handling-errors-with-dynamic-agent-loading}

ログにエラーが表示された場合、または検証手順でエージェントの読み込みの問題が検出された場合は、エージェントを手動で読み込みます。 また、JDK(Java™ Development Toolkit) の代わりに JRE(Java™ Runtime Environment) を使用する場合も、動的読み込み用のツールを使用できないので、このワークフローを使用することをお勧めします。

エージェントを手動で読み込むには、次の手順を実行します。

1. 次のオプションを追加して、CQ jar の JVM 起動パラメーターを編集します。

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   エージェントがフォークされた JVM で有効になっていないので、適切な JVM メモリ設定と共に —nofork CQ/AEMオプションも使用する必要があります。

   >[!NOTE]
   Adobe 配布版の NotSoSerial エージェント JAR は、AEM インストールの `crx-quickstart/opt/notsoserial/` フォルダーにあります。

1. JVM を停止して再開します。

1. 上記の手順に従って、エージェントのアクティベーションを再度確認します。 [エージェントのアクティベーションの確認](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation).

## その他の注意点 {#other-considerations}

IBM® JVM で実行している場合は、次の場所にある Java™ Attach API のサポートに関するドキュメントを参照してください。 [この場所](https://www.ibm.com/docs/en/sdk-java-technology/8?topic=documentation-java-attach-api).
