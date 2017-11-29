---
title: "unit 型 (F#)"
description: "ここで、値が必要、言語構文によって値はありませんが必要なまたは必要なときに、場所を保持するために f# 'unit' の型を使用する多くの場合について説明します。"
keywords: "visual f#, f#, 関数型プログラミング"
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: eabbb6d7-80f3-4fa5-80b4-0f48982466a7
ms.openlocfilehash: 60ac08c0e3f8380a8f9dec7a083ede93c68bb0e8
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2017
---
# <a name="unit-type"></a><span data-ttu-id="766bf-104">Unit 型</span><span class="sxs-lookup"><span data-stu-id="766bf-104">Unit Type</span></span>

<span data-ttu-id="766bf-105">`unit`型は、型がない場合、特定の値を示す、`unit`の種類が単一の値のみ、その他の値はありませんが存在するか、必要なときに、プレース ホルダーとして機能します。</span><span class="sxs-lookup"><span data-stu-id="766bf-105">The `unit` type is a type that indicates the absence of a specific value; the `unit` type has only a single value, which acts as a placeholder when no other value exists or is needed.</span></span>


## <a name="syntax"></a><span data-ttu-id="766bf-106">構文</span><span class="sxs-lookup"><span data-stu-id="766bf-106">Syntax</span></span>

```fsharp
// The value of the unit type.
()
```

## <a name="remarks"></a><span data-ttu-id="766bf-107">コメント</span><span class="sxs-lookup"><span data-stu-id="766bf-107">Remarks</span></span>
<span data-ttu-id="766bf-108">すべての f# 式は、値に評価される必要があります。</span><span class="sxs-lookup"><span data-stu-id="766bf-108">Every F# expression must evaluate to a value.</span></span> <span data-ttu-id="766bf-109">型の値、関心のある値を生成しない式の`unit`を使用します。</span><span class="sxs-lookup"><span data-stu-id="766bf-109">For expressions that do not generate a value that is of interest, the value of type `unit` is used.</span></span> <span data-ttu-id="766bf-110">`unit`型に似ています、 `void` c# および C++ などの言語を入力します。</span><span class="sxs-lookup"><span data-stu-id="766bf-110">The `unit` type resembles the `void` type in languages such as C# and C++.</span></span>

<span data-ttu-id="766bf-111">`unit`型には、単一の値とその値は、トークンで示される`()`です。</span><span class="sxs-lookup"><span data-stu-id="766bf-111">The `unit` type has a single value, and that value is indicated by the token `()`.</span></span>

<span data-ttu-id="766bf-112">値、`unit`型が f# の値はありませんが必要なまたは必要な場合は、言語の構文では、値が必要な場所を保持するためにプログラミングでよく使用されています。</span><span class="sxs-lookup"><span data-stu-id="766bf-112">The value of the `unit` type is often used in F# programming to hold the place where a value is required by the language syntax, but when no value is needed or desired.</span></span> <span data-ttu-id="766bf-113">たとえば場合の戻り値があります、`printf`関数。</span><span class="sxs-lookup"><span data-stu-id="766bf-113">An example might be the return value of a `printf` function.</span></span> <span data-ttu-id="766bf-114">の重要な操作、`printf`操作が、関数で発生する、関数が、実際の値を返す必要はありません。</span><span class="sxs-lookup"><span data-stu-id="766bf-114">Because the important actions of the `printf` operation occur in the function, the function does not have to return an actual value.</span></span> <span data-ttu-id="766bf-115">このため、戻り値は型`unit`です。</span><span class="sxs-lookup"><span data-stu-id="766bf-115">Therefore, the return value is of type `unit`.</span></span>

<span data-ttu-id="766bf-116">一部のコンストラクトが想定して、`unit`値。</span><span class="sxs-lookup"><span data-stu-id="766bf-116">Some constructs expect a `unit` value.</span></span> <span data-ttu-id="766bf-117">たとえば、`do`バインドまたはモジュールの最上位レベルに任意のコードを評価する必要が、`unit`値。</span><span class="sxs-lookup"><span data-stu-id="766bf-117">For example, a `do` binding or any code at the top level of a module is expected to evaluate to a `unit` value.</span></span> <span data-ttu-id="766bf-118">コンパイラ警告を報告するときに、`do`バインドまたはモジュールの最上位レベルにコード以外の場合、結果を生成、`unit`使用されていない、次の例で示すように値。</span><span class="sxs-lookup"><span data-stu-id="766bf-118">The compiler reports a warning when a `do` binding or code at the top level of a module produces a result other than the `unit` value that is not used, as shown in the following example.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet901.fs)]

<span data-ttu-id="766bf-119">この警告は、;、関数型プログラミングの特性その他の .NET プログラミング言語ではありません。</span><span class="sxs-lookup"><span data-stu-id="766bf-119">This warning is a characteristic of functional programming; it does not appear in other .NET programming languages.</span></span> <span data-ttu-id="766bf-120">副作用は関数がない、純粋関数型のプログラムでは、最終的な戻り値は、関数呼び出しの結果だけがします。</span><span class="sxs-lookup"><span data-stu-id="766bf-120">In a purely functional program, in which functions do not have any side effects, the final return value is the only result of a function call.</span></span> <span data-ttu-id="766bf-121">したがって、結果を無視すると、潜在的なプログラミング エラーを勧めします。</span><span class="sxs-lookup"><span data-stu-id="766bf-121">Therefore, when the result is ignored, it is a possible programming error.</span></span> <span data-ttu-id="766bf-122">F# ではありませんが、純粋関数型プログラミング言語は、機能のプログラミング スタイル可能な場合に従うことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="766bf-122">Although F# is not a purely functional programming language, it is a good practice to follow functional programming style whenever possible.</span></span>

## <a name="see-also"></a><span data-ttu-id="766bf-123">関連項目</span><span class="sxs-lookup"><span data-stu-id="766bf-123">See Also</span></span>
[<span data-ttu-id="766bf-124">プリミティブ</span><span class="sxs-lookup"><span data-stu-id="766bf-124">Primitive</span></span>](primitive-types.md)

[<span data-ttu-id="766bf-125">F# 言語リファレンス</span><span class="sxs-lookup"><span data-stu-id="766bf-125">F# Language Reference</span></span>](index.md)