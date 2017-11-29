---
title: "ICorProfilerInfo::GetILFunctionBodyAllocator メソッド"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorProfilerInfo.GetILFunctionBodyAllocator
api_location: mscorwks.dll
api_type: COM
f1_keywords: ICorProfilerInfo::GetILFunctionBodyAllocator
helpviewer_keywords:
- GetILFunctionBodyAllocator method [.NET Framework profiling]
- ICorProfilerInfo::GetILFunctionBodyAllocator method [.NET Framework profiling]
ms.assetid: 5da1bf3d-dddf-4892-b266-578ee54d570b
topic_type: apiref
caps.latest.revision: "12"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 45a50fc39f2df9d4998f8490ff4382c84c5aa9bb
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2017
---
# <a name="icorprofilerinfogetilfunctionbodyallocator-method"></a><span data-ttu-id="25d2e-102">ICorProfilerInfo::GetILFunctionBodyAllocator メソッド</span><span class="sxs-lookup"><span data-stu-id="25d2e-102">ICorProfilerInfo::GetILFunctionBodyAllocator Method</span></span>
<span data-ttu-id="25d2e-103">Microsoft intermediate language (MSIL) コード内のメソッドの本体を交換するために使用されるメモリを割り当てる方法を提供するインターフェイスを取得します。</span><span class="sxs-lookup"><span data-stu-id="25d2e-103">Gets an interface that provides a method to allocate memory to be used for swapping out the body of a method in Microsoft intermediate language (MSIL) code.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="25d2e-104">構文</span><span class="sxs-lookup"><span data-stu-id="25d2e-104">Syntax</span></span>  
  
```  
HRESULT GetILFunctionBodyAllocator(  
    [in]  ModuleID      moduleId,  
    [out] IMethodMalloc **ppMalloc);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="25d2e-105">パラメーター</span><span class="sxs-lookup"><span data-stu-id="25d2e-105">Parameters</span></span>  
 `moduleId`  
 <span data-ttu-id="25d2e-106">[in]メソッドが含まれているモジュールの ID。</span><span class="sxs-lookup"><span data-stu-id="25d2e-106">[in] The ID of the module in which the method resides.</span></span>  
  
 `ppMalloc`  
 <span data-ttu-id="25d2e-107">[out]ポインター、 [IMethodMalloc](../../../../docs/framework/unmanaged-api/profiling/imethodmalloc-interface.md)メモリを割り当てる方法を提供するインターフェイスです。</span><span class="sxs-lookup"><span data-stu-id="25d2e-107">[out] A pointer to an [IMethodMalloc](../../../../docs/framework/unmanaged-api/profiling/imethodmalloc-interface.md) interface that provides a method to allocate the memory.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="25d2e-108">コメント</span><span class="sxs-lookup"><span data-stu-id="25d2e-108">Remarks</span></span>  
 <span data-ttu-id="25d2e-109">MSIL コードでメソッドの本体は、4 GB 内のモジュールに従っていることを意味、読み込まれたモジュールの基準とした相対仮想アドレス (RVA) として配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="25d2e-109">A method body in MSIL code must be located as a relative virtual address (RVA), relative to the loaded module, which means that it follows the module within 4 GB.</span></span> <span data-ttu-id="25d2e-110">メソッドの本体のスワップ アウトするためのツールを容易にできるように、`GetILFunctionBodyAllocator`メソッドにより、メモリはその範囲内で割り当てられています。</span><span class="sxs-lookup"><span data-stu-id="25d2e-110">To make it easier for a tool to swap out the body of a method, the `GetILFunctionBodyAllocator` method ensures that memory is allocated within that range.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="25d2e-111">要件</span><span class="sxs-lookup"><span data-stu-id="25d2e-111">Requirements</span></span>  
 <span data-ttu-id="25d2e-112">**プラットフォーム:**を参照してください[システム要件](../../../../docs/framework/get-started/system-requirements.md)です。</span><span class="sxs-lookup"><span data-stu-id="25d2e-112">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="25d2e-113">**ヘッダー** : CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="25d2e-113">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="25d2e-114">**ライブラリ:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="25d2e-114">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="25d2e-115">**.NET framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="25d2e-115">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="25d2e-116">関連項目</span><span class="sxs-lookup"><span data-stu-id="25d2e-116">See Also</span></span>  
 [<span data-ttu-id="25d2e-117">ICorProfilerInfo インターフェイス</span><span class="sxs-lookup"><span data-stu-id="25d2e-117">ICorProfilerInfo Interface</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)