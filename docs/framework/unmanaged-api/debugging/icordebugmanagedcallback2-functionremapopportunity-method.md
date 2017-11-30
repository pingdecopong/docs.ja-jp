---
title: "ICorDebugManagedCallback2::FunctionRemapOpportunity メソッド"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugManagedCallback2.FunctionRemapOpportunity
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugManagedCallback2::FunctionRemapOpportunity
helpviewer_keywords:
- FunctionRemapOpportunity method [.NET Framework debugging]
- ICorDebugManagedCallback2::FunctionRemapOpportunity method [.NET Framework debugging]
ms.assetid: 0d6471bc-ad9b-4b1d-a307-c10443918863
topic_type: apiref
caps.latest.revision: "14"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 8a8360913597dfb5156399a45f86d2cc1a9f453d
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="icordebugmanagedcallback2functionremapopportunity-method"></a><span data-ttu-id="3eaf5-102">ICorDebugManagedCallback2::FunctionRemapOpportunity メソッド</span><span class="sxs-lookup"><span data-stu-id="3eaf5-102">ICorDebugManagedCallback2::FunctionRemapOpportunity Method</span></span>
<span data-ttu-id="3eaf5-103">コードの実行が編集された関数の古いバージョンのシーケンス ポイントに達したことをデバッガーに通知します。</span><span class="sxs-lookup"><span data-stu-id="3eaf5-103">Notifies the debugger that code execution has reached a sequence point in an older version of an edited function.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="3eaf5-104">構文</span><span class="sxs-lookup"><span data-stu-id="3eaf5-104">Syntax</span></span>  
  
```  
HRESULT FunctionRemapOpportunity (  
    [in] ICorDebugAppDomain   *pAppDomain,  
    [in] ICorDebugThread      *pThread,  
    [in] ICorDebugFunction    *pOldFunction,  
    [in] ICorDebugFunction    *pNewFunction,  
    [in] ULONG32              oldILOffset  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="3eaf5-105">パラメーター</span><span class="sxs-lookup"><span data-stu-id="3eaf5-105">Parameters</span></span>  
 `pAppDomain`  
 <span data-ttu-id="3eaf5-106">[in]編集済みの関数を含む、アプリケーション ドメインを表す ICorDebugAppDomain オブジェクトへのポインター。</span><span class="sxs-lookup"><span data-stu-id="3eaf5-106">[in] A pointer to an ICorDebugAppDomain object that represents the application domain containing the edited function.</span></span>  
  
 `pThread`  
 <span data-ttu-id="3eaf5-107">[in]リマップ ブレークポイントが発生しました、スレッドを表す ICorDebugThread オブジェクトへのポインター。</span><span class="sxs-lookup"><span data-stu-id="3eaf5-107">[in] A pointer to an ICorDebugThread object that represents the thread on which the remap breakpoint was encountered.</span></span>  
  
 `pOldFunction`  
 <span data-ttu-id="3eaf5-108">[in]現在のスレッドで実行されている関数のバージョンを表す ICorDebugFunction オブジェクトへのポインター。</span><span class="sxs-lookup"><span data-stu-id="3eaf5-108">[in] A pointer to an ICorDebugFunction object that represents the version of the function that is currently running on the thread.</span></span>  
  
 `pNewFunction`  
 <span data-ttu-id="3eaf5-109">[in]関数の最新バージョンを表す ICorDebugFunction オブジェクトへのポインター。</span><span class="sxs-lookup"><span data-stu-id="3eaf5-109">[in] A pointer to an ICorDebugFunction object that represents the latest version of the function.</span></span>  
  
 `oldILOffset`  
 <span data-ttu-id="3eaf5-110">[in]命令ポインターの古いバージョンの関数での Microsoft intermediate language (MSIL) オフセットします。</span><span class="sxs-lookup"><span data-stu-id="3eaf5-110">[in] The Microsoft intermediate language (MSIL) offset of the instruction pointer in the old version of the function.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="3eaf5-111">コメント</span><span class="sxs-lookup"><span data-stu-id="3eaf5-111">Remarks</span></span>  
 <span data-ttu-id="3eaf5-112">このコールバックは、デバッガーを呼び出すことによって、新しいバージョンの指定された関数内の正しい場所への命令ポインターを再マップする機会を与える、 [icordebugilframe 2::remapfunction](../../../../docs/framework/unmanaged-api/debugging/icordebugilframe2-remapfunction-method.md)メソッドです。</span><span class="sxs-lookup"><span data-stu-id="3eaf5-112">This callback gives the debugger an opportunity to remap the instruction pointer to its proper place in the new version of the specified function by calling the [ICorDebugILFrame2::RemapFunction](../../../../docs/framework/unmanaged-api/debugging/icordebugilframe2-remapfunction-method.md) method.</span></span> <span data-ttu-id="3eaf5-113">場合は、デバッガーを呼び出しません`RemapFunction`呼び出す前に、 [icordebugcontroller::continue](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-continue-method.md)メソッド、ランタイムの古いコードの実行を続行し、別が起動されます`FunctionRemapOpportunity`次のシーケンス ポイントでのコールバック。</span><span class="sxs-lookup"><span data-stu-id="3eaf5-113">If the debugger does not call `RemapFunction` before calling the [ICorDebugController::Continue](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-continue-method.md) method, the runtime will continue to execute the old code and will fire another `FunctionRemapOpportunity` callback at the next sequence point.</span></span>  
  
 <span data-ttu-id="3eaf5-114">デバッガーが S_OK を返すまで、指定された関数の古いバージョンを実行しているすべてのフレームには、このコールバックが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="3eaf5-114">This callback will be invoked for every frame that is executing an older version of the given function until the debugger returns S_OK.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="3eaf5-115">要件</span><span class="sxs-lookup"><span data-stu-id="3eaf5-115">Requirements</span></span>  
 <span data-ttu-id="3eaf5-116">**プラットフォーム:**を参照してください[システム要件](../../../../docs/framework/get-started/system-requirements.md)です。</span><span class="sxs-lookup"><span data-stu-id="3eaf5-116">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="3eaf5-117">**ヘッダー:** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="3eaf5-117">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="3eaf5-118">**ライブラリ:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="3eaf5-118">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="3eaf5-119">**.NET framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="3eaf5-119">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3eaf5-120">関連項目</span><span class="sxs-lookup"><span data-stu-id="3eaf5-120">See Also</span></span>  
 [<span data-ttu-id="3eaf5-121">ICorDebugManagedCallback2 インターフェイス</span><span class="sxs-lookup"><span data-stu-id="3eaf5-121">ICorDebugManagedCallback2 Interface</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback2-interface.md)  
 [<span data-ttu-id="3eaf5-122">ICorDebugManagedCallback インターフェイス</span><span class="sxs-lookup"><span data-stu-id="3eaf5-122">ICorDebugManagedCallback Interface</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-interface.md)