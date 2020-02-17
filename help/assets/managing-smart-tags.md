---
title: スマートタグと検索の管理
description: 不正確なスマートタグを更新または削除して、タグの関連性を向上させます。
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# スマートタグと検索の管理 {#manage-smart-tags-and-searches}

<!--
TBD: This article should be merged into a new, uber article for Smart Tags. Delete this article then. Cloud service article is merged.
-->

スマートタグをキュレーションして、ブランド画像に割り当てられている不正確なタグを削除し、最も関連性の高いタグのみを表示できます。

また、スマートタグをモデレートすると、画像が最も関連性の高いタグの検索結果に表示されるようになるので、画像のタグベース検索の精度が向上します。実質的には、検索結果に関連性のない画像が表示されないようにすることができます。

また、タグに高いランクを割り当てて、画像に対する関連性を高めることもできます。 画像のタグのランクを高くすることで、特定のタグに基づいて検索が実行されたときに、その画像が検索結果に表示される可能性が高くなります。

1. オムニサーチボックスで、タグに基づいてアセットを検索します。
1. 検索結果を調査し、検索に関連性のない画像を特定します。
1. Select the image, and then tap **[!UICONTROL Manage Tags]** from the toolbar.
1. **[!UICONTROL タグを管理]**&#x200B;ページで、タグを調査します。If you don&#39;t want the image to be searched based on a specific tag, select the tag and then tap **[!UICONTROL Delete]** from the toolbar. Alternatively, click/tap `X` symbol that appears beside the label.
1. To assign a higher rank to a tag, select the tag and tap **[!UICONTROL Promote]** from the toolbar. 昇格したタグは、「**[!UICONTROL タグ]**」セクションに移動されます。
1. Click/tap **[!UICONTROL Save]**, and then click/tap **[!UICONTROL OK]** to close the Success dialog.
1. 画像のプロパティページに移動します。昇格したタグに高い関連性が割り当てられていること、その結果として検索結果の上位に表示されることを確認します。

## スマートタグ付き AEM 検索結果について {#understandsearch}

デフォルトでは、検索用語どうしを `AND` 句で組み合わせて AEM 検索がおこなわれます。スマートタグを使用しても、このデフォルトの動作は変わりません。スマートタグを使用すると、適用されたスマートタグ内にある検索用語のいずれかを探すための `OR` 句が追加されます。For example, consider searching for `woman running`. デフォルトでは、「`woman`」のみ、または「`running`」のみがメタデータに含まれているアセットは、検索結果に表示されません。しかし、スマートタグを使って「`woman`」または「`running`」のどちらかがタグ付けされているアセットは、そうした検索結果に表示されます。つまり、検索結果は、以下を組み合わせたものになります。

* assets with `woman` and `running` keywords in the metadata.

* 上記どちらかのキーワードがメタデータ内にあるアセット。

メタデータフィールド内のすべての検索用語に一致する検索結果が最初に表示され、スマートタグ内の検索用語のいずれかに一致する検索結果はその後に表示されます。上記の例の場合、検索結果が表示される順序はおおよそ次のようになります。

1. matches of `woman running` in the various metadata fields.
1. matches of `woman running` in smart tags.
1. matches of `woman` or of `running` in smart tags.
