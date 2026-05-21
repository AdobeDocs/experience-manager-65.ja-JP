---
title: AEM 6.5 の AI アシスタント
description: AI アシスタントを使用して回答を見つけ、Adobe Experience Manager で使用可能なソリューションのトラブルシューティングを行います。
solution: Experience Manager, Experience Manager 6.5
feature: Authoring, AI Assistant, AI Tools
role: Admin, Developer, User
exl-id: 3b4a484e-55b5-4924-82dd-56735f6ed46d
autotag-review: '2026-05-18T18:36:07.915Z'
TQID: 'https://experienceleague.adobe.com/dlFmrtn05S20z96wtAfkpGliITeVJhVkofqPix6QMxk'
product_v2: id: e14eb250-3c22-4a07-9061-a78112b2b826id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
feature_v2: id: ac5ecfc1-cc78-4ecc-a90a-0362685062ce
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: c1579802-ddd4-4214-8a91-97b2066abe11id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adebid: d095671a-1355-40aa-8b5f-06c33c68080bid: e1e0219c-f879-479f-8427-888ed2a6e9c2id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 9c96b6744c7af2f061b4dfbf403560047485f9b5
workflow-type: tm+mt
source-wordcount: 1379
ht-degree: 94%

---

# AEM 6.5 の AI アシスタント {#about-ai-assistant-in-aem}

>[!IMPORTANT]
>
>AEM 6.5 および AEM 6.5 LTS のお客様で、Cloud Manager/Experience Hub を使用していないお客様は、Adobe カスタマーサクセスエンジニアに連絡して、AI アシスタントへのアクセスをリクエストする必要があります。

AEM 6.5/AEM 6.5 LTSのAI アシスタントは、Adobe Experience Manager関連の質問に対する回答を効率的に見つけるように設計された、会話型インターフェイスを提供します。 これにより、AEM 製品関連の質問への回答を即座に得ることができ（*すべてのユーザーが使用可能*）、サポートチケットの作成を自動化できます（*サポート管理者が使用可能*）。

AI アシスタントは、次のソリューションを含む AEM as a Cloud Service をサポートしています。

* Experience Hub の概要ページ
* Edge Delivery Services
* Sites
* Assets
* Forms
* Dynamic Media
* Cloud Manager


AEM に直接埋め込まれ、AEM Experience Hub、Cloud Manager、オーサー UI からアクセスできます。

次の 3 分 25 秒のビデオでは、AEM の AI アシスタントの使い方を順を追って紹介しています。

