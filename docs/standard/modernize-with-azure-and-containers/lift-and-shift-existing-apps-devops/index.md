---
title: "既存のアプリの DevOps のリフト アンド シフト"
description: "Azure クラウドおよび Windows コンテナーで既存の .NET アプリケーションを最新化する"
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 10/26/2017
ms.openlocfilehash: 6c1bbbcd99c2abee43a789fddf4546e7ee8d3380
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="lift-and-shift-existing-apps-devops"></a><span data-ttu-id="7ddf9-103">既存のアプリの DevOps のリフト アンド シフト</span><span class="sxs-lookup"><span data-stu-id="7ddf9-103">Lift and shift existing apps DevOps</span></span>
> <span data-ttu-id="7ddf9-104">ビジョン: 既存の .NET Framework アプリケーションを Cloud DevOps 対応アプリケーションにリフト アンド シフトすると、展開の機敏性が大幅に改善され、短期間で少ない配信コストで出荷できるようになります。</span><span class="sxs-lookup"><span data-stu-id="7ddf9-104">Vision: Lift and shift your existing .NET Framework applications to Cloud DevOps-Ready applications to drastically improve your deployment agility, so you can ship faster and lower app delivery costs.</span></span>

<span data-ttu-id="7ddf9-105">クラウドやコンテナーなどの新しいテクノロジのメリットを活用するために、既存の .NET アプリケーションを少なくとも部分的に最新化する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7ddf9-105">To take advantage of the benefits of the cloud and new technologies like containers, you should at least partially modernize your existing .NET applications.</span></span> <span data-ttu-id="7ddf9-106">最終的に、エンタープライズ アプリケーションを最新化すると、総保有コストが低下します。</span><span class="sxs-lookup"><span data-stu-id="7ddf9-106">Ultimately, modernizing your enterprise applications will lower your total cost of ownership.</span></span>

<span data-ttu-id="7ddf9-107">アプリを部分的に最新化しても、完全な移行と再構築とは限りません。</span><span class="sxs-lookup"><span data-stu-id="7ddf9-107">Partially modernizing an app doesn't necessarily mean a full migration and re-architecture.</span></span> <span data-ttu-id="7ddf9-108">簡単かつ高速であるリフト アンド シフト プロセスを使用して、既存のアプリケーションを最初に最新化することができます。</span><span class="sxs-lookup"><span data-stu-id="7ddf9-108">You can initially modernize your existing applications by using a lift and shift process that's easy and fast.</span></span> <span data-ttu-id="7ddf9-109">Windows および IIS の依存関係がある既存の .NET Framework のバージョンで作成された現在のコード ベースを保守することができます。</span><span class="sxs-lookup"><span data-stu-id="7ddf9-109">You can maintain your current code base, written in existing .NET Framework versions, with any Windows and IIS dependencies.</span></span> <span data-ttu-id="7ddf9-110">図 4-1 は、Azure アプリケーション最新化成熟度モデル内でのクラウド DevOps 対応アプリの位置付けを示しています。</span><span class="sxs-lookup"><span data-stu-id="7ddf9-110">Figure 4-1 highlights how Cloud DevOps-Ready apps are positioned in Azure application modernization maturity models.</span></span>

![クラウド DevOps 対応アプリケーションの位置付け](./media/image1.png)

> <span data-ttu-id="7ddf9-112">**図 4-1**</span><span class="sxs-lookup"><span data-stu-id="7ddf9-112">**Figure 4-1.**</span></span> <span data-ttu-id="7ddf9-113">クラウド DevOps 対応アプリケーションの位置付け</span><span class="sxs-lookup"><span data-stu-id="7ddf9-113">Positioning Cloud DevOps-Ready applications</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="7ddf9-114">[前へ](../migrate-your-relational-databases-to-azure.md)
[次へ](reasons-to-lift-and-shift-existing-net-apps-to-cloud-devops-ready-applications.md)</span><span class="sxs-lookup"><span data-stu-id="7ddf9-114">[Previous](../migrate-your-relational-databases-to-azure.md)
[Next](reasons-to-lift-and-shift-existing-net-apps-to-cloud-devops-ready-applications.md)</span></span>