>[!VIDEO](https://video.tv.adobe.com/v/3475357/?learn=on&enablevpops)

## AEM の AI アシスタントにアクセスする{#get-access}

AEM の AI アシスタントにアクセスするには、次の要件を満たしている必要があります。

* 製品知識向けの AEM の AI アシスタント使用権限。 この権限を持つユーザーは、AI アシスタントのチャットで製品関連の質問をすることができます。 この権限を有効にする必要があります。
* サポートチケットを開く権限。これには&#x200B;**サポート管理者**&#x200B;の役割が必要です。

>[!NOTE]
>
>AEM の AI アシスタントのリクエストは、Adobe Identity Management サービス（IMS）を通じて認証されます。 詳しくは、[Adobe Identity Management サービスの概要](https://www.adobe.com/content/dam/cc/en/trust-center/ungated/whitepapers/corporate/adobe-identity-management-services-security-overview.pdf)を参照してください。

**AEM の AI アシスタントにアクセスするには：**

1. Adobe Experience Manager の AI を活用したエージェント機能のほとんどにアクセスするには、お客様は追加契約を締結する必要があります。 詳しくは、アドビ担当者にお問い合わせください。

1. AEM で AI アシスタントを使用するには、AI アシスタントを通じて製品知識にアクセスする権限が必要です。 この権限はデフォルトでオンになっています。

   製品知識にアクセスできるユーザーを管理するには、Adobe ID に関連付けられているメールアドレスから [aemaiassistant@adobe.com](mailto:aemaiassistant@adobe.com) にメールを送信してください。 アドビでは、ユーザーレベルのアクセス制御を有効にできます。 有効にすると、管理者は [AEM の AI アシスタントの設定](/help/ai-assistant-in-aem-admin.md)の手順に従って、ユーザーレベルのアクセス権を付与できます。


## 範囲 {#scope}

AEMのAI アシスタントの現在の範囲は、AEMr as a Cloud Serviceの製品知識に関する質問への対応に重点を置いています。 この範囲には、主要分野に対する包括的なサポートが含まれます。<!--, such as Sites, Assets, Forms, Edge Delivery Services, Dynamic Media, and Cloud Manager. -->

* **サーフェス**：AEM Experience Hub、オーサー UI、Cloud Manager 全体で使用可能です。
* **機能**：製品知識の提供、トラブル対応や案内の一次窓口、サポートチケットの自動作成や検索を行います。
* **価値**：時間を節約し、学習と価値実現までの時間を短縮し、サポートチケットを手動で作成する必要性を減らし、サポートチケット作成の効率を向上させます。

## プライバシー、セキュリティ、ガバナンス{#privacy-security-governance}

AEM の AI アシスタントは、プライバシー、セキュリティ、ガバナンスを重視して設計されています。

この記事では、AEM の AI アシスタントが提供する、信頼の向上を重視した機能の概要を説明します。

* AEM の AI アシスタントでは、トレーニング目的を含め、個人データは使用されません。
* AEM の AI アシスタントは、消費者データにアクセスできません。
* AEM の AI アシスタントを利用するには、明示的な権限が必要です。
* ユーザーが提供したプロンプト（質問、クエリなど）は、他の顧客と共有されることはありません。

<!-- See also [Security at Adobe whitepaper](). NEED ACTIVE LINK FROM ADRIAN NICOLAE TANASE. CURRENTLY 404. -->

## AEM の AI アシスタントを利用して、製品知識とサポートチケットの自動作成について学ぶ {#ai-prod-insights}

製品知識には、Adobe Experience League ドキュメントから派生した概念やトピックが含まれます。 これらの質問は、次のサブグループに分類できます。


| 製品知識 | すべてのユーザーが利用可能<br>例 |
| :--- | :--- |
| ターゲットを絞った学習 | <ul><li>ユニバーサルエディターとは？</li><li>Cloud Manager でプログラムを作成する方法を教えてください。</li></ul> |
| 自由探索型の質問 | <ul><li>ユニバーサルエディターの使用方法を教えてください。</li><li>ある環境から別の環境にコンテンツをコピーする方法はありますか？</li></ul> |
| トラブルシューティング | <ul><li>ユニバーサルエディターにアクセスできないのはなぜですか？</li><li>パイプラインが失敗する理由</li></ul> |
| **チケット作成をサポート** | **サポート管理者のみが利用可能&#x200B;**<br>**例** |
| AI アシスタントのチャット履歴とコンテキストを取得したサポートチケットの自動作成 | <ul><li>サポートチケットを作成します。</li></ul> |
| サポートチケットのステータスの取得 | <ul><li>私が開いたサポートチケットをすべて見せてください。</li><li>チケット「E-----------」のステータスを表示</li></ul> |

{style="table-layout:auto"}


## 効果的な質問を作成する方法 {#ai-craft-questions}

AEM の AI アシスタントから最も正確な回答を得るには、質問を明確かつ文脈が分かるように表現することが重要です。 次のヒントを使用して、クエリを明確かつ適切に構成してください。

* タスクや質問を簡潔かつ明確に表現してください。
* 分かりやすさを高めるため、あいまいな表現や複雑すぎる構文を避けてください。
* 質問やタスクに関する関連コンテキストを含めることで、AEM の AI アシスタントがより正確で関連性の高い回答を提供できます。
例えば、プロンプトに、作業中の AEM ソリューション（Sites、Assets、Dynamic Media、Edge Delivery Services、Cloud Manager、Forms）の名前を付けると役立ちます。

### サポートされていない質問の例 {#ai-unsupported-questions}

| 領域 | 例 |
| --- | --- |
| 運用上のインサイト | <ul><li>テナントに存在する開発環境の数は？</li><li>最後の実稼動パイプラインを開始したのは誰ですか？</li></ul> |
| トラブルシューティング | <ul><li>実稼動パイプラインが失敗する理由</li></ul> |
| タスクと自動化 | <ul><li>開発ブランチからコード品質パイプラインを設定します。</li></ul> |


## AEM AI アシスタントの使用 {#ai-use}

<!--
UNHIDE AFTER BETA or at GA
### Enable AI Assistant in AEM access through Admin Console 

To use AI Assistant in AEM, your organization must opt in at the Admin Console level. A product administrator creates (or chooses) a user group and grants it the new "AI Assistant" permission. Anyone added to that group instantly gains access to the Assistant across AEM. If the goal is company-wide availability, the admin simply assigns all users to that group.

![AI Assistant in AEM in the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console.png)

From an employee's perspective, the process is straightforward: identify the product administrator for Adobe Experience Manager in your organization and request to be added to the AI-enabled user group. Once you appear in that group, the Assistant icon shows up automatically the next time you sign in.

Administrators should keep normal Cloud Manager governance in mind. Hold product administrator rights in the Admin Console to create profiles, manage user groups, or edit permissions. If users also need the Assistant's built-in **Create Support Ticket** feature, add the standard **Support Admin** role (standard Admin Console role) to the same individuals or group.

![Technical support ticket creation in AI Assistant in AEM of the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console-support-ticket.png)

For a guided walkthrough of setting up users and groups in AEM as a Cloud Service, see [Configuring access to AEM as a Cloud Service ](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/accessing/overview). 

See also [Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md).
-->


### AEM で AI アシスタントとの対話を開始する

トピックを変更したい場合は、AEM の AI アシスタントをリセットして、新しい会話を開始できます。 この機能は、クエリの不具合や誤った情報を提供しているクエリのトラブルシューティングに特に役立ちます。

**AEM で AI アシスタントとの対話を開始するには：**

1. AEM ユーザーインターフェイスの右上隅付近（Cloud Manager ページまたは AEM 環境のオーサーインスタンス）で、「**AI アシスタント**」アイコンをクリックします。

   ![ツールバーの AI アシスタントアイコン](/help/assets/assets-ai/ai-assistant-icon.png)

1. 下部付近の **AI アシスタント**&#x200B;パネルのテキストボックスに、質問またはプロンプトを入力し、`Enter` を押すか「![送信アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Send_18_N.svg)」をクリックします。

   >[!NOTE]
   >
   >このツールの利用に個人データは不要なので、入力に含めないでください。

   ![AI アシスタントパネルの下部にあるテキストボックス](/help/assets/assets-ai/ai-assistant-prompt-text-box.png)

1. 新しい会話（新しいトピックまたはトピックの変更）を開始するには、![詳細アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)／**新しい会話を開始**&#x200B;をクリックします。

   ![省略記号アイコンから AI アシスタントで新しい会話を開始](/help/assets/assets-ai/ai-assistant-start-new-conversation.png)

### カテゴリ別のプロンプトを見つける

AEM の AI アシスタントには、対応しているトピックやカテゴリを調べられる検出機能が搭載されています。

**カテゴリ別にプロンプトを見つけるには：**

1. AI アシスタントパネルで、「![学習アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg)」をクリックして、プロンプト検出パネルをオンにします。

   ![AI アシスタントのカテゴリ別にプロンプトを検索できるパネル](/help/assets/assets-ai/ai-assistant-discover-prompts.png)
   *AI アシスタントのプロンプトカテゴリを表示するパネル。*

1. カテゴリを選択すると、関連するプロンプトのリストが表示されます。
1. プロンプトを選択すると、AI アシスタントが回答できる質問の例が表示されます。

1. プロンプト検出パネルを非表示にするには、「![学習アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg)」をもう一度クリックします。

### AEM の AI アシスタントに関するフィードバックを共有する

お客様のフィードバック内容は、アドビが AI アシスタントのパフォーマンスと精度を向上させるのに役立ちます。

AEM の AI アシスタントの利用体験について、次の方法でフィードバックを共有できます。

![サムズアップ／サムズダウン、フラグアイコン](/help/assets/assets-ai/ai-assistant-feedback-icons.png)

| Click | 説明 |
| --- | --- |
| ![アウトラインのサムズアップアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbUpOutline_18_N.svg) | うまくいった内容を示し、肯定的なフィードバックを共有します。 |
| ![アウトラインのサムズダウンアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbDownOutline_18_N.svg) | 改善策を提案します。 ご利用体験について具体的なコメントを追加してください。これらは毎日確認されています。 |
| ![フラグアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Flag_18_N.svg) | AEM の AI アシスタントとの対話について、懸念を報告したり、詳細なフィードバックを提供したりできます。 |

## AEM の AI アシスタントに関するよくある質問 {#ai-faq}

ここでは、AI アシスタントに関するよくある質問に対する回答を紹介します。

* **AEM の AI アシスタントはリアルタイムの情報を提供しますか？**\
  いいえ。 AI アシスタントは、Adobe Experience League のドキュメントを情報源としています。 コンテンツの更新が反映されるまでには、時間がかかる場合があります。
* **AEM の AI アシスタントでサポートされているアドビのアプリケーションはどれですか？**\
  現在、AI アシスタントは、Sites、Assets、Dynamic Media、Cloud Manager、Formsなど、AEM as a Cloud Serviceでの製品知識の問い合わせをサポートしています。
* **AEM の AI アシスタントの機能は何ですか？**\
  AEMのAI アシスタントは、Adobeの製品知識に関する質問に答えるために設計されています。
* **AEM の AI アシスタントは、トレーニングデータに個人情報を使用していますか？**\
  いいえ。 AEM の AI アシスタントは、トレーニング目的で個人情報を使用しません。 AEM の AI アシスタントでは、氏名や連絡先情報など、自身や他者に関する個人情報を共有しないでください。

<!--
IS THE DOCUMENTATION BELOW STILL NEEDED? IF SO, GO AHEAD AND DELETE THE COMMENT TAGS!!

## AEM Forms AI Assistant (Forms Experience Builder) {#ai-forms-builder}

In addition to the general AI Assistant in AEM for product knowledge, AEM offers a specialized **[AEM Forms AI Assistant (Forms Experience Builder)](/help/edge/docs/forms/forms-ai-assistant.md)**. This enhanced assistant can actively help you create and configure forms through natural language prompts and answer questions specific to forms.

### Key capabilities

The AEM Forms AI Assistant provides:

* **Form Creation**: Create new forms from scratch using natural language descriptions.
* **Design Import**: Convert existing designs (PDF, Figma, images) into functional AEM Forms. 
* **Form Configuration**: Add fields, panels, validation rules, and conditional logic.
* **Layout Management**: Organize form structure and optimize for different devices.
* **Integration Setup**: Configure form submissions and data handling.
* **Product Knowledge**: Answer questions about AEM Forms features and best practices.

### Where to access

The AEM Forms AI Assistant is available in the following:

* **Universal Editor**: For Edge Delivery Services forms with visual editing capabilities.
* **Adaptive Forms Editor**: For detailed form configuration and advanced features.
* **Forms Management UI**: For high-level form creation and management tasks.

### Getting started

>[!NOTE]
>
> The AEM Forms AI Assistant (Forms Experience Builder) is available under the private beta program. Send an email from your work address to [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) to request access.

To learn more about using the AEM Forms AI Assistant , see the [AEM Forms AI Assistant](/help/edge/docs/forms/forms-ai-assistant.md) documentation.

### Example Use Cases

* **"Create a customer feedback form with name, email, rating, and comments fields"**
* **"Convert this uploaded PDF application form into a digital adaptive form"**  
* **"Add conditional logic to show spouse information only when marital status is 'Married'"**
* **"Configure this form to submit data to the Customer Relationship Management system"**

This specialized AEM Forms AI Assistant represents the next evolution in form building, combining the power of AI with AEM's robust forms capabilities to streamline your form creation workflow.
-->
